# Model Context Protocol (MCP) - Expert Guide

## Table of Contents
1. [Protocol Deep Dive](#protocol-deep-dive)
2. [Crafting Specialized Servers](#crafting-specialized-servers)
3. [Advanced Compositional Patterns](#advanced-compositional-patterns)
4. [Custom Resource Types](#custom-resource-types)
5. [Protocol Extensions](#protocol-extensions)
6. [High-Performance Optimization](#high-performance-optimization)
7. [Enterprise Architecture](#enterprise-architecture)
8. [Machine Learning Integration](#machine-learning-integration)
9. [Real-Time Streaming](#real-time-streaming)
10. [Production Hardening](#production-hardening)

---

## Protocol Deep Dive

### JSON-RPC 2.0 Specification Mastery

MCP is built on JSON-RPC 2.0. Understanding the nuances enables optimization:

```javascript
// Batch requests for optimal throughput
class BatchedRPCClient {
  constructor(maxBatchSize = 50, maxWaitMs = 100) {
    this.maxBatchSize = maxBatchSize;
    this.maxWaitMs = maxWaitMs;
    this.batch = [];
    this.pendingCallbacks = [];
    this.batchTimer = null;
  }

  async call(method, params) {
    return new Promise((resolve, reject) => {
      const id = this.batch.length;
      
      this.batch.push({
        jsonrpc: "2.0",
        method,
        params,
        id
      });

      this.pendingCallbacks.push({ resolve, reject });

      // Send immediately if batch is full
      if (this.batch.length >= this.maxBatchSize) {
        this.flush();
      } else if (!this.batchTimer) {
        // Schedule flush with delay
        this.batchTimer = setTimeout(() => this.flush(), this.maxWaitMs);
      }
    });
  }

  async flush() {
    if (this.batch.length === 0) return;

    clearTimeout(this.batchTimer);
    this.batchTimer = null;

    const batch = this.batch;
    const callbacks = this.pendingCallbacks;
    this.batch = [];
    this.pendingCallbacks = [];

    try {
      const responses = await this.transport.send(batch);
      
      // Match responses to callbacks
      responses.forEach((response, index) => {
        if (response.error) {
          callbacks[index].reject(new Error(response.error.message));
        } else {
          callbacks[index].resolve(response.result);
        }
      });
    } catch (error) {
      callbacks.forEach(cb => cb.reject(error));
    }
  }
}
```

### Request/Response Correlation

Advanced request handling with correlation tracking:

```javascript
class CorrelatedRPCServer {
  constructor() {
    this.pendingRequests = new Map();
    this.requestIdCounter = 0;
    this.correlationMiddleware = [];
  }

  generateRequestId() {
    return ++this.requestIdCounter;
  }

  async handleRequest(jsonRpcRequest, context = {}) {
    const requestId = this.generateRequestId();
    const correlationId = context.correlationId || this.generateUUID();

    // Store correlation context
    this.pendingRequests.set(requestId, {
      requestId,
      correlationId,
      method: jsonRpcRequest.method,
      startTime: Date.now(),
      context
    });

    try {
      // Execute with correlation context
      const result = await this.executeWithContext(
        jsonRpcRequest,
        { requestId, correlationId }
      );

      return {
        jsonrpc: "2.0",
        result,
        id: jsonRpcRequest.id,
        "X-Correlation-ID": correlationId
      };
    } catch (error) {
      return {
        jsonrpc: "2.0",
        error: {
          code: error.code || -32603,
          message: error.message,
          data: { requestId, correlationId }
        },
        id: jsonRpcRequest.id
      };
    } finally {
      const duration = Date.now() - this.pendingRequests.get(requestId).startTime;
      this.logRequestMetrics(requestId, duration);
      this.pendingRequests.delete(requestId);
    }
  }

  async executeWithContext(request, context) {
    // Execute middleware chain with context
    for (const middleware of this.correlationMiddleware) {
      await middleware(request, context);
    }

    // Execute actual handler
    return await this.handleJSONRPC(request);
  }

  logRequestMetrics(requestId, duration) {
    const req = this.pendingRequests.get(requestId);
    console.log({
      timestamp: new Date().toISOString(),
      requestId: req.requestId,
      correlationId: req.correlationId,
      method: req.method,
      duration,
      context: req.context
    });
  }

  generateUUID() {
    return "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".replace(/[xy]/g, c => {
      const r = Math.random() * 16 | 0;
      const v = c === "x" ? r : (r & 0x3 | 0x8);
      return v.toString(16);
    });
  }
}
```

---

## Crafting Specialized Servers

### Domain-Specific Language (DSL) Server

```javascript
class DSLServer {
  constructor() {
    this.parser = new DSLParser();
    this.executor = new DSLExecutor();
    this.queryCache = new Map();
  }

  // Tool for parsing DSL expressions
  defineParseTool(server) {
    server.defineTool(
      "parse_dsl",
      "Parse a domain-specific language expression",
      {
        expression: z.string(),
        context: z.record(z.unknown()).optional()
      },
      async ({ expression, context = {} }) => {
        const cacheKey = `parse:${expression}`;
        
        if (this.queryCache.has(cacheKey)) {
          return this.queryCache.get(cacheKey);
        }

        const ast = this.parser.parse(expression);
        const validated = this.parser.validate(ast, context);

        this.queryCache.set(cacheKey, {
          ast,
          validated,
          metadata: {
            complexity: this.calculateComplexity(ast),
            dependencies: this.extractDependencies(ast)
          }
        });

        return this.queryCache.get(cacheKey);
      }
    );
  }

  // Tool for executing parsed expressions
  defineExecuteTool(server) {
    server.defineTool(
      "execute_dsl",
      "Execute a parsed DSL expression",
      {
        ast: z.unknown(),
        bindings: z.record(z.unknown())
      },
      async ({ ast, bindings }) => {
        const startTime = Date.now();
        
        try {
          const result = await this.executor.execute(ast, bindings);
          
          return {
            success: true,
            result,
            executionTime: Date.now() - startTime,
            resultType: typeof result
          };
        } catch (error) {
          return {
            success: false,
            error: error.message,
            executionTime: Date.now() - startTime
          };
        }
      }
    );
  }

  calculateComplexity(ast) {
    let complexity = 0;
    const traverse = (node) => {
      complexity++;
      if (node.children) {
        node.children.forEach(traverse);
      }
    };
    traverse(ast);
    return complexity;
  }

  extractDependencies(ast) {
    const deps = new Set();
    const traverse = (node) => {
      if (node.type === "reference") {
        deps.add(node.value);
      }
      if (node.children) {
        node.children.forEach(traverse);
      }
    };
    traverse(ast);
    return Array.from(deps);
  }
}
```

### Graph Database Server

```javascript
class GraphDatabaseServer {
  constructor(graphEngine) {
    this.engine = graphEngine;
    this.queryOptimizer = new QueryOptimizer();
    this.transactionLog = [];
  }

  defineGraphQueries(server) {
    server.defineTool(
      "graph_query",
      "Execute a graph query with optimization",
      {
        query: z.string(),
        parameters: z.record(z.unknown()).optional(),
        timeout: z.number().optional()
      },
      async ({ query, parameters = {}, timeout = 5000 }) => {
        // Optimize query execution plan
        const executionPlan = this.queryOptimizer.optimize(query, parameters);

        // Execute with timeout
        const result = await Promise.race([
          this.engine.execute(executionPlan),
          this.createTimeout(timeout)
        ]);

        // Log transaction
        this.transactionLog.push({
          timestamp: Date.now(),
          query,
          parameters,
          resultCount: result.length,
          executionPlan: executionPlan.summary
        });

        return result;
      }
    );

    server.defineTool(
      "graph_traverse",
      "Traverse graph with path collection",
      {
        startNode: z.string(),
        targetNode: z.string(),
        maxDepth: z.number().optional(),
        filter: z.string().optional()
      },
      async ({ startNode, targetNode, maxDepth = 10, filter }) => {
        const paths = [];
        
        const traverse = async (node, depth = 0, path = []) => {
          if (depth > maxDepth) return;
          
          path.push(node);

          if (node === targetNode) {
            paths.push([...path]);
            return;
          }

          const neighbors = await this.engine.getNeighbors(node);
          
          for (const neighbor of neighbors) {
            if (!path.includes(neighbor)) {
              await traverse(neighbor, depth + 1, path);
            }
          }

          path.pop();
        };

        await traverse(startNode);

        return {
          paths,
          count: paths.length,
          shortestPath: paths.reduce((a, b) => 
            a.length < b.length ? a : b
          )
        };
      }
    );
  }

  createTimeout(ms) {
    return new Promise((_, reject) =>
      setTimeout(() => reject(new Error("Query timeout")), ms)
    );
  }
}
```

---

## Advanced Compositional Patterns

### Decorator Pattern for Tools

```javascript
class ToolDecorator {
  static withCaching(tool, ttl = 3600000) {
    const cache = new Map();

    return async (args) => {
      const cacheKey = JSON.stringify(args);

      if (cache.has(cacheKey)) {
        const cached = cache.get(cacheKey);
        if (Date.now() - cached.timestamp < ttl) {
          return cached.result;
        }
      }

      const result = await tool(args);
      cache.set(cacheKey, { result, timestamp: Date.now() });

      return result;
    };
  }

  static withRetry(tool, maxRetries = 3, backoff = 1000) {
    return async (args) => {
      let lastError;

      for (let attempt = 0; attempt <= maxRetries; attempt++) {
        try {
          return await tool(args);
        } catch (error) {
          lastError = error;
          if (attempt < maxRetries) {
            await new Promise(resolve =>
              setTimeout(resolve, backoff * Math.pow(2, attempt))
            );
          }
        }
      }

      throw lastError;
    };
  }

  static withValidation(tool, validator) {
    return async (args) => {
      const validated = await validator(args);
      return await tool(validated);
    };
  }

  static withAudit(tool, auditLog) {
    return async (args) => {
      const timestamp = Date.now();
      const result = await tool(args);

      auditLog.push({
        timestamp,
        args,
        result,
        duration: Date.now() - timestamp
      });

      return result;
    };
  }

  static compose(...decorators) {
    return (tool) =>
      decorators.reduce((decorated, decorator) =>
        decorator(decorated), tool);
  }
}

// Usage
const enhancedTool = ToolDecorator.compose(
  tool => ToolDecorator.withCaching(tool, 60000),
  tool => ToolDecorator.withRetry(tool, 3),
  tool => ToolDecorator.withValidation(tool, validateInput),
  tool => ToolDecorator.withAudit(tool, auditLog)
)(originalTool);
```

### Proxy Pattern for Remote Servers

```javascript
class ServerProxy {
  constructor(remoteEndpoint) {
    this.endpoint = remoteEndpoint;
    this.localCache = new Map();
    this.failoverServers = [];
  }

  registerFailover(endpoint) {
    this.failoverServers.push(endpoint);
  }

  async callRemote(method, params, retryCount = 0) {
    const maxRetries = this.failoverServers.length + 1;

    try {
      const response = await this.executeRequest(
        this.endpoint,
        method,
        params
      );
      return response;
    } catch (error) {
      if (retryCount < maxRetries && this.failoverServers.length > 0) {
        const failoverEndpoint = this.failoverServers[retryCount - 1];
        return await this.executeRequest(
          failoverEndpoint,
          method,
          params
        );
      }
      throw error;
    }
  }

  async executeRequest(endpoint, method, params) {
    const request = {
      jsonrpc: "2.0",
      method,
      params,
      id: Date.now()
    };

    const response = await fetch(endpoint, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(request)
    }).then(r => r.json());

    if (response.error) {
      throw new Error(response.error.message);
    }

    return response.result;
  }

  invalidateCache(pattern) {
    for (const key of this.localCache.keys()) {
      if (key.match(pattern)) {
        this.localCache.delete(key);
      }
    }
  }
}
```

---

## Custom Resource Types

### Binary Resource Handler

```javascript
class BinaryResourceServer {
  constructor() {
    this.binaryResources = new Map();
  }

  defineImageResource(server) {
    server.defineResource(
      "image://gallery/*",
      "Image files from gallery",
      "image/*",
      async (uri) => {
        const imagePath = uri.replace("image://gallery/", "");
        const imageBuffer = await fs.promises.readFile(imagePath);

        // Return as base64 encoded data URL
        const base64 = imageBuffer.toString("base64");
        const ext = imagePath.split(".").pop();
        return `data:image/${ext};base64,${base64}`;
      }
    );
  }

  defineVideoResource(server) {
    server.defineResource(
      "video://library/*",
      "Video files with streaming support",
      "video/*",
      async (uri) => {
        const videoPath = uri.replace("video://library/", "");
        const videoBuffer = await fs.promises.readFile(videoPath);

        // Return video metadata and chunk info
        return JSON.stringify({
          url: videoPath,
          size: videoBuffer.length,
          chunks: Math.ceil(videoBuffer.length / 1024 / 1024),
          mimeType: this.getMimeType(videoPath)
        });
      }
    );
  }

  defineStreamResource(server) {
    server.defineResource(
      "stream://data/*",
      "Real-time data streams",
      "application/json",
      async (uri) => {
        // Return stream info instead of content
        const streamName = uri.replace("stream://data/", "");
        return JSON.stringify({
          stream: streamName,
          isActive: true,
          subscribers: await this.getSubscriberCount(streamName),
          bufferSize: await this.getBufferSize(streamName)
        });
      }
    );
  }

  getMimeType(filename) {
    const ext = filename.split(".").pop().toLowerCase();
    const mimeTypes = {
      mp4: "video/mp4",
      webm: "video/webm",
      mp3: "audio/mpeg",
      wav: "audio/wav"
    };
    return mimeTypes[ext] || "application/octet-stream";
  }
}
```

### Computed Resource Server

```javascript
class ComputedResourceServer {
  constructor(database) {
    this.database = database;
    this.computedCache = new Map();
  }

  defineAnalyticsResource(server) {
    server.defineResource(
      "analytics://reports/*",
      "Dynamically computed analytics reports",
      "application/json",
      async (uri) => {
        const reportType = uri.replace("analytics://reports/", "");
        const cacheKey = `analytics:${reportType}`;

        // Check cache
        const cached = this.computedCache.get(cacheKey);
        if (cached && Date.now() - cached.timestamp < 300000) {
          return cached.data;
        }

        // Compute report
        const reportData = await this.computeReport(reportType);

        // Cache result
        this.computedCache.set(cacheKey, {
          data: reportData,
          timestamp: Date.now()
        });

        return reportData;
      }
    );
  }

  async computeReport(reportType) {
    switch (reportType) {
      case "monthly-summary":
        return await this.generateMonthlySummary();
      case "user-metrics":
        return await this.generateUserMetrics();
      case "performance":
        return await this.generatePerformanceReport();
      default:
        throw new Error(`Unknown report type: ${reportType}`);
    }
  }

  async generateMonthlySummary() {
    const data = await this.database.query(
      "SELECT * FROM events WHERE date >= NOW() - INTERVAL 30 DAY"
    );

    return {
      period: "monthly",
      eventCount: data.length,
      uniqueUsers: new Set(data.map(d => d.userId)).size,
      aggregates: this.computeAggregates(data)
    };
  }

  computeAggregates(data) {
    return {
      avgEventsPerUser: data.length / new Set(data.map(d => d.userId)).size,
      peakHour: this.findPeakHour(data),
      topEvents: this.getTopEvents(data, 10)
    };
  }

  findPeakHour(data) {
    const hourCounts = {};
    data.forEach(d => {
      const hour = new Date(d.timestamp).getHours();
      hourCounts[hour] = (hourCounts[hour] || 0) + 1;
    });
    return Object.entries(hourCounts).sort((a, b) => b[1] - a[1])[0][0];
  }

  getTopEvents(data, limit) {
    const eventCounts = {};
    data.forEach(d => {
      eventCounts[d.eventType] = (eventCounts[d.eventType] || 0) + 1;
    });
    return Object.entries(eventCounts)
      .sort((a, b) => b[1] - a[1])
      .slice(0, limit)
      .map(([event, count]) => ({ event, count }));
  }
}
```

---

## Protocol Extensions

### Custom Request/Response Types

```javascript
class ExtendedProtocolServer {
  constructor() {
    this.customHandlers = new Map();
  }

  registerCustomMethod(method, handler) {
    this.customHandlers.set(method, handler);
  }

  async handleRequest(request) {
    if (this.customHandlers.has(request.method)) {
      const handler = this.customHandlers.get(request.method);
      return await handler(request);
    }

    return super.handleRequest(request);
  }

  // Custom: Streaming results
  defineStreamingTool(server) {
    server.defineTool(
      "stream_data",
      "Stream large dataset in chunks",
      { dataset: z.string(), chunkSize: z.number().optional() },
      async function* ({ dataset, chunkSize = 1000 }) {
        const data = await this.loadDataset(dataset);
        
        for (let i = 0; i < data.length; i += chunkSize) {
          yield {
            chunk: Math.floor(i / chunkSize),
            data: data.slice(i, i + chunkSize),
            hasMore: i + chunkSize < data.length
          };
        }
      }
    );
  }

  // Custom: Progressive result refinement
  registerProgressiveMethod(methodName, computeFn) {
    this.registerCustomMethod(methodName, async (request) => {
      const results = [];
      let quality = 0.2; // Start with low quality

      while (quality <= 1.0) {
        const result = await computeFn(
          request.params,
          quality
        );

        results.push({
          quality,
          result,
          timestamp: Date.now()
        });

        quality += 0.2; // Increase quality incrementally
      }

      return results;
    });
  }

  // Custom: Async completion notification
  registerAsyncMethod(methodName, computeFn) {
    const callbacks = new Map();
    let callbackId = 0;

    this.registerCustomMethod(methodName, async (request) => {
      const id = ++callbackId;
      const callbackUrl = request.params.callbackUrl;

      // Start async computation
      computeFn(request.params).then(result => {
        // Notify via callback
        fetch(callbackUrl, {
          method: "POST",
          body: JSON.stringify({
            computationId: id,
            result,
            completedAt: new Date().toISOString()
          })
        });
      });

      return { computationId: id, status: "processing" };
    });
  }
}
```

---

## High-Performance Optimization

### Memory-Efficient Streaming

```javascript
class StreamingServer {
  defineStreamingResource(server) {
    server.defineResource(
      "stream://large-files/*",
      "Large files with streaming support",
      "application/octet-stream",
      async (uri) => {
        const filePath = uri.replace("stream://large-files/", "");
        
        // Use readable stream instead of loading entire file
        const stream = fs.createReadStream(filePath, {
          highWaterMark: 1024 * 1024 // 1MB chunks
        });

        return await this.streamToString(stream);
      }
    );
  }

  async streamToString(stream) {
    const chunks = [];
    
    for await (const chunk of stream) {
      chunks.push(chunk);
    }

    return Buffer.concat(chunks).toString();
  }

  defineLargeDatasetTool(server) {
    server.defineTool(
      "process_large_dataset",
      "Process large dataset with streaming",
      {
        datasetPath: z.string(),
        processor: z.string(),
        batchSize: z.number().optional()
      },
      async function* ({ datasetPath, processor, batchSize = 1000 }) {
        const reader = fs.createReadStream(datasetPath);
        let buffer = [];

        for await (const chunk of reader) {
          buffer.push(chunk);

          if (buffer.length >= batchSize) {
            const processed = await this.processChunk(buffer, processor);
            yield {
              batchSize: buffer.length,
              results: processed
            };
            buffer = [];
          }
        }

        // Process remaining
        if (buffer.length > 0) {
          const processed = await this.processChunk(buffer, processor);
          yield {
            batchSize: buffer.length,
            results: processed,
            isFinal: true
          };
        }
      }
    );
  }
}
```

### Zero-Copy Data Transfer

```javascript
class ZeroCopyServer {
  defineSharedMemoryResource(server) {
    server.defineResource(
      "shm://buffers/*",
      "Shared memory buffers for zero-copy data transfer",
      "application/octet-stream",
      async (uri) => {
        const bufferId = uri.replace("shm://buffers/", "");
        
        // Return reference to shared memory instead of copying
        const buffer = await this.getSharedBuffer(bufferId);
        
        return {
          bufferId,
          size: buffer.length,
          offset: 0,
          // Client must read from shared memory directly
          sharedMemoryKey: `shm_${bufferId}`
        };
      }
    );
  }

  defineZeroCopyTool(server) {
    server.defineTool(
      "process_shared_buffer",
      "Process data in shared memory without copying",
      {
        bufferId: z.string(),
        offset: z.number().optional(),
        length: z.number().optional()
      },
      async ({ bufferId, offset = 0, length }) => {
        const buffer = await this.getSharedBuffer(bufferId);
        const view = buffer.slice(offset, offset + length);

        // Process without copying
        const result = await this.inPlaceProcess(view);

        return {
          bufferId,
          processed: result.length,
          resultBufferId: `shm_result_${Date.now()}`
        };
      }
    );
  }

  async inPlaceProcess(buffer) {
    // Process buffer in-place using typed arrays
    const view = new Float32Array(buffer);
    
    for (let i = 0; i < view.length; i++) {
      view[i] = Math.sqrt(view[i]); // Example: square root
    }

    return buffer;
  }
}
```

---

## Enterprise Architecture

### Multi-Tenant Server

```javascript
class MultiTenantServer {
  constructor() {
    this.tenants = new Map();
    this.resourceQuotas = new Map();
  }

  initializeTenant(tenantId, config) {
    this.tenants.set(tenantId, {
      id: tenantId,
      config,
      tools: new Map(),
      resources: new Map(),
      dataStore: new Map()
    });

    this.resourceQuotas.set(tenantId, {
      maxRequests: config.maxRequests || 1000,
      maxStorage: config.maxStorage || 1024 * 1024 * 1024,
      currentRequests: 0,
      currentStorage: 0
    });
  }

  defineMultiTenantTool(server) {
    server.defineTool(
      "tenant_aware_operation",
      "Execute operation with tenant isolation",
      {
        tenantId: z.string(),
        operation: z.string(),
        params: z.record(z.unknown())
      },
      async ({ tenantId, operation, params }) => {
        const tenant = this.tenants.get(tenantId);
        
        if (!tenant) {
          throw new Error(`Tenant not found: ${tenantId}`);
        }

        // Check quota
        const quota = this.resourceQuotas.get(tenantId);
        if (quota.currentRequests >= quota.maxRequests) {
          throw new Error("Tenant quota exceeded");
        }

        // Execute with tenant context
        const result = await this.executeInTenantContext(
          tenant,
          operation,
          params
        );

        // Update quota
        quota.currentRequests++;

        return {
          tenantId,
          result,
          quotaUsage: {
            requests: quota.currentRequests,
            limit: quota.maxRequests
          }
        };
      }
    );
  }

  async executeInTenantContext(tenant, operation, params) {
    // Isolate execution to tenant's data and config
    const context = {
      tenantId: tenant.id,
      dataStore: tenant.dataStore,
      config: tenant.config
    };

    // Execute operation with context binding
    return await this.executeWithContext(operation, params, context);
  }
}
```

### Service Mesh Integration

```javascript
class ServiceMeshServer {
  constructor(serviceMeshConfig) {
    this.config = serviceMeshConfig;
    this.serviceRegistry = new Map();
    this.circuitBreakers = new Map();
  }

  registerMicroservice(name, endpoint, config = {}) {
    this.serviceRegistry.set(name, {
      name,
      endpoint,
      config,
      health: "healthy",
      lastHealthCheck: Date.now()
    });

    // Initialize circuit breaker for service
    this.circuitBreakers.set(name, new CircuitBreaker(
      config.circuitBreakerThreshold || 5
    ));
  }

  defineMicroserviceProxy(server, serviceName) {
    server.defineTool(
      `${serviceName}_call`,
      `Call ${serviceName} microservice`,
      {
        method: z.string(),
        params: z.record(z.unknown()).optional()
      },
      async ({ method, params = {} }) => {
        const service = this.serviceRegistry.get(serviceName);
        
        if (!service) {
          throw new Error(`Service not registered: ${serviceName}`);
        }

        const circuitBreaker = this.circuitBreakers.get(serviceName);

        return await circuitBreaker.execute(async () => {
          const response = await fetch(
            `${service.endpoint}/${method}`,
            {
              method: "POST",
              headers: {
                "Content-Type": "application/json",
                "X-Service-Mesh": this.config.meshName
              },
              body: JSON.stringify(params)
            }
          );

          if (!response.ok) {
            throw new Error(
              `Service error: ${response.status} ${response.statusText}`
            );
          }

          return await response.json();
        });
      }
    );
  }
}
```

---

## Machine Learning Integration

### ML Model Server

```javascript
class MLModelServer {
  constructor(modelRegistry) {
    this.modelRegistry = modelRegistry;
    this.inferenceCache = new Map();
    this.batchQueue = [];
    this.batchProcessor = null;
  }

  defineInferenceTool(server) {
    server.defineTool(
      "predict",
      "Run inference with ML model",
      {
        modelName: z.string(),
        input: z.record(z.number()),
        batchMode: z.boolean().optional()
      },
      async ({ modelName, input, batchMode = false }) => {
        const model = this.modelRegistry.get(modelName);
        
        if (!model) {
          throw new Error(`Model not found: ${modelName}`);
        }

        if (batchMode) {
          return await this.queueForBatchInference(model, input);
        }

        return await this.runInference(model, input);
      }
    );
  }

  async runInference(model, input) {
    // Check cache
    const cacheKey = this.getCacheKey(model.name, input);
    
    if (this.inferenceCache.has(cacheKey)) {
      const cached = this.inferenceCache.get(cacheKey);
      if (Date.now() - cached.timestamp < 3600000) {
        return cached.prediction;
      }
    }

    // Run model
    const startTime = Date.now();
    const prediction = await model.predict(input);
    const latency = Date.now() - startTime;

    // Cache result
    this.inferenceCache.set(cacheKey, {
      prediction,
      timestamp: Date.now()
    });

    return {
      prediction,
      latency,
      model: model.name,
      cached: false
    };
  }

  async queueForBatchInference(model, input) {
    return new Promise((resolve) => {
      this.batchQueue.push({
        model,
        input,
        resolve,
        timestamp: Date.now()
      });

      // Process batch when queue reaches threshold or timeout
      if (this.batchQueue.length >= 32 || !this.batchProcessor) {
        this.processBatch();
      } else if (!this.batchProcessor) {
        this.batchProcessor = setTimeout(() => this.processBatch(), 1000);
      }
    });
  }

  async processBatch() {
    if (this.batchQueue.length === 0) return;

    const batch = this.batchQueue.splice(0, 32);
    const startTime = Date.now();

    // Group by model
    const byModel = new Map();
    
    for (const item of batch) {
      if (!byModel.has(item.model.name)) {
        byModel.set(item.model.name, []);
      }
      byModel.get(item.model.name).push(item);
    }

    // Run batch inference per model
    for (const [modelName, items] of byModel) {
      const model = items[0].model;
      const inputs = items.map(item => item.input);
      
      const predictions = await model.batchPredict(inputs);

      items.forEach((item, index) => {
        item.resolve({
          prediction: predictions[index],
          latency: Date.now() - startTime,
          model: modelName,
          batched: true
        });
      });
    }

    clearTimeout(this.batchProcessor);
    this.batchProcessor = null;
  }

  getCacheKey(modelName, input) {
    return `${modelName}:${JSON.stringify(input)}`;
  }
}
```

### Feature Engineering Server

```javascript
class FeatureEngineeringServer {
  constructor() {
    this.featurePipeline = new Map();
    this.featureStore = new Map();
  }

  defineFeatureExtraction(server) {
    server.defineTool(
      "extract_features",
      "Extract engineered features from raw data",
      {
        datapoint: z.record(z.unknown()),
        features: z.array(z.string())
      },
      async ({ datapoint, features }) => {
        const engineered = {};

        for (const featureName of features) {
          if (this.featurePipeline.has(featureName)) {
            const pipeline = this.featurePipeline.get(featureName);
            engineered[featureName] = await pipeline(datapoint);
          }
        }

        return engineered;
      }
    );
  }

  registerFeature(name, extractorFn) {
    this.featurePipeline.set(name, extractorFn);
  }

  // Example features
  registerDefaultFeatures() {
    // Normalize numeric feature
    this.registerFeature("normalized_age", async (data) => {
      return (data.age - 25) / 20; // Assume mean 25, std 20
    });

    // Categorical encoding
    this.registerFeature("encoded_category", async (data) => {
      const categoryMap = { A: 0, B: 1, C: 2 };
      return categoryMap[data.category] || -1;
    });

    // Time-based feature
    this.registerFeature("day_of_week", async (data) => {
      return new Date(data.timestamp).getDay();
    });

    // Interaction feature
    this.registerFeature("interaction_age_category", async (data) => {
      const age = (data.age - 25) / 20;
      const category = data.category.charCodeAt(0);
      return age * category;
    });
  }
}
```

---

## Real-Time Streaming

### Event Stream Server

```javascript
class EventStreamServer {
  constructor() {
    this.streams = new Map();
    this.subscribers = new Map();
    this.eventBuffer = new Map();
  }

  defineEventStream(server, streamName) {
    server.defineResource(
      `event://stream/${streamName}`,
      `Real-time event stream: ${streamName}`,
      "application/json",
      async (uri) => {
        return JSON.stringify({
          stream: streamName,
          status: "active",
          subscribers: this.subscribers.get(streamName)?.size || 0,
          bufferedEvents: this.eventBuffer.get(streamName)?.length || 0
        });
      }
    );

    server.defineTool(
      `subscribe_${streamName}`,
      `Subscribe to ${streamName} stream`,
      {
        filter: z.string().optional(),
        bufferSize: z.number().optional()
      },
      async ({ filter, bufferSize = 100 }) => {
        const subscription = {
          id: this.generateSubscriptionId(),
          stream: streamName,
          filter: filter ? new RegExp(filter) : null,
          buffer: [],
          maxSize: bufferSize,
          subscriptionTime: Date.now()
        };

        if (!this.subscribers.has(streamName)) {
          this.subscribers.set(streamName, new Set());
        }

        this.subscribers.get(streamName).add(subscription);

        return {
          subscriptionId: subscription.id,
          stream: streamName,
          status: "subscribed"
        };
      }
    );
  }

  publishEvent(streamName, event) {
    // Buffer event
    if (!this.eventBuffer.has(streamName)) {
      this.eventBuffer.set(streamName, []);
    }

    const buffer = this.eventBuffer.get(streamName);
    buffer.push({
      ...event,
      timestamp: Date.now()
    });

    // Notify subscribers
    const subscribers = this.subscribers.get(streamName) || new Set();
    
    for (const subscription of subscribers) {
      if (!subscription.filter || subscription.filter.test(JSON.stringify(event))) {
        subscription.buffer.push(event);
        
        // Trim buffer
        if (subscription.buffer.length > subscription.maxSize) {
          subscription.buffer.shift();
        }
      }
    }
  }

  generateSubscriptionId() {
    return `sub_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`;
  }
}
```

---

## Production Hardening

### Comprehensive Health Monitoring

```javascript
class ProductionServer {
  constructor() {
    this.healthChecks = new Map();
    this.metrics = new Map();
    this.alerts = [];
  }

  registerHealthCheck(name, checkFn, interval = 5000, critical = false) {
    this.healthChecks.set(name, {
      name,
      checkFn,
      interval,
      critical,
      lastStatus: "unknown",
      lastCheck: null,
      failures: 0,
      consecutiveFailures: 0
    });

    this.runHealthCheck(name);
  }

  async runHealthCheck(name) {
    const check = this.healthChecks.get(name);
    
    try {
      await check.checkFn();
      check.lastStatus = "healthy";
      check.consecutiveFailures = 0;
    } catch (error) {
      check.lastStatus = "unhealthy";
      check.consecutiveFailures++;
      check.failures++;

      if (check.critical && check.consecutiveFailures >= 3) {
        this.alerts.push({
          severity: "critical",
          check: name,
          message: error.message,
          timestamp: Date.now()
        });
      }
    }

    check.lastCheck = Date.now();

    // Schedule next check
    setTimeout(() => this.runHealthCheck(name), check.interval);
  }

  getHealthStatus() {
    const status = {
      timestamp: Date.now(),
      overall: "healthy",
      checks: {}
    };

    for (const [name, check] of this.healthChecks) {
      status.checks[name] = {
        status: check.lastStatus,
        lastCheck: check.lastCheck,
        failures: check.failures
      };

      if (check.lastStatus === "unhealthy") {
        status.overall = "degraded";
        if (check.critical) {
          status.overall = "unhealthy";
        }
      }
    }

    return status;
  }

  getAlerts() {
    return this.alerts.filter(alert =>
      Date.now() - alert.timestamp < 3600000 // Last hour
    );
  }
}
```

### Graceful Degradation

```javascript
class ResilientServer {
  constructor() {
    this.degradedMode = false;
    this.readOnlyMode = false;
    this.toolOverrides = new Map();
  }

  async enterDegradedMode(reason) {
    console.warn(`Entering degraded mode: ${reason}`);
    this.degradedMode = true;

    // Disable non-essential tools
    this.disableTool("heavy_computation");
    this.disableTool("external_api_calls");

    // Enable fallbacks
    this.registerToolOverride("heavy_computation", async (args) => {
      return { cached: true, approximation: await this.getCachedApproximation(args) };
    });
  }

  async enterReadOnlyMode(reason) {
    console.error(`Entering read-only mode: ${reason}`);
    this.readOnlyMode = true;

    // Disable write operations
    this.disableTool("write_data");
    this.disableTool("delete_data");
    this.disableTool("modify_data");
  }

  registerToolOverride(toolName, overrideFn) {
    this.toolOverrides.set(toolName, overrideFn);
  }

  async getToolHandler(toolName) {
    if (this.toolOverrides.has(toolName)) {
      return this.toolOverrides.get(toolName);
    }
    return await this.getOriginalHandler(toolName);
  }

  async exitDegradedMode() {
    console.info("Exiting degraded mode");
    this.degradedMode = false;
    this.toolOverrides.clear();
  }
}
```

---

## Performance Benchmarking

```javascript
class PerformanceBenchmark {
  async benchmarkServer(server, testCases) {
    const results = [];

    for (const testCase of testCases) {
      const measurements = [];

      for (let i = 0; i < testCase.iterations || 100; i++) {
        const startTime = performance.now();
        
        try {
          await testCase.fn();
          measurements.push({
            duration: performance.now() - startTime,
            success: true
          });
        } catch (error) {
          measurements.push({
            duration: performance.now() - startTime,
            success: false,
            error: error.message
          });
        }
      }

      results.push({
        name: testCase.name,
        measurements,
        stats: this.calculateStats(measurements)
      });
    }

    return results;
  }

  calculateStats(measurements) {
    const durations = measurements
      .filter(m => m.success)
      .map(m => m.duration)
      .sort((a, b) => a - b);

    return {
      count: durations.length,
      min: Math.min(...durations),
      max: Math.max(...durations),
      mean: durations.reduce((a, b) => a + b, 0) / durations.length,
      median: durations[Math.floor(durations.length / 2)],
      p95: durations[Math.floor(durations.length * 0.95)],
      p99: durations[Math.floor(durations.length * 0.99)],
      errors: measurements.filter(m => !m.success).length
    };
  }
}
```

---

## Conclusion

Expert-level MCP mastery requires:

1. **Deep protocol understanding** - Optimize batch requests and correlation
2. **Domain expertise** - Build specialized servers for specific use cases
3. **Architectural patterns** - Composition, proxying, decoration
4. **Performance obsession** - Streaming, zero-copy, caching
5. **Enterprise standards** - Multi-tenancy, service mesh, monitoring
6. **Resilience planning** - Circuit breakers, graceful degradation
7. **Continuous optimization** - Benchmarking and metrics

---

**Last Updated**: February 2026  
**Difficulty**: Expert  
**Prerequisites**: Advanced MCP, systems design, production operations experience
