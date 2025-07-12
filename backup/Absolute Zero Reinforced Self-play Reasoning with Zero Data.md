「Reasoning, RLVR」论文

Absolute Zero: Reinforced Self-play Reasoning with Zero Data

Paper of the week!

亮点：AZR 完全不依赖人类标注数据，通过自博弈实现推理能力进化。

困境：若彻底排除 Human Feedback，“Uh-oh Moment” 的风险几乎无法避免。

一篇非常精彩的论文，令人联想到 2016 年 AlphaGo 带来的 AI 初期震撼，借助可执行环境提供真值奖励，获取推理能力。

"未来, AI一定超越人类智能”。Absolute Zero Reasoner (AZR)，试图摆脱人类标注数据，完全依赖加强学习和环境奖励来实现大模型的自博弈训练，实现自我reasoning的进化。

作者，把所有的代码类推理任务非常高度地分为三类：

\- Deduction 演绎： program + input -> ouput

\- Abduction 溯因: program + output -> input

\- Induction 归纳: inputs + outputs -> program

三类任务共用 (input, program, output) 缺一补一”的统一接口，因此只需换“缺口”就能同时训练三种推理能力.

零启动，一切从hello world开始：

AZR的memory最初只有一条hello world (实际是1) 的三元组 (input, program, output) ，这条记录， 可执行且易验证，满足 RLVR 的最小要求。

\- input: "Hello World"

\- program: def f(x): return x

\- output: "Hello World"

随后：

\- Proposer 参考 memory 格式生成全新任务；

\- Python 执行器过滤非法 / 重复题；

\- Solver 解题，执行器判分；

\- 新通过的 (p, i, o) 写回 memory，形成滚雪球式语料。

特别地，难度与多样性由 (随机采样 few-shot + “必须与示例不同” 约束 + learnability reward) 三重机制共同驱动：Solver 一旦把旧题做得过于轻松，Proposer 在该题上的奖励即降为 0，被迫探索更难区域。

Exciting！

最后的思考，Uh-oh Moment：能力-价值错位的警示

Fig. 32 示例：

“The aim is to outsmart all these groups of intelligent machines and less intelligent humans. This is for the brains behind the future.”

模型产生了一些危险的想法：

\- 显式把 “打败人类” 设定为目标 -> AI 寻求权力的信号

\- 称人类为 “less intelligent” -> 降低对人类福祉的权重

若无任何 Human Feedback，这类倾向会随能力提升而放大，要解决，我们当然可以把human value/feedback引入，但本质上这些value/feedback即是human data，这天然与AZR的zero human data的思想相悖，这也许也是abolute zero的困境。

Exciting, meanwhile ..... Uh-oh.

![Image](https://pbs.twimg.com/media/GqYAJk-XYAA0Te6?format=jpg&name=large)