# Model Context Protocol (MCP) - Getting Started Guide

## Table of Contents
1. [What is MCP?](#what-is-mcp)
2. [Core Concepts](#core-concepts)
3. [Quick Start](#quick-start)
4. [Architecture](#architecture)
5. [Creating Your First MCP Server](#creating-your-first-mcp-server)
6. [Common Use Cases](#common-use-cases)
7. [Best Practices](#best-practices)
8. [Resources](#resources)

---

## What is MCP?

**Model Context Protocol (MCP)** is an open standard that enables AI models and applications to communicate with external tools, services, and data sources in a standardized way. Think of it as a universal adapter that allows Claude, ChatGPT, and other AI models to safely and efficiently access any backend system.

### Key Features
- **Standardized Communication**: Consistent interface for AI models to interact with tools
- **Secure by Default**: Built-in authentication and permission controls
- **Composable**: Combine multiple MCP servers seamlessly
- **Stateless Design**: Easy to scale and distribute
- **JSON-RPC Based**: Uses familiar, widely-supported protocol

---

## Core Concepts

### Client vs Server
- **MCP Client**: The AI application (Claude, VS Code extension, etc.) that makes requests
- **MCP Server**: The backend service that provides tools, resources, or data

### Three Main Types of Resources

#### 1. **Tools** (Functions)
Functions that the AI can call to perform actions.

```json
{
  "name": "get_user",
  "description": "Retrieve user information by ID",
  "inputSchema": {
    "type": "object",
    "properties": {
      "user_id": { "type": "string" }
    }
  }
}
```

#### 2. **Resources** (Data)
Files, documents, or data that can be read and analyzed.

```json
{
  "uri": "file:///path/to/document.txt",
  "name": "Important Document",
  "mimeType": "text/plain"
}
```

#### 3. **Prompts** (Templates)
Pre-configured prompts and context templates.

```json
{
  "name": "code_review",
  "description": "Prepare for code review task",
  "arguments": [
    { "name": "language", "description": "Programming language" }
  ]
}
```

---

## Quick Start

### Prerequisites
- Node.js 16+ or Python 3.8+
- Basic understanding of APIs
- An MCP client (Claude Desktop, VS Code, etc.)

### Installation

#### Using Node.js
```bash
npm install @modelcontextprotocol/sdk
```

#### Using Python
```bash
pip install mcp
```

---

## Architecture

### Request/Response Flow

```
┌─────────────┐
│  MCP Client │ (Claude, VS Code, etc.)
└──────┬──────┘
       │ JSON-RPC 2.0
       ▼
┌──────────────────┐
│  MCP Transport   │ (stdio, HTTP, WebSocket)
└──────┬───────────┘
       │
       ▼
┌─────────────────┐
│  MCP Server     │ (Your backend service)
└─────────────────┘
       │
       ▼
┌─────────────────┐
│  Backend System │ (Database, API, Files, etc.)
└─────────────────┘
```

### Supported Transports
- **stdio**: Local processes (default for local development)
- **HTTP**: REST endpoints
- **WebSocket**: Real-time bidirectional communication
- **SSE**: Server-sent events

---

## Creating Your First MCP Server

### Node.js Example

#### 1. Initialize Project
```bash
mkdir my-mcp-server
cd my-mcp-server
npm init -y
npm install @modelcontextprotocol/sdk
```

#### 2. Create Server (server.js)
```javascript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server({
  name: "my-mcp-server",
  version: "1.0.0",
});

// Define a tool
server.setRequestHandler(CallToolRequest, async (request) => {
  if (request.params.name === "greet") {
    return {
      content: [
        {
          type: "text",
          text: `Hello, ${request.params.arguments.name}!`
        }
      ]
    };
  }
  throw new Error("Unknown tool");
});

// Define tool list
server.setRequestHandler(ListToolsRequest, async () => {
  return {
    tools: [
      {
        name: "greet",
        description: "Greet someone by name",
        inputSchema: {
          type: "object",
          properties: {
            name: { type: "string" }
          }
        }
      }
    ]
  };
});

const transport = new StdioServerTransport();
await server.connect(transport);
```

#### 3. Run Server
```bash
node server.js
```

### Python Example

#### 1. Install MCP
```bash
pip install mcp
```

#### 2. Create Server (server.py)
```python
from mcp.server import Server
from mcp.types import Tool, TextContent, CallToolResult

server = Server("my-mcp-server")

@server.call_tool()
async def call_tool(name: str, arguments: dict):
    if name == "greet":
        return CallToolResult(
            content=[
                TextContent(
                    type="text",
                    text=f"Hello, {arguments.get('name')}!"
                )
            ]
        )
    raise ValueError(f"Unknown tool: {name}")

@server.list_tools()
async def list_tools():
    return [
        Tool(
            name="greet",
            description="Greet someone by name",
            inputSchema={
                "type": "object",
                "properties": {
                    "name": {"type": "string"}
                }
            }
        )
    ]

if __name__ == "__main__":
    server.run()
```

---

## Common Use Cases

### 1. **Database Access**
Create an MCP server that allows AI to query databases safely.
- Example: SQL query executor with pre-approved tables
- Benefit: AI can analyze data without direct database access

### 2. **File System Operations**
Expose file system capabilities in a controlled manner.
- Example: Read/write files in specific directories
- Benefit: AI can create, edit, and organize files safely

### 3. **API Integration**
Wrap third-party APIs with business logic.
- Example: GitHub API wrapper with custom authentication
- Benefit: Simplified access control and audit trails

### 4. **Code Analysis**
Tools for analyzing and understanding codebases.
- Example: Linting, formatting, complexity analysis
- Benefit: AI gets insights into code quality

### 5. **DevOps Automation**
Automate deployment and infrastructure tasks.
- Example: Deployment status, log retrieval, rollback
- Benefit: AI can assist with infrastructure decisions

### 6. **Knowledge Base**
Provide domain-specific knowledge to AI.
- Example: Company docs, best practices, runbooks
- Benefit: AI answers are grounded in your knowledge

---

## Best Practices

### 1. **Security First**
```javascript
// ✅ Good: Validate inputs and limit scope
if (!isValidUserId(userId)) {
  throw new Error("Invalid user ID");
}

// ❌ Bad: Direct string concatenation
const query = `SELECT * FROM users WHERE id = ${userId}`;
```

### 2. **Clear Tool Descriptions**
```javascript
{
  name: "create_file",
  description: "Create a new file in the workspace directory. " +
               "Only allows .txt and .md files. " +
               "Existing files will not be overwritten.",
  inputSchema: {
    type: "object",
    properties: {
      filename: { 
        type: "string",
        pattern: "\\.(txt|md)$"
      },
      content: { type: "string" }
    },
    required: ["filename", "content"]
  }
}
```

### 3. **Error Handling**
```javascript
try {
  const result = await executeQuery(params);
  return { success: true, data: result };
} catch (error) {
  return { 
    success: false, 
    error: error.message,
    code: error.code
  };
}
```

### 4. **Rate Limiting**
```javascript
const rateLimiter = new RateLimiter({
  maxRequests: 100,
  windowMs: 60000 // 1 minute
});

server.setRequestHandler(CallToolRequest, async (request) => {
  if (!rateLimiter.allow(request.clientId)) {
    throw new Error("Rate limit exceeded");
  }
  // ... handle request
});
```

### 5. **Logging and Monitoring**
```javascript
server.setRequestHandler(CallToolRequest, async (request) => {
  const startTime = Date.now();
  try {
    const result = await callTool(request);
    logger.info("Tool called", {
      tool: request.params.name,
      duration: Date.now() - startTime,
      status: "success"
    });
    return result;
  } catch (error) {
    logger.error("Tool error", {
      tool: request.params.name,
      error: error.message,
      duration: Date.now() - startTime
    });
    throw error;
  }
});
```

### 6. **Versioning**
```json
{
  "name": "my-server",
  "version": "1.0.0",
  "protocolVersion": "2024-11-05"
}
```

---

## Deployment

### Local Development
```bash
# Terminal 1: Start MCP Server
node server.js

# Terminal 2: Use with Claude Desktop or VS Code extension
# Configure client to connect to stdio transport
```

### Docker Deployment
```dockerfile
FROM node:20-slim
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "server.js"]
```

### Cloud Platforms
- **AWS**: Lambda + API Gateway
- **Google Cloud**: Cloud Functions
- **Azure**: Azure Functions
- **Heroku**: Direct deployment

---

## Testing Your MCP Server

### Using MCP Inspector

The MCP team provides a browser-based inspector for testing:

```bash
npm install -g @modelcontextprotocol/inspector
mcp-inspector node server.js
```

Then visit `http://localhost:5173` to test your server.

### Manual Testing with curl

```bash
# List tools
curl -X POST http://localhost:3000 \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc": "2.0", "id": 1, "method": "tools/list"}'

# Call tool
curl -X POST http://localhost:3000 \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "tools/call",
    "params": {
      "name": "greet",
      "arguments": {"name": "World"}
    }
  }'
```

---

## Resources

### Official Documentation
- [MCP Official Docs](https://modelcontextprotocol.io/)
- [GitHub Repository](https://github.com/anthropics/model-context-protocol)
- [SDK Reference](https://modelcontextprotocol.io/docs/concepts/architecture)

### Community & Examples
- [MCP Ecosystem](https://modelcontextprotocol.io/docs/tools)
- [Example Servers](https://github.com/anthropics/model-context-protocol/tree/main/examples)
- [Community Discord](https://discord.gg/modelcontextprotocol)

### Learning Paths
1. **Beginner**: Read core concepts → Build hello-world server
2. **Intermediate**: Integrate with real backend → Add authentication
3. **Advanced**: Build production server → Deploy to cloud → Monitor & scale

---

## Troubleshooting

### Common Issues

#### Server won't start
```bash
# Check Node version
node --version  # Should be 16+

# Verify dependencies
npm list @modelcontextprotocol/sdk

# Check logs
node server.js 2>&1 | grep -i error
```

#### Client can't connect
```bash
# Verify server is running
ps aux | grep node

# Check transport settings in config
cat ~/.config/Claude/claude_desktop_config.json

# Test with curl
curl http://localhost:3000
```

#### Tool not appearing in AI
- Verify `ListToolsRequest` returns the tool
- Check tool name matches exactly
- Ensure `inputSchema` is valid JSON Schema

---

## Next Steps

1. **Clone an example**: Start with existing MCP server templates
2. **Build for your use case**: Identify what your AI needs to access
3. **Test locally**: Use inspector and manual testing
4. **Deploy**: Choose your deployment platform
5. **Monitor**: Set up logging and alerting

---

**Last Updated**: February 2026  
**Status**: Actively Maintained
