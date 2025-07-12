*2025年06月14日 12:12*

机器之心报道

**编辑：Panda**

  

近段时间，关于 AI 自我演进/进化这一话题的研究和讨论开始变得愈渐密集。

  

本月初我们就曾梳理报道了一些，包括 Sakana AI 与不列颠哥伦比亚大学等机构合作的「达尔文-哥德尔机（DGM）」、CMU 的「自我奖励训练（SRT）」、上海交通大学等机构提出的多模态大模型的持续自我改进框架「MM-UPT」、香港中文大学联合 vivo 等机构的自改进框架「UI-Genie」，参阅文章《 [LSTM 之父 22 年前构想将成真？一周内 AI「自我进化」论文集中发布，新趋势涌现？](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650971628&idx=1&sn=1f3baa09a3d3953449c96f91b1e4b205&scene=21#wechat_redirect) 》

  

那之后，相关研究依然还在不断涌现，以下拼图展示了一些例子：

  

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gWic9azdeeuXskgMJmSdcFrs8a9jsk3aqicTyGzeAgRjVVlVpqJy8L832J6wNJWcjknYiaYLVyDrZHRkQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

而前些天，OpenAI CEO、著名 𝕏 大 v 山姆・奥特曼在其博客《 [温和的奇点（The Gentle Singularity）](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650973028&idx=1&sn=a2f73b4f163a3375c182af86c31eb933&scene=21#wechat_redirect) 》中更是畅想了一个 AI/智能机器人实现自我改进后的未来。他写道：「我们必须以传统的方式制造出第一批百万数量级的人形机器人，但之后它们能够操作整个供应链来制造更多机器人，而这些机器人又可以建造更多的芯片制造设施、数据中心等等。」

  

不久之后，就有 𝕏 用户 @VraserX 爆料称有 OpenAI 内部人士表示，该公司已经在内部运行能够递归式自我改进的 AI。这条推文引起了广泛的讨论 —— 有人表示这不足为奇，也有人质疑这个所谓的「OpenAI 内部人士」究竟是否真实。

  

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gWic9azdeeuXskgMJmSdcFrs8tA06GmJia8MDrRiaicrrwnib8sHib6dxdibFWYuFzH5OGvUBUxcribEfpuBOQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

https://x.com/VraserX/status/1932842095359737921

  

但不管怎样，AI 也确实正向实现自我进化这条路前进。

  

MIT 昨日发布的《Self-Adapting Language Models》就是最新的例证之一，其中提出了一种可让 LLM 更新自己的权重的方法： SEAL🦭 ，即 Self-Adapting LLMs。在该框架中，LLM 可以生成自己的训练数据（自编辑 /self-editing），并根据新输入对权重进行更新。而这个自编辑可通过强化学习学习实现，使用的奖励是更新后的模型的下游性能。

  

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gWic9azdeeuXskgMJmSdcFrs8eibwntPiaSorqkrSsJTVRTelZ0CMXHbK9KVNW7C7ya5250QZicUVfNPUQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

- 论文标题：Self-Adapting Language Models
- 论文地址：https://arxiv.org/pdf/2506.10943
- 项目页面：https://jyopari.github.io/posts/seal
- 代码地址：https://github.com/Continual-Intelligence/SEAL

  

这篇论文发布后引发了广泛热议。在 Hacker News 上，有用户评论说，这种自编辑方法非常巧妙，但还不能说就已经实现了能「持续自我改进的智能体」。

  

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gWicmlEGrdiaLjDZic1oJAJLG6qlragzMcxc7h1dFBLCKehn8QWFkoNsj4gMwVcosnJGk5Via3Q2ocKEjA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

论文一作 Adam Zweiger 也在 𝕏 上给出了类似的解释：

  

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gWicmlEGrdiaLjDZic1oJAJLG6qKlIhFWpSIkib5vWrmLmqeYj7PhJJeSIn7zx3vT9YBAibfQF5u2ZUpHqw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

也有人表示，这表明我们正在接近所谓的 事件视界（event horizon） —— 这个概念其实也出现在了山姆・奥特曼《温和的奇点》博客的第一句话，不过奥特曼更激进一点，他的说法是「我们已经越过了事件视界」。简单来说，event horizon（事件视界）指的是一个不可逆转的临界点，一旦越过，人类将不可避免地迈入某种深刻变革的阶段，比如通向超级智能的道路。

  

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gWicmlEGrdiaLjDZic1oJAJLG6q1nDIEYvvyDrIPyl7rAiaqXdiabwjhSwOlXh9KmPwLLziaED2vlEsBKaEA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

当然，也有人对自我提升式 AI 充满了警惕和担忧。

  

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/KmXPKA19gWicmlEGrdiaLjDZic1oJAJLG6qduDZiae7EKJpoCjTq8iby4LNcpHcStG3Iye79oaicbYhRFSAiaTfqibguGA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

下面就来看看这篇热门研究论文究竟得到了什么成果。

  

自适应语言模型（SEAL）

  

SEAL 框架可以让语言模型在遇到新数据时，通过生成自己的合成数据并优化参数（ 自编辑 ），进而实现自我提升。

  

该模型的训练目标是：可以使用模型上下文中提供的数据，通过生成 token 来直接生成这些自编辑（SE）。

  

自编辑生成需要通过强化学习来学习实现，其中当模型生成的自编辑在应用后可以提升模型在目标任务上的性能时，就会给予模型奖励。

  

因此，可以将 SEAL 理解为一个包含两个嵌套循环的算法：一个外部 RL 循环，用于优化自编辑生成；以及一个内部更新循环，它使用生成的自编辑通过梯度下降更新模型。

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

该方法可被视为 元学习 的一个实例，即研究的是如何以元学习方式生成有效的自编辑。

  

通用框架

  

令 θ 表示语言模型 LM\_θ 的参数。 SEAL 是在单个任务实例 (C, τ) 上运作，其中 C 是包含与任务相关信息的上下文，τ 定义了用于评估模型适应度（adaptation）的下游评估。

  

比如，在知识整合任务中，C 是旨在整合到模型内部知识中的段落，τ 是关于该段落的一组问题及其相关答案。而在少样本学习任务中，C 包含某个新任务的少样本演示，τ 是查询输入和 ground-truth 输出。

  

给定 C，模型会生成一个自编辑 SE（其形式因领域而异），并通过监督微调更新自己的参数：θ′ ← SFT (θ, SE)。

  

该团队使用了强化学习来优化自编辑的生成过程：模型执行一个动作（生成 SE），再根据 LM\_θ′ 在 τ 上的表现获得奖励 r，并更新其策略以最大化预期奖励：

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

不过，与标准强化学习设置不同，在这里的设置中，分配给给定动作的奖励取决于执行动作时的模型参数 θ（因为 θ 会更新为 θ′，然后再被评估）。

  

如此一来，底层的强化学习状态必定会包含策略的参数，并由 (C, θ) 给出，即使策略的观测值仅限于 C（将 θ 直接置于上下文中是不可行的）。

  

这意味着，使用先前版本模型 θ\_old 收集的 (state, action, reward) 三元组可能会过时，并且与当前模型 θ\_current 不一致。因此，该团队采用一种基于策略的方法，其中会从当前模型中采样自编辑 SE，并且至关重要的是，奖励也会使用当前模型进行计算。

  

该团队尝试了各种在线策略方法，例如组相对策略优化 (GRPO) 和近端策略优化 (PPO) ，但发现训练不稳定。

  

最终，他们选择了来自 DeepMind 论文《Beyond human data: Scaling self-training for problem-solving with language models.》的 ReST^EM ，这是一种基于已过滤行为克隆的更简单的方法 —— 也就是「 拒绝采样 + SFT 」。

  

ReST^EM 可以被视为一个期望最大化 (EM) 过程：E-step 是从当前模型策略采样候选输出，M-step 是通过监督微调仅强化那些获得正奖励的样本。这种方法可在以下二元奖励下优化目标 (1) 的近似：

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

更准确地说，在优化 (1) 时，必须计算梯度 。然而，在这里的设置中，奖励项 r (SE, τ, θ\_t) 取决于 θ\_t，但不可微分。为了解决这个问题，该团队的做法是将奖励视为相对于 θ\_t 固定。通过这种近似，对于包含 N 个上下文和每个上下文 M 个采样得到自编辑的小批量，其蒙特卡洛估计器变为：

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

其中 p\_θ\_t 表示模型的自回归分布，y\_s^(i,j) 是自编辑 SE\_ij 的第 s 个 token，即上下文 C\_i 的第 j 个样本。由于在 (4) 中可以忽略 r = 0 的序列，该团队研究表明：在二元奖励 (2) 下（对奖励项应用停止梯度），ReST^EM 只需使用简单的「在好的自编辑上进行 SFT」，就能优化 (1)。算法 1 给出了 SEAL 的训练循环。

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

最后，他们还注意到，虽然本文的实现是使用单个模型来生成自编辑并从这些自编辑中学习，但也可以将这些角色分离。在这样一种「教师-学生」形式中，学生模型将使用由另一个教师模型提出的编辑进行更新。然后，教师模型将通过强化学习进行训练，以生成能够最大程度提高学生学习效果的编辑。

  

针对具体领域实例化 SEAL

  

理论有了，该团队也打造了 SEAL 的实例。具体来说，他们选择了两个领域：知识整合和少样本学习。

  

其中，知识整合的目标是有效地将文章中提供的信息整合到模型的权重中。下图展示了相关设置。

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

而下图则给出了少样本学习的设置。

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

对这两种实例化的更详细描述请访问原论文，下面来看看 SEAL 的实际表现。

  

实验结果

  

少样本学习

  

实验所用的模型是 Llama-3.2-1B-Instruct，基准为 ARC。参与对比的方法包括 ICL（上下文学习）、TTT + 自编辑（无强化学习）、Oracle TTT。结果见下表。

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

可以看到，与基线相比，SEAL 显著提高了适应成功率：72.5% vs. 20%（使用基础模型的自编辑但未进行强化学习训练）和 0%（无适应），但性能仍低于 Oracle TTT，表明新方法仍有进一步改进的空间。

  

知识整合

  

知识整合则使用了更大一些的 Qwen2.5-7B，目标是整合 SQuAD 文章中的新事实内容。这里对比的方法包括基础模型、仅在文章上训练的模型、在文章 + 合成数据训练的模型、在文章 + GPT-4.1 合成数据上训练的模型。结果见下表。

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

可以看到，在单篇文章（n = 1）和持续预训练（n = 200）这两种情况下，SEAL 方法的准确度表现都超过了基准。

  

首先使用基础 Qwen-2.5-7B 模型生成的合成数据训练后，模型的表现已经能获得明显提升，从 32.7% 分别提升到了 39.7% 和 41.0%，之后再进行强化学习，性能还能进一步提升（47.0% 和 43.8%）。

  

图 4 展现了每次外部强化学习迭代后的准确度。

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

可以看到，两次迭代足以使 SEAL 超越使用 GPT-4.1 数据的设置；后续迭代的收益会下降，这表明该策略快速收敛到一种将段落蒸馏为易于学习的原子事实的编辑形式（参见图 5 中的定性示例）。

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

在这个例子中，可以看到强化学习如何导致生成更详细的自编辑，从而带来更佳的性能。虽然在这个例子中，进展很明显，但在其他例子中，迭代之间的差异有时会更为细微。

  

另外，该团队也在论文中讨论了 SEAL 框架在灾难性遗忘、计算开销、上下文相关评估方面的一些局限，详见原论文。

  

最后，来个小调查，你认为真正的 自我进化式 AI 将在何时实现？

  

  

![Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

© THE END

转载请联系本公众号获得授权

投稿或寻求报道：liyazhou@jiqizhixin.com

继续滑动看下一个

机器之心

向上滑动看下一个

Drag & drop here to download

图片将完成下载

AIX Downloader