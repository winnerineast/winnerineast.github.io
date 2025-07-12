
原创 和你一起进步的 Zilliz

 _2025年02月13日 19:06_

![图片](https://mmbiz.qpic.cn/mmbiz_png/MqgA8Ylgeh69MGal1BGtDcKwvTTfp5d0DHtYLLGMqYNKG5qwPU0VWeyZibj6YxULOqb3M2heiaUflhftAyLmniciag/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1&tp=wxpic)

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/MqgA8Ylgeh5IGBMTYqBrAcxy5ZYQ8PyPustqwVcWc7JZ44y2ibSqYia0apqCylI22ia3goM9kmP8CHvwef4CgOLicw/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

# **前言**

近日，Open AI的Deep Research（深度研究）功能一经推出，迅速受到诸多关注，通过将大模型+超级搜索+研究助理的三合一，金融机构一键生成报告、科研党一键生成综述成为可能。

但囿于企业场景私有化数据的敏感性以及成本问题，如何基于Deep Research做开源的本地化部署，成为不少人关心的问题。

在本篇文章里，我们将对市面上复现Deep Research的各类开源项目做一个简单的分析，并**结合Deepseek等主流开源模型，推出开源项目Deep Searcher，帮助大家在企业级场景中，基于Deep Research思路，做私有化部署。**这个方案也在目前常见的RAG方案上做了重大升级。

Github 尝鲜链接https://github.com/zilliztech/deep-searcher；欢迎大家前去体验并给出反馈。

# **01** 

# **什么是Deep Research，为什么需要开源平替？**

OpenAI近期推出了一款名为Deep Research的高级AI研究工具，旨在帮助用户高效完成复杂的研究任务。该工具基于OpenAI最新的o3模型，专为网络浏览和数据分析优化。

## **主要功能**

**（1）多步骤信息收集与推理：**Deep Research能够自主进行多步骤的网络调查，快速整合来自互联网的海量信息，包括文本、图像和PDF文件。

**（2）专业级报告生成：**通过分析和综合数百个在线资源，Deep Research能在5到30分钟内生成一份带有详细引用的专业报告，大幅缩短传统研究所需时间。

## **应用场景**

**（1）学术研究：**学生和研究人员可以利用Deep Research快速获取相关领域的深入资料，辅助论文写作和课题研究。

**（2）市场分析：**企业可以使用该工具进行市场调研、竞争对手分析及产品比较等，支持商业决策。

**（3）产品评估：**消费者能够借助Deep Research对比不同产品的特性和评价，做出明智的购买决策。

总的来说，Deep Research作为OpenAI推出的深度研究产品，旨在通过自动化的信息收集和分析，帮助用户高效完成复杂的研究任务。不过目前，Deep Research仅向美国地区的OpenAI Pro用户开放，**成本需要每月200美金，且每月仅能进行100次查询**。

## **开源方案**

目前，大部分用户尚无法使用OpenAI的Deep Research功能。不过好在OpenAI发布该功能后，许多开源贡献者纷纷投入分析，尝试复现该功能。

目前Github上已有许多开源方案，其大致实现思路分为四个步骤：

**步骤一，问题分析：**大模型分析用户输入问题，确定回答该问题所需的角度和步骤。目前许多大模型（如DeepSeek、ChatGPT、Gemini等）只需勾选推理选项即可生成这一过程。

![图片](https://mmbiz.qpic.cn/mmbiz_png/MqgA8Ylgeh5IGBMTYqBrAcxy5ZYQ8PyPm1jm3YwudexkCh9o1HQK86uQB9LBznpzN01wmrSKSJXphwYEfD84uA/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**步骤二，在线搜索：**根据生成的问题逐一进行在线搜索，并获取搜索结果的前k项，将其内容反馈给大模型。

**步骤三，内容总结：**大模型根据在线内容总结出简洁答案。

**步骤四，答案判定：**将所有内容汇总后，由大模型判断答案是否完整、准确。

如果完整准确，则输出最终答案。

如果达到设定的循环次数或token上限，也输出最终答案。

否则，生成新的问题，重新进入第一步，同时将历史解决信息带入下一次循环。

# **02** 

# **相比传统RAG，Deep Research有何亮点与不足**

相对于之前的RAG（Retrieval-Augmented Generation），该方案有三点突破：

**一、额外判定逻辑：通过添加判定逻辑，提高答案的准确性。**Deep Research 可以采用多源验证、逻辑推导等质量控制机制，确保研究结果的可靠性，并避免了传统 RAG 中存在的盲目检索和过度检索问题。相比之下，传统 RAG 在信息整合和验证方面可能不够完善

**二、搜索结果为主：答案更多来源于搜索结果，而非大模型生成**。大模型主要负责内容总结和相关性判定，从而提高答案的可信度。

**三、深度思考与复杂任务处理**：Deep Research 能够像人类研究员一样自主进行多步骤的互联网研究，理解信息、整合资源，并根据新发现调整研究计划，这种自主性和多步骤解决问题的能力，普通RAG难以做到。

优点很突出，但缺点也不容忽视，从前面给出的实现方案中不难看出，Deep Research 除了响应速度较慢、对算力、网络都有着更高需求之外，其答案的主要信息来源依然还是公开的网络搜索结果。

但对于绝大多数企业场景来说，**真正有价值的数据，多以企业内部数据的形式存在，既无法通过在线搜索获取，也不能被上传给大模型，出现隐私泄露风险**，这也就导致了它们无法被Deep Research利用。此外，在线搜索引擎的搜索结果可能存在误导（如广告），且小众搜索引擎可能存在延时问题。

因此，**在大多数企业级场景中，基于Deep Research思路，做私有化部署，或许是一个更优解决方案。**

接下来，我们以Deep Searcher为例，来展示如何通过开源项目+本地数据，部署一个本地升级版Deep Research。

# **03**

# **如何针对私有数据，做Deep Research**

下图是基于大部分开源Deep Research方案基础上进行改良，做出的Deep Searcher开源实现方案架构：

![图片](https://mmbiz.qpic.cn/mmbiz_png/MqgA8Ylgeh5IGBMTYqBrAcxy5ZYQ8PyPsK6SYicROuAX5yqycFISCFVdVheCKuhDD1gEzWkfBJgDUsrbjvE1SKA/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，Deep Searcher通过引入向量数据库Milvus,可以对用户存储在本地的数据进行海量低延时的离线搜索。

**具体实现思路上，****Deep Searcher****分为三步：**

**第一步，问题分析：**获取用户问题后，通过LLM分析生成多个子问题，并确定每个问题涉及的数据集合。

**第二步，信息检索：**根据大模型的分析结果，从向量数据库中检索相关信息。值得注意的是，向量数据库中的数据均为离线数据，因此在查询前需先将数据写入数据库。这些数据可以是内部私有数据、在线获取后下载的数据，或其他流系统中定期输入的数据。

**第三步，内容判定：**向量数据库检索到相似信息后，将用户原始问题、每个子问题及其相似搜索结果交由大模型进行内容判定。

如果问题已被完整回答，则进入最终回答阶段。

如果达到设定的循环次数或token上限，也进入最终回答阶段。

否则，大模型生成新的问题，进入下一次循环。

## **亮点**

（1）**私有数据利用**：最大化利用私有数据，更好地接入大模型。

（2）向量数据库优势：充分利用向量数据库的**海量数据处理能力、低延时搜索、多种索引参数、高可用性和资源弹性管理**等优势。

（3）数据管理：通过向量数据库有效管理私有数据，针对不同类型的数据进行分**库分表，接入多种应用，最大化利用数据，降低数据管理成本**。

值得注意的是，为更好地保护私有数据，**使用的LLM应为离线模型**。如使用LLM API，虽然仅返回检索的部分数据，但仍存在数据泄露风险。

# **04**

# **Deep Searcher 尝鲜**

基于以上思路，Deep Research的本地部署开源版方案Deep Searcher已在Github开源，项目地址为https://github.com/zilliztech/deep-searcher

## **目前功能现状**

**（1）LLM支持：**DeepSeek官方版本、DeepSeek硅基流动、DeepSeek TogetherAI、OpenAI

**（2）Embedding模型支持**：Pymilvus中的内置模型、OpenAI Embedding、VoyageAI Embedding

**（3）数据Loader支持**：离线文档（如PDF、Markdown、TXT）、在线文档（通过FireCrawl、JinaReader、Crawl4AI获取）

**（4）向量数据库支持**：Milvus、Zilliz Cloud（注册即可免费体验，注册地址：https://cloud.zilliz.com.cn/login 海外：https://cloud.zilliz.com/）

## **最终效果预览**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

更多细节欢迎访问我们的开源项目Github-Deep Searcher：https://github.com/zilliztech/deep-searcher项目目前处于快速迭代阶段，期待您的反馈。

# **05** 

# **写在最后：从地表最强，到最佳部署范式，仍有漫长的磨合期**

在本文写作过程中，笔者在思索如何对Deep Research做本地化复现的过程中，也有几个思考想要做一个分享：

**1、数据会成为未来企业的生存红线**，掌握优质数据的企业，也就拥有了Deep Research +N，脱颖而出的机会，而在这一背景下，数据隐私大于天，如何做好数据保护，是在接入AI能力之前要更早考虑的事情。

**2、全能的AI需要人类的Know how来做管理**：在本地部署Deep Searcher过程中，如果互联网公开数据与本地数据冲突（尤其是金融类数据更新频繁的行业），我们如何做权重分配？如果AI生成的内容有疏漏，如何进行核查？需要花更多精力去解决。

**3、最优不等于最适合**：私有数据不适合在线大模型已经是常识，在此之外，我们是不是需要“最优大模型”？复杂高成本的推理，是不是可以通过向量数据库分库分表等方式，就能低成本解决，这也是我们需要考虑的问题。

作者介绍

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

Milvus资深研发工程师：付邦

推荐阅读

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](https://mp.weixin.qq.com/s?__biz=MzUzMDI5OTA5NQ==&mid=2247508149&idx=1&sn=c91a47109054c8c03610c9d5acf6b36c&scene=21#wechat_redirect)[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](https://mp.weixin.qq.com/s?__biz=MzUzMDI5OTA5NQ==&mid=2247508124&idx=1&sn=cecd7b708360c44a95271a94be8a6235&scene=21#wechat_redirect)

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

大模型1016

Milvus100

大模型13

RAG 修炼手册27

探索 RAG51

大模型101 · 目录

上一篇美国连锁百货Nordstrom：推荐系统如何做到让你刚买跑鞋，就推防晒

阅读原文

阅读 2.1万

​

喜欢此内容的人还喜欢

教你本地复现Deep Research：DeepSeek R1+ LangChain+Milvus

我关注的号

Zilliz

不喜欢

不看的原因

确定

- 内容低质
- 不看此公众号内容

![相关阅读封面](https://mmbiz.qpic.cn/mmbiz_jpg/MqgA8Ylgeh6Uu2CteFvKvrcrJPkf0wbYAXNib2KXkviadpUVW1eLSGNtZj2PcYo6sZskCGNpWwnNAvVyhO3pQl9w/0?wx_fmt=jpeg&tp=wxpic)

李国良教授团队：Chat2Data，一个基于RAG、向量数据库和LLMs的交互式数据分析系统

数据库应用创新实验室

不喜欢

不看的原因

确定

- 内容低质
- 不看此公众号内容

![相关阅读封面](https://mmbiz.qpic.cn/mmbiz_jpg/BqvmAb5joHZa7nicTXDn1AED5ByTjbjicq3IGxp58TyoCceT5QPTXYrS4iazgic862c30WVKLc0cnslnx3maoXTqsA/0?wx_fmt=jpeg&tp=wxpic)

接入deepseek-r1的腾讯ima，强大到我有点陌生

2个朋友分享

大瑜聊AI

不喜欢

不看的原因

确定

- 内容低质
- 不看此公众号内容

![相关阅读封面](https://mmbiz.qpic.cn/mmbiz_jpg/MpREkIqiasHeTuIGnqSBHnUeibzTKYh6D6Aopa9PLQCycW6icXh919Gn386XFcSEMaTjRuQqvYZvuBcM5KvNbyF4g/0?wx_fmt=jpeg&tp=wxpic)

[](javacript:;)

![](http://mmbiz.qpic.cn/mmbiz_png/MqgA8Ylgeh6icloMEicsabgianxn9qXIbntoEsbyrOlUB3AgRJmcia09Qn5GicdC0oQKmyUHialiccFZxH9pib1V78QRbg/300?wx_fmt=png&wxfrom=18)

Zilliz

168244111327

![](http://wx.qlogo.cn/mmopen/ajNVdqHZLLCoRqcLMZr3N3WeRcYvKMjSoib6yRUy22yw3D0ZdW6uPfia5GyFpvdUoEt9uwo5ZQVBou8pSgoMeAQd7kSic3yx6l6y9vj8a3tKQaa1xjiahIyickq8V1GO9HicibT/96)

Li Ling

写留言

**留言 27**

- ![](http://wx.qlogo.cn/mmopen/00GYaClAoOqEQ49D6IlVOCiaEAplOJYVoexQrX9ZXXYFJ7OniavhyTQTYHFeV9pLibAUMPb2SpzncOpbG5omD7GZGU6CZfjvezI/64?extra=0.40776188974997085)
    
    巍海
    
    北京昨天
    
    赞5
    
    不过目前，Deep Research仅向美国地区的OpenAI Pro用户开放，成本需要每月200美金，且每月仅能进行100次查询。
    
    ![](http://wx.qlogo.cn/mmopen/jvNVbGBZaqNlQVJD1K2Uq5icP8oXPAuNs8LMbSGOziaSdm9BXmCLpTtQmeVf4nZTd5Ynqgia2nrl1HbFZFku346AbibOy4KyZpd3/64?extra=0.6896223447907064)
    
    朱淦
    
    广东昨天
    
    赞2
    
    哈 用不起
    
- ![](http://wx.qlogo.cn/mmopen/WJeIwwLWSkDyjfutOIES8wPKFL369xEicyRjVNTibs0ZpjYLOuBSw0TL91JDvIdCg7YxwXTzuJCD7nSuJDytjswda8aMoo7DLU/64?extra=0.4938414118581711)
    
    @洛@
    
    广西昨天
    
    赞1
    
    有没有效果比较？
    
    ![](http://wx.qlogo.cn/mmhead/Q3auHgzwzM7c1bCicegkbO7PTCGC1OBaLd4TPM68A87uf5FvAU0TCXQ/64?extra=0.7237544876664479)
    
    Zilliz
    
    作者昨天
    
    赞3
    
    后续推文会持续跟进话题，敬请期待![[嘿哈]](https://res.wx.qq.com/mpres/zh_CN/htmledition/comm_htmledition/images/pic/common/pic_blank.gif)
    
- ![](http://wx.qlogo.cn/mmopen/ajNVdqHZLLAKxpKicWibNr6jG9Dp3prcRFJ97nCKB0ibJkpSYHUgTz6YBY7Y9Ko6Vb3wia27O6m2NDKh4ovd1ACoqA/64?extra=0.9743410182051135)
    
    秦始皇
    
    河南11小时前
    
    赞1
    
    不就是 rag？
    
    ![](http://wx.qlogo.cn/mmopen/bibGqOMwvr5letB70NS5GLFGiahDunBpNCXGBGU4gRAqaicICgHbK03Ug1fMf88LV13hSs1csfic6E6ZOEUjx4srM9hJXVKUlAuM/64?extra=0.36589068419457593)
    
    想忘
    
    北京5小时前
    
    赞1
    
    都是通过炒概念来忽悠
    
    1条回复
    
- ![](http://wx.qlogo.cn/mmopen/ajNVdqHZLLD4POlqg0bGyezbplBfgBYlfVXfPpFnSGdb0dEMYMevBhe3HhICnNpw8GBe3KroaLQXPhicUo1OyTQ/64?extra=0.5397268244673614)
    
    周满超
    
    安徽12小时前
    
    赞1
    
    能不能提供Java版本实现
    
    ![](http://wx.qlogo.cn/mmopen/BDbj75fnJWewnjVj3FeYz5BOaQrQB7cOShhE1GjiboNU3QcKiciaBC5StxfPaaPbHSTPkhKQYibUGZ6vfLvFkE1ALYL54Z5OibdXI/64?extra=0.8533085508868326)
    
    jason
    
    福建9小时前
    
    赞
    
    劝你别想着java了，用python吧，Java在这个领域是不太可能有作为了，不是语音问题是生态问题，就像当初的Delphi![[呲牙]](https://res.wx.qq.com/mpres/zh_CN/htmledition/comm_htmledition/images/pic/common/pic_blank.gif)
    
    ![](http://wx.qlogo.cn/mmopen/ajNVdqHZLLD4POlqg0bGyezbplBfgBYlfVXfPpFnSGdb0dEMYMevBhe3HhICnNpw8GBe3KroaLQXPhicUo1OyTQ/64?extra=0.429842437445052)
    
    周满超
    
    安徽8小时前
    
    赞
    
    回复 **jason**：langchain4j不是开了很好的头吗
    
    1条回复
    
- ![](http://wx.qlogo.cn/mmopen/ajNVdqHZLLAd1DHhjUG0iaoyEAic9Izgw3iaQpPzvgvYicichoybnSib1icuR98dZYexjsR2hjlR6iaaiaYOumse1dx5gAw/64?extra=0.6094104611030258)
    
    好听的声音
    
    浙江16小时前
    
    赞
    
    根因追溯是不是适合此种场景实践，deep research的思路多次调用大模型，拆分原始问题为n个子问题，得到子问题答案再汇总推理生成最终答案，是这样子的么
    
    ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    SimFg
    
    浙江9小时前
    
    赞1
    
    得到子问题的答案后，有一个reflection的过程，也就是由大模型评估下当前问题根据现有的子问题答案是否可以得出，如果可以就生成最终答案，否则在进行下一轮循环
    
- ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    超毅
    
    北京20小时前
    
    赞1
    
    和GPTResearcher啥区别？
    
- ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    几何矩阵
    
    广东22小时前
    
    赞1
    
    图夫AI，前来支持![[强]](https://res.wx.qq.com/mpres/zh_CN/htmledition/comm_htmledition/images/pic/common/pic_blank.gif)![[强]](https://res.wx.qq.com/mpres/zh_CN/htmledition/comm_htmledition/images/pic/common/pic_blank.gif)
    
- ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    Jonny
    
    广东2小时前
    
    赞
    
    我觉得第三点不冲突，向量库管理分库分表只能算是提升输出结果准确性，但是最优大模型分析推理能力也是必要的，不一定是通用大模型，可以训练的垂直类大模型
    
- ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    Tom先生
    
    江苏2小时前
    
    赞
    
    请问一下，这个搜索本地文件，只搜索单个文件吗，我看文件地址就是指向一个pdf
    
- ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    黄思远
    
    浙江4小时前
    
    赞
    
    LLM provider 全是在线的？那内部数据不全都发出去了……
    
    ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    SimFg
    
    浙江4小时前
    
    赞
    
    其实在最后有提到，如果要保护私有数据，需要本地的llm
    
    ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    黄思远
    
    浙江4小时前
    
    赞
    
    回复 **SimFg**：我是说他源代码里全是在线的，没提供配置
    
    1条回复
    
- ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    超级奶爸感恩的心
    
    广东9小时前
    
    赞
    
    用户输入一个问题 -- map(同一个question或多个子quesiton）: 通过api同时发给多个云端或者本地的llm（deepseek官方，硅基， openai等） -- reduce(anser）: 后端一个llm合并，或者api传给一个云端llm合并 这样会不会更优？ 时间效率上提升很多
    
    ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    SimFg
    
    浙江9小时前
    
    赞
    
    这个基本上就是开源的deep research方案了
    
- ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    Yn@Yzh
    
    广东13小时前
    
    赞
    
    sub query是由大模型生成？
    
    ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    SimFg
    
    浙江9小时前
    
    赞
    
    是的，大模型对问题先进行分析
    
- ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    啊～～
    
    北京23小时前
    
    赞
    
    请问大模型使用API的话需要什么样的机器配置可跑？
    
    ![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHZpZXdCb3g9IjAgMCA0MCA0MCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBjbGlwLXBhdGg9InVybCgjY2xpcDBfNDIyMF8yNjc0KSI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGg0MHY0MEgweiIvPjxwYXRoIGZpbGw9IiNFREVERUQiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgMjlhMSAxIDAgMCAxLTEtMXYtLjY4NGMwLS42ODYuNDk4LTEuNDg0IDEuMTE0LTEuNzg1bDUuNjYtMi43NjJjLjgyMS0uNCAxLjAxMi0xLjI4OC40Mi0xLjk5bC0uMzYyLS40MjljLS43MzYtLjg3Mi0xLjMzMi0yLjUtMS4zMzItMy42NFYxNWMwLTIuMjEgMS43OTUtNCA0LTQgMi4yMSAwIDQgMS43OTMgNCA0djEuNzFjMCAxLjE0LS42IDIuNzczLTEuMzMyIDMuNjQybC0uMzYxLjQyOGMtLjU5LjY5OS0uNDA2IDEuNTg4LjQxOSAxLjk5bDUuNjYgMi43NjJjLjYxNS4zIDEuMTE0IDEuMDkzIDEuMTE0IDEuNzg0VjI4YTEgMSAwIDAgMS0xIDFoLTE3eiIgZmlsbD0iIzAwMCIgZmlsbC1vcGFjaXR5PSIuOSIgb3BhY2l0eT0iLjIiLz48L2c+PGRlZnM+PGNsaXBQYXRoIGlkPSJjbGlwMF80MjIwXzI2NzQiPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNDB2NDBIMHoiLz48L2NsaXBQYXRoPjwvZGVmcz48L3N2Zz4=)
    
    好听的声音
    
    浙江16小时前
    
    赞
    
    32G内存的虚拟机就可以跑了
    

已无更多数据