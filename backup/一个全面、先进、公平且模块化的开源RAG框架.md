
两个关键问题限制了 RAG 的发展：

- 新型 RAG 算法之间缺乏**全面和公平**的比较。
    
- 像 LlamaIndex 和 LangChain 这样的开源工具使用了高级抽象，这导致了透明度的缺失，并限制了**开****发新算法和评估指标**的能力。
    

RAGLAB：是一个**模块化**的开源库。RAGLAB 复现了 6 种**先进的**算法，并为研究 RAG 算法提供了一个**全面的**生态系统。利用 RAGLAB，对 10 个基准上的 6 种 RAG 算法进行了**公平**比较。有了 RAGLAB，研究人员可以高效地比较各种算法的性能并**开发新算法**。

**不同 RAG 库和框架的比较**。**公平比较**指的是在评估过程中对所有基本组件进行对齐，包括随机种子、生成器、检索器和指令。**数据收集器**指的是能够收集或生成训练和测试数据的能力，无论是通过从现有的原始数据集中抽样，还是通过使用LLM构建标记数据。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricHz5yb9zLapkt4FVK0V56whTTxToQcYcvwWBXyHCQnXnQaXtFYJg0nWN9ouvdz3wPiaNgT90aYBngA/640?wx_fmt=png&from=appmsg&wxfrom=13)

**RAGLAB**提供了一个模块化的架构，允许用户轻松地替换和扩展算法的各个组成部分，包括检索器（retriever）、生成器（generator）和指令（instruction）。

**RAGLAB 框架的架构和组件**

**![](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricHz5yb9zLapkt4FVK0V56whwTB9E2PcA2ricDNA1mUpXA5o0mU2EMKIAhkNF6R5hEGxzzO9yRPU4xA/640?wx_fmt=png&from=appmsg&wxfrom=13)**

- 检索器（Retriever）：集成了基于BERT的模型，如Contriever和ColBERT，提供了统一的查询接口和客户端-服务器架构，以及检索缓存机制。
    
- 语料库（Corpus）：提供预处理的Wikipedia语料库，包括2018年和2023年的版本，以及对应的索引和嵌入。
    
- 生成器（Generator）：集成了Huggingface Transformers和VLLM，支持量化和低秩适应（LoRA）技术，允许使用大型模型。
    
- 指令实验室（Instruction Lab）：包含系统指令、任务指令和算法指令，允许用户自定义和组合指令。
    
- 训练器（Trainer）：集成了Accelerate和DeepSpeed库，支持模型的微调，包括LoRA和量化LoRA技术。
    
- 数据集和度量（Dataset and Metric）：收集了10个广泛使用的基准数据集，覆盖五种不同的任务类型，并提供了灵活的数据适配机制和多种评估指标  
      
    
- ![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricHz5yb9zLapkt4FVK0V56whVuiac6v1dK18vNia0Iw9rfUcLTTrAN4guZHq8mjPzuBjh710e4UHLt9Q/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
    

RAGLAB进行了全面的实验，使用不同的基础模型作为生成器，同时保持其他基本组件的一致性，以促进不同高级RAG算法之间的公平比较。

**一个使用 RAGLAB 来复现 Self-RAG 算法的脚本**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricHz5yb9zLapkt4FVK0V56whW0hAvDKE7aY9b407UZ4Vom8bjJsMNeqp0SAEY8XnQsqgiaFQGc7iby1g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

分析了使用不同基础模型的RAG算法（**Naive RAG、RRR 、ITER-RETGEN、Self-Ask、Active RAG、Self-RAG**）在多个基准上的性能，发现**Self-RAG算法**在使用特定生成器时显著优于其他算法。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricHz5yb9zLapkt4FVK0V56wh7jyADZgG1VPLcxibtOK78mSgs6dEfUuBGyhYFC1lAX9vticdX9TjJtZg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricHz5yb9zLapkt4FVK0V56whcNicC8FGeZloR6JWFMkYLibNKx4nLcgV3P5d8hibXQqeZlCbMfeyA2myg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**不同算法的指令**

```
Naive RAG
```

**RAGLAB 系统用户评估问卷**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricHz5yb9zLapkt4FVK0V56whW5dt9icDKibb9BFGLmaFiaViaSTBeHrpGbLbRNZHh7nALkT2RmkFzUtYRw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

```
RAGLAB: A Modular and Research-Oriented Unified Framework for Retrieval-Augmented Generation
https://arxiv.org/pdf/2408.11381
https://github.com/fate-ubw/RAGLab
```