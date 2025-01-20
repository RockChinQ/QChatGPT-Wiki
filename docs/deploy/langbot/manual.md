# 手动部署(推荐，可以在所有平台上使用)

:::warning
1. 请使用Python 3.10.1（不包含3.10.0）及以上版本，推荐3.10.14版本，没有Python的需自行安装。
::: 


## 安装主程序

1. 前往[Release](https://github.com/RockChinQ/LangBot/releases)页面下载最新版本的压缩包（推荐）`langbot-xxx-all.zip`（请勿下载 Source Code，因为其中不包含 WebUI）。解压，在解压目录打开命令行（终端）

![下载Release](/assets/image/dl_release.png)

:::info

您也可以使用以下命令克隆最新代码（有可能包含不稳定的代码）并使用：

```bash
git clone https://github.com/RockChinQ/LangBot
cd LangBot

# 构建前端，需要 NodeJS >= 22
cd web
npm install && npm run build
cd ..
```
:::

2. （建议）创建虚拟环境

在一些使用系统包管理器管理 Python 依赖的 Linux 系统上，可能会出现依赖冲突，故请使用 venv 创建虚拟环境。Windows 用户可以跳过此步骤。

```bash
python -m venv venv
source venv/bin/activate
```

3. 安装依赖

```bash
pip install -r requirements.txt
```

或者使用清华源

```bash
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple 
```

3. 运行一次主程序，生成配置文件

```bash
python main.py
```

提示如下信息

```
 _                   ___      _   
| |   __ _ _ _  __ _| _ ) ___| |_ 
| |__/ _` | ' \/ _` | _ \/ _ \  _|
|____\__,_|_||_\__, |___/\___/\__|
               |___/              

⭐️开源地址: https://github.com/RockChinQ/LangBot
📖文档地址: https://docs.langbot.app

以下文件不存在，已自动生成，请按需修改配置文件后重启：
- plugins/__init__.py
- plugins/plugins.json
- data/config/command.json
- data/config/pipeline.json
- data/config/platform.json
- data/config/provider.json
- data/config/system.json
- data/config/sensitive-words.json
- data/scenario/default.json
```

接下来可以使用 Ctrl+C 退出程序，继续查看[部署消息平台](/deploy/platforms/readme)页。

当你部署消息平台和填写配置文件后，再次运行
```bash
python main.py
```
