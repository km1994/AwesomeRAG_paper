### GraphInsight【图谱解读】
> **图谱解读**：像个擅长信息图表分析的专家，知道把重要信息放在最显眼的位置，同时在需要时查阅参考资料来补充细节，并能step by step地推理复杂图表，让AI既能把握全局又不遗漏细节。
>

* 发表时间：2024.09.05
* 论文名称：[GraphInsight: Unlocking Insights in Large Language Models for Graph Structure Understanding](https://arxiv.org/abs/2409.03258)
* 论文地址：[https://arxiv.org/abs/2409.03258](https://arxiv.org/abs/2409.03258)
* Github 地址：

#### 一、论文动机

- **LLMs在图理解上的挑战**：尽管LLMs在处理图方面展现出潜力，但在通过图描述序列的提示来理解图形结构信息时，尤其是在图规模增大时，仍面临困难。这种困难被称为“位置偏差”，即LLMs在图描述序列中不同位置的记忆表现不均。
- **现有方法的不足**：现有方法在处理大规模图时存在“理解崩溃”的问题，即随着图规模的增加，LLMs的理解能力急剧下降。

#### 二、论文思路

![](20240905_GraphInsight/img/v2-37ca375f71cf71d336483ff1b1ae9561_1440w.png)

- 基于重要性的宏观层面的图形理解

 **基于重要性的图描述重组**：计算图中每个节点的PageRank分数以衡量其重要性，将图分解为一系列互不相交的子图描述，并根据PageRank分数对子图描述进行排序，将最重要的子图描述放置在LLMs的强记忆区域（序列的头部和尾部）。

- 基于检索增强生成（RAG）的微观层面的图形理解

**基于RAG的轻量级外部知识库**：对于弱记忆区域中的节点和边，提取其信息并存储在GraphRAG知识库中。当需要进行微图理解任务时，从知识库中检索相关信息，并将其与输入的图描述序列结合，形成增强提示输入LLMs进行推理。

#### 三、实验设计与结果

- 实验设计
  - **数据集**：引入了GraphSQA基准，涵盖从15到200个节点的多种图结构，包括多重边和自环。
  - **任务类型**：GraphSQA包括5个宏观图任务和15个微观图任务，后者进一步细分为8个复合任务。
  - **评估指标**：根据答案类型的不同，采用布尔值、数值和集合类型三种评估指标。
  - **模型选择**：使用了多种开源模型，包括Mistral 7B、Llama3-8B、Qwen2-7B和Vicuna-7B等，这些模型有的经过长时间序列的微调。
- 结果与分析
  - **宏观图任务**：GraphInsight在所有大型模型上均优于其他方法，特别是在Vicuna-7B模型上，得分提高了4.61倍。
  - **微观图任务**：GraphInsight在微观图任务中也表现出色，特别是在Vicuna-7B模型上，得分提高了14.02倍。
  - **复合任务**：在常见邻居查找和三阶邻居查找等复合任务中，GraphInsight分别实现了12.75倍和3.25倍的提升。
  - **消融研究**：图描述组织和GraphRAG对宏图和微图任务均有优化效果，特别是GraphRAG在微观图任务中带来了显著的改进。

#### 四、论文创新点

突出了GraphInsight相较于其他方法的优势，例如更高效地利用节点特征和边信息，提高模型对于图结构上下文的学习效果。

#### 五、论文总结

GraphInsight旨在提升LLMs对宏观和微观层面图形信息理解的新框架。GraphInsight基于两大关键策略：1）将关键图形信息置于LLMs记忆性能较强的位置；2）借鉴检索增强生成（RAG）的思想，对记忆性能较弱的区域引入轻量级外部知识库。此外，GraphInsight探索将这两种策略整合到LLM代理过程中，以应对需要多步推理的复合图任务。
## 致谢

* 参考：[https://mp.weixin.qq.com/s/xDKTBtso3ONCGyskvmfAcg](https://mp.weixin.qq.com/s/xDKTBtso3ONCGyskvmfAcg)