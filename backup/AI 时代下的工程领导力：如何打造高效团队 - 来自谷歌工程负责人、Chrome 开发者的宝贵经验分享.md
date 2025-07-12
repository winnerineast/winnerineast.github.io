Original 邵猛 *2025年03月25日 19:32*

今天偶然读到 Chrome 开发者、Google 工程负责人、著名技术书籍作者 - Addy Osmani 的一篇文章 「 Leading Effective Engineering Teams in the Age of GenAI」 ，讲的特别好，对于产品和研发方向如何变得高效，不管你是团队领导者、还是团队成员，都很有价值，分享给朋友们，可以先看我的阅读笔记，针对自己感兴趣的部门再阅读原文（推荐阅读，作者信息和文章链接放在文末）

![Image](https://mmbiz.qpic.cn/mmbiz_png/5CmZha6ohm38sDnEfwzjLtq29sCwghGUjmFhN5danpeEvVtb5WDldZDnQ2ycAe4FIymxLYyBbQyQfk54eflBDA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

> 文章的核心观点是：在生成式 AI 时代，领导一个工程团队不是为了让代码写得更快，而是要让软件做得更好。AI 是个好帮手，但不能全靠它，领导者得搞清楚“更好”到底是啥意思，然后带着团队更快地往那儿走。

先看看文章的结构：

1\. Introduction to GenAI in Engineering - 介绍生成式 AI 在工程领域的兴起及其重要性

2\. The Evolving Role of Engineering Leaders - 探讨生成式 AI 如何改变工程领导者的角色和职责

3\. Integrating GenAI into Engineering Workflows - 提供将 生成式 AI 融入工程工作流程的实用策略

4\. Managing Teams in the GenAI Era - 讨论在 生成式 AI 环境下如何有效管理和激励团队

5\. Case Studies: Leadership with GenAI - 展示通过 生成式 AI 实现成功领导的实际案例

6\. Conclusion: The Future of Engineering Leadership - 总结关键要点并展望工程领导力的未来

### 几个关键点

#### 1\. AI 像个新手同事

· AI 就跟一个刚入行的小伙伴差不多，干活快、有热情，但经验少（跟你的团队相关的），容易出错。

· 领导者得让团队学会“信任但要验证”，用 AI 生成的代码不能直接拿来就上，得好好检查，确保没问题。

· 别让大家太依赖 AI，不然时间长了，自己的本事可能会退步。

#### 2\. 领导的活儿变了

· 以前领导可能盯着代码细节，现在得更多想想大方向，比如“我们为啥要做这个”。

· AI 能帮你解决“怎么做”，但“为啥做”还得人来定。

· 领导得干这些事儿：

\- 教团队怎么用好 AI，比如怎么问 AI 问题、怎么检查它给的东西。

\- 定个计划，把 AI 融入工作，保证跟公司的目标和底线不冲突。

\- 立规矩，确保代码安全、公平、不出乱子。

#### 3\. “70% 问题”

· AI 干活儿通常能搞定 70%，比如写个初稿很快，但剩下的 30%——需要人动脑子的部分——特别重要。

· 领导得鼓励大家把 AI 当伙伴，别当拐杖。

· 有些基本功，比如系统设计、调试问题，AI 还替代不了，得让团队继续练。

#### 4\. 知识悖论

· 有经验的老手用 AI，能干得更牛；但新手用 AI，可能稀里糊涂就信了错的东西。

· 领导得多花心思带新手，让他们搞懂 AI 给的东西，不能瞎用。

#### 5\. 领导得干啥

· 建个“信任但要验证”的氛围，AI 的代码必须过关。

· 经常培训团队，让他们用 AI 用得溜。

· 别忘了基本功，比如怎么思考、怎么判断。

· 盯着质量、代码好维护，还有知识传下去，别只图快。

### 一些具体内容

AI 在开发中的角色

AI 工具正在改变开发者的日常工作方式。想象一下，根据谷歌的数据，超过 75% 的开发者 已经在用或者计划用 AI 工具。这意味着领导者得在提升效率、保证代码质量和培养团队技能之间找到一个平衡点。比如，既要让 AI 帮忙干活，又不能让团队完全依赖它。

具体工具和例子

AI 工具种类不少，功能也很实在，这里举几个例子：

\- GitHub Copilot： 微软研究发现，用它之后开发者的效率能提高 26% 。具体点说，每周提交的代码量多了 13.5% ，而且代码质量还稳得住。

\- Cursor： 这是一款基于 VSCode 的 AI IDE，特别擅长大改代码，比如一次性能搞定几百行的调整。

\- Windsurf： 又一个基于 VSCode 的 AI IDE，能干多步骤任务，比如自动跑测试、找 bug 还顺手修好。

\- Cline： 开源的 AI 助手，免费又好用，很适合预算不多但想试水的团队。

面对挑战的解决方案

AI 用起来爽，但也有些坑要躲开，这里是几招应对方法：

\- 别太依赖 AI： 可以试试搞个“无 AI 日”，让大家纯手工写代码，保持基本功。或者让老手带新人，教他们怎么聪明地用 AI。

\- 代码质量别翻车： 多搞几轮审查和测试，确保 AI 写的代码靠谱。微软研究说，用 Copilot 后代码质量没下降，说明管得好就没问题。

\- 隐私别漏： 用自托管的 AI 模型，别把敏感代码传出去。比如，三星就因为有人把代码泄露给 ChatGPT，直接禁了外部 AI。

团队与技能提升

AI 不只是工具，还能帮团队成长：

\- 别怕丢饭碗： KPMG 调查显示， 50% 的程序员 觉得 AI 能让他们干更有创意的事，而不是抢活儿。

\- 学点新技能： 团队得学会怎么跟 AI 打交道，比如怎么问问题、怎么检查 AI 的输出。微软数据说，新手用 AI 后效率能提升 35-40% ，跟老手的差距都缩小了。

伦理与规范

用 AI 得有规矩，不然容易乱套：

\- 责任得扛： AI 写的代码出了问题，人得担着，不能甩锅给工具。

\- 安全得保： 有些公司（比如 IBM）用 AI 扫描代码，找出安全漏洞，还会给改进建议，确保不出岔子。

实际案例

看看别人是怎么玩转 AI 的：

\- Bancolombia（拉美银行）： 用了 AI，代码产出速度快了 30% ，每年自动改动 1.8 万次 应用，每天部署 42 次 。

\- LambdaTest（测试平台）： 开发时间缩短 30% ，新功能上线快，新手也能快速上手。

\- Infosys（IT 服务公司）： 项目交付速度提升 20% ，代码更扎实，bug 也少了。

#### 原文信息

作者信息：Addy Osmani - Engineering leader and senior thinker

https://addyosmani.com/

文章：Leading Effective Engineering Teams in the Age of GenAI

https://addyo.substack.com/p/leading-effective-engineering-teams-c9b

  

欢迎朋友们关注❤️和星标⭐️

  

素材来源官方媒体/网络新闻 [Read more](https://mp.weixin.qq.com/s/)

素材来源官方媒体/网络新闻 [Read more](https://mp.weixin.qq.com/s/) 继续滑动看下一个

向上滑动看下一个 [Got It](https://mp.weixin.qq.com/s/): ， ， ， ， ， ， ， ， ， ， ， ，.Video Mini Program Like ，轻点两下取消赞 Wow ，轻点两下取消在看 Share Comment Favorite 听过