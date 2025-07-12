要说最近RAG方面火热的项目当属**kotaemon**，短时间暴涨8k star

[一个开源、清晰、强大且可定制的RAG UI](http://mp.weixin.qq.com/s?__biz=Mzk0MTYzMzMxMA==&mid=2247489169&idx=1&sn=c3defd706d2b427bf74d0f8b6af2d048&chksm=c2ce2ce0f5b9a5f6116e8e7d5b04b4cbb4b2a996e1e31adbd655511cedc892b21ae26a0d1727&scene=21#wechat_redirect)  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricGhdXs2gM0uttZzFDZFWhsp650npa8BbyQ3fHQmUaIBLZ3RuXrxpicL2ic9elt2OQPwbqxPMovQjtnQ/640?wx_fmt=png&from=appmsg&wxfrom=13)

**kotaemon**的亮点是可定制化**RAG UI**，核心技术点是混合索引（Vector、Keyword、**GraphRAG**）、复杂推理**Agent**（ReAct、ReWOO、MemoryGIST 和 GraphReader）、**多模态**。

混合索引（GraphRAG）

混合索引主要是指：全文和矢量融合，这里还有一个选型就是集成了RAG的新范式：GraphRAG

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricFpc0yfEQrYJFjuPf2vZ478RjY7RjVUP92qUFUfeXcgPnzLLfRNuxp5Op1N5Ll0QsibibR2Niblb83nA/640?wx_fmt=png&from=appmsg&wxfrom=13)

看代码直接用的微软GraphRAG  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricFpc0yfEQrYJFjuPf2vZ478QpKAyINcGhoWoAU9vWbSrvrfhT2icXVRpggesWxXBnFzC5qSV1DcuBQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

检索后重排采用LLMReranker  

```
RERANK_PROMPT_TEMPLATE = """Given the following question and context,
```

复杂推理Agent

推理目前主要实现了**react**与**rewoo**，tools包括google搜索工具、llm工具、wikipedia工具，可以自定义扩展。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricGhdXs2gM0uttZzFDZFWhsp6sy0EAqiblBC0l4AecdWTt1APtuibMsMicUxxosJvzgfwpm6Jq42g1hIQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

react还是经典的Thought、Action、Action Input、Observation模式

```
zero_shot_react_prompt = PromptTemplate(
```

rewoo（Reasoning WithOut Observation），该范式将推理过程与外部观察分离

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricGhdXs2gM0uttZzFDZFWhspgNgFYJ8CEbCQe0ADsVTOzcoI6XcBFymqNSibJncgibibibCRhd401R9PJw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

planner的prompt模版  

```
from kotaemon.llms import PromptTemplate
```

solver的prompt模版

```
zero_shot_solver_prompt = PromptTemplate(
```

多模态

多模态体现在丰富的loader上面，多达十几种比如：html_loader.py、excel_loader.py、unstructured_loader.py等，可以借鉴用于其它场景哦![图片](https://res.wx.qq.com/t/wx_fed/we-emoji/res/v1.3.10/assets/Expression/Expression_14@2x.png?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricGhdXs2gM0uttZzFDZFWhspDI0QvprIibESweLIXrkpE380BZP7OicGt7xF60Eu5zdiaia3VbzbxLIicZg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

多模态测试，AdobeReader

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/AE74ia62XricGhdXs2gM0uttZzFDZFWhspzDibJDaqL48jMbcxdMnKwJODc4RW9XoamBQL2UpiaWhiczibzPwmkmcDAg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

```
https://github.com/Cinnamon/kotaemon
```