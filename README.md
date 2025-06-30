# MCP
Model Context Protocol - Overview, how to secure and exmaples

### What is Model Context Protocol (MCP)?

As a result of the emergence of AI agents and RAG-based applications in recent years, there’s an increasing demand for customizing Large Language Models (LLMs) by integrating with external resources (e.g. RAG-based systems) and tools (e.g. Agent-based systems). This enhances LLMs’ existing capabilities by incorporating external knowledge and enabling autonomous task execution.

**Model Context Protocol (MCP)**, first introduced in November 2024 by Anthropic, has grown in popularity as it offers a more coherent and consistent way to connect LLMs with external tools and resources, making it a compelling alternative to building custom API integrations for each use case. MCP is a standardized, open-source protocol that provides a consistent interface that enable LLM to interact with various external tools and resources, hence allow end users to MCP server that has been encapsulated with enhanced functionalities. Compared to current agentic system design patterns, MCP offers several key benefits:

* Increase scalability and maintainability of the system through standardized integrations.
* Reduce duplicate development effort since a single MCP server implementation works with multiple MCP clients.
* Avoid vendor lock-in by providing flexibility to switch between LLM providers, since the LLM is no longer tightly coupled with the agentic system.
* Speed up the development process significantly by enabling rapid creation of workable products.
