# Implementing a Message Platform Adapter

This article will use the `aiocqhttp` adapter as an example to explain how to implement a new message platform adapter for LangBot, in order to integrate new message platform protocols such as WhatsApp and Discord.

## Registration

```text
Add a new message platform adapter, for example: integrate WhatsApp, Discord, etc.

- Base class: `pkg.platform.adapter.MessageSourceAdapter`
- Decorator: `pkg.platform.adapter.adapter_class(name: str)`
- Reference implementation: `pkg.platform.sources/`
```

To implement a message platform adapter, we essentially need to implement a class that inherits from the `base class` and register it using the `decorator`. Finally, it will be available for users to select and use during runtime.

### Contributing to the Main Repository

Create a new file `aiocqhttp.py` in the `pkg/platform/sources/` directory:

```python
from .. import adapter

@adapter.adapter_class("aiocqhttp")
class AiocqhttpAdapter(adapter.MessageSourceAdapter):
    pass
```

Also import this module in `pkg/platform/manager.py` at line 40:

```python
        from .sources import nakuru, aiocqhttp, qqbotpy
```

Finally, write your own manifest file by referring to other adapters' manifest files.

## Event and Message Converters

The main work of a message platform adapter is to `receive events from the message platform protocol, convert them into LangBot's format`, pass them to the core components, and after LangBot's core components process them, pass the content that needs to be replied to the message platform adapter, which then `converts the content into the platform protocol format and sends it to the message platform`.

The following diagram shows the processing patterns for two scenarios: message platform protocol without SDK and with mature SDK. In the first case, we need to implement connection management and network format data conversion to LB message Python objects according to the message platform protocol documentation. In the second case, the message platform has a mature SDK, we only need to create connections according to the SDK documentation, register event listeners, and implement message converters.

![alt text](/assets/image/zh/workshop/impl-platform-adapter/workshop_impl_platform_adapter_01.png)

In the `pkg.platform.sources.aiocqhttp` file, we can see not only `AiocqhttpAdapter`, but also `class AiocqhttpMessageConverter(adapter.MessageConverter):` and `class AiocqhttpEventConverter(adapter.EventConverter):`.

- `MessageConverter` is used for converting between LangBot messages and platform messages.
- `EventConverter` is used for converting between LangBot events and platform events.

TBC...
