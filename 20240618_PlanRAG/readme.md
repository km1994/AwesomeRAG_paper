### PlanRAG【战略家】
> **战略家**：先制定完整作战计划，再根据规则和数据分析局势，最后做出最佳战术决策。
>

* 发表时间：2024.06.18
* 论文名称：[PlanRAG: A Plan-then-Retrieval Augmented Generation for Generative Large Language Models as Decision Makers](https://arxiv.org/abs/2406.12430)
* 论文地址：[https://arxiv.org/abs/2406.12430](https://arxiv.org/abs/2406.12430)
* Github 地址：[https://github.com/myeon9h/PlanRAG](https://github.com/myeon9h/PlanRAG)

#### 一、论文动机

- **决策问答（Decision QA）任务**：定义为根据决策问题Q、业务规则R和数据库D，确定最佳决策。这种任务在商业环境中非常重要，但现有的RAG方法在处理这类任务时表现不佳，尤其是在制定决策计划方面.
- **DQA基准**：为了评估Decision QA，论文提出了一个包含两个场景（定位和构建）的基准DQA。这两个场景源自两款视频游戏（《欧陆风云IV》和《维多利亚3》），模拟了真实的商业环境.

#### 二、论文思路

![](20240618_PlanRAG/img/v2-647599497ae2e715312cfe4f88791f08_1440w.png)

- **规划步骤**：基于PlanRAG的语言模型首先生成决策计划，描述为决策所需执行的一系列数据分析任务.
- **检索与回答步骤**：语言模型不仅接收问题、业务规则和数据库模式，还接收初始计划作为输入，生成用于决策的数据分析查询，并从数据库中检索数据.
- **重新规划步骤**：当初始计划不足以解决决策问题时，进行重新规划。语言模型根据每次检索步骤的结果评估当前计划，并生成新的计划以进行进一步分析.

#### 三、实验设计与结果

- 实验设计
  - **实验设置**：论文实现了四种不同的决策型LM进行比较，包括基于单轮RAG的SingleRAG-LM、基于迭代RAG的IterRAG-LM、基于PlanRAG的PlanRAG-LM，以及无重新规划的PlanRAG-LM。所有实验在零样本和单次运行的设置下进行.
  - **数据库**：使用MySQL作为关系数据库管理系统（RDBMS），Neo4j作为图形数据库管理系统（GDBMS）.
  - **评估指标**：只有当决策者的答案在语义上与DQA上的真实最佳决策完全一致时，才被认为是正确的. 
- 结果与分析
  - **主要结果**：PlanRAG在定位场景中比最先进的迭代RAG方法提高了15.8%，在构建场景中提高了7.4%。这充分展示了PlanRAG在决策制定任务中的有效性.
  - **单次检索（SR）和多次检索（MR）问题**：PlanRAG在SR问题上的表现远超IterRAG-LM，而在MR问题上也有显著优势。这是因为PlanRAG通过规划步骤减少了理解问题难度的可能性，并根据计划执行多次检索.
  - **RDB和GDB的分析**：PlanRAG在两种数据库类型上都比其他LMs更有效。在建筑场景中，PlanRAG在GDB上的效果比在RDB上更好，因为建筑场景需要在GDB中进行更长的遍历来回答问题.
  - **错失数据查询率分析**：PlanRAG的遗漏率较低，分别为1.3%和21.8%，而IterRAG-LM的遗漏率较高，分别为3.3%和33.2%。这意味着PlanRAG能更有效地查询问题的关键数据.
  - **失败案例分析**：PlanRAG在两种场景下均显著降低了CAN和MIS错误，表明PlanRAG能更好地理解决策QA问题，并更有效地查询问题的关键数据.
  - **重新规划分析**：PlanRAG在Building场景中比在Locating场景中更频繁地重新规划，表明在Building场景中制定计划（无论是初始规划还是重新规划）时遇到更多困难.

#### 四、论文总结

PlanRAG通过结合规划、检索和重新规划步骤，显著提高了复杂决策问答任务的性能。实验结果表明，PlanRAG在定位和构建场景中均优于现有的RAG基线，特别是在减少理解问题难度和有效查询关键数据方面表现出色。PlanRAG为利用LLMs进行复杂数据分析的决策提供了一种有效的解决方案.

## 致谢

* 参考：[https://mp.weixin.qq.com/s/q3x2jOFFibyMXHA57sGx3w](https://mp.weixin.qq.com/s/q3x2jOFFibyMXHA57sGx3w)