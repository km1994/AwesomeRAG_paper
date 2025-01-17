### HybridRAG【中医合方】
> **中医合方**：就像中医讲究的"合方"，单味药不如几味药合在一起效果好。向量数据库负责快速检索，知识图谱补充关系逻辑，两者优势互补。
>

* 发表时间：2024.08.09
* 论文名称：[HybridRAG: Integrating Knowledge Graphs and Vector Retrieval Augmented Generation for Efficient Information Extraction](https://arxiv.org/abs/2408.04948)
* 论文地址：[https://arxiv.org/abs/2408.04948](https://arxiv.org/abs/2408.04948)
* Github 地址：[https://github.com/tahmidmir/HyrbridRAG](https://github.com/tahmidmir/HyrbridRAG)

#### 一、论文动机

- **背景**：在金融领域，从非结构化文本数据（如财报电话会议记录）中提取和解释复杂信息对大型语言模型（LLMs）来说是一个挑战，尤其是当这些文档包含特定领域的术语和复杂格式时。
- **目的**：HybridRAG结合了GraphRAG和VectorRAG的优势，从向量数据库和知识图谱中检索上下文信息，以提供给LLMs，从而生成更准确的回答。

#### 二、论文思路

- **VectorRAG 工作流程**：
  - 从与外部文档相关的查询开始，这些文档不是LLM训练数据集的一部分。
  - 查询用于搜索外部存储库（如向量数据库或索引语料库），以检索包含有用信息的相关文档或段落。
  - 检索到的文档随后作为额外上下文反馈到LLM中，从而生成基于查询的响应。
  - 这确保了生成内容不仅基于内部训练数据，还结合了检索到的外部信息。

![](20240809_HybridRAG/img/微信截图_20250115084506.png)

- **GraphRAG 工作流程**：
  - 利用知识图谱来增强NLP任务的性能，通过将知识图谱与RAG技术整合，GraphRAG能够基于从金融文档中提取的结构化信息生成更准确和上下文感知的回答。
  - **知识图谱构建**：
    - **知识提取**：从非结构化或半结构化数据中提取结构化信息，包括实体识别、关系提取和共指消解。
    - **知识改进**：通过移除冗余和填补信息空白来提高知识图谱的质量和完整性。
    - **知识融合**：结合来自多个源的信息，创建一个一致和统一的知识图谱。
  - **GraphRAG**：从用户输入的查询开始，查询用于搜索知识图谱以检索与查询相关的节点（实体）和边（关系）。然后从完整的知识图谱中提取包含这些相关节点和边的子图，以提供上下文。

![](20240809_HybridRAG/img/微信截图_20250115084559.png)

![](20240809_HybridRAG/img/微信截图_20250115084620.png)

- **HybridRAG 结合优势**：HybridRAG结合了VectorRAG和GraphRAG的优势，从向量数据库和知识图谱中检索上下文信息，以提供给LLMs，从而生成更准确的回答。

#### 三、实验设计与结果

![](20240809_HybridRAG/img/v2-cb27363fc1dec9e42cc6bf96c29884a3_1440w.png)

- **实验结果**：
  - **忠实度**：GraphRAG和HybridRAG显示出更优越的性能，两者都达到了0.96的得分，而VectorRAG略低一些，得分为0.94。
  - **答案相关性得分**：HybridRAG以0.96的得分领先，其次是VectorRAG的0.91，GraphRAG的0.89。
  - **上下文精确度**：GraphRAG以0.96的得分最高，显著超过了VectorRAG的0.84和HybridRAG的0.79。然而，在**上下文召回率**方面，VectorRAG和HybridRAG都达到了完美的1分，而GraphRAG落后于0.85。

#### 四、论文总结

一种基于知识图谱RAG技术（GraphRAG）和VectorRAG技术相结合的新方法，称为HybridRAG，以增强从金融文档中提取信息的问答系统，该方法被证明能够生成准确且与上下文相关的答案。在检索和生成阶段，就检索准确性和答案生成而言，从向量数据库和知识图谱中检索上下文的HybridRAG优于传统的VectorRAG和GraphRAG。


## 致谢

* 参考：[https://mp.weixin.qq.com/s/59e_bEcxGkM4N0GeCTTF4w](https://mp.weixin.qq.com/s/59e_bEcxGkM4N0GeCTTF4w)
