# 部署消息平台 NapCat

通过 OneBot 11 协议接入，需选择使用``OneBot v11``作为适配器。

## NapCat安装教程

按照 [NapCat 官方文档安装](https://napcat.napneko.icu/guide/start-install)

## NapCat配置教程

仅以 webui 操作为例，其他的配置方式请查看 NapCat 文档。

登录后，在控制台或Bash上可以查看日志 , 找到 `[NapCat] [WebUi] WebUi Publish Panel Url: http://x.x.x.x:6099/webui?token=xxxxx ` 
![napcat_webui_01](/assets/image/zh/deploy/bots/qq/onebot/napcat/napcat_webui_01.png)

复制Url到浏览器或者 Windows11 按照Ctrl点击Url即可 扫码登录后即可进入网络配置一页

点击添加网络配置 WebSocket客户端 点击启用 然后在Url一栏填入 `ws://127.0.0.1:2280/ws`  并保存即可
![napcat_webui_02](/assets/image/zh/deploy/bots/qq/onebot/napcat/napcat_webui_02.png)

## NapCat 对接

接下来打开 LangBot 配置页面

点击机器人，点击添加

`平台/适配器选择`为`OneBot v11`

![napcat_webui_03](/assets/image/zh/deploy/bots/qq/onebot/napcat/napcat_webui_03.png)

::: info
注意，如果涉及多个 docker 容器的网络连接问题，请参考[网络配置详解](/zh/workshop/network-details)
:::