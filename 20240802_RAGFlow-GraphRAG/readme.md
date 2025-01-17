### RAGFlow-GraphRAG【导航员】
> **导航员**：在问答的迷宫里开辟捷径，先画张地图把知识点都标好，重复的路标合并掉，还特地给地图瘦身，让问路的人不会绕远路。
>

* 发表时间：2024.08.02
* Github 项目：[https://github.com/infiniflow/ragflow](https://github.com/infiniflow/ragflow)

#### 一、论文动机

- **背景**：GraphRAG由微软开源，被视为下一代RAG，其在RAGFlow体系中是RAG 2.0的一个单元。RAG 2.0是一个以搜索为中心的端到端优化系统，分为数据抽取、预处理、索引与检索四个阶段，其中数据抽取和预处理是重点。
- **GraphRAG的重要性**：知识图谱对改进RAG效果至关重要，它能解决简单RAG只能找到与提问相似结果而未必是答案的问题，尤其在总结性问题等场景下，通过知识图谱聚合内容生成总结，可更好回答问题。此外，知识图谱还能为RAG返回结果添加更多上下文，使LLM产生更有解释性的回答。

#### 二、GraphRAG与HippoRAG的对比
- **离线处理阶段**：两者都先将用户文档送给LLM进行命名实体自动抽取。GraphRAG只抽取实体，用“相关”作为实体间联系，后续用社区检测算法和Graph Embedding（可选，采用Node2Vec）补全关系；HippoRAG则抽取整个三元组，之后利用现成知识图谱补全。
- **在线处理阶段**：GraphRAG将用户查询转成向量，找知识图谱中最接近节点，再根据节点所在社区及摘要信息返回给LLM，同时查询原文并归并结果；HippoRAG在查询阶段利用类似PageRank的随机游走算法在知识图谱上做子图遍历，确定LLM的上下文。两者都用到PageRank做子图遍历，原因是人类回忆过程和PageRank算法输出有相关性。

#### 三、GraphRAG的简化与优势

- **简化**：GraphRAG对知识图谱的抽象和构建做了简化，不要三元组和图抽象表达，使工程上推出标准产品可行性增加。
- **优势**：RAGFlow借鉴GraphRAG实现，在文档预处理阶段引入知识图谱构建作为可选项，服务于高级问答场景。

#### 四、RAGFlow对GraphRAG的改进

- **引入去重步骤**：原版GraphRAG直接用抽取的命名实体构建知识图谱，易因同义词实体影响结构。RAGFlow借鉴LLM能力去重，因LLM可视为超级大的知识图谱。
- **降低Token消耗**：GraphRAG工作原理需消耗大量Token，RAGFlow通过流程优化确保文档只提交LLM一次，避免无效消耗。未来还会提供类似Triplex的小模型解决方案降低成本。

#### 五、论文总结

RAGFlow借鉴了GraphRAG的实现，在文档预处理阶段，引入知识图谱构建作为可选项，服务于QFS问答场景，并引入了实体去重、Token优化等改进。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/c5-0dCWI0bIa2zHagM1w0w](https://mp.weixin.qq.com/s/c5-0dCWI0bIa2zHagM1w0w)