Heisenberg 人工世界Artificial World

![profile_qrcode](https://mp.weixin.qq.com/mp/qrcode?scene=10000005&size=102&__biz=MzkxMjY3MDMxMQ==&mid=2247484600&idx=1&sn=d24556d20e9dd8878b0239ce98741f0f&send_time=)

人工世界Artificial World

揭示隐藏变量，处于AGI的边缘。

29篇原创内容

*2024年12月08日 08:01*

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/8mFTT4sdlNXSMwKmaXTFaSvPe5oW4aR7GIJzOc9DfP08lOeceCEEuUNWu9Btp2vH0t7ibjibIniapZ9JOETHmwVoQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**Letta 是一家专注于 AI agents 的公司，提供开源工具和云服务，帮助开发者构建、部署和管理具有记忆能力和工具调用能力的 AI agents。**

原文：https://www.letta.com/blog/ai-agents-stack

（由ChatGPT翻译）

**理解AI Agents 的生态版图**

尽管市面上已经有许多关于代理技术堆栈和代理市场的地图，但我们往往对其分类方式持不同意见，并发现它们很少真实反映开发者实际使用的工具和技术。在过去的几个月中，随着记忆机制、工具使用、安全执行以及部署等方面的进展，代理软件生态系统取得了显著发展。因此，我们决定基于我们一年多的开源AI开发经验和七年以上的AI研究积累，分享我们自己的“代理技术堆栈”。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/8mFTT4sdlNXSMwKmaXTFaSvPe5oW4aR76ibHMr9f1bJdwnPtiaDHdF1eox1dvibVj6HpjC1GNjYeDZWibX77lyvLRw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

2024 年底的 AI agents 技术栈，分为三个关键层次：

agent 托管/服务、agent 框架以及 LLM 模型与存储。

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

从 LLMs 到 LLM agents

在 2022 年和 2023 年，我们见证了 LLM 框架和 SDK 的兴起，例如 LangChain（于 2022 年 10 月发布）和 LlamaIndex（于 2022 年 11 月发布）。同时，也出现了一些“标准”平台，用于通过 API 消费 LLMs，以及自部署的 LLM 推理工具（如 vLLM 和 Ollama）。

到了 2024 年，市场对 AI “agents” 以及更广泛意义上的复合系统的兴趣发生了显著转变。尽管“agents”作为 AI 领域的一个术语已存在数十年（尤其是在强化学习中），但在 ChatGPT 之后的时代，“agents” 成为了一个定义较为宽泛的概念，通常指被赋予任务以输出动作（工具调用）并在自主环境中运行的 LLMs。

从 LLM 转变为 agent 所需的工具使用、自主执行以及记忆机制的结合，推动了新的 agents 技术堆栈的开发。

Agents 技术堆栈的独特

与基础的 LLM 聊天机器人相比，agents 面临着更大的工程挑战。这是因为它们需要进行状态管理（保留消息/事件历史、存储长期记忆、在 agents 循环中执行多次 LLM 调用）以及工具执行（安全地执行 LLM 输出的动作并返回结果）。

因此，AI agents 的技术堆栈与传统的 LLM 技术堆栈有很大的不同。接下来，我们将从最底层的模型服务层开始，逐步剖析当今的 AI agents 技术堆栈：

模型服务

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

在 AI agents 的核心是 LLM。为了使用 LLM，模型需要通过推理引擎提供服务，这通常运行在收费的 API 服务背后。  

在基于封闭 API 的模型推理提供商中，OpenAI 和 Anthropic 凭借私有的前沿模型处于领先地位。Together.AI、Fireworks 和 Groq 是一些流行的选项，它们通过收费 API 提供开放权重模型（如 Llama 3）的服务。在本地模型推理提供商中，vLLM 是生产级 GPU 服务负载的领先者，而 SGLang 则是一个面向类似开发者群体的新兴项目。  

对于爱好者（“AI 爱好者”），Ollama 和 LM Studio 是两种运行本地模型的热门选择，特别适合在个人电脑（例如 M 系列的苹果 MacBook）上运行模型。

存储

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

存储是构建具备状态的 agents 的基础模块之一。agents 的定义依赖于持久化的状态，例如其对话历史、记忆，以及用于 RAG（检索增强生成）的外部数据源。  

向量数据库在存储 agents 的“外部记忆”方面非常流行，例如 Chroma、Weaviate、Pinecone、Qdrant 和 Milvus。它们允许 agents 利用无法放入上下文窗口的大量数据源和对话历史。此外，自上世纪 80 年代起便存在的传统数据库 Postgres，现在也通过 pgvector 扩展支持向量搜索。  

一些基于 Postgres 的公司也在为 agents 提供嵌入式搜索与存储功能，例如 Neon（无服务器 Postgres）和 Supabase，它们同样是这一领域的重要玩家。

工具&库

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

标准 AI 聊天机器人与 AI agents 之间的主要区别之一在于 agents 能够调用“工具”（或称“函数”）。在大多数情况下，这种调用机制是由 LLM 生成结构化输出（例如 JSON 对象），指定要调用的函数及其参数来实现的。  

关于 agent 工具执行的一个常见误解是，工具的实际执行并非由 LLM 提供商完成。LLM 的职责仅限于选择调用哪个工具以及提供哪些参数。支持任意工具或参数的 agent 服务必须使用沙盒环境（如 Modal、E2B）来确保安全执行。  

所有 agents 都通过 OpenAI 定义的 JSON 架构调用工具，这意味着不同框架下的 agents 和工具可以实现兼容。例如，Letta agents 能够调用 LangChain、CrewAI 和 Composio 的工具，因为它们遵循相同的架构。正因如此，一个为常用工具服务的生态系统正在快速成长。  

Composio 是一个流行的通用工具库，同时负责授权管理；Browserbase 是用于网页浏览的专用工具；而 Exa 则提供了专注于网络搜索的工具。随着更多 agents 的开发，我们预计工具生态系统将进一步扩大，并引入新功能，例如针对 agents 的认证与访问控制服务。

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

Agent框架

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

Agent 框架：编排 LLM 调用与管理 agent 状态

Agent 框架负责协调 LLM 调用并管理 agent 的状态。不同的框架在以下几个方面设计有所不同：  

1\. Agent 状态管理

大多数框架引入了某种“状态序列化”的概念，允许将 agent 的状态（如对话历史、记忆和执行阶段）序列化为文件（如 JSON 或字节），以便稍后重新加载至同一脚本中。而在 Letta 中，所有状态均由数据库支持（如消息表、agent 状态表、记忆块表），因此不存在“序列化”概念，因为状态始终持久化存储。这种方式便于查询 agent 状态，例如按日期查找过去的消息。  

状态的表示与管理方式不仅决定了 agent 应用程序能否随着对话历史延长或 agent 数量增加而扩展，还影响了状态访问和修改的灵活性。  

2\. Agent 上下文窗口的结构

每次调用 LLM 时，框架都会将 agent 的状态“编译”到上下文窗口中。不同框架对上下文窗口中数据（如指令、消息缓冲区等）的组织方式各异，从而影响性能。我们建议选择能使上下文窗口透明的框架，因为这直接影响您对 agent 行为的控制能力。  

3\. Agent 间的通信（多 agent 系统）

Llama Index 通过消息队列实现 agents 间通信，而 CrewAI 和 AutoGen 提供了明确的抽象器来支持多 agent 系统。Letta 和 LangGraph 则允许 agents 直接相互调用，从而支持集中式（通过监督 agent）或分布式通信。大多数框架目前都同时支持单 agent 和多 agent 系统，因为设计良好的单 agent 系统应易于扩展为多 agent 协作。  

4\. 记忆管理的方法

由于 LLM 存在上下文窗口的限制，必须通过技术手段管理记忆。部分框架内置记忆管理功能，而另一些则要求开发者自行管理。CrewAI 和 AutoGen 仅依赖于基于 RAG（检索增强生成）的记忆，而 phidata 和 Letta 采用了额外技术，如自编辑记忆（来自 MemGPT）和递归总结。Letta agents 自带一套记忆管理工具，允许 agents 按文本或日期搜索历史消息、撰写记忆并编辑自身的上下文窗口。  

5\. 对开放模型的支持

模型提供商通常会在幕后执行许多操作，使 LLM 以正确格式生成文本（如工具调用）。例如，当 LLM 没有生成正确的工具参数时，重新采样其输出，或在提示中添加线索（如“请以 JSON 格式输出”）。支持开放模型要求框架能够处理这些挑战，因此有些框架仅支持主流模型提供商。  

如何选择合适的框架

在构建 agent 时，选择框架需根据具体应用而定，例如您是构建对话型 agent 还是工作流型 agent，是否希望在 notebook 中运行 agent 或作为服务运行，以及对开放权重模型支持的要求。  

我们预计，各框架在部署工作流上的设计差异将成为主要竞争点，尤其是在状态/记忆管理和工具执行的设计选择上，这些将对实际应用产生更大的影响。

Agent 托管与 Agent 服务

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

大多数 agent 框架的现状与未来趋势

目前，大多数 agent 框架设计的 agents 仅限于存在于编写它们的 Python 脚本或 Jupyter notebook 中。然而，我们认为 agents 的未来应是作为服务存在，部署在本地或云基础设施中，并通过 REST API 提供访问。正如 OpenAI 的 ChatCompletion API 已成为与 LLM 服务交互的行业标准，我们预期未来也会出现一个统一的 Agents API 标准，但这一“赢家”尚未出现。  

将 agents 部署为服务比将 LLM 部署为服务复杂得多，这主要归因于状态管理和安全工具执行的问题。工具及其所需的依赖和环境必须显式存储在数据库中，因为服务需要重新创建运行工具的环境（而当工具与 agents 在同一脚本中运行时，这并不是问题）。  

此外，应用可能需要运行数百万个 agents，每个 agent 的对话历史不断增长。从原型开发到生产阶段，不可避免地需要对 agent 状态进行数据规范化处理，同时通过 REST API 定义 agent 的交互方式。目前，这一过程通常由开发者自行编写 FastAPI 和数据库代码来完成，但我们预计，随着 agents 的成熟，这些功能将更深地集成到框架中。  

\---

结论

Agent 技术栈仍处于非常早期的发展阶段，但我们对其生态系统未来的扩展和演变充满期待。

---

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)