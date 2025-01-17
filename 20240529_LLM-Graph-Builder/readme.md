这篇文章介绍了Neo4j开源的基于LLM提取知识图谱的生成器：llm-graph-builder。以下是文章的主要内容总结：

### 背景知识
- **知识图谱的重要性**：知识图谱能够将非结构化数据转换为结构化形式，便于存储和查询，对于对话系统和知识问答等应用具有重要意义.
- **LLM的应用**：利用大型语言模型（LLM）如OpenAI、Gemini、Llama3、Diffbot、Claude、Qwen等从非结构化数据中提取节点、关系及其属性，可以提高知识图谱的构建效率和质量.

### llm-graph-builder的主要特征
1. **知识图谱创建**：使用LLMs将非结构化数据（如PDF、文档、文本、YouTube视频、网页等）转换为存储在Neo4j中的结构化知识图谱.
2. **提供Schema**：用户可以提供自定义的Schema或使用已有的Schema来生成知识图谱，增加了灵活性和可定制性.
3. **查看图表**：在Bloom中可以一次查看特定源或多个源的知识图谱，方便用户直观地理解和分析数据.
4. **AI聊天**：通过对话即可查询与Neo4j数据库中的数据进行交互，还可以提供来源的元数据，支持使用不同的RAG方法（如GraphRAG、Vector、Text2Cypher）进行知识问答.

### 参考文献
- **GitHub**：[https://github.com/neo4j-labs/llm-graph-builder](https://github.com/neo4j-labs/llm-graph-builder)
- **在线体验**：[https://llm-graph-builder.neo4jlabs.com/](https://llm-graph-builder.neo4jlabs.com/)
- **官方文档**：[https://neo4j.com/labs/genai-ecosystem/llm-graph-builder/](https://neo4j.com/labs/genai-ecosystem/llm-graph-builder/)
- **问题反馈**：[https://github.com/neo4j-labs/llm-graph-builder/issues](https://github.com/neo4j-labs/llm-graph-builder/issues)

### NLP工程化公众号
- **技术分享**：专注于对话系统领域的技术分享，涵盖Python/C++/CUDA、ML/DL/RL和NLP/KG/DS/LLM等领域.
- **Roadmap**：可以通过飞书文档查看公众号的Roadmap：[https://z0yrmerhgi8.feishu.cn/wiki/Zpewwe2T2iCQfwkSyMOcgwdInhf](https://z0yrmerhgi8.feishu.cn/wiki/Zpewwe2T2iCQfwkSyMOcgwdInhf)

### 结论
llm-graph-builder通过结合LLM和Neo4j，提供了一个强大的工具，能够将非结构化数据高效地转换为结构化知识图谱，并支持多种交互和查询方式，为对话系统和知识问答等应用提供了新的解决方案.