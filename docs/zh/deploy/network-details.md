# 网络配置详解

::: info
某些消息平台（如 QQ 个人号）需要使用独立的协议端来处理消息，如果您使用的是此类消息平台，请参考以下网络配置。  
同时，若您的 LangBot 实例需要连接其他在容器中运行的服务（如 Ollama），也可以参考以下配置，自行替换`消息平台`为`您要连接的服务`。
:::

LangBot 和部分消息平台均可采用 Docker 部署，以下是四种情况下的网络配置详解。

:::info 目录
[[toc]]
:::

## LangBot 和消息平台均运行在 Docker 容器中

如果消息平台（NapCat/Lagrange）和 LangBot 均使用 Docker 启动，那么你需要配置 Docker 的网络连接。

新建一个网络：

```bash
docker network create langbot-network
```

在 LangBot 目录的 `docker-compose.yaml` 文件中添加网络配置(添加到 `services.langbot` 字段下，并在 `networks` 字段下添加 `langbot-network` 网络配置)：

```yaml
services:
  langbot:
    ...
    networks:
      - langbot-network
    ...

networks:
  langbot-network:
    external: true
```

然后在消息平台的 `docker-compose.yaml` 文件中添加同样的网络配置（如果是直接 docker run 命令启动的，请在启动命令中添加 `--network langbot-network`）。接着在消息平台配置文件中，把 WS 反向连接地址中的 IP 地址修改为 `langbot`（例如：`ws://langbot:2280/ws`）。

重启两个容器。



## 仅 LangBot 运行在 Docker 容器中

当只有 LangBot 采用 Docker 部署时，默认已经映射 2280 到 2290 端口到容器外。此时 LangBot 只能作为 WebSocket 服务器，接受消息平台作为客户端连接。

请把消息平台设置为 ReverseWebSocket（称为 `反向 ws` 或 `WebSocket 客户端`），端口对应 LangBot 的 aiocqhttp 适配器启用的端口，连接本地 127.0.0.1 即可。


## LangBot 和消息平台都不使用 Docker 部署

根据文档配置消息平台和 LangBot 设置，两者端口设置为统一的不被占用的即可，都连接本地 127.0.0.1。

## 仅消息平台运行在 Docker 容器中（不建议）

:::warning
仅支持 Linux ，或其他支持 host 模式 docker 网络的系统。
:::

目前 LangBot 的 aiocqhttp 适配器仅支持 反向 WebSocket 连接，当消息平台运行在 Docker 容器中而 LangBot 直接运行在宿主机时，必须由 消息平台作为客户端连接 LangBot。此时只能将 消息平台的 network 设置为 `host` 模式，再设置其 WS 连接地址为 127.0.0.1，端口对应 LangBot 的 aiocqhttp 适配器启用的端口。
