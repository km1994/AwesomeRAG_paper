### Multi-Meta-RAG【元筛选器】
> **元筛选器**：像个经验丰富的资料管理员，通过多重筛选机制，从海量信息中精准定位最相关的内容。它不只看表面，还会深入分析文档的"身份标签"（元数据），确保找到的每份资料都真正对题。
>

* 发表时间：2024.06.19
* 论文名称：[Multi-Meta-RAG: Improving RAG for Multi-Hop Queries using Database Filtering with LLM-Extracted Metadata](https://arxiv.org/abs/2406.13213)
* 论文地址：[https://arxiv.org/abs/2406.13213](https://arxiv.org/abs/2406.13213)
* Github 地址：[https://github.com/mxpoliakov/multi-meta-rag](https://github.com/mxpoliakov/multi-meta-rag)

#### 一、论文动机

- **RAG的挑战**：传统的RAG方法在回答多跳问题时表现不佳，因为这些问题需要从多个信息源中提取并推理出答案。传统的RAG技术很难从多个文档中找到正确的信息片段，单一的向量很难召回出差异较大的信息源.
- **多跳问题**：多跳问题是指那些需要从多个信息源中提取并推理出答案的问题。例如，询问“Engadget在The Verge之前报道了13.6英寸MacBook Air的折扣吗？”这类问题需要从多个来源中提取信息并进行推理.

#### 二、论文思路

![](20240619_Multi-Meta-RAG/img/v2-78e8857116cc94aca21e6dc9ab8443cd_1440w.png)

- **核心思想**：使用数据库过滤和LLM提取的元数据来提高文档选择的相关性。具体步骤如下：
  1. **问题分析**：使用一个辅助的LLM分析问题，提取出问题中的关键信息，如新闻来源或发布日期.
  2. **数据库过滤**：用提取的关键信息作为过滤条件，从数据库中找到最相关的文档片段.
  3. **生成答案**：基于过滤后的文档片段，生成最终的答案.

#### 三、实验设计与结果

- 实验设计
  - **基准测试数据集**：使用MultiHop-RAG基准测试数据集，该数据集包含了很多多跳查询的例子.
  - **评估指标**：评估文档片段的检索效果和LLM生成答案的准确性.
- 实验结果
  - **显著提升**：Multi-Meta-RAG在文档片段的检索和LLM生成答案的准确性上都有显著提升。具体表现为：
    - **文档检索**：能够更准确地从多个信息源中提取相关信息片段.
    - **答案生成**：生成的答案更准确，减少了错误信息的出现.

#### 四、论文总结

尽管存在一些局限性，Multi-Meta-RAG仍然是一个简单易懂且效果显著的方法，能够显著提高RAG在多跳查询中的表现。通过结合数据库过滤和LLM提取的元数据，Multi-Meta-RAG在多跳查询任务中表现出色，为RAG技术的发展提供了新的思路和方法.

## 致谢

* 参考：[https://mp.weixin.qq.com/s/Jf3qdFR-o_A4FXwmOOZ3pg](https://mp.weixin.qq.com/s/Jf3qdFR-o_A4FXwmOOZ3pg)