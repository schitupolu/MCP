# MCP
Model Context Protocol - Overview, how to secure and exmaples

### What is Model Context Protocol (MCP)?

As a result of the emergence of AI agents and RAG-based applications in recent years, there’s an increasing demand for customizing Large Language Models (LLMs) by integrating with external resources (e.g. RAG-based systems) and tools (e.g. Agent-based systems). This enhances LLMs’ existing capabilities by incorporating external knowledge and enabling autonomous task execution.

**Model Context Protocol (MCP)**, first introduced in November 2024 by Anthropic, has grown in popularity as it offers a more coherent and consistent way to connect LLMs with external tools and resources, making it a compelling alternative to building custom API integrations for each use case. MCP is a standardized, open-source protocol that provides a consistent interface that enable LLM to interact with various external tools and resources, hence allow end users to MCP server that has been encapsulated with enhanced functionalities. Compared to current agentic system design patterns, MCP offers several key benefits:

* Increase scalability and maintainability of the system through standardized integrations.
* Reduce duplicate development effort since a single MCP server implementation works with multiple MCP clients.
* Avoid vendor lock-in by providing flexibility to switch between LLM providers, since the LLM is no longer tightly coupled with the agentic system.
* Speed up the development process significantly by enabling rapid creation of workable products.

### MCP Architecture :

![MCP Architecture](/images/MCP_Architecture.png) 

The **Model Context Protocol** follows a **client-host-server** architecture: This separation of concerns allows for modular, composable systems where each server can focus on a specific domain (like file access, web search, or database operations).

**MCP Hosts**: Programs like Claude Desktop, IDEs, or your python application that want to access data through MCP

**MCP Clients**: Protocol clients that maintain 1:1 connection with servers

**MCP Servers**: Lightweight programs that each expose specific capabilities through the standardized Model Context Protocol (tools, resources, prompts)

**Local Data Sources**: Your computer’s files, databases, and services that MCP servers can securely access

**Remote Services**: External systems available over the internet (e.g., through APIs) that MCP servers can connect to

This separation of concerns allows for modular, composable systems where each server can focus on a specific domain (like file access, web search, or database operations).

The **Model Context Protocol (MCP)** addresses challenge by providing a standardized way for LLMs to connect with external data sources and tools—essentially a “universal remote” for AI apps. Released by Anthropic as an open-source protocol, MCP builds on existing function calling by eliminating the need for custom integration between LLMs and other apps. This means developers can build more capable, context-aware applications without reinventing the wheel for each combination of AI model and external system.

![MCP Learning Center](/images/MCP_learning_center.png) 

**MCP defines three core primitives that servers can implement**:

**Tools**: Model-controlled functions that LLMs can invoke (like API calls, computations)

**Resources**: Application-controlled data that provides context (like file contents, database records)

**Prompts**: User-controlled templates for LLM interactions

### MCP Core Components :

![MCP Core Components](/images/MCP_core_components.png)

1. **Host application**: LLMs that interact with users and initiate connections. This includes Claude Desktop, AI-enhanced IDEs like Cursor, and standard web-based LLM chat interfaces.
2. **MCP client**: Integrated within the host application to handle connections with MCP servers, translating between the host’s requirements and the Model Context Protocol. Clients are built into host applications, like the MCP client inside Claude Desktop.
3. **MCP server**: Adds context and capabilities, exposing specific functions to AI apps through MCP. Each standalone server typically focuses on a specific integration point, like GitHub for repository access or a PostgreSQL for database operations.
4. **Transport layer**: The communication mechanism between clients and servers. MCP supports two primary transport methods:
  * **STDIO (Standard Input/Output)**: Mainly local integrations where the server runs in the same environment as the client.
    * Uses standard input/output for communication
    * Ideal for local processes
  * **HTTP+SSE (Server-Sent Events)**: Remote connections, with HTTP for client requests and SS for server responses and streaming.
    * Uses HTTP with optional Server-Sent Events for streaming
    * HTTP POST for client-to-server messages

All communication in MCP uses JSON-RPC 2.0 as the underlying message standard, providing a standardized structure for requests, responses, and notifications.

### How MCP works

When a user interacts with a host application (an AI app) that supports MCP, several processes occur behind the scenes to enable quick and seamless communication between the AI and external systems. Let’s take a closer look at what happens when a user asks Claude Desktop to perform a task that invokes tools outside the chat window.

#### Protocol handshake
1.  **Initial connection**: When an MCP client (like Claude Desktop) starts up, it connects to the configured MCP servers on your device.
2.  **Capability discovery**: The client asks each server "What capabilities do you offer?" Each server responds with its available tools, resources, and prompts.
3.  **Registration**: The client registers these capabilities, making them available for the AI to use during your conversation.

![MCP Workflow](/images/MCP_workflow.png)

### Best practices

#### Transport selection

*Local communication*
 1. Use stdio transport for local processes
 2. Efficient for same-machine communication
 3. Simple process management
    
*Remote communication*
 * Use Streamable HTTP for scenarios requiring HTTP compatibility
 * Consider security implications including authentication and authorization

## Security Risks and Considerations for MCP

The **security of a Model Context Protocol (MCP)** implementation is critical, especially when you’re handling:

1. **User data**
2. **Conversation history**
3. **Potentially sensitive model responses**
4. **External API integration data**
5. **Long-lived or persistent memory**

And since most MCP setups today are custom — built on top of frameworks like LangChain, FastAPI, Redis, OpenAI APIs — the security depends entirely on **how well you design and enforce safeguards across your context management lifecycle**.

### Is MCP Secure by Default?

**No.**

Because MCP is typically **custom-built**, its security is entirely dependent on how well your architecture, context storage, API authentication, and data handling practices are implemented.

If you treat it as a first-class data and privacy boundary and apply solid security engineering practices — it can be

### Top 10 Security Risks in MCP

![MCP Security Risks](/images/MCP_Security_Risks.png)

### Security Risks in MCP Implementations

| Risk Category | Examples |
| --- | --- |
| Data Leakage | Exposing user conversations to other users or systems |
| Unauthorized Access | Redis DB or context store accessible without authentication |
| Injection Risks | Unvalidated inputs causing prompt injection (prompt hacking) |
| Token/Key Exposure | OpenAI API keys or external API credentials leaking |
| Context Integrity Risks | Tampered context data leading to unsafe or manipulated responses |
| Privacy Compliance Issues | Storing sensitive PII or regulated data without consent/protection |
| Denial of Service (DoS) | Malicious users flooding context storage or API endpoints |
