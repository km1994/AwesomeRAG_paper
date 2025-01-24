### SubgraphRAG【定位仪】
> **定位仪**：不是漫无目的地大海捞针，而是精准绘制一张小型知识地图，让 AI 能快速找到答案。
>

* 发表时间：2024.10.28
* 论文名称：[Simple is Effective: The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation](https://arxiv.org/abs/2410.20724)
* 论文地址：[https://arxiv.org/abs/2410.20724](https://arxiv.org/abs/2410.20724)
* Github 地址：[https://github.com/Graph-COM/SubgraphRAG](https://github.com/Graph-COM/SubgraphRAG)

#### 一、论文动机

大型语言模型（LLMs）在多种领域表现出色，但在推理能力上仍存在局限性，**例如幻觉（hallucination）、知识过时以及缺乏特定领域的专业知识**。

检索增强生成（RAG）通过整合外部知识来解决这些问题，但现有方法在检索效率和有效性之间难以平衡。本文提出了一种新的框架——SubgraphRAG，通过检索知识图谱（KG）的子图并利用LLMs进行推理和答案预测，旨在提高RAG系统的效率和准确性。

#### 二、论文思路

![](20241028_SubgraphRAG/img/v2-0436969ea9917e8888e18e4eaaacdc7d_1440w.png)

SubgraphRAG的核心是将知识图谱中的子图检索与LLMs的推理能力相结合。该框架通过以下步骤实现：

1. 查询解析和实体提取：从用户查询中识别出主题实体（topic entities），这些实体为检索提供关键线索。
2. 子图检索：
   1. 结构特征构建：使用方向性距离编码（Directional Distance Encoding, DDE）为每个三元组编码，捕捉其与查询主题实体的结构关系。
   2. 并行提取相关三元组：通过轻量级多层感知器（MLP）对三元组进行评分，选择与查询最相关的三元组构建子图。
3. LLM推理：将检索到的子图以线性化列表的形式嵌入到提示中，指导LLMs进行推理并生成答案。

#### 三、实验设计与结果

- 数据集

实验使用了两个多跳知识图谱问答（KGQA）基准数据集：WebQSP和CWQ。这些数据集需要模型进行复杂的推理才能生成答案。

- 检索性能

SubgraphRAG在检索召回率和效率方面显著优于现有方法。例如，在WebQSP数据集上，SubgraphRAG的三元组召回率达到88.3%，而其他方法如RoG和G-Retriever的召回率分别为71.3%和33.5%。同时，SubgraphRAG的检索时间仅为6秒，远低于其他方法。

- 知识问答性能

SubgraphRAG在知识问答任务中表现出色，尤其是在多跳推理和多主题实体问题上。例如，在CWQ数据集上，SubgraphRAG的Macro-F1和Hit指标分别达到89.8%和66.69%，显著优于其他方法。此外，SubgraphRAG在减少幻觉方面表现出色，生成的答案更加基于知识图谱中的事实信息。

- 可解释性

SubgraphRAG能够提供详细的推理过程和知识来源，显著提高了模型的可解释性。例如，对于复杂问题，SubgraphRAG可以清晰地展示推理路径和关键证据，而其他方法往往无法提供这样的解释。

#### 四、论文总结

SubgraphRAG通过高效的子图检索和知识接地的推理，显著提高了知识图谱增强的检索生成系统的性能。该框架在多跳推理和复杂问题上表现出色，同时减少了幻觉现象，提高了答案的可解释性。未来的工作将集中在进一步优化子图检索算法和扩展框架的适用范围。

#### 五、论文创新点

- 高效灵活的子图检索

SubgraphRAG通过以下方式实现高效子图检索：

1. **轻量级MLP**：使用MLP对三元组进行评分，避免了复杂模型（如GNNs）带来的计算开销。
2. **并行化处理**：通过并行提取相关三元组，显著提高了检索效率。
3. **灵活的子图形式**：检索到的子图形式灵活，可以根据LLMs的推理能力调整子图大小。

- 结构特征编码

SubgraphRAG通过方向性距离编码（DDE）为每个三元组编码，捕捉其与查询主题实体的结构关系。这种编码方式显著提高了检索的有效性，尤其是在多跳推理和多主题实体的复杂问题中。

-  知识接地的推理

SubgraphRAG通过将检索到的子图嵌入到LLMs的推理过程中，确保生成的答案基于知识图谱中的事实信息。这种方法不仅减少了幻觉现象，还提高了答案的可解释性。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/ns22XLKsABly7RjpSjQ_Fw](https://mp.weixin.qq.com/s/ns22XLKsABly7RjpSjQ_Fw)