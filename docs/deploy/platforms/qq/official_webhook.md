# 使用 QQ 官方机器人 API（使用webhook方式）

本文章只提供测试版机器人的发布，具体机器人上线请按照 [发布流程](https://q.qq.com/qqbot/#/home) 进行部署。

## 注册 QQ 机器人（测试机器人）

### 配置机器人基本信息

前往 [QQ开放平台](https://q.qq.com/#/) ，找到下方的 `应用管理` ，点击创建机器人，填写基本信息之后，进入机器人页面，如图：

![机器人主页面](/assets/image/qqofficial1.png)

`首页` 选项中的 `发布流程` 即为上线机器人的步骤。由于部署的是测试版机器人，所以只需要进行其中的 `资料` 和 `沙箱配置` 。<br>

先进行资料填写，然后点击沙箱配置。

#### 配置沙箱配置项

点击 `沙箱配置` 。
如果要部署在QQ群中，那么按照 `QQ群ID` 下方的要求进行选择群聊，在消息列表配置中添加有私聊权限的用户。<br>
如果要部署在QQ频道中，那么按照 `频道ID` 下方的要求选择频道ID，机器人类型为0。

#### 配置开发管理项

点击 `开发管理` 。

![开发管理页面](/assets/image/qqofficial2.png)

记录其中的 `AppID` , `Token` , `AppSecret` ,并将 LangBot 所在服务器的IP地址填写到IP白名单中。

## 填写适配器

将上文获取的 `AppID` , `Token` , `AppSecret` 填写入 [配置信息](/deploy/quick-config/config.md) 中的 qqofficial适配器（使用webhook方式）中。<br>
**配置项内容：**
```json
{
    "adapter": "qqofficial",
    "enable": false,
    "appid": "",
    "secret": "",
    "port": 2284,
    "token": ""
},
```


## 配置回调地址

由于QQ官方机器人必须要求回调地址是 https 请求，但 LangBot 仅提供 http 方式，所以需要自行配置反向代理。<br>
本文建议使用 [Caddy](https://caddy2.dengxiaolong.com/docs/) 反向代理，操作流程如下文。

### 操作caddy流程

#### 安装caddy

进入[Caddy安装文档](https://caddy2.dengxiaolong.com/docs/install)。选择对应自己操作系统的安装步骤，进行安装。

#### 填写Caddyfile

本文假设使用 ubuntu 系统部署 LangBot ，那么在系统中，Caddyfile 的默认位置为 `/etc/caddy/Caddyfile`。
使用 vim 或 nano 编辑 Caddyfile ，Caddyfile文件填写为：
```json
your_domain_name {
        reverse_proxy 127.0.0.1:2284
}
```
例如，如果你有域名 testlb.com，并且解析地址为本机，同时开启**443**端口，那么填写为：
```json
testlb.com {
        reverse_proxy 127.0.0.1:2284
}
```

保存并且退出文件。

**注，Caddyfile文件的填写要求非常严苛，请按照正确的格式填写，如果遇到问题请自行查询Caddy文档或者询问AI。**

#### 启动caddy
输入命令
```bash
sudo systemctl start caddy
```

成功启动后，检查 Caddy 状态命令：
```bash
sudo systemctl status caddy
```


#### 后续配置

若 Caddy 启动不成功，请自行阅读 [Caddy文档](https://caddy2.dengxiaolong.com/docs/quick-starts/caddyfile)，或者加入 LangBot 社区群请求帮助。<br>

以下是一些可能出现的问题：

- 没有开启443端口
- 没有将域名解析到本机
- 没有成功保存 Caddyfile

### 设置管理端回调地址


首先 **启动 LangBot** 。<br>

点击 机器人管理端网页中的 `回调配置`，勾选下面 `添加事件` 中的所有事件。 在请求地址中填写 Caddyfile 中设置的域名，后缀为/callback/command。<br>
比如域名为 testlb.com，那么请求地址中填写 testlb.com/callback/command ，点击确定配置。如果回调地址保存成功，那么意味着部署成功。若出现 `校验失败` 字样，请认真检查上述配置项是否填写正确。

## 发布方式

进入 `首页` 的发布流程 ，按照流程进行机器人发布，上线。
