### GraphRAG【社区摘要】
> **社区摘要**：先把小区居民的关系网理清楚，再给每个邻里圈做个简介。有人问路时，各个邻里圈提供线索，最后整合成最完整的答案。
>

* 发表时间：2024.04.24
* 论文名称：[From Local to Global: A Graph RAG Approach to Query-Focused Summarization](https://arxiv.org/abs/2404.16130)
* 论文地址：[https://arxiv.org/abs/2404.12457](https://arxiv.org/abs/2404.12457)
* Github 项目：[https://github.com/microsoft/graphrag](https://github.com/microsoft/graphrag)

#### 一、论文动机

- **RAG的局限性**：传统的检索增强生成（RAG）方法适用于局部查询，即在特定文本区域内寻找答案，但对于需要对整个文本语料库进行全局理解的问题（如“数据集的主要主题是什么？”），RAG表现不佳.
- **查询聚焦摘要（QFS）的挑战**：现有的QFS方法在处理大规模文本时存在扩展性问题，无法有效处理RAG系统通常索引的大量文本.

#### 二、论文思路

![](20240424_GraphRAG/img/v2-3f3b3bc0cf974ae7d580cc949199f780_1440w.png)

- **核心思想**：结合知识图谱生成、检索增强生成（RAG）和查询聚焦摘要（QFS），通过构建基于LLM的知识图谱来支持对整个文本语料库的全局查询.
- **具体步骤**：
  
1. **构建知识图谱**：首先从源文档中提取实体和关系，构建一个实体知识图谱.
2. **社区检测**：使用社区检测算法（如Leiden算法）将图谱划分为多个紧密相关的社区.
3. **生成社区摘要**：为每个社区生成摘要，这些摘要在索引时和查询时都可以并行生成.
4. **回答查询**：对于每个查询，使用社区摘要生成部分响应，然后将所有部分响应汇总成最终的全局响应.

#### 三、实验设计与结果

- **数据集**：使用两个约100万token的数据集进行评估，一个是播客访谈的转录文本，另一个是新闻文章.
- **查询生成**：通过活动中心的方法自动生成全局理解问题，例如“哪些播客节目主要讨论技术政策和政府监管？”
- **评估指标**：使用LLM作为评估器，比较不同方法在全面性、多样性和赋能性（帮助读者理解和做出判断的能力）方面的表现.
- **结果**：Graph RAG在全面性和多样性方面显著优于传统的RAG方法，并且在资源消耗（token成本）方面也更为高效.

#### 四、论文创新点

1. **结合知识图谱与RAG**
   1. **知识图谱构建**：传统的RAG方法主要依赖于文本检索和生成，而这篇论文提出了一种结合知识图谱的方法。通过从源文档中提取实体和关系，构建一个实体知识图谱，使得系统能够更好地理解和组织文本中的信息.
   2. **社区检测与摘要生成**：利用社区检测算法将知识图谱划分为多个紧密相关的社区，并为每个社区生成摘要。这种方法不仅提高了对全局信息的理解能力，还为生成全面和多样化的答案提供了基础.
2. **全局查询处理能力**
   1. **全局查询聚焦**：传统的RAG方法在处理需要对整个文本语料库进行全局理解的问题时表现不佳。而Graph RAG通过构建知识图谱和社区摘要，能够有效地处理这类全局查询问题，生成更全面和多样化的答案.
   2. **多阶段回答生成**：在回答查询时，Graph RAG采用多阶段的方法，首先使用社区摘要生成部分响应，然后将所有部分响应汇总成最终的全局响应。这种分阶段的方法提高了生成答案的质量和效率.
3. **资源效率的提升**
   1. **降低token成本**：与传统的基于文本的全局摘要方法相比，Graph RAG在生成答案时所需的token数量大幅减少。例如，对于根级别的社区摘要，Graph RAG所需的token数量比传统的全局文本摘要方法减少了97%以上.
   2. **高效的社区划分**：通过社区检测算法，Graph RAG能够将知识图谱划分为多个层次的社区，使得在不同层次上生成摘要和回答查询变得更加高效.

#### 五、论文总结

GraphRAG分两个阶段构建基于图的文本索引：首先从源文档中推导出实体知识图，然后为所有紧密相关实体的组预生成社区摘要。给定一个问题，每个社区摘要用于生成部分响应，然后在向用户的最终响应中再次总结所有部分响应。


