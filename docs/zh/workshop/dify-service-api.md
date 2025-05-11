# 在 LangBot 上使用 Dify

[Dify](https://dify.ai) 是一款开源的大语言模型(LLM) 应用开发平台。它融合了后端即服务（Backend as Service）和 LLMOps 的理念，使开发者可以快速搭建生产级的生成式 AI 应用。  
Dify 可以创建聊天助手（含Chatflow）、Agent、文本生成应用、工作流等应用。

LangBot 目前支持`聊天助手`（含Chatflow）、`Agent`、`工作流`三种 Dify 应用类型。

## 在 Dify 上创建应用

请根据 [Dify文档](https://docs.dify.ai) 部署dify并创建你的应用。  

发布应用后，在应用的 `访问API` 页面，生成 API 密钥。

![Dify 应用 API 密钥](/assets/image/zh/workshop/dify-service-api/dify_sv_api_01.png)

保存 API 服务器和 API 密钥，在 LangBot 的流水线的`AI 能力`配置。

:::info
以上为 Dify 云服务版本的示例，若您使用本地自部署的社区版本，请使用 LangBot 访问你自己 Dify 服务的地址作为 `base-url`，后方需要添加 `/v1` 作为路径。

- 若 LangBot 与 Dify 部署在同一台主机，并且都是使用 Docker 部署的，可以参考文章：[网络配置详解](/zh/workshop/network-details.html#langbot-%E5%92%8C%E6%B6%88%E6%81%AF%E5%B9%B3%E5%8F%B0%E5%9D%87%E8%BF%90%E8%A1%8C%E5%9C%A8-docker-%E5%AE%B9%E5%99%A8%E4%B8%AD)。其中，请将启动 Dify 的 docker-compose.yaml 中所有容器的`networks`均添加`langbot-network`，并为`nginx`容器添加容器名`dify-nginx`，最后在 LangBot 配置中将`base-url`设置为`http://dify-nginx/v1`。
- 其他情况请咨询贵司运维人员。
:::

## 配置 LangBot

打开 LangBot WebUI 页面，添加一个新的流水线或在已有流水线中切换到 AI 能力配置页面。

![设置开发项](/assets/image/zh/deploy/pipelines/dify/dify01.png)

::: info
### 工作流输出键

如果使用的是 Dify 的工作流应用，那么请使用 `summary` 作为键传递输出内容。

![Dify 工作流应用的输出键](/assets/image/zh/workshop/dify-service-api/dify_workflow_output_key.png)

## 输出处理

使用 工作流 应用或 Agent 应用时，如果开启了 LangBot 流水线`输出处理`中的`track-function-calls`，将会在 Dify 执行每个工具调用时，输出一个`调用函数xxx`的消息给用户。  
但如果是使用`chat`应用下的`ChatFlow`（聊天助手->工作流编排），无论如何只会输出 Answer（直接回复）节点返回的文本。
:::