# Module 04 — Introduction to MCP

<p align="center">
  <img src="https://img.shields.io/badge/Module-04-blue"/>
  <img src="https://img.shields.io/badge/Status-Completed-success"/>
  <img src="https://img.shields.io/badge/Skill%20Check-100%25-success"/>
</p>

---

## 📌 Module Overview

This module introduces the **Model Context Protocol (MCP)**, an open protocol designed to connect AI applications with external tools, data sources and services.

It explores the core concepts of MCP, its architecture, communication lifecycle and the role of MCP servers in extending AI agent capabilities.

The module also provides practical demonstrations of connecting MCP servers to AI agents using LangChain, Codex and real-world integrations.

The learning focus is on understanding how MCP enables AI agents to interact with external systems through standardized interfaces.

---

# 🎯 Learning Objectives

By completing this module, I aim to develop an understanding of:

* What the Model Context Protocol (MCP) is.
* Why MCP is important for AI agent development.
* Core components of MCP architecture.
* The role of MCP clients and MCP servers.
* How MCP tools, resources and prompts work.
* JSON-RPC 2.0 communication in MCP.
* The MCP connection lifecycle.
* How to add an MCP server to an AI agent.
* How MCP integrates with LangChain and Codex.
* Real-world applications of MCP.
* How external tools can extend AI agent capabilities.

---

# 📚 Module Contents

| # | Topic                                            | Duration | Status |
| - | ------------------------------------------------ | -------: | ------ |
| 1 | Module Intro                                     |    3 min | ✅      |
| 2 | What is Model Context Protocol                   |    7 min | ✅      |
| 3 | MCP Core Components                              |   11 min | ✅      |
| 4 | Add MCP Server to your first Agent               |   14 min | ✅   |
| 5 | Demo: MCP server with LangChain Client and Codex |    9 min | ✅      |
| 6 | Real-world MCP Walkthrough                       |   11 min | ✅    |
| 7 | Demo: Real World MCP Server                      |    8 min | ✅      |
| 8 | Summary                                          |    4 min | ✅    |
| 9 | Skill Check: Introduction to MCP                 |        — | ✅      |

> **Progress:** The first three lessons have been completed. The module is currently in progress.

---

# 🧠 Core Concepts

## 1. What is Model Context Protocol?

The **Model Context Protocol (MCP)** is a standardized protocol that allows AI applications to connect with external tools, resources and services.

It provides a common communication interface between AI agents and external systems.

Instead of building a separate custom integration for every tool, MCP enables AI applications to interact with compatible MCP servers through a standardized protocol.

### Simplified representation

```text
              AI APPLICATION
                    │
                    ▼
               MCP CLIENT
                    │
                    ▼
             MCP PROTOCOL
                    │
                    ▼
               MCP SERVER
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
        Tools    Resources   Prompts
          │         │         │
          └─────────┼─────────┘
                    ▼
           External Systems
```

The important idea is that MCP acts as a bridge between AI applications and external capabilities.

---

# 🧩 MCP Core Components

MCP consists of several important components that work together to enable communication between AI applications and external services.

## 1. MCP Host

The host is the AI application that provides the environment in which MCP clients operate.

Examples include AI assistants, agent applications and development environments.

### Responsibilities

* Manage AI interactions.
* Create and manage MCP clients.
* Coordinate communication with MCP servers.
* Provide context to the AI model.
* Control access to external capabilities.

---

## 2. MCP Client

The MCP client is the component responsible for communicating with an MCP server.

It is usually created and managed by the MCP host.

### Responsibilities

* Establish connections with MCP servers.
* Perform the MCP initialization handshake.
* Exchange JSON-RPC messages.
* Discover available tools and resources.
* Send requests to MCP servers.
* Receive and process responses.

---

## 3. MCP Server

An MCP server exposes external capabilities to AI applications through the MCP protocol.

It acts as the bridge between an AI agent and an external system.

### Responsibilities

* Expose tools.
* Provide resources.
* Provide prompts.
* Process client requests.
* Execute supported operations.
* Return structured results.

Examples of MCP servers include:

* File system server.
* Database server.
* GitHub server.
* Weather server.
* Search server.
* Custom business application server.

---

## 4. Tools

Tools are executable functions exposed by an MCP server.

They allow AI agents to perform actions beyond model-only generation.

Examples:

```text
search_database()
read_file()
create_ticket()
get_weather()
search_github()
```

A tool generally includes:

* Tool name.
* Description.
* Input schema.
* Execution logic.
* Result.

---

## 5. Resources

Resources represent data or information that an MCP server can provide to an AI application.

Examples include:

* Files.
* Documents.
* Database records.
* Application data.
* API responses.

Resources are primarily used to provide context and information to AI applications.

---

## 6. Prompts

Prompts are reusable prompt templates exposed by an MCP server.

They can help standardize common workflows and provide structured instructions to an AI application.

Examples:

```text
summarize_document
analyze_code
generate_report
review_database_schema
```

---

# 🔄 MCP Communication Architecture

A simplified MCP architecture can be represented as:

```text
                    AI AGENT
                       │
                       ▼
                     HOST
                       │
                       ▼
                    CLIENT
                       │
             JSON-RPC 2.0 Messages
                       │
                       ▼
                    SERVER
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
        Tools       Resources     Prompts
          │            │            │
          └────────────┼────────────┘
                       ▼
               External Services
```

This architecture separates the AI application from the implementation of external capabilities.

---

# 🌐 JSON-RPC 2.0 in MCP

MCP uses **JSON-RPC 2.0** as the message format for communication between clients and servers.

JSON-RPC stands for JavaScript Object Notation Remote Procedure Call.

It allows one system to request an operation from another system using structured JSON messages.

## Example Request

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/list"
}
```

### Important Fields

| Field     | Description                               |
| --------- | ----------------------------------------- |
| `jsonrpc` | Specifies the JSON-RPC version.           |
| `id`      | Identifies the request.                   |
| `method`  | Specifies the requested operation.        |
| `params`  | Contains method parameters when required. |

---

## Types of JSON-RPC Messages

### Request

A message that asks the server to perform an operation.

### Response

A message containing the result or error corresponding to a request.

### Notification

A message that does not expect a response.

Example:

```json
{
  "jsonrpc": "2.0",
  "method": "notifications/initialized"
}
```

---

# 🔌 MCP Connection Lifecycle

The MCP connection lifecycle describes how an MCP client establishes communication with an MCP server, performs operations and terminates the connection.

A traditional MCP lifecycle can be represented as:

```text
          CLIENT
             │
             ▼
      Create Connection
             │
             ▼
        Initialize
             │
             ▼
    Protocol Negotiation
             │
             ▼
    Capabilities Exchange
             │
             ▼
       Initialized
             │
             ▼
      Normal Operations
             │
             ▼
    Tool / Resource Calls
             │
             ▼
       Close Connection
```

## Initialization

The client sends an `initialize` request containing:

* Supported protocol version.
* Client capabilities.
* Client information.

The server responds with:

* Selected protocol version.
* Server capabilities.
* Server information.

The client then sends the `notifications/initialized` notification.

After successful initialization, normal MCP operations can begin.

---

# 🤖 Add MCP Server to Your First Agent

This lesson introduces the process of connecting an MCP server to an AI agent.

The objective is to extend an AI agent with external capabilities through MCP.

## General Workflow

```text
             AI AGENT
                 │
                 ▼
          Select MCP Server
                 │
                 ▼
          Configure Server
                 │
                 ▼
          Create MCP Client
                 │
                 ▼
          Connect to Server
                 │
                 ▼
          Discover Tools
                 │
                 ▼
          Agent Uses Tools
                 │
                 ▼
             Get Result
```

### Learning Focus

1. Understand the purpose of an MCP server.
2. Select a suitable MCP server.
3. Configure the server connection.
4. Connect the MCP client to the server.
5. Discover available tools.
6. Allow the AI agent to use the tools.
7. Process the returned results.
8. Evaluate the agent workflow.

The practical goal is to understand how external capabilities can be added to an existing AI agent.

---

# 🔬 MCP Server with LangChain Client and Codex

This lesson demonstrates an MCP server integration with a LangChain client and Codex.

The learning focus is on understanding how an AI agent can communicate with MCP servers and use their capabilities.

## Conceptual Architecture

```text
              AI AGENT
                  │
                  ▼
               CODEX
                  │
                  ▼
             MCP CLIENT
                  │
                  ▼
            MCP SERVER
                  │
                  ▼
              MCP TOOLS
                  │
                  ▼
          External Services
```

### Key Learning Areas

* MCP server configuration.
* MCP client communication.
* LangChain integration.
* Codex integration.
* Tool discovery.
* Tool execution.
* Processing tool results.
* Agent-to-server interaction.

This provides a practical bridge between MCP concepts and agent development frameworks.

---

# 🌍 Real-World MCP Walkthrough

This lesson introduces a real-world walkthrough of MCP usage.

The focus is on understanding how MCP can be used to connect AI agents with practical external systems.

## Real-World Use Cases

### 1. Database Interaction

An AI agent can use an MCP server to query databases and retrieve information.

```text
AI Agent
   ↓
MCP Database Server
   ↓
SQL Database
   ↓
Query Result
```

---

### 2. File System Interaction

An AI agent can interact with files through an MCP server.

Possible operations include:

* Reading files.
* Searching files.
* Accessing project information.
* Retrieving documents.

```text
AI Agent
   ↓
MCP File Server
   ↓
File System
   ↓
File Content
```

---

### 3. GitHub Integration

An MCP server can provide access to GitHub-related capabilities.

Examples include:

* Reading repositories.
* Searching code.
* Accessing issues.
* Working with pull requests.

```text
AI Agent
   ↓
MCP GitHub Server
   ↓
GitHub Repository
   ↓
Repository Information
```

---

### 4. API Integration

MCP can be used to expose external API capabilities to AI agents.

```text
AI Agent
   ↓
MCP Server
   ↓
External API
   ↓
API Response
```

The key idea is that MCP allows AI agents to interact with external systems through standardized interfaces.

---

# 🛠️ Demo: Real-World MCP Server

This lesson demonstrates a real-world MCP server implementation.

The learning focus is on understanding the practical structure of an MCP server and how it exposes capabilities to AI applications.

## General Server Architecture

```text
              MCP SERVER
                  │
        ┌─────────┼─────────┐
        ▼         ▼         ▼
      Tools    Resources   Prompts
        │         │         │
        └─────────┼─────────┘
                  ▼
           Business Logic
                  │
                  ▼
          External Services
```

### Practical Learning Focus

* MCP server structure.
* Tool registration.
* Request handling.
* Response generation.
* External service integration.
* AI agent communication.
* Testing MCP capabilities.

The objective is to understand how a real-world MCP server can expose useful functionality to AI agents.

---

# 🔐 MCP Security and Responsible Integration

MCP integrations can provide AI agents with access to external tools and data.

Therefore, security and access control are important when designing practical MCP systems.

Important considerations include:

* Validate tool inputs.
* Restrict access to sensitive resources.
* Use appropriate authentication.
* Limit unnecessary tool permissions.
* Protect API credentials.
* Avoid exposing unsafe operations.
* Validate external data.
* Monitor tool execution.
* Apply application-level guardrails.

A useful design principle is:

```text
External Capability
        +
Controlled Access
        +
Input Validation
        +
Monitoring
        =
Safer MCP Integration
```

---

# 🔬 My Work

My hands-on notes and experiments for this module are maintained in:

```text
my-work/
```

Recommended structure:

```text
my-work/
├── module-notes.md
├── mcp-concepts.md
├── json-rpc-and-lifecycle.md
├── first-mcp-agent/
│   └── README.md
├── langchain-mcp/
│   └── README.md
└── real-world-mcp/
    └── README.md
```

This section should contain my own understanding, implementation details, code experiments and MCP integration evidence.

---

# 📝 Summary

### Key Takeaways

* MCP is a standardized protocol for connecting AI applications with external capabilities.
* MCP uses a client-server architecture.
* MCP hosts manage MCP clients.
* MCP clients communicate with MCP servers.
* MCP servers expose tools, resources and prompts.
* JSON-RPC 2.0 defines the structure of MCP messages.
* The MCP lifecycle includes initialization, operation and shutdown.
* MCP tools allow AI agents to interact with external systems.
* MCP can integrate with frameworks such as LangChain and development tools such as Codex.
* Real-world MCP servers can connect AI agents with databases, APIs, files and other services.
* Secure access control and validation are important for practical MCP implementations.

---

# 🧪 Skill Check

### Assessment

**Skill Check:** Introduction to MCP

### Result

**Score:** 100%

**Passing Requirement:** To be updated

**Status:** Completed

The skill check will evaluate understanding of the Model Context Protocol, its components, communication process and practical AI agent integrations.

Detailed assessment notes will be maintained in:

```text
skill-check/
```

> Assessment questions themselves are not reproduced here. The repository focuses on concepts evaluated, learning outcomes and personal reflections.

---


# 📂 Module Structure

```text
04-introduction-to-mcp/
│
├── README.md
│
├── my-work/
│   ├── module-notes.md
│   ├── mcp-concepts.md
│   ├── json-rpc-and-lifecycle.md
│   │
│   ├── first-mcp-agent/
│   │   └── README.md
│   │
│   ├── langchain-mcp/
│   │   └── README.md
│   │
│   └── real-world-mcp/
│       └── README.md
│
├── summary/
│   └── key-takeaways.md
│
└── skill-check/
    ├── README.md
    └── result.md
```

---

# 🚀 Skills Gained

| Skill                               | Level             |
| ----------------------------------- | ----------------- |
| Model Context Protocol Fundamentals | 🟢 Foundation     |
| MCP Architecture                    | 🟢 Foundation     |
| MCP Core Components                 | 🟢 Foundation     |
| JSON-RPC 2.0                        | 🟢 Foundation     |
| MCP Connection Lifecycle            | 🟢 Foundation     |
| MCP Server Integration              | 🟢 Foundation     |
| LangChain MCP Integration           | 🟢 Foundation     |
| Real-World MCP Understanding        | 🟢 Foundation     |
| AI Agent Tool Integration           | 🟢 Foundation     |

---

## ➡️ Next Module

Continue to:

**Module 05 — Next Course Module**

Update the module link once the next module title and folder name are confirmed.

---

<p align="center">
  <b>From AI Agents to Connected Intelligence — Learning the Model Context Protocol.</b>
</p>
