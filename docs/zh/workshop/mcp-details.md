# MCP 生态详解

[MCP协议](https://modelcontextprotocol.io/) 是一种描述应用程序与 LLM 交互的协议，目前已经被多种产品采用。LangBot 可以作为 MCP Client 接入 MCP Server，大量扩展工具供 LLM 在与用户对话时使用。

## 寻找 MCP Server

要在 LangBot 使用 MCP 工具，需要找到已有的 MCP Server 并接入。  
市面上有两种类型的 MCP Server：

- 基于 node 或 python 实现的可执行文件，通过 `stdio`（标准输入输出）与 LangBot 通信
- 基于 http 协议的 web 服务，通过 http 协议与 LangBot 通信


:::info

- 可以到 [MCP Server 列表](https://github.com/punkpeye/awesome-mcp-servers) 查看已有的 MCP Server。
- 在线托管的 MCP Server 可以到 [Composio MCP](https://mcp.composio.dev/) 查找。
- 自行编写 MCP Server 可以参考 [MCP 协议文档](https://modelcontextprotocol.io/quickstart/server) 和 [MCP Server 示例](https://modelcontextprotocol.io/examples)。

:::

## 配置 MCP Server

查看 [系统设置文档](/zh/deploy/settings.html)

配置完成后即可在聊天中通过`!func`命令查看已经注册的 MCP 工具，在与支持 Function Calling 的模型对话时，LangBot 会自动调用 MCP 工具。