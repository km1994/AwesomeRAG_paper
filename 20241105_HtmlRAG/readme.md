### HtmlRAG【排版师】
> **排版师**：把知识不是当作流水账来记，而是像排版杂志一样，该加粗的加粗，该标红的标红。就像一个挑剔的美编，觉得光有内容不够，还得讲究排版，这样重点才能一目了然。
>

* 发表时间：2024.11.05
* 论文名称：[HtmlRAG: HTML is Better Than Plain Text for Modeling Retrieved Knowledge in RAG Systems](https://arxiv.org/abs/2411.02959)
* 论文地址：[https://arxiv.org/abs/2411.02959](https://arxiv.org/abs/2411.02959)
* Github 地址：[https://github.com/plageon/HtmlRAG](https://github.com/plageon/HtmlRAG)

#### 一、论文动机

- 背景：大型语言模型（LLM）在自然语言处理领域展现了强大的能力，但也面临知识遗忘、过时信息和幻觉等问题。检索增强生成（RAG）系统通过检索外部知识并将其融入生成过程中，增强了LLM的响应能力。
- 问题：传统RAG系统将HTML文档转换为纯文本，导致结构化和语义信息丢失。为解决这一问题，提出使用HTML作为外部知识的格式，保留更多有用信息。

#### 二、论文思路

- **HTML清理**：移除HTML文档中的冗余内容（如CSS、JavaScript、注释等），压缩HTML结构，同时保留重要语义信息。
- **块树构建**：将HTML文档解析为块树，每个块代表一段逻辑上相关的内容。通过合并DOM树中的多个子节点，形成大小适中的块。
- **HTML修剪**：
  - **基于文本嵌入的块修剪**：使用文本嵌入模型对块进行初步修剪，保留与用户查询高度相关的块。
  - **基于生成模型的精细块修剪**：使用生成模型对剩余块进行进一步修剪，评估每个块的重要性并删除不重要的块。

#### 三、实验设计与结果

- 数据集选择：使用六个数据集（ASQA、HotpotQA、NQ、Trivia-QA、MuSiQue、ELI5）进行实验，涵盖不同类型的问答任务。
- 实验设置及评价指标：使用Llama-3.1-70B-Instruct和Llama-3.1-8B-Instruct模型，评价指标包括精确匹配（Exact Match）、Hit@1、ROUGE-L和BLEU评分。
- 实验结果：HtmlRAG在所有评估指标上均超过基线方法，证明了HTML修剪的有效性。
- 分析：HTML格式在保留结构和语义信息方面具有优势，更强大的语言模型（如70B）在处理HTML格式知识时表现更好。

#### 四、论文总结

HtmlRAG 旨在通过直接利用HTML格式的外部知识来提升检索增强生成（RAG）系统的性能。该方法通过保留HTML文档中的结构化和语义信息，解决了传统RAG系统中因使用纯文本而导致的信息丢失问题。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/A4vjN1eJr7hJd75UH0kuXA](https://mp.weixin.qq.com/s/A4vjN1eJr7hJd75UH0kuXA)