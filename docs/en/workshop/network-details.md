# Network Configuration Details

::: info
Some messaging platforms (such as personal QQ accounts) require an independent protocol endpoint to process messages. If you are using such messaging platforms, please refer to the following network configuration.  
At the same time, if your LangBot instance needs to connect to other services running in containers (such as Ollama), you can also refer to the following configuration, replacing `messaging platform` with `the service you want to connect to`.
:::

LangBot and some messaging platforms can both be deployed using Docker. Below are network configuration details for four different scenarios.

:::info Table of Contents
[[toc]]
:::

## Both LangBot and Messaging Platform Running in Docker Containers

If the messaging platform (NapCat/Lagrange) and LangBot are both started using Docker, you need to configure Docker's network connection.

Create a new network:

```bash
docker network create langbot-network
```

Add network configuration to the `docker-compose.yaml` file in the LangBot directory (add to the `services.langbot` field, and add the `langbot-network` network configuration under the `networks` field):

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

Then add the same network configuration to the messaging platform's `docker-compose.yaml` file (if started directly with docker run command, add `--network langbot-network` to the startup command). Then in the messaging platform configuration file, change the IP address in the WS reverse connection address to `langbot` (for example: `ws://langbot:2280/ws`).

Restart both containers.



## Only LangBot Running in Docker Container

When only LangBot is deployed using Docker, ports 2280 to 2290 are already mapped to outside the container by default. At this time, LangBot can only act as a WebSocket server, accepting connections from messaging platforms as clients.

Please set the messaging platform to ReverseWebSocket (called `reverse ws` or `WebSocket client`), with the port corresponding to the port enabled by LangBot's aiocqhttp adapter, connecting to local 127.0.0.1.


## Neither LangBot nor Messaging Platform Using Docker Deployment

Configure the messaging platform and LangBot settings according to the documentation, set both ports to the same unused port, and both connect to local 127.0.0.1.

## Only Messaging Platform Running in Docker Container (Not Recommended)

:::warning
Only supports Linux, or other systems that support host mode docker networking.
:::

Currently, LangBot's aiocqhttp adapter only supports reverse WebSocket connections. When the messaging platform runs in a Docker container while LangBot runs directly on the host machine, the messaging platform must act as a client connecting to LangBot. In this case, you can only set the messaging platform's network to `host` mode, and then set its WS connection address to 127.0.0.1, with the port corresponding to the port enabled by LangBot's aiocqhttp adapter.
