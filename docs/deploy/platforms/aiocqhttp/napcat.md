# 部署消息平台 NapCat

## NapCat介绍

NapCat 是一个 QQNT 协议逆向工程框架。

可选平台：

- Windows
- Linux Docker
- Linux 非 Docker

## NapCat安装教程

按照 [NapCat 官方文档安装](https://napneko.github.io/zh-CN/guide/getting-started)

运行后扫码登录

## NapCat配置教程

登录后，可以在config文件夹中，找到并修改文件（数字对应机器人QQ号）：![image-20240514231529613](/assets/image/napcat_cfg_1.png)

参考下图红框修改内容，确保地址中 IP地址 是 QChatGPT 运行的主机的地址（若在同一网络内运行则为 127.0.0.1），后缀须为`/ws`：

![image-20240514231932514](/assets/image/napcat_cfg_2.png)

然后重新运行登录即可，看到提示：

![image-20240514232647329](/assets/image/napcat_cfg_3.png)