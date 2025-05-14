# Deploy Message Platform NapCat

Connect through the OneBot 11 protocol, you need to select ``OneBot v11`` as the adapter.

## NapCat Installation Tutorial

Follow the [NapCat official documentation for installation](https://napcat.napneko.icu/guide/start-install)

## NapCat Configuration Tutorial

Only using webui operation as an example, for other configuration methods, please check the NapCat documentation.

After logging in, you can check the logs in the console or Bash, find `[NapCat] [WebUi] WebUi Publish Panel Url: http://x.x.x.x:6099/webui?token=xxxxx `
![napcat_webui_01](/assets/image/zh/deploy/bots/qq/onebot/napcat/napcat_webui_01.png)

Copy the Url to your browser or on Windows 11, press Ctrl and click the Url. After scanning the QR code to log in, you will enter the network configuration page.

Click Add Network Configuration, select WebSocket Client, click Enable, then fill in `ws://127.0.0.1:2280/ws` in the Url field and save.
![napcat_webui_02](/assets/image/zh/deploy/bots/qq/onebot/napcat/napcat_webui_02.png)

## NapCat Integration

Next, open the LangBot configuration page

Click on Bots, then click Add

Select `OneBot v11` for `Platform/Adapter Selection`

![napcat_webui_03](/assets/image/zh/deploy/bots/qq/onebot/napcat/napcat_webui_03.png)

::: info
Note, if you have network connection issues involving multiple docker containers, please refer to [Network Configuration Details](/en/workshop/network-details)
:::
