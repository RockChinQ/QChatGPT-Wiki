# Connect to Discord Bot

## Create Bot

Go to the [Discord Developer Portal](https://discord.com/developers/applications), log in, and create an application.

![alt text](/assets/image/zh/deploy/bots/discord/discord_01.png)

Modify the basic information, click `Save Changes` to save.

![alt text](/assets/image/zh/deploy/bots/discord/discord_02.png)

Click `Bot` on the left, click `Reset Token`, copy the generated Token.

![alt text](/assets/image/zh/deploy/bots/discord/discord_03.png)

And check all options in `Privileged Gateway Intents` on this page, click `Save Changes` to save.

![alt text](/assets/image/zh/deploy/bots/discord/discord_05.png)

**Finally, click `OAuth2` on the left, copy the `Client ID` on the page.**

## Connect to LangBot

Click to add a new bot, fill in the `Client ID` and `Token` obtained in the previous step into the configuration.

![alt text](/assets/image/zh/deploy/bots/discord/connect_to_langbot.png)

:::warning

If you are using this adapter within mainland China, you may need to set up a network proxy.

:::

After filling in, start LangBot. If configured successfully, the log will show `[02-02 16:48:15.263] manager.py (68) - [INFO] : Initializing platform adapter 1: discord`, keep LangBot running.

## Invite Bot to Server

You need to create a server first, then invite the bot to the server.

Go to the `OAuth2` page, select `URL Generator`, select `bot`, check the permissions as shown in the image.

![alt text](/assets/image/zh/deploy/bots/discord/discord_06.png)

![alt text](/assets/image/zh/deploy/bots/discord/discord_07.png)

Click `Copy`, paste the generated URL into your browser to open it, and invite the bot to your server.

![alt text](/assets/image/zh/deploy/bots/discord/discord_08.png)

## Use Bot

Now you can use the bot normally in groups or private messages.

![alt text](/assets/image/zh/deploy/bots/discord/discord_09.png)
