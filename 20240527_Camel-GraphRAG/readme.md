### Camel-GraphRAG【左右开弓】
> **左右开弓**：一只眼睛用Mistral扫描文本提取情报，另只眼睛用Neo4j编织关系网。查找时左右眼配合，既能找相似的，又能顺着线索图追踪，让搜索更全面精准。
>

* 发表时间：2024.05.27
* Github 项目：[https://github.com/camel-ai/camel](https://github.com/camel-ai/camel)

#### 一、论文动机

- **RAG方法**：RAG结合了检索系统和生成模型，可以提供更精准和相关的答案。然而，传统的RAG方法在处理复杂查询时存在一些问题，如模型幻觉问题。
- **GraphRAG**：为了减缓这些问题，Mistral和CAMEL共同开发了GraphRAG，通过将知识图谱和向量检索结合，显著提高了检索的准确性和性能。

#### 二、论文思路

![](20240527_Camel-GraphRAG/img/v2-4d6313f25b7157550aa7692f67ce2966_1440w.png)

- 技术栈细节
  - **CAMEL**：作为一个多智能体系统框架，提供了知识图谱代理和聊天代理等功能，简化了工作流程。
  - **MistralAI**：提供了Mistral Large 2大语言模型和Mistral Embed嵌入模型。
  - **Neo4j**：提供了知识图谱数据库。
  - **Qdrant**：提供了向量数据库，存储文本嵌入并支持快速向量检索。
  - **Unstructured.io**：负责将非结构化数据转换为结构化格式，为RAG系统做好准备。
- GraphRAG的工作流程

1. **数据准备**：通过Unstructured.io将原始数据转换为适合处理的格式。
2. **知识提取和存储**：使用Mistral Large 2从数据源中提取有用的信息，构建知识图谱，并存储在Neo4j数据库中。
3. **向量生成和存储**：使用Mistral Embed将文本转换为向量表示，并存储在Qdrant向量数据库中。
4. **混合检索**：结合向量检索和知识图谱检索，通过CAMEL框架的智能体系统处理用户查询，提供更加准确和相关的答案。
5. **回答用户问题**：使用Agent生成回复。

#### 三、论文总结

Camel-GraphRAG依托Mistral模型提供支持，从给定的内容中提取知识并构建知识结构，然后将这些信息存储在 Neo4j图数据库中。随后采用一种混合方法，将向量检索与知识图谱检索相结合，来查询和探索所存储的知识。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/DhnAd-k-CtdGFVrwGat90w](https://mp.weixin.qq.com/s/DhnAd-k-CtdGFVrwGat90w)