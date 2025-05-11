# 部署消息平台 LiteLoaderQQNT

通过 OneBot 11 协议接入，需选择使用``OneBot v11``作为适配器。

# LiteLoaderQQNT

- [LiteLoaderQQNT 的 OneBot API 插件](https://github.com/LLOneBot/LLOneBot) 注入 QQ 客户端并将其转换为 OneBot 11 协议

安装LiteLoaderQQNT的教程：https://llonebot.github.io/zh-CN/guide/getting-started

![图片1](/assets/image/zh/deploy/bots/qq/onebot/llonebot/llob_cfg.png)

确保地址中 IP地址 是 LangBot 运行的主机的地址（若在同一网络内运行则为 127.0.0.1）

## Lagrange 对接

接下来打开 LangBot 配置页面

点击机器人，点击添加

`平台/适配器选择`为`OneBot v11`

![napcat_webui_03](/assets/image/zh/deploy/bots/qq/onebot/napcat/napcat_webui_03.png)

::: info
注意，如果涉及多个 docker 容器的网络连接问题，请参考[网络配置详解](/zh/workshop/network-details)
:::