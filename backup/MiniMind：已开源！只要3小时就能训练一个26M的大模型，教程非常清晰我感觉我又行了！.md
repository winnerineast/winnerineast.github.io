很多人都觉得训练大模型是个很难的事情，包括大部分的程序员自己也搞不出来。而且百亿参数个人设备也达不到训练的要求。
MiniMind的开源，恰好是解决了这个问题。让有一点代码基础的人都能很快训练出自己的大模型，注意，是从0开始训练，不是微调。
只需要3小时，就能从0训练一个26M参数的大模型，模型大小是GPT3的1/7000，而且最低最低2G显卡就能推理。
作者说：“这是一个既是开源项目，又是入门LLM教程，同时也是一个初具雏形的开源模型，希望能起到抛砖引玉的作用。”
**项目简介**
MiniMind 是一个轻量级的大语言模型项目，让用户可以在个人设备上快速训练和运行GPT模型。该项目可以使用极小的数据和计算资源，在3小时内训练出一个26M的模型，使大模型技术使用更加简单。MiniMind 支持单机单卡和多卡训练，兼容多个流行的框架，并提供完整的代码和文档支持，帮助初学者和研究者快速上手并进行定制和扩展。

MiniMind现在总共有5个模型，最小的是26M，已经有不错的对话能力了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/l2VB7h1M5NZd5jGjCTtBic4CDzLT82ciasY3yK75Rd0dwOMboAiaYqLVlacAQeOReucyYkCtQsZbN0vwE9ztWThmg/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**DEMO**

![图片](https://mmbiz.qpic.cn/mmbiz_png/l2VB7h1M5NZd5jGjCTtBic4CDzLT82ciasPFeweMYljhlNMhXjZ5bzFgmEib1kb7jiaEDUTFkm6NnE7f1DOmFGP9CA/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/l2VB7h1M5NZd5jGjCTtBic4CDzLT82cias7BFzrztxmncCflmDhiabjHgcBJNlybaEp7dttcibyGgLjg3EQdKeBfzg/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)
我自己也用了下这个模型，对于一些问题的回答上肯定不如千亿模型的效果好，但是也肯定有它的用武之地，比如训练一个对某方面知识及其了解的专家，他只对一个问题非常了解，当然也需要具备基础的大模型能力。

那么如果几千个这样的模型，就是几千个专家，这对一个行业来说，极有可能是回答效果极好的。只需要再有个大模型去给这些专家分配任务并总结，这样对于一个垂直领域大模型来讲，能力绝对是质的提升。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/l2VB7h1M5NZd5jGjCTtBic4CDzLT82ciasicRWbTNypib26LJY7rFXV54PIfuLWnGQUbZ8iaVuic8iaQTGwMRFuHTWfDA/640?wx_fmt=jpeg&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

**训练步骤**

**1.环境配置：**首先设置Python环境，安装如PyTorch等必要的库。

**2.数据准备：**下载并预处理训练所需的文本数据，例如从网上获取文本，然后使用提供的脚本进行数据清洗和格式化。项目作者已经给大家准备好了一些标注好的数据，大家可以直接下载试用。

**3.模型配置：**选择或调整模型的配置，如模型大小和训练参数等。

**4.模型训练：**使用提供的训练脚本开始训练。根据计算资源，可以调整批量大小和学习率等参数。

**5.模型评估与推理：**训练完成后，评估模型的性能并使用推理脚本进行测试，查看生成的文本质量。


注意：本文训练步骤只讲述的大体流程，具体的训练步骤可以到Github一步一步跟着做。

**项目链接**
https://github.com/jingyaogong/minimind