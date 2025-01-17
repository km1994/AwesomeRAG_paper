### OP-RAG【注意力管理】
> **注意力管理**：就像看一本特别厚的书，你不可能把每个细节都记住，但懂得在关键章节做好标记的人才是高手。它不是漫无目的地看，而是像个资深读书人，边读边在重点处画下重点，需要的时候直接翻到标记页。
>

* 发表时间：2024.09.03
* 论文名称：[In Defense of RAG in the Era of Long-Context Language Models](https://arxiv.org/abs/2409.01666)
* 论文地址：[https://arxiv.org/abs/2409.01666](https://arxiv.org/abs/2409.01666)
* Github 地址：[https://github.com/qhjqhj00/MemoRAG](https://github.com/qhjqhj00/MemoRAG)

#### 一、论文动机

- **背景**：随着长文本LLM的出现，这些模型能处理更长的文本序列，RAG的吸引力似乎下降。然而，英伟达认为LLMs中的极长语境会导致对相关信息的关注度降低，并导致答案质量的潜在下降。

#### 二、论文思路

- **模型机制**：OP-RAG（顺序保留检索增强生成）机制，保持检索到的文本块在原文中的顺序，与传统RAG将检索到的文本块按相关性降序排列不同。
- **性能表现**：使用OP-RAG，随着检索块数量的增加，答案质量先上升，然后下降，形成倒U形曲线。与将整个上下文作为输入的长上下文LLM相比，OP-RAG可以用更少的标记获得更高的答案质量。

#### 三、实验设计与结果

- **实验设置**：在长文本问答任务中，OP-RAG的表现比传统的RAG和长文本LLM都要好。
- **关键数据**：特别是在使用Llama3.1-70B模型时，OP-RAG在只使用16K tokens的情况下，就达到了44.43的F1分数，而没有使用RAG的Llama3.1-70B，即使使用了128K tokens，也只得到了34.32的F1分数。

#### 四、论文总结

OP-RAG通过保持检索到的文本块的原始顺序，显著提高了RAG在长上下文问答应用中的性能，证明了在长上下文答案生成中，RAG仍然具有重要的价值和优势。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/WLaaniD7RRgN0h2OCztDcQ](https://mp.weixin.qq.com/s/WLaaniD7RRgN0h2OCztDcQ)
