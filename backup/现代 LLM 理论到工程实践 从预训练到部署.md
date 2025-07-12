
讲师

[@yanndubs](https://x.com/yanndubs)

(

[@OpenAI](https://x.com/OpenAI)

| PhD

[@StanfordAILab](https://x.com/StanfordAILab)

) 这门课程非常系统地介绍了构建现代 LLM 的完整技术栈, 从基础概念到实践细节都有涉及。它反映了当前 LLM 发展的前沿进展, 特别是在模型训练、评估和系统优化等方面提供了很多实用的见解。 LLM 训练的核心要素: - 架构 (Architecture) - 训练算法和损失函数 (Training algorithm/loss) - 数据 (Data) - 评估 (Evaluation) - 系统实现 (Systems) 语言建模的基础概念: - 语言模型本质是对 token /词序列的概率分布建模 - 使用自回归 (Autoregressive) 方式, 基于已有上文预测下一个 token - 训练目标是最大化文本的对数似然 (log-likelihood) Tokenizer 处理: - 使用 BPE 等算法将文本切分成子词单元 - 好处是可以处理拼写错误, 序列更短, 且比字符级更通用 模型评估: - 使用困惑度 (Perplexity) 作为基础指标 - 使用 MMLU 等标准 NLP 基准测试 - 需要注意提示词敏感性等挑战 数据处理: - 主要使用互联网数据 (如 Common Crawl) - 需要经过严格的清洗和过滤流程 - 数据量级从数百亿到万亿 tokens 不等 扩展规律 (Scaling Laws): - 更多数据和更大模型一般会带来更好性能 - Chinchilla 法则建议参数和训练数据比例为 1:20 - 帮助优化资源分配 对齐训练: - SFT: 基于人工标注数据进行监督微调 - RLHF: 基于人类反馈的强化学习 - 评估方法包括人工评估和 LLM 评估 系统优化: - GPU 并行计算优化 - 模型并行和数据并行 - 低精度计算 - 算子融合等技术 当前挑战: - 计算资源限制 - 数据收集的合法性 - 推理效率 - 上下文长度 关于 Stanford AI Lab: 成立于 1963 年, 致力于 AI 的研究、理论、实践和教学, 实验内包括

[@stanfordnlp](https://x.com/stanfordnlp)

[@StanfordSVL](https://x.com/StanfordSVL)

statsml 等研究组 

Youtube 视频: [https://m.youtube.com/watch?v=9vM4p9NN0Ts…](https://t.co/GDjmY1JgMw) 
课件文件: [https://drive.google.com/file/d/1B46VFrqFAPAEj3kaCrBAtQqeh2_Ztawl/view](https://t.co/3b2qvgoLnC)