# Lab 6: Creating MCP Servers and Custom Modes

## Overview

In this advanced lab, you'll learn how to extend Bob's capabilities by creating custom Model Context Protocol (MCP) servers and custom modes. This allows you to integrate Bob with your organization's tools, APIs, and workflows, making Bob even more powerful and tailored to your specific needs.

> **🔧 Bob Differentiator: [Extensible Architecture](../bob-differentiators.md#1--extensible-architecture)**
> This lab showcases Bob's most powerful differentiator—its extensible architecture. Through customizable modes and MCP server integrations, Bob adapts to YOUR environment and workflows. Unlike other AI assistants that work in isolation, Bob can connect to internal APIs, databases, documentation systems, and custom tools. This extensibility makes Bob uniquely valuable for enterprise teams with specific needs and existing toolchains.

**Duration:** 75-90 minutes
**Difficulty:** Advanced
**Prerequisites:** Completion of Labs 1-5, understanding of REST APIs, Node.js or Python experience

## Learning Objectives

By the end of this lab, you will be able to:

1. Understand the Model Context Protocol (MCP) architecture
2. Create a custom MCP server from scratch
3. Implement MCP server endpoints and tools
4. Integrate external APIs and services with Bob
5. Create custom Bob modes for specific workflows
6. Deploy and configure MCP servers
7. Test and debug MCP integrations
8. Share custom modes with your team

## What is MCP?

**Model Context Protocol (MCP)** is an open protocol that enables AI assistants like Bob to:
- Access external data sources
- Execute custom tools and functions
- Integrate with third-party services
- Extend capabilities beyond built-in features

> **🎯 Why MCP Matters**
> MCP is a key part of Bob's [extensible architecture](../bob-differentiators.md#mcp-server-integration). It allows Bob to integrate with your company's internal tools, APIs, and services. This means Bob can access your documentation, query your databases, create tickets in your issue tracker, and deploy to your infrastructure—all through natural language. Bob adapts to YOUR environment, not the other way around.

**Key Concepts:**
- **MCP Server**: A service that exposes tools and resources to Bob
- **Tools**: Functions that Bob can call to perform actions
- **Resources**: Data sources that Bob can query
- **Prompts**: Pre-defined prompt templates
- **Custom Mode**: A specialized Bob configuration for specific tasks

## Lab Structure

```
lab6/
├── README.md                           # This file
├── mcp-server/                         # MCP server implementation
│   ├── package.json                    # Node.js dependencies
│   ├── server.js                       # Main server implementation
│   ├── tools/                          # Tool implementations
│   │   ├── jira-tools.js              # JIRA integration
│   │   ├── database-tools.js          # Database queries
│   │   └── deployment-tools.js        # Deployment automation
│   ├── resources/                      # Resource providers
│   │   ├── documentation.js           # Doc access
│   │   └── metrics.js                 # System metrics
│   └── config/                         # Configuration
│       ├── server-config.json         # Server settings
│       └── tools-config.json          # Tool definitions
├── custom-mode/                        # Custom mode definitions
│   ├── devops-mode.json               # DevOps workflow mode
│   ├── code-review-mode.json          # Code review mode
│   └── architecture-mode.json         # Architecture design mode
├── examples/                           # Usage examples
│   ├── using-jira-integration.md      # JIRA examples
│   ├── database-queries.md            # Database examples
│   └── deployment-automation.md       # Deployment examples
└── deployment/                         # Deployment guides
    ├── docker-compose.yml             # Docker deployment
    ├── kubernetes.yaml                # K8s deployment
    └── deployment-guide.md            # Deployment instructions
```

## Part 1: Understanding MCP Architecture (Read Only - No Actions Required)

> **📖 This section is informational only. No actions are required yet.**

### Step 1.1: MCP Protocol Basics

MCP uses a client-server architecture:

```
┌─────────────┐         MCP Protocol        ┌─────────────┐
│             │◄──────────────────────────►│             │
│  Bob Client │    JSON-RPC over stdio     │ MCP Server  │
│             │    or HTTP/WebSocket       │             │
└─────────────┘                            └─────────────┘
       │                                          │
       │                                          │
       ▼                                          ▼
  User Requests                            External Services
  - Ask questions                          - JIRA API
  - Execute tasks                          - Database
  - Get information                        - Deployment tools
                                          - Custom APIs
```

**Key Components:**

1. **Tools**: Functions Bob can call
   ```json
   {
     "name": "create_jira_ticket",
     "description": "Create a new JIRA ticket",
     "parameters": {
       "title": "string",
       "description": "string",
       "priority": "string"
     }
   }
   ```

2. **Resources**: Data Bob can access
   ```json
   {
     "uri": "docs://api-reference",
     "name": "API Documentation",
     "mimeType": "text/markdown"
   }
   ```

3. **Prompts**: Pre-defined templates
   ```json
   {
     "name": "code_review",
     "description": "Perform code review",
     "template": "Review this code for: {criteria}"
   }
   ```

### Step 1.2: MCP Server Lifecycle

```
1. Initialize → 2. Register Tools → 3. Handle Requests → 4. Cleanup
     │                  │                    │               │
     │                  │                    │               │
     ▼                  ▼                    ▼               ▼
  Setup            Define tools        Execute tools    Close connections
  connections      and resources       return results   cleanup resources
```

## Part 2: Creating Your First MCP Server

> **✅ ACTION REQUIRED: Complete Steps 2.1-2.4**

### Step 2.1: Initialize MCP Server Project

**🔨 ACTION: Set up the MCP server**

The MCP server files are already provided in `lab6/mcp-server/`. Install dependencies:

```bash
cd lab6/mcp-server
npm install
```

This will install:
- `@modelcontextprotocol/sdk` - MCP protocol implementation
- `express` - Web server framework
- `axios` - HTTP client
- `dotenv` - Environment variable management
- `winston` - Logging

> **💡 OPTIONAL: Using Bob UI for Setup**
>
> If you prefer, you can use Bob to help with setup:
> 1. Open Bob in VS Code
> 2. Switch to **Advanced mode** (required for MCP server configuration)
> 3. Ask Bob: "Help me set up an MCP server project in lab6/mcp-server"
> 4. Bob will guide you through the setup process

### Step 2.2: Examine the MCP Server Implementation

**📖 REVIEW: Understand the server structure**

Open and examine the main server file:

**File: `mcp-server/server.js`**

This file implements a basic MCP server with tool registration and request handling. The server:
- Initializes the MCP protocol
- Registers available tools
- Handles tool execution requests
- Manages resources and prompts
- Provides error handling and logging

Key features:
- **Tool Registration**: Defines what Bob can do
- **Request Handling**: Processes Bob's requests
- **Resource Management**: Provides access to data
- **Error Handling**: Graceful failure management

### Step 2.3: Review Tool Implementations

**📖 REVIEW: Examine the tool files**

Tools are the core functionality of your MCP server. The following tools are already implemented:

**File: `mcp-server/tools/jira-tools.js`**

This file implements JIRA integration tools:
- `create_ticket`: Create new JIRA tickets
- `update_ticket`: Update existing tickets
- `search_tickets`: Search for tickets
- `get_ticket`: Get ticket details
- `add_comment`: Add comments to tickets

Each tool:
- Validates input parameters
- Calls JIRA API
- Handles errors
- Returns structured results

### Step 2.4: Review Resource Implementations

**📖 REVIEW: Examine the resource files**

Resources provide Bob with access to data. The following resources are already implemented:

**File: `mcp-server/resources/documentation.js`**

This file provides access to documentation:
- API documentation
- Architecture diagrams
- Runbooks
- Best practices guides

Resources can be:
- Static files
- Dynamic queries
- External API calls
- Database queries

## Part 3: Advanced Tool Implementation (Read Only - No Actions Required)

> **📖 This section explains the advanced tools already implemented. No actions required.**

### Step 3.1: Database Query Tool

**📖 REVIEW: Understanding database tools**

The database tool is already implemented in:

**File: `mcp-server/tools/database-tools.js`**

Features already included:
- Execute read-only queries
- Get table schemas
- Analyze query performance
- Generate reports

**Security Considerations:**
- Read-only access
- Query validation
- SQL injection prevention
- Rate limiting
- Audit logging

### Step 3.2: Deployment Automation Tool

**📖 REVIEW: Understanding deployment tools**

The deployment tool is already implemented in:

**File: `mcp-server/tools/deployment-tools.js`**

Capabilities already included:
- Deploy applications
- Rollback deployments
- Check deployment status
- View deployment logs
- Manage environments

**Safety Features:**
- Approval workflows
- Rollback capabilities
- Health checks
- Notification integration

### Step 3.3: Custom Business Logic (Optional Extension)

**💡 OPTIONAL: This is an example for extending the server**

You can implement organization-specific tools like this:

```javascript
// Example: Customer lookup tool
async function lookupCustomer(customerId) {
  // Validate input
  if (!customerId) {
    throw new Error('Customer ID required');
  }
  
  // Call internal API
  const response = await fetch(`${API_BASE}/customers/${customerId}`, {
    headers: {
      'Authorization': `Bearer ${API_TOKEN}`
    }
  });
  
  // Return structured data
  return {
    customer: await response.json(),
    metadata: {
      timestamp: new Date().toISOString(),
      source: 'internal-api'
    }
  };
}
```

## Part 4: Creating Custom Modes (Read Only - No Actions Required)

> **📖 This section explains custom modes. The mode files are already provided.**

### Step 4.1: Understanding Custom Modes

> **🎯 Bob Differentiator: [Customizable Modes](../bob-differentiators.md#customizable-modes)**
> Custom modes are another key differentiator for Bob. You can create specialized modes for code review, documentation, architecture design, DevOps workflows, or any team-specific process. These modes can be shared through the marketplace, ensuring consistent behavior across your team. This level of customization is unique to Bob.

Custom modes configure Bob for specific workflows:

```json
{
  "name": "DevOps Mode",
  "description": "Specialized mode for DevOps tasks",
  "capabilities": [
    "deployment",
    "monitoring",
    "incident-response"
  ],
  "tools": [
    "deploy_application",
    "check_health",
    "view_logs"
  ],
  "prompts": [
    "deployment_checklist",
    "incident_runbook"
  ]
}
```

### Step 4.2: DevOps Mode

**File: `custom-mode/devops-mode.json`**

This mode is optimized for DevOps workflows:

**Features:**
- Deployment automation
- Infrastructure management
- Monitoring and alerting
- Incident response
- Log analysis

**Tools Available:**
- `deploy`: Deploy applications
- `rollback`: Rollback deployments
- `scale`: Scale services
- `logs`: View logs
- `metrics`: Get metrics
- `alert`: Create alerts

**Prompts:**
- Deployment checklist
- Incident response runbook
- Post-mortem template
- Change request template

### Step 4.3: Code Review Mode

**File: `custom-mode/code-review-mode.json`**

Specialized for code reviews:

**Features:**
- Automated code analysis
- Security scanning
- Best practices checking
- Performance analysis
- Documentation review

**Tools:**
- `analyze_code`: Deep code analysis
- `check_security`: Security scan
- `review_pr`: PR review
- `suggest_improvements`: Improvement suggestions

**Prompts:**
- Code review checklist
- Security review template
- Performance review guide

### Step 4.4: Architecture Mode

**File: `custom-mode/architecture-mode.json`**

For architecture and design:

**Features:**
- System design assistance
- Architecture documentation
- Technology recommendations
- Scalability analysis
- Cost estimation

**Tools:**
- `design_system`: System design help
- `evaluate_tech`: Technology evaluation
- `estimate_cost`: Cost estimation
- `generate_diagram`: Architecture diagrams

## Part 5: Testing Your MCP Server

> **✅ ACTION REQUIRED: Complete Steps 5.1-5.3 to test your MCP server**

### Step 5.1: Configure MCP Server in Bob

**🔨 ACTION: Configure the MCP server in Bob**

Follow these steps to connect your MCP server to Bob:

1. Open Bob Settings (gear icon)
2. Navigate to **MCP** section
3. Choose configuration scope:
   - **Global MCPs** - Available across all projects
   - **Project MCPs** - Only available in current project
4. Click to edit the JSON configuration file
5. Add your server configuration:
   ```json
   {
     "mcpServers": {
       "my-custom-server": {
         "command": "node",
         "args": ["server.js"],
         "cwd": "/absolute/path/to/lab6/mcp-server"
       }
     }
   }
   ```
6. Save the file
7. Restart Bob or reload VS Code

> **⚠️ Important:** While you can configure MCP servers in any mode, MCP tools can only be used when Bob is in **Advanced mode**. Make sure to switch to Advanced mode before testing your MCP server tools.

### Step 5.2: Start and Test Your Server

**🔨 ACTION: Start the server and test it with Bob**

1. **Start the MCP server:**
   ```bash
   cd lab6/mcp-server
   node server.js
   ```

2. **Switch Bob to Advanced mode** (required to use MCP tools)

3. Test your MCP server tools by asking Bob:
   - "What MCP servers are connected?"
   - "Create a JIRA ticket for bug fix: Login page not loading"
   - "Show me the top 10 customers by revenue"
   - "Deploy version 2.1.0 to staging environment"

Bob will automatically use the appropriate tools from your MCP server when in Advanced mode.

### Step 5.3: Integration Testing (Optional)

**💡 OPTIONAL: The test file is already created at `test/integration.test.js`**

To run the integration tests:

```bash
cd lab6/mcp-server
npm test
```

The test file includes:

```javascript
// test/integration.test.js
const { MCPClient } = require('@modelcontextprotocol/sdk');

describe('MCP Server Integration', () => {
  let client;
  
  beforeAll(async () => {
    client = new MCPClient({
      serverCommand: 'node',
      serverArgs: ['server.js']
    });
    await client.connect();
  });
  
  test('should list available tools', async () => {
    const tools = await client.listTools();
    expect(tools).toContain('create_jira_ticket');
  });
  
  test('should execute tool successfully', async () => {
    const result = await client.callTool('create_jira_ticket', {
      title: 'Test ticket',
      description: 'Test description'
    });
    expect(result.success).toBe(true);
  });
  
  afterAll(async () => {
    await client.disconnect();
  });
});
```

## Part 6: Deployment (Optional)

> **💡 OPTIONAL: Deploy the MCP server using Docker or Kubernetes**

### Step 6.1: Docker Deployment

**🔨 OPTIONAL ACTION: Deploy with Docker Compose**

The deployment files are already configured. To deploy:

```bash
# Build and start
cd lab6/deployment
docker-compose up -d

# View logs
docker-compose logs -f mcp-server

# Stop
docker-compose down
```

### Step 6.2: Kubernetes Deployment

**🔨 OPTIONAL ACTION: Deploy with Kubernetes**

The Kubernetes configuration is already provided. To deploy:

```bash
# Apply configuration
kubectl apply -f kubernetes.yaml

# Check status
kubectl get pods -l app=mcp-server

# View logs
kubectl logs -l app=mcp-server -f

# Scale
kubectl scale deployment mcp-server --replicas=3
```

### Step 6.3: Configuration Management

Manage configuration securely:

```bash
# Store secrets in environment variables
export JIRA_API_TOKEN="your-token"
export DATABASE_URL="your-db-url"

# Or use secrets management
kubectl create secret generic mcp-secrets \
  --from-literal=jira-token="${JIRA_API_TOKEN}" \
  --from-literal=db-url="${DATABASE_URL}"
```

## Part 7: Best Practices (Read Only - Reference Material)

> **📖 This section provides best practices for reference. No actions required.**

### 7.1: Security Best Practices

1. **Authentication & Authorization**
   - Use API tokens, not passwords
   - Implement role-based access control
   - Validate all inputs
   - Use HTTPS for all communications

2. **Data Protection**
   - Encrypt sensitive data
   - Don't log secrets
   - Implement rate limiting
   - Use secure credential storage

3. **Audit & Monitoring**
   - Log all tool executions
   - Monitor for suspicious activity
   - Set up alerts
   - Regular security reviews

### 7.2: Performance Best Practices

1. **Caching**
   - Cache frequently accessed data
   - Implement cache invalidation
   - Use appropriate TTLs

2. **Async Operations**
   - Use async/await for I/O
   - Implement timeouts
   - Handle concurrent requests

3. **Resource Management**
   - Connection pooling
   - Proper cleanup
   - Memory management

### 7.3: Reliability Best Practices

1. **Error Handling**
   - Graceful degradation
   - Meaningful error messages
   - Retry logic with backoff
   - Circuit breakers

2. **Monitoring**
   - Health checks
   - Metrics collection
   - Logging
   - Alerting

3. **Testing**
   - Unit tests
   - Integration tests
   - Load testing
   - Security testing

## Part 8: Advanced Topics (Read Only - Reference Material)

> **📖 This section covers advanced topics for reference. No actions required.**

### 8.1: Multi-Server Architecture

**💡 REFERENCE: How to configure multiple MCP servers**

1. Open Bob Settings (gear icon) → MCP
2. Edit the Global or Project MCP configuration JSON
3. Add multiple servers:
   ```json
   {
     "mcpServers": {
       "jira-server": {
         "command": "node",
         "args": ["jira-server.js"],
         "cwd": "/path/to/jira-server"
       },
       "db-server": {
         "command": "node",
         "args": ["db-server.js"],
         "cwd": "/path/to/db-server"
       },
       "deploy-server": {
         "command": "node",
         "args": ["deploy-server.js"],
         "cwd": "/path/to/deploy-server"
       }
     }
   }
   ```
4. Save and restart Bob

When you ask Bob (in Advanced mode) to "Create a JIRA ticket and deploy the fix", it will intelligently use tools from multiple servers.

### 8.2: Custom Protocol Extensions

Extend MCP with custom capabilities:

```javascript
// Custom protocol extension
class CustomMCPServer extends MCPServer {
  async handleCustomRequest(request) {
    // Custom logic
    return {
      result: 'custom response'
    };
  }
}
```

### 8.3: AI Model Integration

Integrate with custom AI models:

```javascript
// Use custom model for specific tasks
async function analyzeWithCustomModel(code) {
  const response = await fetch('https://your-model-api.com/analyze', {
    method: 'POST',
    body: JSON.stringify({ code }),
    headers: { 'Content-Type': 'application/json' }
  });
  return await response.json();
}
```

## Exercises (Optional Extensions)

> **💡 OPTIONAL: These are suggested exercises to extend your learning**

### Exercise 1: Create a Slack Integration

**💡 OPTIONAL EXERCISE**

Create an MCP server that integrates with Slack:
- Send messages
- Create channels
- Get channel history
- Post code snippets

### Exercise 2: Build a Monitoring Dashboard

Create tools for system monitoring:
- Get system metrics
- View application logs
- Check service health
- Generate reports

### Exercise 3: Implement CI/CD Integration

Create deployment automation:
- Trigger builds
- Deploy to environments
- Run tests
- Rollback if needed

## Part 9: Managing Custom Modes and MCP Servers (Optional)

> **💡 OPTIONAL: Learn how to manage modes and servers**

### Step 9.1: Installing Custom Modes

**💡 OPTIONAL: How to install custom modes**

1. Open Bob Settings
2. Navigate to **Custom Modes**
3. Click **Import Mode**
4. Select your mode file (e.g., `devops-mode.json`)
5. The mode appears in Bob's mode selector

### Step 9.2: Removing Custom Modes

**To remove a custom mode:**

1. Open Bob Settings
2. Navigate to **Custom Modes**
3. Find the mode you want to remove
4. Click the **trash/delete icon** next to the mode
5. Confirm deletion

**Alternative - Manual removal:**
- Custom modes are stored in: `~/.bob/modes/`
- Delete the JSON file for the mode you want to remove
- Restart VS Code

### Step 9.3: Removing MCP Servers

**To remove an MCP server:**

1. Open Bob Settings (gear icon)
2. Navigate to **MCP** section
3. Choose **Global MCPs** or **Project MCPs**
4. Edit the JSON configuration file
5. Remove the server entry from the `mcpServers` object
6. Save the file
7. Restart Bob or reload VS Code

**Configuration file locations:**
- Global MCPs: `~/.bob/mcp.json`
- Project MCPs: `.bob/mcp.json` in your project root

**Example - Removing a server:**
```json
{
  "mcpServers": {
    "my-custom-server": {
      "command": "node",
      "args": ["server.js"],
      "cwd": "/path/to/server"
    },
    "server-to-remove": {  // Delete this entire block
      "command": "node",
      "args": ["other-server.js"],
      "cwd": "/path/to/other"
    }
  }
}
```

After removal:
```json
{
  "mcpServers": {
    "my-custom-server": {
      "command": "node",
      "args": ["server.js"],
      "cwd": "/path/to/server"
    }
  }
}
```

> **💡 Tip:** Keep a backup of your MCP configuration before making changes, so you can easily restore servers if needed.

## Troubleshooting

### Common Issues

1. **Server Won't Start**
   - Check server logs in terminal
   - Verify dependencies: `npm install` in server directory
   - Check configuration files in `config/`
   - Ensure ports aren't already in use

2. **Tools Not Available in Bob**
   - **Most Common:** Verify you're in **Advanced mode** - MCP tools only work in Advanced mode
   - Check MCP server is configured in Bob Settings → MCP (Global or Project)
   - Verify the server is running: `ps aux | grep node`
   - Check server logs for errors in the terminal
   - Restart the MCP server and reload VS Code
   - Verify the `cwd` path in your MCP configuration is correct

3. **Authentication Failures**
   - Check environment variables are set
   - Verify API tokens haven't expired
   - Test API directly with curl
   - Check server logs for auth errors

4. **Custom Mode Not Working**
   - Verify mode file is valid JSON
   - Check mode is enabled in Bob Settings
   - Restart VS Code after importing
   - Review mode configuration for errors

## Summary

In this lab, you learned:

✅ Understanding MCP architecture and protocol
✅ Creating custom MCP servers from scratch
✅ Implementing tools for external integrations
✅ Creating custom Bob modes for specific workflows
✅ Deploying MCP servers (Docker, Kubernetes)
✅ Testing and debugging MCP integrations
✅ Security and performance best practices
✅ Advanced topics and extensions

> **🎯 Extensibility: Bob's Superpower**
> You've now experienced Bob's [extensible architecture](../bob-differentiators.md#1--extensible-architecture) firsthand. By creating MCP servers and custom modes, you can tailor Bob to your organization's unique needs. This extensibility—combined with Bob's other differentiators like [intelligent resource optimization](../bob-differentiators.md#2--intelligent-resource-optimization), [Bob Findings](../bob-differentiators.md#3--bob-findings-automated-analysis-engine), and [Java modernization](../bob-differentiators.md#4--enterprise-java-modernization)—makes Bob a uniquely powerful tool for enterprise development teams.

## Next Steps

- Deploy your MCP server to production
- Create organization-specific tools
- Share custom modes with your team
- Contribute to the MCP ecosystem
- Explore advanced MCP features

## Additional Resources

- [MCP Protocol Specification](https://modelcontextprotocol.io/docs)
- [MCP SDK Documentation](https://github.com/modelcontextprotocol/sdk)
- [Bob MCP Integration Guide](https://ibm.com/bob/docs/mcp)
- [Example MCP Servers](https://github.com/modelcontextprotocol/servers)
- [Community MCP Servers](https://github.com/topics/mcp-server)

---

**Need Help?** If you encounter issues:
1. Check the troubleshooting section
2. Review the MCP documentation
3. Test with the example servers
4. Ask in the Bob community forums

**Feedback:** Help us improve this lab by sharing your experience and suggestions!

**Congratulations!** You've completed all 6 labs of the Bob Bootcamp. You now have comprehensive knowledge of Bob's capabilities and how to leverage them in your development workflow.