# 接入 Telegram 机器人

## 创建机器人

前往 [Telegram 机器人创建页面](https://t.me/botfather)，按照提示操作，创建一个机器人。

![Telegram 机器人创建](/assets/image/zh/deploy/bots/telegram/telegram_01.png)

![Telegram 机器人创建](/assets/image/zh/deploy/bots/telegram/telegram_02.png)

创建完成后，BotFather 会返回一个 API Token，请妥善保存。接下来关闭`Privacy Mode`，以便在群聊中使用。

![Telegram 机器人 API Token](/assets/image/zh/deploy/bots/telegram/telegram_03.png)

## 对接 LangBot

打开 LangBot Webui 页面，创建一个新机器人

![对接 LangBot](/assets/image/zh/deploy/bots/telegram/connect_to_langbot.png)

填写完成后启动 LangBot，若成功配置，日志中会出现`[02-02 16:48:15.263] manager.py (68) - [INFO] : 初始化平台适配器 1: telegram`的字样，保持 LangBot 运行。

## 使用机器人

现在在群里或者私聊机器人都可以正常使用了。

![Telegram 机器人使用](/assets/image/zh/deploy/bots/telegram/telegram_04.png)

![Telegram 机器人使用](/assets/image/zh/deploy/bots/telegram/telegram_05.png)