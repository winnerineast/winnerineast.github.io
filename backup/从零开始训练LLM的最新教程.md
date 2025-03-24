模型训练专家Sebastian Raschka发布了一个从零开始预训练LLM的最新教程，内容包括理解、计算和优化损失函数的详细步骤，以及如何使用温度缩放和top-k采样更新文本生成功能。

教程还提供了10个加速LLM训练的技巧：    

（1）动态创建因果掩码以减少内存使用

（2）使用张量核心（适用于A100等Ampere GPU及更新版本）

（3）使用AdamW的CUDA融合内核

（4）通过数据加载器中的锁定内存设置预分配和重用GPU内存

（5）从32位浮点切换到16位脑浮点(bfloat16)精度

（6）用PyTorch优化的CUDA内核替代从头实现的注意力机制等

（7）使用FlashAttention提高内存读写效率

（8）编译模型

（9）优化词汇表大小

（10）在节省内存后增加批处理大小

这些技巧不仅适用于LLM，也适用于视觉Transformer等其他基于Transformer的模型。

教程链接：https://www.youtube.com/watch?v=Zar2TJv-sE0