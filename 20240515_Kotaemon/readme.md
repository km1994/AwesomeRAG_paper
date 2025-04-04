### Kotaemon【乐高】
> **乐高**：一套现成的问答积木套装，既能直接拿来用，又能自由拆装改造。用户要用就用，开发要改就改，随心所欲不失章法。
>

* 发表时间：2024.05.15
* Github 地址：[https://github.com/Cinnamon/kotaemon](https://github.com/Cinnamon/kotaemon)

#### 一、论文动机

- **RAG（Retrieval-Augmented Generation）**：一种结合检索和生成的模型，通过检索相关文档来增强大型语言模型（LLM）的生成能力，从而提高问答系统的性能.
- **kotaemon**：一个开源的RAG UI工具，适用于最终用户和开发者，提供了丰富的功能和高度的可定制性.

#### 二、kotaemon的主要特点

1. **自托管文档问答Web UI**：允许用户自己托管文档问答界面，提供了完整的前端和后端集成解决方案.
2. **支持多用户登录**：可以组织私人或公共文件集合，支持协作和分享，适合团队使用.
3. **组织LLM和嵌入模型**：支持本地LLM和流行的API提供商，如OpenAI、Azure、Ollama、Groq等，提供了灵活的模型选择.
4. **混合RAG管道**：提供混合（全文和向量）检索器和重新排名，确保最佳的检索质量，提高了检索的准确性和效率.
5. **多模态问答支持**：支持在包含图表和表格的多个文档上进行问答，并支持多模态文档解析，扩展了问答系统的应用范围.
6. **高级引用与文档预览**：系统默认提供详细的引用以确保LLM答案的正确性，可以在浏览器内的PDF查看器中查看引用（包括相关分数）并高亮显示，提高了答案的可信度.
7. **支持复杂推理方法**：使用问题分解来回答复杂或多跳问题，支持基于Agent的推理，如ReAct、ReWOO和其他代理，增强了系统的推理能力.
8. **可配置的设置UI**：可以在UI上调整检索和生成过程中的大多数重要方面（包括提示），提供了高度的可定制性.
9. **可扩展性**：基于Gradio构建，用户可以自由定制或添加任何UI元素，同时支持多种文档索引和检索策略，提供了GraphRAG索引管道作为示例.

#### 三、论文总结

一个开源的干净且可定制的RAG UI，用于构建和定制自己的文档问答系统。既考虑了最终用户的需求，也考虑了开发者的需求。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/SzoE2Hb82a6yUU7EcfF5Hg](https://mp.weixin.qq.com/s/SzoE2Hb82a6yUU7EcfF5Hg)

