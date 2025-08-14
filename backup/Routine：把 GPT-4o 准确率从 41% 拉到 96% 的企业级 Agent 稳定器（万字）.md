“ Routine 框架用 400 行 JSON 把 GPT-4o 在企业场景的端到端准确率从 41% 拉到 96%，14B 小模型也能逼近 SOTA——本文章拆解它到底做对了什么。”



大家好，我是肆〇柒。在企业落地 AI 的进程中，自主智能体凭借其强大的自主决策与任务执行能力，可以成为企业提升效率、优化流程的关键力量。然而，当我们将视角聚焦于企业级应用场景时，不难发现，部署智能体系统并非易事。在企业级 LLM 智能体（Agent）系统的落地过程中，开发者往往被两个问题反复折磨：

1. 工具调用链路的正确率不可控；
2. 一旦工具规模超过 20 个，准确率便雪崩式下滑。
比如，以企业财务报表智能分析为例，智能体需精准调度数据采集、预处理、指标计算等工具。然而，实际运行中，规划模型常因缺乏对财务系统深度耦合的认知，生成的执行方案漏洞百出：关键的财务指标计算工具未被调用，数据预处理步骤顺序颠倒，最终导致整个分析流程陷入混乱。这样的案例揭示出企业在利用智能体解决复杂任务时遭遇的瓶颈——智能体系统难以在企业特定场景中保持执行的稳定性和准确性。

这引发了一个需要解答的关键问题：如何为智能体系统注入强大的“导航仪”，使其在企业复杂的数字化场景中稳定、精准地执行任务？

本文聚焦的 Routine 框架（Digital China AI Research）正是为了解决上述痛点而生。它用“结构化规划”取代“自由生成”，用“可验证步骤”取代“模糊指令”，从而在真实企业场景中把 GPT-4o 的端到端正确率从 41% 提升到 96%，让 14B 参数的本地模型逼近 GPT-4o 水平。下面将围绕 Routine 的机制设计、系统架构、数据工程与训练策略展开，所有结论均基于企业级实验验证。

Image

Routine 机制设计：从痛点到解决方案
为了更好地理解Routine框架如何解决痛点，下图展示了其引导LLM智能体完成多步骤工具调用的机制。通过这种结构化的方式，Routine为智能体的执行过程提供了清晰的指导。

Image
Routine框架引导LLM智能体完成多步骤工具调用的机制示意图
显式工具字段
早期痛点：工具选择错误率高，模型在无明确指引时难以从海量工具中精准挑选适配工具。当工具池规模达到 25 个及以上时，GPT-4o 的工具选择错误率高达 58.9%。在企业级场景中，智能体需要从海量工具中精准挑选适配工具，但现有模型在无明确指引时难以胜任这一任务。

Routine 约束：在每一步骤中显式标注工具名称（Step Tool）。

实现方式：定义了 “Step Tool” 字段，确保智能体在执行时直接读取指定工具，无需推理工具选择。这为执行模块提供了精准的工具调用蓝图，减少了因规划模糊导致的工具误调用等问题。

输入输出参数描述
早期痛点：参数幻觉问题频发，模型常因缺乏参数上下文而生成错误调用指令。

Routine 约束：为每一步骤提供详细的输入描述（Input Description）和输出描述（Output Description）。

实现方式：通过自然语言明确参数来源和目标，帮助智能体准确填充工具参数。这为模型提供了丰富的上下文信息，尤其对中小规模模型助力显著，使其参数准确率大幅提升。

变量内存优化
早期痛点：企业任务流程复杂且环环相扣，对准确性和稳定性要求极高。以金融领域的风险评估为例，智能体需从多个异构数据库中提取数据，运用复杂模型运算，最终生成评估报告。任何一个微小偏差都可能引发巨大风险。现有智能体架构在处理此类任务时，常因上下文管理效率低下而陷入混乱。所以，上下文爆炸问题导致模型执行效率低下，尤其在多步骤工具调用中表现明显。

Routine 约束：引入 Variable Memory 机制，采用 key-value 映射优化参数传递。

实现方式：智能体只需传递变量键而非完整值，显著降低上下文压力。当工具返回 10KB 的 JSON 时，执行模块仅存储键 memory_xxx，后续步骤通过键引用实际值，使上下文长度降低 90%。

AI 驱动的 Routine 优化
AI驱动的Routine优化是提升智能体执行效率的关键环节。下图详细展示了AI如何优化和管理Routine的流程，通过这种方式， Routine能够更好地适应企业不断变化的需求。

Image
 AI优化和管理Routine的流程图
早期痛点：现有智能体系统对领域专家的依赖程度较高。当前系统对专家草稿的耦合度≈100%。当企业引入新型工具（如区块链溯源工具）时，规划模型无法自主识别其在流程中的精准定位，需依赖专家重新起草规划草稿。领域专家稀缺，智能体系统难以快速复用专家知识。

Routine 约束：通过 AI 优化专家草稿，生成结构化 Routine。

实现方式：AI 将专家草稿转化为包含工具映射的完整 Routine，减少专家重复劳动。例如，专家提供 “查询库存 → 比对订单 → 生成补货单” 的草稿，AI 通过附录 A.1 的 Prompt 模板将其转化为包含工具名的 5 步 Routine，其中 “比对订单” 被拆分为两个子步骤以适配工具接口限制。

分支逻辑处理
早期痛点：复杂流程中的分支逻辑导致执行稳定性下降，模型在面对条件判断时容易出错。

Routine 约束：支持分支结构（Branch），通过条件判断引导不同执行路径。

实现方式：定义了分支步骤格式（Branch X-n Step i），为智能体提供清晰的条件判断逻辑。若 Routine 第 3 步为分支判断（如 “库存 < 阈值？”），执行模块需调用库存查询工具，解析返回结果中的数值，根据条件跳转到 “生成补货单” 或 “通知采购” 分支。

Routine 框架与系统架构：从规划到执行的闭环设计
下图呈现了Routine框架在智能体系统中的整体架构，展示了从规划到执行的各个模块如何协同工作。这一架构设计确保了智能体能够在企业复杂场景中高效、稳定地执行任务。

Image
 Routine框架与系统架构图
一条 Routine 的生命周期：从文本到 JSON
组成要素
Image
Routine 的组成部分。注：标有 * 的组件为可选元素
Routine 的设计比较严谨，其组成部分环环相扣，共同构建起智能体执行的坚实基础。步骤编号为智能体指明执行顺序；步骤名称以简洁语言概括步骤核心功能；步骤描述则详细阐述执行条件、目标及操作细节，为智能体提供详尽的操作指南。
输入描述清晰界定步骤所需参数，确保智能体在执行前就备齐“弹药”。输出描述提前规划步骤完成后产生的结果，为后续步骤衔接提供保障。步骤工具精准锚定每一步骤对应的工具，实现智能体能力与任务需求的完美匹配。

以企业财务报表智能分析场景为例，一个典型的 Routine 可能包含以下步骤：

• 步骤 1 为“数据采集”，利用“数据库查询工具”从财务系统中提取特定时间段的收入、支出等数据；
• 步骤 2 为“数据预处理”，调用“数据清洗工具”对采集到的数据进行缺失值填充、异常值处理等操作；
• 步骤 3 为“财务指标计算”，运用“财务分析模型工具”计算毛利率、净利率等关键指标。
对于包含分支结构的 Routine，其格式如下：

Step X. <Step Name>: This step performs a branch condition check:
• Branch X-1 Step 1. <Step Name>: If <Condition>, perform <Step Description>, using the <Tool Name> tool;
• Branch X-1 Step 2. <Step Name>: <Step Description>, using the <Tool Name> tool;
• Branch X-2 Step 1. <Step Name>: If <Condition>, perform <Step Description>, using the <Tool Name> tool; Step Y. <Step Name>: <Step Description>, using the <Tool Name> tool; Step Z. <Step Name>: <Step Description>, using the <Tool Name> tool, and terminate the workflow;
双格式表示
Routine 支持自然语言格式与结构化 JSON 格式并存，二者相得益彰，满足不同场景需求。自然语言 Routine 以流畅语言描述步骤流程，便于人类专家快速理解与审核，相当于为智能体执行流程撰写了一份通俗易懂的“说明书”。

结构化 JSON 格式则以严谨的数据结构呈现 Routine，为智能体系统解析与执行提供便利。它将每一步骤的编号、名称、描述、工具等信息封装为标准字段，确保智能体能够精准无误地读取与解析。

JSON 格式示例如下：

[
  {
    "step":"1",
    "name":"Get announcements",
    "description":"Download the latest employee handbook file from the company’s internal system",
    "tool":"fetch_latest_announcements",
    "type":"node"
},
{
    "step":"2",
    "name":"Download handbook",
    "description":"Obtain the company’s most recent official announcement for consistency check with the employee handbook",
    "tool":"download_file",
    "type":"node"
},
{
    "step":"3",
    "name":"Read PDF content",
    "description":"Use text parsing tools to extract all text content from the employee handbook PDF file",
    "tool":"read_pdf",
    "type":"node"
},
{
    "step":"4",
    "name":"Compare text differences",
    "description":"Compare the relevant content in the employee handbook with the company’s latest announcement word by word",
    "tool":"compare_texts",
    "type":"finish"
}
]
特别地，type: finish 字段用于标记流程终止步骤，确保智能体在执行到该步骤时能够正确结束工作流程。

AI 优化生成
Routine 的生成从专家编写的规划提示开始。专家根据对企业任务流程的深刻理解，以自然语言草稿形式勾勒出任务执行的大致轮廓，包括关键步骤、目标等核心要素。

AI 驱动的优化过程首先把规划拆解为更小的可操作任务。首先对规划进行深度分解，将模糊的步骤细化为具体可操作的子步骤。以“处理客户投诉”任务为例，专家草稿仅提及“分析投诉原因”，AI 则将其细化为“提取投诉关键词”“识别投诉类别”“定位问题根源”等子步骤。

接下来，模型将这些子步骤精准映射到可用工具上。在映射过程中，模型充分考量工具的功能说明、参数要求等细节，确保工具选用契合度。最终，AI 输出结构化的 Routine，其语言流畅、逻辑严谨，为执行模块提供清晰指引。

为助力 Routine 生成，研究者设计了如下 Prompt 模板：

prompt = f"""You are a Routine workflow writer for a company. You can write the operation step flow based on the process information provided by the user and the available tools.
The steps are written in structured json and lists. Write the flow in the following way:
[{{"step": "1", "name": "xxxxx", "description": "xxxxxxxxxxxx", "tool": "tool_X", "type": "node"}},
{{"step": "2", "name": "xxxxx", "description": "xxxxxxxxxxxx", "tool": "tool_Y", "type": "node"}}]

The format is a json list. Each step contains the step number, step name, step action description, step input, step output, step tool, and node type.
The input and output of the step do not have to be very specific. Use natural language to write the possible input and output according to the tool. Only one tool is used for each step.
When you may encounter branch condition judgment in a certain step, express it in the following way and indicate under what conditions to enter a branch, what tool to use;

{{"step": "x", "name": "xxxxx", "type": "branch"}},
{{"step": "x-1_1", "name": "xx", "description": "xxxx", "tool": "tool_X1", "type": "branchnode"}},
{{"step": "x-2_1", "name": "xx", "description": "xxxx", "tool": "tool_X2", "type": "branchnode"}},
{{"step": "y", "name": "xxxxx", "description": "xxxxxx", "tool": "tool_Y", "type": "node"}}
If the next branch step involves multiple steps, you can open a new branch workflow, for example:
{{"step": "x-n_1", "name": "xx", "description": "xxxx", "tool": "tool_X", "type": "branchnode"}},
{{"step": "x-n_2", "name": "xx", "description": "xxxx", "tool": "tool_Y", "type": "branchnode"}}

Regarding the writing of step numbers, x-n_i represents the i-th step in the n-th branch of the main line step x;
Please pay attention to the description in the tool and the parameters that need to be filled in, which need to be fed back in the input of each step;
Pay attention to the branch judgment in the process information, and do not write multiple possibilities of branch conditions in the steps of the same line;
When a step is completed and the workflow needs to be ended, please change the node type of the step to "finish", set "type": "finish"; For example:
{{"step": "x", "name": "xxxxx", "description": "xxx", "tool": "tool_X", "type": "finish"}}
Note: Each workflow step must use a tool provided in the tool list, or perform branch condition judgment. There will be no "no tool needed", "no tool used ", or use of non-existent tools. Each step only uses one tool.
The following is the process information provided by this user: {routine_draft};
In the tool list, these tools are available: {tool_list}; Now please convert it into a structured Routine workflow. Do not output other prefixes, suffixes, or meaningless information, and please output in Chinese."""
数据工程：让 Routine 可训练、可蒸馏
通用 Routine 数据合成
研究团队利用 BUTTON 开源数据集合成通用 Routine 数据，以增强模型在不同场景下的鲁棒性。BUTTON 数据集包含 8,000 个单轮多步工具调用实例，涵盖多种常见任务类型。每个实例交替包含 tool_call 和 observation，形成清晰的执行轨迹。

通过 GPT-4o 和专用 Prompt 模板，研究团队生成精准结构化的 Routine，每个 Routine 包括步骤索引、名称、功能目标和对应工具名称。基于标准化执行 Prompt 模板构建新系统 Prompt，提升模型对多种工作流机制的适应性。

数据过滤规则：

1. Routine 文本验证：过滤掉空响应或异常输出；
2. 移除自然语言摘要：保留用户查询、工具调用和对应观察；
3. 长度和结构过滤：剔除超过 8 个工具调用步骤的实例，移除含复杂数据结构的实例。
最终保留 4,209 条高质量轻量级训练数据。

以下是通用 Routine 跟随数据集过滤流程图，展示了如何通过一系列步骤筛选出高质量的训练数据：

Image
常规 Routine-following 数据集过滤流程
场景特定数据的 GPT-4o 蒸馏
在特定场景中，Routine 还可用于知识蒸馏。以 HR 智能体场景为例，研究团队设计 50-60 个用户查询模板，基于 10 个非分支子场景生成约 50-60 个用户查询。通过数据清洗和 LLM 同义改写，增强数据多样性。

使用 GPT-4o 和 Routine 蒸馏生成 537 条单轮多步用户查询，包含 3,108 个标注工具调用指令。这些数据用于训练场景特定的执行模型，显著提升模型在特定场景下的准确率。

系统模块：执行、工具与记忆
执行模块与小型 LLM 设计
执行模块负责接收规划模块生成的 Routine，并按其路径输出工具调用指令。考虑到执行过程中的大量上下文，执行模块通常由小型专用指令跟随模型驱动。

选择小型模型的优势：

1. 节省资源：小型模型在执行每一步骤时消耗较少算力和时间，易于在企业环境中部署；
2. 高效指令跟随：只需关注指令跟随和多步工具调用，无需复杂逻辑推理。
Qwen3 系列小型 Instruct 模型在指令跟随和中文理解方面表现出色，且参数量小，是执行模块的理想选择。

工具模块与 MCP 协议
工具模块负责接收工具调用指令并返回执行结果。MCP 服务器作为工具模块的核心，定义和管理智能体可用的工具集合。

MCP 协议的优势：

1. 工具标准化：统一描述工具名称、参数类型和调用约束，使执行模块无需管理工具实现细节；
2. 高可扩展性：便于开发者添加新功能或连接新系统，构建多样化工具生态。
记忆模块
记忆模块负责存储和检索任务执行过程中的关键信息。它包含两种内存形式：长期 Procedure Memory 和短期 Variable Memory。

Procedure Memory 存储专家与规划模块协作生成的 Routine 集合。在部署前，专家将必要的 Routine 集合存入内存基座。系统接收查询时，基于 Routine 描述与用户任务的相似性计算，检索对应 Routine，协助执行模块。

Variable Memory 优化多步工具调用间的参数传递。当工具调用返回过长参数时，系统自动存储至变量内存基座。模型只需提供对应键，而非完整值。接收工具调用请求时，记忆模块将键回溯为实际参数值。Variable Memory 通过键值映射减少 90% 上下文长度，显著降低上下文压力，减少 token 消耗和语法错误，提升执行模块性能。

以下是智能体变量内存机制示意图，展示了 Variable Memory 如何优化多步工具调用中的参数传递：

Image
 智能体可变记忆机制示意图
训练策略：场景化 LoRA 微调
基模选择与训练目标
在 HR 智能体场景中，执行模型需要具备指令跟随、初步工具调用能力和较强中文理解能力。选择 Qwen3 系列小型 Instruct 模型作为基模。训练目标是提升模型对 Routine 的遵循能力，而非利用推理生成工具调用指令。

LoRA 超参数与硬件配置
采用 LoRA 轻量级微调策略，避免过拟合，提升计算性价比。实验使用 LLaMA-Factory 框架，结合 DeepSpeed ZeRO-3 和 Flash Attention-2，最大化计算效率，显著降低多 GPU 训练时的 GPU 内存使用。

训练参数：

• LoRA 秩：8
• 批大小：1×4 GPU
• 有效批大小：16
• 学习率：1e-4
• 训练周期：3 epoch
以下是智能体执行模型训练过程图，展示了整个训练流程，包括通用 Routine 跟随能力训练和场景特定工具调用能力训练：

Image
智能体执行 routine（模型训练流程）
实验验证与结果分析
工具调用准确率提升
在未引入 Routine 时，模型表现不佳。实验数据显示，工具选择错误占比高达 85%。在企业智能法务审核场景中，模型需从 30 余种工具中精准挑选，无 Routine 指导时，工具选择错误率高达 78%。

引入 Routine 后，模型执行流程变得有序。在 HR 智能体测试集（1,148 个样本）中，GPT-4o 的端到端准确率从 41.1% 提升至 96.3%。Qwen3-14B 在有分支 Routine 下的准确率为 81.3%，无分支 Routine 下的准确率为 83.6%。GPT-4o 基于 Routine 蒸馏生成的 537 条场景特定数据，使 Qwen3-14B 的准确率达到 95.5%。

具体到各项指标：

• 结构正确率从 68% 提升至 97%；
• 工具选择准确率从 35% 提升至 88%；
• 参数准确率从 52% 提升至 81%。
以下是企业场景中 AST 评估工作流程图，展示了如何基于 BFCL 框架对模型的工具调用进行评估：

Image
 企业场景下的 AST evaluation workflow（沿用 routine 框架）
以下是不同 Routine 配置下 HR 智能体系统场景中各模型的整体准确率表：

Image
在 HR 智能体系统场景下，不同 Routine 配置下模型的整体准确率
训练策略的影响
常规 Routine 跟随微调
基于通用 Routine 跟随数据集的微调可显著提升模型在有 Routine 指导场景下的执行准确率。以 Qwen3-14B 为例，微调后整体准确率提升 14.6 个百分点。但此类模型在无 Routine 指导场景下的表现有所下降，表明其更擅长执行明确规划的任务，而非自主规划。

场景特定数据蒸馏微调
基于场景特定数据蒸馏的微调可显著提升模型在无 Routine 指导场景下的表现。以 Qwen3-14B 为例，微调后整体准确率提升 22.9 个百分点，甚至超越原始模型在有 Routine 指导下的表现。这表明场景特定数据蒸馏可将 procedural knowledge 内化于模型权重中，减少模型对显式规划的依赖。

消融研究
Routine 组件的影响
以下是不同 Routine 组件对模型整体准确率的影响表：

Image
整体模型精度在不同 routine 组件上的表现
实验表明，工具规格说明是提升准确率的核心要素。当 Routine 中包含工具名称时，模型准确率较不含工具名称时平均提升 18.3 个百分点。输入输出参数描述为模型提供了丰富的上下文信息，尤其对中小规模模型助力显著，使其参数准确率提升 12.7 个百分点。

AI 优化机制的价值
以下是不同 Routine 生成方法下模型整体准确率表：

Image
Routine 在不同生成方法下的整体模型准确率
AI 优化可显著提升 Routine 质量。以 Qwen3-14B 为例，AI 优化后的 Routine 使模型准确率达到 76.7%，接近手动标注 Routine 的效果（83.3%）。这表明 AI 优化是企业场景下高效生成高质量 Routine 的可行路径。

Routine 数量的影响
以下是智能体规划的不同方式图，展示了从用户草稿到 AI 优化再到手动标注的 Routine 生成过程：

Image
智能体规划的多种实现路径
实验显示，提供单个正确 Routine 时模型表现最佳。当引入干扰 Routine 时，高性能模型的准确率显著下降，但随着 Routine 数量增加，准确率逐渐恢复。这表明模型可能从“组合步骤”转向“选择机制”，识别并执行最相关的 Routine。

以下是不同数量 Routine 下模型整体准确率表：

Image
整体模型在多个 Routine 上的综合准确率
Routine 的局限性
当前规划模型在生成 Routine 流程时，对企业领域专家草稿的依赖程度较高。这在一定程度上限制了智能体系统面对新工具引入或工作流变更时的泛化能力。当企业引入新型区块链溯源工具，试图将其融入现有供应链智能管理 Routine 时，规划模型往往无法自主识别该工具在流程中的精准定位，需依赖专家重新起草规划草稿。

执行模型主要通过指令微调和知识蒸馏进行适应，这种方式在面对企业流程的细微变更时，如订单处理流程中新增的环保合规审查步骤，模型难以迅速调整自身以匹配新的 Routine 要求。这表明当前智能体系统在动态适应性方面仍有较大提升空间。

针对上述挑战，研究者提出将基于强化学习（RL）的智能体框架引入工作流的改进方向。强化学习通过构建奖励模型，让智能体在与环境交互中自主学习优化 Routine 生成策略。例如，在智能体尝试生成包含新引入区块链工具的 Routine 时，奖励模型可根据流程执行效率、结果准确性等指标给予即时反馈。若智能体尝试将区块链工具错误放置在“订单创建”步骤，导致执行效率低下，奖励模型会给予负向反馈，引导智能体调整工具位置至“产品发货”步骤。

多智能体框架的探索同样前景广阔。在该框架下，高级智能体犹如调度员，依据结构化的 Routine 流和集中交互协议，协调多个专业智能体。在企业智能工厂场景中，高级智能体根据生产调度 Routine，指挥生产执行智能体、质量检测智能体、物流配送智能体协同作业。这种层次化交互方案有效降低了单个智能体承担的 Routine 计划复杂度，让每个智能体专注于自身擅长的领域任务，大幅提升企业工作流执行的稳定性与智能性。

总结：从规划到落地的关键跃迁
Routine 作为一款结构精巧、内容全面的规划框架，为企业智能体系统的多步骤工具执行提供了精准导航。

Routine 的四重价值主张
1. 结构化导航：它通过卓越的流程编排手段，将复杂的企业任务分解为清晰有序的步骤序列，确保智能体在执行过程中每一步都踩在关键节点上。
2. 数据蒸馏引擎：在训练数据合成领域，Routine 展现出强大的蒸馏能力。通过将专家规划草稿转化为结构化的 Routine 数据集，为模型训练提供了高质量的营养源泉。
3. 小模型杠杆：用 14B 参数逼近 GPT-4o 的 96% 准确率。在企业智能运维场景中，基于 Routine 合成的数据集让模型精准学习到服务器巡检、故障排查等复杂任务的执行逻辑。更值得一提的是，Routine 在特定领域多步骤工具调用数据集生成方面的作用无可替代。通过对企业业务流程的深度建模，Routine 生成的数据集完美契合企业实际需求。
4. 场景即插即用：在智能体系统开发中，开发者依据 Routine 数据集训练出的模型，能够深度适配企业的财务审计、客户关系管理等核心业务流程。
实验结果的总结
在 HR 智能体测试集（1,148 个样本）中，GPT-4o 的端到端准确率从 41.1%（无 Routine）提升至 96.3%（Routine 指导）。

该测试包含 3 个含分支的 Routine，分支逻辑使 Qwen3-14B 准确率从 83.6%（无分支）降至 81.3%（有分支）。

GPT-4o 基于 Routine 蒸馏生成的 537 条场景特定数据，包含 3,108 个标注工具调用指令，用于训练 Qwen3-14B，使其准确率达 95.5%。LoRA 微调参数为：秩 8，批大小 1×4 GPU，有效批大小 16，学习率 1e-4，训练 3 epoch。

下一步：从 “流程执行” 到 “流程进化”
动态适应：RLHF 驱动的 Routine 自进化机制
多智能体编排：用「主-专」架构降低单 Routine 复杂度
零样本迁移：新工具接入时的自主工作流重构能力

AI for Process
Routine 机制，让智能体系统深度融入企业流程，成为企业智能自动化与决策支持的中流砥柱。在企业智能决策场景中，智能体依据 Routine 调用数据分析工具、构建预测模型，为企业管理层提供精准决策依据。从生产排程到市场营销策略制定，Routine 驱动的智能体系统全方位提升企业运营效率与质量。


参考资料
• Routine: A Structural Planning Framework for LLM Agent System in Enterprise
https://arxiv.org/pdf/2507.14447
https://github.com/davidkimai/Context-Engineering