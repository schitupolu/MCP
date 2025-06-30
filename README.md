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

![MCP Architecture](/images/MCP_Architecture.png)
