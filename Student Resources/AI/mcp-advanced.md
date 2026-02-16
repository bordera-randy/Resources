# Model Context Protocol (MCP) - Advanced Guide

## Table of Contents
1. [Advanced Architecture](#advanced-architecture)
2. [Building Production-Grade Servers](#building-production-grade-servers)
3. [Authentication & Authorization](#authentication--authorization)
4. [Performance Optimization](#performance-optimization)
5. [Distributed Systems](#distributed-systems)
6. [Custom Transports](#custom-transports)
7. [State Management](#state-management)
8. [Testing Strategies](#testing-strategies)
9. [Monitoring & Observability](#monitoring--observability)
10. [Security Deep Dive](#security-deep-dive)

---

## Advanced Architecture

### Multi-Server Orchestration

When building complex systems, you may need to coordinate multiple MCP servers:

```javascript
// orchestrator.js
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { RPCClient } from "@modelcontextprotocol/sdk/client/index.js";

class ServerOrchestrator {
  constructor() {
    this.servers = new Map();
    this.cache = new Map();
  }

  async registerServer(name, transport) {
    const client = new RPCClient(transport);
    this.servers.set(name, client);
    
    // Discover available tools
    const tools = await client.request({
      jsonrpc: "2.0",
      method: "tools/list",
      id: 1
    });
    
    console.log(`Registered ${name} with ${tools.length} tools`);
  }

  async routeToolCall(toolName, args) {
    // Parse tool name format: "server:tool"
    const [serverName, actualTool] = toolName.split(":");
    
    if (!this.servers.has(serverName)) {
      throw new Error(`Server ${serverName} not found`);
    }

    const client = this.servers.get(serverName);
    return await client.request({
      jsonrpc: "2.0",
      method: "tools/call",
      params: {
        name: actualTool,
        arguments: args
      },
      id: Date.now()
    });
  }

  clearCache() {
    this.cache.clear();
  }
}

export default ServerOrchestrator;
```

### Middleware Pattern

Implement middleware for cross-cutting concerns:

```javascript
class MiddlewareChain {
  constructor() {
    this.middlewares = [];
  }

  use(middleware) {
    this.middlewares.push(middleware);
    return this;
  }

  async execute(context) {
    let index = 0;

    const next = async () => {
      if (index < this.middlewares.length) {
        const middleware = this.middlewares[index++];
        await middleware(context, next);
      }
    };

    await next();
    return context.result;
  }
}

// Usage
const chain = new MiddlewareChain();

chain
  .use(async (context, next) => {
    // Authentication middleware
    if (!context.headers.authorization) {
      throw new Error("Unauthorized");
    }
    context.user = parseToken(context.headers.authorization);
    await next();
  })
  .use(async (context, next) => {
    // Logging middleware
    const startTime = Date.now();
    await next();
    console.log(`Request took ${Date.now() - startTime}ms`);
  })
  .use(async (context, next) => {
    // Rate limiting middleware
    if (!rateLimiter.allow(context.user.id)) {
      throw new Error("Rate limit exceeded");
    }
    await next();
  });
```

---

## Building Production-Grade Servers

### Structured Server Factory

```javascript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import pino from "pino";
import { z } from "zod";

class MCPServerFactory {
  constructor(config = {}) {
    this.config = {
      name: config.name || "mcp-server",
      version: config.version || "1.0.0",
      env: config.env || "development",
      ...config
    };
    
    this.logger = pino({
      level: this.config.logLevel || "info",
      transport: {
        target: "pino-pretty",
        options: {
          colorize: true
        }
      }
    });

    this.server = new Server({
      name: this.config.name,
      version: this.config.version
    });

    this.tools = new Map();
    this.resources = new Map();
    this.prompts = new Map();
  }

  defineTool(name, description, schema, handler) {
    // Validate schema
    const validSchema = z.object(schema).strict();

    this.tools.set(name, {
      name,
      description,
      inputSchema: {
        type: "object",
        properties: schema,
        required: Object.keys(schema)
      },
      handler: async (args) => {
        // Validate input
        const validated = validSchema.parse(args);
        
        this.logger.info(`Calling tool: ${name}`, { args: validated });
        
        try {
          const result = await handler(validated);
          this.logger.info(`Tool succeeded: ${name}`);
          return result;
        } catch (error) {
          this.logger.error(`Tool failed: ${name}`, { error: error.message });
          throw error;
        }
      }
    });
  }

  defineResource(uri, name, mimeType, loader) {
    this.resources.set(uri, {
      uri,
      name,
      mimeType,
      loader
    });
  }

  definePrompt(name, description, handler, args = []) {
    this.prompts.set(name, {
      name,
      description,
      arguments: args,
      handler
    });
  }

  async start() {
    // Set up request handlers
    this.server.setRequestHandler(ListToolsRequest, async () => {
      return {
        tools: Array.from(this.tools.values()).map(t => ({
          name: t.name,
          description: t.description,
          inputSchema: t.inputSchema
        }))
      };
    });

    this.server.setRequestHandler(CallToolRequest, async (request) => {
      const tool = this.tools.get(request.params.name);
      if (!tool) {
        throw new Error(`Tool not found: ${request.params.name}`);
      }

      const result = await tool.handler(request.params.arguments);
      return {
        content: [{
          type: "text",
          text: JSON.stringify(result, null, 2)
        }]
      };
    });

    this.server.setRequestHandler(ListResourcesRequest, async () => {
      return {
        resources: Array.from(this.resources.values()).map(r => ({
          uri: r.uri,
          name: r.name,
          mimeType: r.mimeType
        }))
      };
    });

    this.server.setRequestHandler(ReadResourceRequest, async (request) => {
      const resource = this.resources.get(request.params.uri);
      if (!resource) {
        throw new Error(`Resource not found: ${request.params.uri}`);
      }

      const content = await resource.loader();
      return {
        contents: [{
          uri: resource.uri,
          mimeType: resource.mimeType,
          text: content
        }]
      };
    });

    const transport = new StdioServerTransport();
    await this.server.connect(transport);
    this.logger.info("MCP Server started successfully");
  }
}

export default MCPServerFactory;
```

### Usage Example

```javascript
const factory = new MCPServerFactory({
  name: "advanced-server",
  version: "2.0.0",
  logLevel: "debug"
});

// Define tools with Zod validation
factory.defineTool(
  "calculate_statistics",
  "Calculate mean, median, and std deviation",
  {
    numbers: z.array(z.number()),
    precision: z.number().optional()
  },
  async ({ numbers, precision = 2 }) => {
    const sorted = [...numbers].sort((a, b) => a - b);
    const mean = numbers.reduce((a, b) => a + b, 0) / numbers.length;
    const median = sorted[Math.floor(sorted.length / 2)];
    
    const variance = numbers.reduce((sum, n) => 
      sum + Math.pow(n - mean, 2), 0) / numbers.length;
    const stdDev = Math.sqrt(variance);

    return {
      mean: parseFloat(mean.toFixed(precision)),
      median: parseFloat(median.toFixed(precision)),
      stdDev: parseFloat(stdDev.toFixed(precision))
    };
  }
);

await factory.start();
```

---

## Authentication & Authorization

### JWT-Based Authentication

```javascript
import jwt from "jsonwebtoken";

class AuthenticationManager {
  constructor(secret, options = {}) {
    this.secret = secret;
    this.options = {
      expiresIn: "24h",
      algorithm: "HS256",
      ...options
    };
  }

  generateToken(payload, expiresIn = null) {
    return jwt.sign(payload, this.secret, {
      ...this.options,
      expiresIn: expiresIn || this.options.expiresIn
    });
  }

  verifyToken(token) {
    try {
      return jwt.verify(token, this.secret);
    } catch (error) {
      throw new Error(`Invalid token: ${error.message}`);
    }
  }

  extractToken(authHeader) {
    if (!authHeader || !authHeader.startsWith("Bearer ")) {
      throw new Error("Missing or invalid Authorization header");
    }
    return authHeader.substring(7);
  }
}

// Usage with middleware
const authManager = new AuthenticationManager(process.env.JWT_SECRET);

server.setRequestHandler(CallToolRequest, async (request) => {
  try {
    const token = authManager.extractToken(request.headers?.authorization);
    const user = authManager.verifyToken(token);
    
    // Attach user to context
    request.user = user;
    
    // Continue with authorization checks
    // ...
  } catch (error) {
    throw new Error(`Authentication failed: ${error.message}`);
  }
});
```

### Role-Based Access Control (RBAC)

```javascript
class AuthorizationManager {
  constructor() {
    this.roles = new Map();
    this.permissions = new Map();
  }

  defineRole(name, permissions) {
    this.roles.set(name, new Set(permissions));
  }

  definePermission(name, description) {
    this.permissions.set(name, description);
  }

  hasPermission(user, permission) {
    if (!user.roles || !Array.isArray(user.roles)) {
      return false;
    }

    return user.roles.some(role => {
      const rolePerms = this.roles.get(role);
      return rolePerms && rolePerms.has(permission);
    });
  }

  requirePermission(permission) {
    return (user) => {
      if (!this.hasPermission(user, permission)) {
        throw new Error(`Permission denied: ${permission}`);
      }
    };
  }
}

// Setup
const authz = new AuthorizationManager();

authz.definePermission("read:resources", "Read resources");
authz.definePermission("write:resources", "Write resources");
authz.definePermission("delete:resources", "Delete resources");
authz.definePermission("admin", "Admin access");

authz.defineRole("viewer", ["read:resources"]);
authz.defineRole("editor", ["read:resources", "write:resources"]);
authz.defineRole("admin", ["read:resources", "write:resources", "delete:resources", "admin"]);

// Usage
server.setRequestHandler(CallToolRequest, async (request) => {
  const user = request.user;
  
  if (request.params.name === "delete_resource") {
    authz.requirePermission("delete:resources")(user);
  }
  
  // Continue with tool execution
});
```

---

## Performance Optimization

### Caching Strategy

```javascript
class CacheManager {
  constructor(ttl = 3600000) { // 1 hour default
    this.cache = new Map();
    this.ttl = ttl;
  }

  set(key, value, customTTL = null) {
    const expiry = Date.now() + (customTTL || this.ttl);
    this.cache.set(key, { value, expiry });
  }

  get(key) {
    const item = this.cache.get(key);
    
    if (!item) return null;
    
    if (Date.now() > item.expiry) {
      this.cache.delete(key);
      return null;
    }

    return item.value;
  }

  async getOrCompute(key, computeFn, customTTL = null) {
    const cached = this.get(key);
    
    if (cached) {
      return cached;
    }

    const value = await computeFn();
    this.set(key, value, customTTL);
    return value;
  }

  invalidate(pattern) {
    for (const [key] of this.cache) {
      if (key.match(pattern)) {
        this.cache.delete(key);
      }
    }
  }

  clear() {
    this.cache.clear();
  }

  stats() {
    return {
      size: this.cache.size,
      entries: Array.from(this.cache.entries()).map(([k, v]) => ({
        key: k,
        ttl: v.expiry - Date.now()
      }))
    };
  }
}

// Usage
const cache = new CacheManager();

server.setRequestHandler(CallToolRequest, async (request) => {
  const cacheKey = `${request.params.name}:${JSON.stringify(request.params.arguments)}`;
  
  const result = await cache.getOrCompute(
    cacheKey,
    () => executeExpensiveOperation(request.params),
    60000 // 1 minute cache
  );

  return { content: [{ type: "text", text: JSON.stringify(result) }] };
});
```

### Connection Pooling

```javascript
class DatabasePool {
  constructor(config, poolSize = 10) {
    this.config = config;
    this.poolSize = poolSize;
    this.connections = [];
    this.availableConnections = [];
    this.waitQueue = [];
  }

  async initialize() {
    for (let i = 0; i < this.poolSize; i++) {
      const conn = await this.createConnection();
      this.connections.push(conn);
      this.availableConnections.push(conn);
    }
  }

  async createConnection() {
    // Implementation depends on database
    // Example for PostgreSQL:
    return await new Promise((resolve, reject) => {
      // connection logic
    });
  }

  async acquire() {
    if (this.availableConnections.length > 0) {
      return this.availableConnections.pop();
    }

    return new Promise((resolve) => {
      this.waitQueue.push(resolve);
    });
  }

  release(connection) {
    if (this.waitQueue.length > 0) {
      const resolve = this.waitQueue.shift();
      resolve(connection);
    } else {
      this.availableConnections.push(connection);
    }
  }

  async query(sql, params) {
    const conn = await this.acquire();
    try {
      return await conn.query(sql, params);
    } finally {
      this.release(conn);
    }
  }

  async close() {
    await Promise.all(
      this.connections.map(conn => conn.close())
    );
  }
}
```

---

## Distributed Systems

### Service Registry Pattern

```javascript
class ServiceRegistry {
  constructor() {
    this.services = new Map();
    this.watchers = new Set();
  }

  register(serviceId, metadata) {
    this.services.set(serviceId, {
      id: serviceId,
      metadata,
      registeredAt: Date.now(),
      healthy: true
    });

    this.notifyWatchers();
  }

  deregister(serviceId) {
    this.services.delete(serviceId);
    this.notifyWatchers();
  }

  discover(serviceName) {
    return Array.from(this.services.values()).filter(
      service => service.metadata.name === serviceName && service.healthy
    );
  }

  healthCheck(serviceId, healthy) {
    const service = this.services.get(serviceId);
    if (service) {
      service.healthy = healthy;
      if (!healthy) {
        this.notifyWatchers();
      }
    }
  }

  watch(callback) {
    this.watchers.add(callback);
    return () => this.watchers.delete(callback);
  }

  notifyWatchers() {
    this.watchers.forEach(callback => {
      callback(Array.from(this.services.values()));
    });
  }

  getMetrics() {
    return {
      totalServices: this.services.size,
      healthyServices: Array.from(this.services.values()).filter(s => s.healthy).length,
      unhealthyServices: Array.from(this.services.values()).filter(s => !s.healthy).length
    };
  }
}
```

### Load Balancing

```javascript
class LoadBalancer {
  constructor(strategy = "round-robin") {
    this.strategy = strategy;
    this.instances = [];
    this.currentIndex = 0;
  }

  addInstance(instance) {
    this.instances.push(instance);
  }

  select() {
    if (this.instances.length === 0) {
      throw new Error("No instances available");
    }

    switch (this.strategy) {
      case "round-robin":
        return this.roundRobin();
      case "least-connections":
        return this.leastConnections();
      case "random":
        return this.random();
      default:
        throw new Error(`Unknown strategy: ${this.strategy}`);
    }
  }

  roundRobin() {
    const instance = this.instances[this.currentIndex];
    this.currentIndex = (this.currentIndex + 1) % this.instances.length;
    return instance;
  }

  leastConnections() {
    return this.instances.reduce((min, instance) => 
      (instance.connections || 0) < (min.connections || 0) ? instance : min
    );
  }

  random() {
    return this.instances[Math.floor(Math.random() * this.instances.length)];
  }
}
```

---

## Custom Transports

### HTTP Transport

```javascript
import express from "express";
import { Server } from "@modelcontextprotocol/sdk/server/index.js";

class HTTPTransport {
  constructor(port = 3000) {
    this.port = port;
    this.app = express();
    this.server = null;
  }

  async start(requestHandler) {
    this.app.use(express.json());

    this.app.post("/jsonrpc", async (req, res) => {
      try {
        const response = await requestHandler(req.body);
        res.json(response);
      } catch (error) {
        res.status(400).json({
          jsonrpc: "2.0",
          error: {
            code: -32603,
            message: error.message
          }
        });
      }
    });

    this.server = this.app.listen(this.port, () => {
      console.log(`HTTP Transport listening on port ${this.port}`);
    });
  }

  async stop() {
    if (this.server) {
      this.server.close();
    }
  }
}
```

### WebSocket Transport

```javascript
import WebSocket from "ws";
import { Server } from "@modelcontextprotocol/sdk/server/index.js";

class WebSocketTransport {
  constructor(port = 8080) {
    this.port = port;
    this.wss = new WebSocket.Server({ port });
    this.requestHandler = null;
  }

  async start(requestHandler) {
    this.requestHandler = requestHandler;

    this.wss.on("connection", (ws) => {
      ws.on("message", async (message) => {
        try {
          const request = JSON.parse(message);
          const response = await requestHandler(request);
          ws.send(JSON.stringify(response));
        } catch (error) {
          ws.send(JSON.stringify({
            jsonrpc: "2.0",
            error: {
              code: -32603,
              message: error.message
            }
          }));
        }
      });
    });

    console.log(`WebSocket Transport listening on port ${this.port}`);
  }

  async stop() {
    this.wss.close();
  }
}
```

---

## State Management

### Persistent State with Events

```javascript
import EventEmitter from "events";

class StatefulServer extends EventEmitter {
  constructor(storePath) {
    super();
    this.storePath = storePath;
    this.state = {};
    this.history = [];
  }

  async loadState() {
    try {
      const data = await fs.promises.readFile(this.storePath, "utf-8");
      this.state = JSON.parse(data);
      this.emit("state-loaded", this.state);
    } catch (error) {
      this.emit("load-error", error);
    }
  }

  async saveState() {
    try {
      await fs.promises.writeFile(
        this.storePath,
        JSON.stringify(this.state, null, 2)
      );
      this.emit("state-saved", this.state);
    } catch (error) {
      this.emit("save-error", error);
    }
  }

  setState(path, value) {
    const oldValue = this.getState(path);
    
    // Navigate to nested property
    const keys = path.split(".");
    let current = this.state;
    for (let i = 0; i < keys.length - 1; i++) {
      if (!current[keys[i]]) {
        current[keys[i]] = {};
      }
      current = current[keys[i]];
    }
    current[keys[keys.length - 1]] = value;

    // Record in history
    this.history.push({
      timestamp: Date.now(),
      path,
      oldValue,
      newValue: value
    });

    this.emit("state-changed", { path, oldValue, newValue: value });
    this.saveState();
  }

  getState(path) {
    const keys = path.split(".");
    let current = this.state;
    for (const key of keys) {
      current = current?.[key];
    }
    return current;
  }

  getHistory(limit = 100) {
    return this.history.slice(-limit);
  }

  rollback(steps = 1) {
    const changes = this.history.slice(-steps);
    for (const change of changes.reverse()) {
      this.setState(change.path, change.oldValue);
    }
  }
}
```

---

## Testing Strategies

### Integration Testing

```javascript
import { describe, it, expect, beforeEach, afterEach } from "@jest/globals";
import MCPServerFactory from "./server-factory.js";

describe("MCP Server Integration Tests", () => {
  let server;
  let client;

  beforeEach(async () => {
    server = new MCPServerFactory({ name: "test-server" });
    
    server.defineTool(
      "add",
      "Add two numbers",
      { a: z.number(), b: z.number() },
      async ({ a, b }) => ({ result: a + b })
    );

    // Start server in test mode
    await server.start();
  });

  afterEach(async () => {
    // Cleanup
  });

  it("should successfully call a tool", async () => {
    const response = await client.call("add", { a: 5, b: 3 });
    expect(response.result).toBe(8);
  });

  it("should validate input types", async () => {
    expect(() => client.call("add", { a: "five", b: 3 }))
      .toThrow("Validation error");
  });

  it("should handle concurrent requests", async () => {
    const promises = Array(100).fill(null).map((_, i) =>
      client.call("add", { a: i, b: 1 })
    );

    const results = await Promise.all(promises);
    expect(results).toHaveLength(100);
  });
});
```

### Unit Testing Tools

```javascript
describe("Tool Definitions", () => {
  it("should validate schema", () => {
    const schema = {
      email: z.string().email(),
      age: z.number().min(0).max(150)
    };

    expect(() => schema.email.parse("invalid")).toThrow();
    expect(() => schema.age.parse(200)).toThrow();
    expect(() => schema.email.parse("test@example.com")).not.toThrow();
  });

  it("should handle errors gracefully", async () => {
    const tool = createTool(
      "risky_operation",
      async () => { throw new Error("Intentional error"); }
    );

    try {
      await tool();
      expect(true).toBe(false); // Should not reach
    } catch (error) {
      expect(error.message).toContain("Intentional error");
    }
  });
});
```

---

## Monitoring & Observability

### Structured Logging with Pino

```javascript
import pino from "pino";

const logger = pino({
  level: process.env.LOG_LEVEL || "info",
  transport: {
    target: "pino-http",
    options: {
      colorize: true,
      translateTime: "SYS:standard",
      ignore: "pid,hostname"
    }
  }
});

// Structured logging
logger.info(
  { userId: "123", action: "tool-called" },
  "User executed tool"
);

logger.error(
  { error: err, toolName: "unsafe-operation" },
  "Tool execution failed"
);
```

### Metrics Collection

```javascript
class MetricsCollector {
  constructor() {
    this.metrics = new Map();
  }

  recordToolCall(toolName, duration, success) {
    const key = `tool.${toolName}`;
    
    if (!this.metrics.has(key)) {
      this.metrics.set(key, {
        calls: 0,
        successes: 0,
        failures: 0,
        totalDuration: 0,
        avgDuration: 0
      });
    }

    const metric = this.metrics.get(key);
    metric.calls++;
    if (success) {
      metric.successes++;
    } else {
      metric.failures++;
    }
    metric.totalDuration += duration;
    metric.avgDuration = metric.totalDuration / metric.calls;
  }

  getMetrics(toolName = null) {
    if (toolName) {
      return this.metrics.get(`tool.${toolName}`);
    }
    return Object.fromEntries(this.metrics);
  }

  exportPrometheus() {
    const lines = [];
    for (const [key, metric] of this.metrics) {
      lines.push(`${key}_calls ${metric.calls}`);
      lines.push(`${key}_successes ${metric.successes}`);
      lines.push(`${key}_failures ${metric.failures}`);
      lines.push(`${key}_avg_duration_ms ${metric.avgDuration.toFixed(2)}`);
    }
    return lines.join("\n");
  }
}
```

### Health Checks

```javascript
class HealthChecker {
  constructor() {
    this.checks = new Map();
  }

  register(name, checkFn, interval = 5000) {
    this.checks.set(name, {
      checkFn,
      interval,
      status: "unknown",
      lastCheck: null,
      error: null
    });

    // Run periodic checks
    setInterval(async () => {
      try {
        await checkFn();
        this.checks.get(name).status = "healthy";
        this.checks.get(name).error = null;
      } catch (error) {
        this.checks.get(name).status = "unhealthy";
        this.checks.get(name).error = error.message;
      }
      this.checks.get(name).lastCheck = Date.now();
    }, interval);
  }

  getStatus() {
    const status = {
      timestamp: Date.now(),
      overall: "healthy",
      checks: Object.fromEntries(this.checks)
    };

    // Set overall status
    if (Array.from(this.checks.values()).some(c => c.status === "unhealthy")) {
      status.overall = "unhealthy";
    }

    return status;
  }
}
```

---

## Security Deep Dive

### Input Validation & Sanitization

```javascript
import DOMPurify from "isomorphic-dompurify";
import validator from "validator";

class InputValidator {
  static sanitizeString(input) {
    if (typeof input !== "string") return "";
    return DOMPurify.sanitize(input);
  }

  static validateEmail(email) {
    if (!validator.isEmail(email)) {
      throw new Error("Invalid email format");
    }
    return email.toLowerCase();
  }

  static validateURL(url) {
    if (!validator.isURL(url)) {
      throw new Error("Invalid URL");
    }
    return url;
  }

  static validateSQLIdentifier(identifier) {
    // Prevent SQL injection
    if (!/^[a-zA-Z_][a-zA-Z0-9_]*$/.test(identifier)) {
      throw new Error("Invalid SQL identifier");
    }
    return identifier;
  }

  static validateFilePath(path) {
    // Prevent directory traversal
    if (path.includes("..") || path.startsWith("/")) {
      throw new Error("Invalid file path");
    }
    return path;
  }
}
```

### Rate Limiting & Throttling

```javascript
class RateLimiter {
  constructor(maxRequests = 100, windowMs = 60000) {
    this.maxRequests = maxRequests;
    this.windowMs = windowMs;
    this.requests = new Map();
  }

  isAllowed(clientId) {
    const now = Date.now();
    
    if (!this.requests.has(clientId)) {
      this.requests.set(clientId, []);
    }

    const clientRequests = this.requests.get(clientId);
    
    // Remove old requests outside window
    while (clientRequests.length > 0 && clientRequests[0] < now - this.windowMs) {
      clientRequests.shift();
    }

    if (clientRequests.length < this.maxRequests) {
      clientRequests.push(now);
      return true;
    }

    return false;
  }

  getStatus(clientId) {
    const requests = this.requests.get(clientId) || [];
    return {
      requests: requests.length,
      limit: this.maxRequests,
      remaining: Math.max(0, this.maxRequests - requests.length)
    };
  }
}
```

### Environment & Secrets Management

```javascript
import dotenv from "dotenv";
import { SecretsManager } from "@aws-sdk/client-secrets-manager";

dotenv.config();

class SecretManager {
  constructor() {
    this.cache = new Map();
    this.client = new SecretsManager();
  }

  async getSecret(secretName) {
    // Check cache
    if (this.cache.has(secretName)) {
      return this.cache.get(secretName);
    }

    try {
      const response = await this.client.getSecretValue({
        SecretId: secretName
      });

      const secret = response.SecretString || response.SecretBinary;
      this.cache.set(secretName, secret);
      return secret;
    } catch (error) {
      throw new Error(`Failed to retrieve secret: ${secretName}`);
    }
  }

  validateEnvironment() {
    const required = ["JWT_SECRET", "DATABASE_URL", "LOG_LEVEL"];
    const missing = required.filter(env => !process.env[env]);

    if (missing.length > 0) {
      throw new Error(`Missing environment variables: ${missing.join(", ")}`);
    }
  }
}
```

---

## Advanced Patterns

### Circuit Breaker Pattern

```javascript
class CircuitBreaker {
  constructor(threshold = 5, timeout = 60000) {
    this.threshold = threshold;
    this.timeout = timeout;
    this.failures = 0;
    this.state = "closed"; // closed, open, half-open
    this.lastFailureTime = null;
  }

  async execute(fn) {
    if (this.state === "open") {
      if (Date.now() - this.lastFailureTime > this.timeout) {
        this.state = "half-open";
      } else {
        throw new Error("Circuit breaker is open");
      }
    }

    try {
      const result = await fn();
      this.onSuccess();
      return result;
    } catch (error) {
      this.onFailure();
      throw error;
    }
  }

  onSuccess() {
    this.failures = 0;
    this.state = "closed";
  }

  onFailure() {
    this.failures++;
    this.lastFailureTime = Date.now();
    
    if (this.failures >= this.threshold) {
      this.state = "open";
    }
  }

  getStatus() {
    return {
      state: this.state,
      failures: this.failures,
      threshold: this.threshold
    };
  }
}
```

### Retry with Exponential Backoff

```javascript
class RetryManager {
  static async execute(
    fn,
    maxRetries = 3,
    baseDelay = 1000,
    maxDelay = 30000
  ) {
    let lastError;

    for (let attempt = 0; attempt <= maxRetries; attempt++) {
      try {
        return await fn();
      } catch (error) {
        lastError = error;

        if (attempt < maxRetries) {
          const delay = Math.min(
            baseDelay * Math.pow(2, attempt),
            maxDelay
          );
          await new Promise(resolve => setTimeout(resolve, delay));
        }
      }
    }

    throw lastError;
  }
}

// Usage
const result = await RetryManager.execute(
  () => unreliableApiCall(),
  3,
  1000,
  30000
);
```

---

## Best Practices Summary

1. **Always validate inputs** - Use Zod or similar schema validators
2. **Implement proper error handling** - Distinguish between different error types
3. **Log structured data** - Use JSON logs for better analysis
4. **Monitor performance** - Track metrics and alerts
5. **Secure secrets** - Never commit secrets to version control
6. **Test thoroughly** - Unit, integration, and load tests
7. **Document APIs** - Clear descriptions and examples
8. **Use versioning** - Maintain backward compatibility
9. **Implement caching** - Reduce unnecessary computation
10. **Plan for scaling** - Consider distributed architecture

---

**Last Updated**: February 2026  
**Difficulty**: Advanced  
**Prerequisites**: Basic MCP knowledge, Node.js/Python proficiency
