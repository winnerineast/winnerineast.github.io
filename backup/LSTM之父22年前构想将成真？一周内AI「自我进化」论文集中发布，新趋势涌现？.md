*2025年06月02日 13:23*

机器之心报道

**编辑：张倩、+0**

  

让 AI 实现自我进化是人类一直以来的梦想。

  

早在 2003 年，AI 先驱、LSTM 之父 Jürgen Schmidhuber 就提出过一种名为「哥德尔机（Gödel Machine）」的构想——它使用一种递归的自我改进协议，如果能够证明新代码的策略较佳，就会重写自己的代码。但这终究只是一个假想。

  

近年来，关于模型自我学习、进化的研究逐渐多了起来，很多研究者的目标在逐渐从单纯的「训练模型」向「让模型学会自我学习和自我进化」转变，谷歌最近发布的 [AlphaEvolve](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650969047&idx=2&sn=ef0aadc0ffa79ae0bea4266da98f2bc0&scene=21#wechat_redirect) 就是其中的重要代表。

  

在过去的一周，这一方向的进展尤其丰富。有人发现，几篇关于「让 LLM（或智能体）学会自我训练」的论文在 arXiv 上集中出现，其中甚至包括受「哥德尔机」构想启发而提出的「达尔文哥德尔机」。或许，AI 模型的自我进化能力正在加速提升。

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2b0t98GBRvGBick8clcjMga4jORZ0fO5Oj4zkueB07ML8xK7ibCB59O3AA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

在这篇文章中，我们将详细介绍最近的几篇论文，它们分别是：

  

- Sakana AI 与不列颠哥伦比亚大学等机构合作的「达尔文哥德尔机（DGM）」 ：DGM 利用基础模型和开放式算法来创建和评估新的 AI 智能体，并能够读取和修改自身的 Python 代码库以进行自我改进，还通过评估在编码基准上的性能来判断更改是否有效。实验表明，DGM 可以持续自我改进，并能在不同模型和编程语言之间实现迁移。

  

- CMU 的「自我奖励训练（SRT）」 ：提出了一种名为「自我奖励训练」的在线自我训练强化学习算法，旨在让大型语言模型通过自身的判断信号进行自我监督和训练，从而在没有外部标签的情况下提升性能。

  

- 上海交通大学等机构提出的多模态大模型的持续自我改进框架「MM-UPT」 ：在完全无监督场景下，通过强化学习框架 GRPO 实现多模态大模型的持续自我改进。他们提出了一种简洁而高效的框架：MM-UPT（Multi-Modal Unsupervised Post-Training），并在多个图文数学推理 benchmarks 上验证了其有效性。

  

- 香港中文大学联合 vivo 等机构的自改进框架「UI-Genie」 ：旨在解决 GUI 智能体中的两大核心挑战：一是轨迹结果的验证十分困难，二是高质量训练数据的规模化获取不易。针对这两个挑战，研究团队分别提出了一种奖励模型和一个自改进流水线。

  

## 达尔文哥德尔机：让 AI 通过重写自己的代码实现自我改进

  

- 论文标题：Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents
- 论文链接：https://arxiv.org/abs/2505.22954
- 博客：https://sakana.ai/dgm/

  

人工智能研究的一个长期目标是创造能够持续学习的 AI 系统。实现这一目标的一条诱人路径是让 AI 通过重写自身代码（包括负责学习的代码）来实现自我改进。这一由 Jürgen Schmidhuber 数十年前提出的构想被称为「哥德尔机」，是一种假想中的自我改进型 AI。当它在数学上证明存在更优策略时，它会通过递归地重写自身代码来优化问题解决方案，因此成为元学习（即「学会学习」）领域的核心概念。

  

虽然理论上的哥德尔机能确保可证明的良性自我修改，但 其实现依赖于一个不切实际的假设：AI 必须能在数学上证明代码修改会带来净效益才会实施变更。

  

针对此问题，Sakana AI 与不列颠哥伦比亚大学 Jeff Clune 实验室合作，提出了一种更可行的方案： 利用达尔文进化等开放式算法的原理，通过实证检验来寻找能提升性能的改进方法。

  

他们将这一成果命名为「达尔文哥德尔机（DGM）」。DGM 系统利用基础模型提出代码改进方案，并采用开放式算法的最新创新来搜索不断增长的多样化优质 AI 智能体库。 实验表明，DGM 获得的算力越多，自我改进效果就越显著。 鉴于依赖学习的 AI 系统终将超越人工设计系统这一明确趋势，DGM 很可能在短期内超越人工设计的 AI 系统。

  

第一个 DGM 是一个编码智能体，它能够：

  

- 读取并修改自己的代码；
- 评估修改是否提高了性能；
- 开放式地探索 AI 设计空间。

  

![Image](https://mmbiz.qpic.cn/sz_mmbiz_gif/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bamtSdK1qfJialHPbmZ4lKMOiaKP0JqapmZRK9YqEDXWV33wME30c4yuw/640?wx_fmt=gif&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

达尔文哥德尔机是一种通过重写自身代码来提升编程任务性能的自我改进型编程智能体。它能实现多种自我改进，包括：增加补丁验证步骤、优化文件查看功能、增强编辑工具、生成并排序多个解决方案以选择最优选项，以及在实施新修改时记录历史尝试记录（包括失败原因）。

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bFLg3QB1wRwtdcs1VRDYyIub4DUSPuEic2BpEmbWeyMk90iaHx3e5AU0Q/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

达尔文哥德尔机通过运用开放式探索原则，逐步构建起一个不断扩增的智能体库。该系统通过交替执行自我修改与下游任务评估的方式，持续创建新智能体并对其进行评分。

  

在 sw-bench 上，DGM 自动将其性能从 20.0% 提高到 50.0%。在 Polyglot 上，DGM 的表现从最初的 14.2% 跃升至 30.7%，远远超过了 Aider 手工设计的代表性智能体。这些可观的收益证明了 DGM 发现并实现对其自身代码的有益更改的能力。

  

## 模型的自我奖励训练：潜力、崩溃与缓解策略

  

- 论文标题：Can Large Reasoning Models Self-Train?
- 论文链接：https://arxiv.org/abs/2505.21444
- 项目地址：https://self-rewarding-llm-training.github.io/
- 代码地址：https://github.com/tajwarfahim/srt
- 数据集：https://huggingface.co/collections/ftajwar/self-rewarding-llm-training-6835218091832c3664176553

通过可验证奖励进行的强化学习显著增强了大语言模型的推理能力，尤其是在数学和编码方面。然而，这种方法依赖于人工创建的真实标签验证器，这使得为每个问题生成奖励信号的成本高昂且受到限制。在这项工作中，研究团队提出以下问题：

  

- 推理模型能否仅使用自身的反馈进行自我训练，而无需访问真实标签？
- 自我训练的性能能否达到基于真实标签的强化学习训练的水平？
- 自我训练能否无限期持续？其改进最终是否会受到限制？
- 哪些策略可以有效地维持模型的自我训练？

  

自我奖励培训（SRT）

  

受先前基于一致性自我提升研究的启发，研究团队引入了一种简单而有效的自我训练强化学习方法论，称为自我奖励训练（Self-Rewarded Training，SRT）。 该方法在强化学习训练期间，通过模型生成的多个解决方案之间的一致性来评估正确性，从而在没有标注数据的情况下提供自监督信号。

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bAF4phn5OuWe5ExHVn6adgYfTNibN6VG3ATcVVf8aEt7teXH1mcCs3SQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

SRT 概览。在 RLVR 方法中，系统通过真实验证器生成用于强化学习训练的奖励信号。与之相反，SRT 方法并不依赖真实验证器，而是通过模型自身生成结果的多数投票机制来估算真实值，并利用这一替代性奖励信号来训练模型。

  

## SRT 与早期训练阶段的 RL 性能相匹配

研究团队通过经验证明，在早期训练阶段，SRT 能够达到与那些在黄金标准答案上进行显式训练的标准强化学习方法相媲美的性能。测试数据集包括：AMC、AIME24、AIME25。 然而，研究团队发现其性能最终会崩溃，例如在最右图中展示的 DAPO 数据集上的训练情况。

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bhBjOKyCEZgADgMAgCDvX9KZ1V8WRTXwwQJN1EBTqlLFalrW4dLyIfA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  
自我训练必然会崩溃

  

研究团队分析了 SRT 在具有挑战性的 DAPO 数据集上训练时的训练动态。

  

![srt_training_dynamics](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2biaxicVG5L5LO8v4Bb29tVzybMDTQq7Dxhiapnv7ZVQxgxKnJks93vvEyw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

srt\_training\_dynamics

  

这些发现表明，模型通过产生一致（见上方第二个图）但错误（见上方最左图）的答案来学习最大化自我分配的奖励。人工检查证实了这一点：在崩溃之后，模型的输出会退化为随机的词元序列，并带有一个固定的、与提示无关的答案（例如，「答案是 1」）。这种行为有一个简单而精确的理论依据：

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bqloyWEmSaDtmwicteVIJ6MosibWrLsics7nG9SYhN8txXn4vHBgn7bcHg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

由 SRT 目标定义的强化学习优化问题明确鼓励输出之间的一致性，而不考虑其正确性。因此，在该目标下的最优策略会退化为无论输入如何都产生相同的答案，从而人为地最大化奖励。在这种代理 (proxy) 目标上持续进行自我训练，自然会驱动模型朝向这种平凡解 (trivial solution) 发展，特别是当这种解比解决实际任务更简单时。

  

缓解策略可能是有效的

  

研究团队提出了一些策略来缓解奖励作弊 (reward hacking)，为未来维持模型持续改进的有效方法奠定基础。

  

（i）早停（Early Stopping）：一个小的验证集可以可靠地检测到模型的最佳性能点，并防止在自我训练过程中发生崩溃。对于所有的留出集（heldout sets），最佳性能点几乎出现在同一位置，因此使用任何一个留出集进行早停都是有效的。

  

![srt_early_stopping](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bDdOiakqc4hXRhq6Q8EAwicgLqaFrMdDhaJrz22Wb4pl8M6jiaic5sqRJAw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

srt\_early\_stopping

  

（ii）使用离线生成的标签进行自我训练：一种有效的方法是从一个稳定的、先前固定的检查点生成伪标签，而不是利用来自演进中的策略的标签。这样做可以稳定训练，同时达到与 SRT 相当的性能。

  

![srt_offline_generated_data](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2b6LJYaAaYycd9mZoJZGaibAM0d2JA8NFE6CWs9W47j87O9LEMeCz5HMA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

srt\_offline\_generated\_data

  

（iii）结合课程学习的自我训练：研究团队假设，在更具挑战性的数据集上训练时，模型崩溃会发生得更快，这一推测与研究团队的经验性发现一致。其直觉是，在更具挑战性的数据集上，模型更容易放弃其预训练知识，转而优化自我一致性，而不是真正学习解决潜在的任务。研究团队利用这一假设，通过根据（a）通过率和（b）多数投票的频率来识别 DAPO 数据集中「最简单」的子集，从而实施一种课程学习策略（更多细节请参见论文）。

  

![srt_curriculum](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bCrMpQ1zZS7uuIMORibVibDAzktiaicmumXYZ7CVmEOseAAOHElARexfecg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

srt\_curriculum

  

在这些课程子集上的性能达到了与在整个 DAPO 数据集上使用真实标签进行标准强化学习训练相当的水平。这些富有前景的结果表明，课程学习策略可能会进一步扩展 SRT 的益处，为未来的研究开辟了激动人心的途径。

  

## MM-UPT：多模态大模型的持续自我进化

  

- 论文标题：Unsupervised Post-Training for Multi-Modal LLM Reasoning via GRPO
- 论文链接：https://arxiv.org/abs/2505.22453
- 项目代码：https://github.com/waltonfuture/MM-UPT

  

近年来，多模态大语言模型在视觉问答、图文推理等任务上取得了显著进展。然而，要在这些强大的基础模型之上进一步提升性能，往往需要依赖高质量人工标注数据进行监督微调或强化学习，这在成本与可扩展性上面临严峻挑战。过往研究虽然探索了无监督后训练方法，但大多流程复杂、难以迭代、数据利用率低。

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bBtmbTicyZx4SdNehsjnd9x1ibPstqaWKvjwzL6X8miblCC7ROcp9hn6Yg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

在这篇论文中，作者首次探索了在完全无监督场景下， 通过强化学习框架 GRPO 实现多模态大模型的持续自我改进。 他们提出了一种简洁而高效的框架：MM-UPT（Multi-Modal Unsupervised Post-Training），并在多个图文数学推理 benchmarks 上验证了其有效性。

  

MM-UPT 的核心思想主要为以下两个关键点：

  

- 强化学习中的 GRPO 提供了稳定高效的在线策略优化能力；
- 多数投票可以在无标签数据上为模型输出生成伪标签，驱动自我优化。

  

整个流程如下：

  

- 给定一张图片和一个问题，模型生成多个候选回答；
- 使用多数投票选出出现频率最高的回答，作为当前输入的「伪标签」；
- 使用这个「伪标签」来计算 reward，引导模型根据 GRPO 策略更新；

  

这整个过程无需任何外部监督信号或真实答案，使得模型可以基于自身的「共识」行为进行强化学习，从而实现持续的性能提升。

  

作者在四个多模态数学推理基准测试集（MathVisioan、MathVista、We-Math、MathVerse）上进行了广泛实验。表格 1 的结果显示：

  

- 在使用标准的训练集但不使用任何人工标注答案的情况下，MM-UPT 可以使 Qwen2.5-VL-7B 的准确率从 66.3% 提升至 72.9%（MathVista）；
- 超过之前的无监督自我改进方法（如 Genixer、STIC、SRLM 等）；
- 表现甚至媲美有监督的 GRPO；

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bxiaRGpDDQOrqxTVia6wmWMicYpD1P8WiahIzP6ClTXd0OawOOLxfBlMfqQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

在标准数据集上遮盖答案进行无监督训练后，作者进一步探究了一个更具挑战的问题：模型能否通过自己生成训练数据来实现自我提升？为此，MM-UPT 引入了两种简单的合成数据生成策略：

  

In-Context Synthesizing（上下文引导生成）

  

模型在给定图像、原问题和原答案的前提下生成一个新的问题。生成的问题与原问题在结构上相近，相当于进行语义改写或条件替换来进行数据增强。

  

Direct Synthesizing（直接生成）

  

仅提供图像输入，模型完全基于图片内容生成问题。这种方法生成的问题更加多样，但也存在一定概率的幻觉。 无论使用哪种方式生成问题，MM-UPT 都采用多数投票生成伪标签，驱动模型进行强化学习更新。

  

表格 2 中的结果显示：即便训练数据完全由模型自己生成，MM-UPT 仍然能显著提升多模态推理能力，甚至在部分任务上超越使用原始问题的数据。这表明，多模态大模型具备一定的「自我提问 + 自我优化」的潜力，为未来依靠 AI 自行生成训练语料进行自我进化的范式提供了坚实基础。

  

MM-UPT 为什么有效？作者用一个简单的例子解释了其有效性。假设模型对某个二分类问题，模型每次预测正确的概率较高， 。从该模型独立采样 个回答 ，多数投票选出出现频率最高的答案作为伪标签。定义随机变量 表示预测正确的次数，则多数投票正确的概率为：

  

  

由于 ，有：

  

  

即： 多数投票比单次预测更可靠。 这就是 MM-UPT 中用多数投票作为伪标签的合理性所在 —— 它可以构造一个有效的自监督奖励信号。但作者也指出了边界条件：当模型对任务缺乏先验时（如在 ThinkLite-11K 这种困难的数据集上），多数投票会反而强化错误预测，导致性能下降。

  

总的来说，MM-UPT 为多模态大模型的后训练阶段提供了一种无需人工标注、无需外部奖励模型的自我提升方式，展现了强化学习在无监督场景下的潜力。后续可以探索结合更强的自我评估机制（如 LLM-as-a-Judge）、复杂 reward 设计等，进一步拓展 MM-UPT 框架的能力边界。

  

UI-Genie：赋能 GUI 智能体高效自改进的新框架

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bBZv2QZibF6k4jmxzhRg7Pjib0setO7icJlK2X4zHCfnoicCcDnjdFEjamw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

- 论文标题：UI-Genie: A Self-Improving Approach for Iteratively Boosting MLLM-based Mobile GUI Agents
- 论文链接：https://arxiv.org/abs/2505.21496
- 项目地址：https://github.com/Euphoria16/UI-Genie

  

在这篇论文中，研究团队介绍了一种名为 UI-Genie 的自改进框架，旨在解决 GUI 智能体中的两大核心挑战：一是轨迹结果的验证十分困难，二是高质量训练数据的规模化获取不易。针对这两个挑战，研究团队分别提出了一种奖励模型和一个自改进流水线。

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bEkmyE04iaDia9a79KMpyz8jXKpRv8R7iaic9MU413DBcAicS1952sFJjsOw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

该奖励模型，即 UI-Genie-RM，采用了一种图文交错的架构，能够高效处理历史上下文信息，并统一了动作级别和任务级别的奖励：

  

- 通过迭代式合成轨迹生成，消除人工标注
- 通过自改进循环，共同演进智能体和奖励模型
- 无需人工干预即可生成高质量数据集

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2bZaZh3aZiaiaf5hewj2ian8SLuBt5eMUpicgSTbGIH6JicnKBiaic35icqnDGKQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

为了支持 UI-Genie-RM 的训练，研究团队开发了精心设计的数据生成策略，包括基于规则的验证、受控的轨迹损坏以及难负例挖掘。

  

为应对第二个挑战，研究团队设计了一个自改进流水线，通过在动态环境中进行奖励引导的探索和结果验证，逐步增强智能体和奖励模型的能力，从而扩展可解决的复杂 GUI 任务范围。

  

在模型训练方面，研究团队生成了 UI-Genie-RM-517k 和 UI-Genie-Agent-16k 数据集，这不仅是首个针对 GUI 智能体的奖励专用数据集，同时也展示了无需人工标注即可生成高质量合成轨迹的能力。

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2boAHb3MuoLSwjWhCG1yKUkJWRZncwz686VicCnDnp57CjMVGKIQ28Ckw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

UI-Genie 数据集统计信息。UI-Genie-RM-517k 是首个专用于 GUI 智能体的奖励数据集，而 UI-Genie-Agent-16k 则包含了无需人工标注的合成轨迹。

  

实验结果表明，经过三代数据与模型的自改进迭代，UI-Genie 在多个 GUI 智能体基准测试中均达到了业界领先水平。研究团队已将完整的框架实现和生成的数据集开源，以促进该领域的进一步研究。

  

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gW8wNC17uMWgqPz0LWF13O2boUEnNKCEHibXPPJf3V5sZic1IZ6DQYUn7ricIBLlhgR7HRghMPFpkuVEQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

UI-Genie、Qwen2.5-VL 和 UI-TARS 在三个基准上的性能比较。

  

关于模型自我改进的论文还有很多，如果你也在做相关研究，欢迎在评论区留言推荐自己的工作。

  

![Image](https://mmbiz.qpic.cn/sz_mmbiz_jpg/KmXPKA19gWic6dWJP4fbjQQ0J78sktTAY8Q0pKoPshHsT1ZicxickLRrlnTclR7SkR5cyxsuWkg44cQoGJ8N7ZibOw/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

© THE END

转载请联系本公众号获得授权

投稿或寻求报道：liyazhou@jiqizhixin.com

继续滑动看下一个

机器之心

向上滑动看下一个

Drag & drop here to download

图片将完成下载

AIX Downloader