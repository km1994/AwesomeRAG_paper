### LazyGraphRAG【精算师】
> **精算师**：能省一步是一步，把贵的大模型用在刀刃上。就像个会过日子的主妇，不是看到超市打折就买，而是货比三家后才决定在哪里花钱最值。

* 发表时间：2024.11.25
* 论文名称：[A modular graph-based Retrieval-Augmented Generation (RAG) system](https://microsoft.github.io/graphrag/)
* 论文地址：[https://microsoft.github.io/graphrag/](https://microsoft.github.io/graphrag/)
* Github 地址：[https://github.com/microsoft/graphrag](https://github.com/microsoft/graphrag)

#### 一、论文动机

微软之前开源的GraphRAG在数据索引阶段，主要利用大型模型提取和描述实体及其关系，并为每个实体和关系生成摘要。

优化实体图并提取层次化社区结构是一个涉及图统计的过程，然而，**这种方法的成本非常高昂。其原因是它需要使用大量的语言模型进行处理，导致GraphRAG的数据索引成本非常昂贵**。

与GraphRAG不同的是，LazyGraphRAG在数据索引阶段不进行任何预先的总结或嵌入生成。相反，它利用NLP名词短语提取来识别概念及其共现关系。然后，通过图统计来优化概念图，并提取层次社区结构。这种方法使得LazyGraphRAG的索引成本极低，仅为GraphRAG的0.1%。也就是说，LazyGraphRAG将成本降低了1000倍。

在查询处理方面，GraphRAG使用广度优先搜索确保考虑整个数据集的广泛性。而LazyGraphRAG则采用迭代加深的方式，结合了最佳优先搜索和广度优先搜索的动态。它首先按相似度对文本片段进行排名，然后通过动态选择相关社区，逐步细化查询结果。

通过这种方法，LazyGraphRAG能够同时支持本地和全局查询，在考虑整个数据集的广度的同时，高效地找到最佳匹配的文本块。

#### 二、论文思路

- LazyGraphRAG 的工作原理

LazyGraphRAG 结合了向量 RAG 和 GraphRAG 的优点，同时克服了它们的局限性：

1. **向量 RAG**：擅长处理本地查询，但无法处理全局查询。
2. **GraphRAG**：擅长处理全局查询，但索引成本较高。

- LazyGraphRAG 的关键机制包括：

1. **延迟索引构建**：使用 NLP 名词短语提取来提取概念及其共现，而不是使用 LLM 提取和总结实体及其关系。
2. **优化查询**：使用 LLM 识别相关子查询并优化查询。
3. **匹配查询**：结合文本块嵌入和块-社区关系，首先按与查询的相似性对文本块进行排名，然后按其排名靠前的社区排名对社区进行排名。
4. **答案生成**：从相关文本块构建概念子图，并使用 LLM 从相关块组中提取与子查询相关的声明。

#### 三、实验设计与结果

LazyGraphRAG 在多个任务中表现出色：

1. 数据集：5,590 篇美联社新闻文章。
2. 查询：100 个综合查询（50 个本地查询和 50 个全局查询）。
3. 指标：全面性、多样性、赋权。

实验结果表明：

1. 在 100 次相关性测试 的最低预算下，LazyGraphRAG 在本地和全局查询上均优于所有竞品，除了全局查询的 GraphRAG 全局搜索。
2. 在 500 次相关性测试 的预算下，LazyGraphRAG 在本地和全局查询上均优于所有竞品。
3. 随着相关性测试预算增加到 1,500，LazyGraphRAG 的胜率不断提高，证明了其在成本与质量方面的可扩展性。

#### 四、论文总结

LazyGraphRAG 是一种新型的图谱增强检索生成方法，通过优化索引和查询机制，显著降低了成本，同时保持或超越了现有方法的查询质量。它适用于多种用例，尤其是需要快速查询和低索引成本的场景。LazyGraphRAG 的灵活性和可扩展性使其成为未来知识检索和生成任务的有力工具。

## 致谢

* [https://mp.weixin.qq.com/s/oOzFBHS_B7FST6YKynD1GA](https://mp.weixin.qq.com/s/oOzFBHS_B7FST6YKynD1GA)