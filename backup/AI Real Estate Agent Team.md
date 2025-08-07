https://cookbook.openai.com/articles/gpt-oss/fine-tune-transfomers

OpenAI gpt-oss (开源 LLM) + 
[@firecrawl_dev](https://x.com/firecrawl_dev)
 (搜索) + 
[@AgnoAgi](https://x.com/AgnoAgi)
 (Agent 框架) 打造一个 Multi-Agents AI 房地产中介团队，帮你快速找到心仪的房子 🏡 —— 来自 
[@Saboo_Shubham_](https://x.com/Saboo_Shubham_)
 的教程 
[@unwind_ai_](https://x.com/unwind_ai_)
 和开源项目实战分享 👏🏻

系统构成
系统基于 Agno Agent 框架，由三个专业 AI Agent 组成：房产搜索 Agent、市场分析 Agent 和 房产估值 Agent。这些 Agents 各司其职，像一个真正的房地产团队一样协作，帮你在竞争激烈的市场中做出明智决策。

核心内容
系统能从 Zillow、Realtor. com 等主流房地产网站抓取房源信息，分析市场趋势，并评估房产的投资价值。具体功能包括：
· 多平台房源搜索：同时搜索多个房地产网站，获取房源的地址、价格、卧室数量等详细信息。
· 市场洞察：分析市场是买方市场还是卖方市场，介绍目标区域的社区特点和投资前景。
· 房产估值：评估每套房子的价格是否合理，投资潜力如何，并给出具体建议。

工作原理
1. 输入需求：你提供 API 密钥、目标城市、预算和房产偏好（比如户型、卧室数）。
2. 搜索房源：房产搜索 Agent 通过 Firecrawl 工具从各大网站抓取符合你需求的房源。
3. 市场分析：市场分析 Agent 根据房源数据，简要分析市场趋势和社区情况。
4. 估值建议：房产估值 Agent 为每套房子提供定价评估和投资建议，比如是否值得入手。

整个过程是流水线式的，每个 Agent 在上一环节的基础上进一步处理信息，确保结果全面又深入。

界面与体验
系统提供了一个直观的 
[@streamlit](https://x.com/streamlit)
 界面，包含：
· 侧边栏：输入 API 密钥和配置。
· 搜索表单：设置城市、预算、房产类型等条件。
· 结果展示：以卡片形式展示房源信息、市场分析和投资建议，还包括平均价格、常见房型等统计数据。