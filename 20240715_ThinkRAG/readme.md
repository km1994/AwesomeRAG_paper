
### ThinkRAG【小秘书】
> **小秘书**：把庞大的知识体系浓缩成口袋版，像个随身携带的小秘书，不用大型设备就能随时帮你查找解答。
>

* 发表时间：2024.07.15
* Github 项目：[https://github.com/wzdavid/ThinkRAG](https://github.com/wzdavid/ThinkRAG)

#### 一、论文动机

ThinkRAG，一个开源的、可以在笔记本电脑上运行的本地知识库大模型检索增强生成系统。

![](20240715_ThinkRAG/img/v2-90e603c75d3e00868104a0c43c5ca968_1440w.png)

#### 二、模型支持

- **LlamaIndex框架**：ThinkRAG基于LlamaIndex数据框架构建，支持所有LlamaIndex支持的模型。
- **模型选择**：
  - **OpenAI API**：支持OpenAI API以及所有兼容的LLM API，包括国内主流大模型厂商如智谱、月之暗面、深度求索等。
  - **Ollama**：支持本地化部署的大模型，如Llama、Gemma、GLM、Mistral、Phi、Llava等。
  - **嵌入模型和重排模型**：支持来自Hugging Face的大多数模型，主要选用BAAI的BGE系列模型。

#### 三、系统特点

- **完整应用**：LlamaIndex框架的完整应用。
- **本地文件存储**：开发模式支持本地文件存储，无需安装任何数据库。
- **无需GPU**：无需GPU支持，即可在笔记本电脑上运行。
- **本地部署**：支持本地部署的模型和离线使用。
- **定制优化**：为国内用户做了大量定制和优化，包括使用Spacy文本分割器处理中文字符、中文标题增强功能、中文提示词模板等。

#### 四、快速开始
1. **下载与安装**：
   - 从Github下载代码后，用pip安装所需组件：
     ```bash
     pip3 install -r requirements.txt
     ```
   - 若要离线运行系统，需从官网下载Ollama，并使用Ollama命令下载大模型。同时，从Hugging Face下载嵌入模型和重排模型到`localmodels`目录中。

2. **系统配置**：
   - 获取LLM服务商的API密钥，配置环境变量：
     ```python
     ZHIPU_API_KEY = ""
     MOONSHOT_API_KEY = ""
     DEEPSEEK_API_KEY = ""
     OPENAI_API_KEY = ""
     ```
   - 在`config.py`配置文件中删除不再使用的服务商，或添加兼容OpenAI API的其他服务商。
   - 默认以开发模式运行，使用本地文件存储。若要切换到生产模式，配置环境变量`THINKRAG_ENV = production`，并使用向量数据库Chroma和键值数据库Redis。

3. **运行系统**：
   - 在包含`app.py`文件的目录中运行以下命令：
     ```bash
     streamlit run app.py
     ```
   - 系统将在浏览器上自动打开`http://localhost:8501/`，展示应用界面。

#### 五、使用指南
1. **系统配置**：
   - 在用户界面配置大模型，包括Base URL和API密钥，选择具体模型。
   - 系统自动检测API和密钥是否可用，并显示当前选择的大模型实例。
   - 可以在用户界面上选择Ollama下载的模型。
   - 可以切换选择使用的嵌入模型和重排模型，并设置重排模型的参数。

2. **管理知识库**：
   - 支持上传PDF、DOCX、PPTX等文件，也支持上传网页URL。
   - 点击“Browse files”按钮选择文件，点击“Load”按钮加载，系统会对文件进行处理并保存到知识库中。
   - 可以输入或粘贴网页URL，获取网页信息并保存到知识库中。
   - 支持对知识库进行管理，分页列出所有文档，选择要删除的文档并删除。

3. **智能问答**：
   - 在左侧导航栏点击“Query”，进入智能问答页面。
   - 输入问题后，系统会对知识库进行检索并给出回答，采用混合检索和重排技术获取准确内容。
   - 例如，上传一个Word文档“大卫说流程.docx”，输入问题“流程有哪三个特征？”系统用时2.49秒，给出准确回答“流程具备目标性、重复性与过程性”，并列出2个相关文档。

#### 六、技术架构

- **开发模式**：
  - RAG框架：LlamaIndex
  - 前端框架：Streamlit
  - 嵌入模型：BAAI/bge-small-zh-v1.5
  - 重排模型：BAAI/bge-reranker-base
  - 文本分割器：SentenceSplitter
  - 对话存储：SimpleChatStore
  - 文档存储：SimpleDocumentStore
  - 索引存储：SimpleIndexStore
  - 向量存储：SimpleVectorStore

- **生产模式**：
  - RAG框架：LlamaIndex
  - 前端框架：Streamlit
  - 嵌入模型：BAAI/bge-large-zh-v1.5
  - 重排模型：BAAI/bge-reranker-large
  - 文本分割器：SpacyTextSplitter
  - 对话存储：Redis
  - 文档存储：Redis
  - 索引存储：Redis
  - 向量存储：Chroma

#### 七、总结

ThinkRAG大模型检索增强生成系统，可以轻松部署在笔记本电脑上，实现本地知识库智能问答。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/VmnVwDyi0i6qkBEzLZlERQ](https://mp.weixin.qq.com/s/VmnVwDyi0i6qkBEzLZlERQ)