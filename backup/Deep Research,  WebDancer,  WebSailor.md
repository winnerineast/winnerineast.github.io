
- 问：“一部知名电视剧：女二 1993 年入行；女一现任丈夫是浙江湖州人；男一六年后登上春晚。剧名是什么？” - 答案：父母爱情 这种题目来自 BrowseComp-ZH，是典型的检测模型 “超级深度” (Level-3) 的 Deep Research 能力的benchmark。 分享两篇文章 WebDancer 和 WebSailor 。 两篇文章介绍了如何端到端训练一个 Deep Research Agent ，以及，如何将这种 Web Agent 推向 BrowseComp - en/zh 等超深基准。 数据方面： WebDancer 通过构建 CRAWLQA和E2HQA，扩大难度渐进的数据量。 WebSailor 则用 SailorFog-QA，人为构造 Level-3 任务。 训练方面： WebDancer和WebSailor都采用ReAct框架，以及类似的post training recipe （SFT + On-policy RL）。 WebDancer 强在 GAIA/WebWalker 这类中等深度任务；而WebSailor 将优势推向 BrowseComp - en/zh 基准。

WebDancer: Towards Autonomous Information Seeking Agency [https://arxiv.org/abs/2505.22648](https://t.co/CAVEc5G6RM) 
WebSailor: Navigating Super-human Reasoning for Web Agent [https://arxiv.org/abs/2507.02592](https://t.co/PlJBwccSKn)