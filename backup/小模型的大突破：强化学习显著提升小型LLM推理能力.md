新加坡Knovel Engineering Lab的研究人员Quy-Anh Dang和Chris Ngo展示了如何用极低成本提升小型LLM的推理能力。他们仅使用4块NVIDIA A40 GPU，在24小时内将1.5B参数的小模型DeepSeek-R1-Distill-Qwen-1.5B的数学推理能力显著提升。

研究表明：

（1）AMC23测试准确率从63%提升至80%

（2）AIME24测试中达到46.7%的准确率，超越了o1-preview模型

（3）仅使用7,000个样本，总训练成本只有$42美元，而基线模型通常需要花费数千美元    

这项研究证明了强化学习在资源受限环境下提升小型LLM推理能力的有效性，为低成本AI研究提供了新方向。

论文标题：Reinforcement Learning for Reasoning in Small LLMs: What Works and What Doesn't

论文链接：https://arxiv.org/abs/2503.16219

代码和数据集：https://github.com/knoveleng/open-rs