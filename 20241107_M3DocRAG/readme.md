### M3DocRAG【感官达人】
> **感官达人**：不是只会读书，还能看图识图，听声辨位。像个综艺节目里的全能选手，图片能看懂，文字能理解，该跳跃思维时就跳跃，该专注细节时就专注，各种挑战都难不倒。
>

* 发表时间：2024.11.07
* 论文名称：[M3DocRAG: Multi-modal Retrieval is What You Need for Multi-page Multi-document Understanding](https://arxiv.org/abs/2411.04952)
* 论文地址：[https://arxiv.org/abs/2411.04952](https://arxiv.org/abs/2411.04952)
* Github 地址：[https://github.com/Omaralsaabi/M3DOCRAG](https://github.com/Omaralsaabi/M3DOCRAG)

#### 一、论文动机

- DocVQA任务：通过解读文档图像中的信息来回答文本问题，广泛应用于金融、医疗和法律等领域。
- 现有方法的局限性：
  - 现有方法主要聚焦于单页文档的视觉问答或基于文本提取（如OCR）的检索增强生成（RAG）。
  - 这些方法难以处理跨多页或多文档的问题，且会忽略文档中的视觉元素（如图表、图形等），导致信息不完整或不准确。

#### 二、论文思路

![](20241107_M3DocRAG/img/v2-3a2da2577b516badf03c3d12c9300217_1440w.png)

- **定义**：M3DocRAG是一个多模态RAG框架，能够灵活适应不同文档上下文（封闭域和开放域）、问题跳转（单跳和多跳）以及证据模式（文本、图表、图形等）。
- 工作流程：
  - **文档嵌入**：将文档页面转换为RGB图像，并提取视觉嵌入（如ColPali）。
  - **页面检索**：通过文本查询检索相似度高的页面，开放域设置中使用近似索引（如倒排文件索引IVF）以加快搜索速度。
  - **问答**：利用多模态语言模型（如Qwen2-VL）从检索到的页面生成答案。

#### 三、实验设计与结果

- 开放领域文档视觉问答：
  - 多模态RAG比文本RAG表现更好，尤其是在处理非文本证据时。
  - M3DocRAG（ColPali + Qwen2-VL 7B）在不同证据模式和问题跳转场景中表现优异。
- 封闭域文档视觉问答：
  - 多模态RAG增强了对长文档的理解能力。
  - 在多个基准测试中，M3DocRAG（ColPali + Qwen2-VL 7B）取得了领先性能。
- 额外分析：
  - 索引方法：近似索引（如IVFFlat）在速度和准确性之间取得了良好平衡。
  - 多模态语言模型：Qwen2-VL 7B在所有基准测试中表现最佳。
  - 多模态检索模型：ColPali表现优于其他检索模型。

#### 四、论文总结

M3DocRAG是一种新颖的多模态RAG框架，能够灵活适应各种文档上下文（封闭域和开放域）、问题跳转（单跳和多跳）和证据模式（文本、图表、图形等）。M3DocRAG使用多模态检索器和MLM查找相关文档并回答问题，因此它可以有效地处理单个或多个文档，同时保留视觉信息。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/A4vjN1eJr7hJd75UH0kuXA](https://mp.weixin.qq.com/s/A4vjN1eJr7hJd75UH0kuXA)