# 实现一个消息平台适配器

本文章将以`aiocqhttp`适配器为例，讲解如何为 LangBot 实现一个新的消息平台适配器，以便接入 WhatsApp、Discord 等新的消息平台协议。

## 注册

```text
新增一个消息平台适配器，例如：接入 WhatsApp、Discord 等。

- 基类：`pkg.platform.adapter.MessageSourceAdapter`
- 装饰器：`pkg.platform.adapter.adapter_class(name: str)`
- 参考实现：`pkg.platform.sources/`
```

我们实现一个消息平台适配器，本质上就是实现一个继承于`基类`的类，并使用`装饰器`进行注册。最后在运行阶段供用户选择并使用。

### 贡献到主仓库

在 `pkg/platform/sources/` 目录下新建一个 `aiocqhttp.py` 文件：

```python
from .. import adapter

@adapter.adapter_class("aiocqhttp")
class AiocqhttpAdapter(adapter.MessageSourceAdapter):
    pass
```

同时在 `pkg/platform/manager.py` 的第40行导入此模块：

```python
        from .sources import nakuru, aiocqhttp, qqbotpy
```

最后参考其他适配器的清单文件，编写自己的清单文件。

## 事件、消息转换器

消息平台适配器，主要的工作就是`接收消息平台协议的事件，将其转换成LangBot的格式`，传递给核心组件，LangBot 核心组件处理完后，将需要回复的内容传递给消息平台适配器，消息平台适配器再`将内容转换成平台协议的格式，发送给消息平台`。

下图展示了两种情况的处理模式：消息平台协议无 SDK、有成熟 SDK。第一种情况我们需要根据消息平台协议的文档，自行实现连接管理、网络格式数据转换成 LB 消息 Python 对象。第二种情况，消息平台有成熟的 SDK，我们只需要根据 SDK 的文档，调用 SDK 的 API 创建连接，注册事件监听器，并实现消息转换器。

![alt text](/assets/image/zh/workshop/impl-platform-adapter/workshop_impl_platform_adapter_01.png)

在`pkg.platform.sources.aiocqhttp`文件里，我们可以看到不只有`AiocqhttpAdapter`，还有`class AiocqhttpMessageConverter(adapter.MessageConverter):` 和 `class AiocqhttpEventConverter(adapter.EventConverter):`。

- `MessageConverter` 用于进行 LangBot 消息和平台消息的互相转换。
- `EventConverter` 用于进行 LangBot 事件和平台事件的互相转换。

TBC...