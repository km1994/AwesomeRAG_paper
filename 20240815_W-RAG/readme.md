### W-RAG【进化搜索】
> **进化搜索**：像个善于自我进化的搜索引擎，通过大模型对文章段落的评分来学习什么是好答案，逐步提升自己找到关键信息的能力。
>

* 发表时间：2024.08.15
* 论文名称：[W-RAG: Weakly Supervised Dense Retrieval in RAG for Open-domain Question Answering](https://arxiv.org/abs/2408.08444)
* 论文地址：[https://arxiv.org/abs/2408.08444](https://arxiv.org/abs/2408.08444)
* Github 地址：[https://github.com/jmnian/weak_label_for_rag](https://github.com/jmnian/weak_label_for_rag)

#### 一、论文动机

- **问题**：密集检索微调需要大量标注数据，耗费人力。
- **解决方案**：利用LLM的重排能力生成弱标记数据，用于训练检索的向量模型。

#### 二、论文思路

W-RAG方法，通过利用LLMs的排名能力为密集检索器创建弱标记数据，从而解决了稀缺的地面真实证据问题。

![](20240815_W-RAG/img/微信截图_20250115090115.png)

W-RAG过程分为三个阶段：

- Step 1: 通过BM25从证据语料库中检索相关段落

使用BM25算法从语料库中检索与问题相关的段落。

- Step 2: 使用LLM生成弱标签

1. 将查询（query）、段落（passage）、指令（instruction）和答案（answer）组装成提示（prompt）。
2. 通过大模型对提示生成答案。
3. 计算每个段落生成ground_truth_answer的概率，作为弱标签。
4. 使用log-likelihood来衡量每个候选段落的相关度分数。

- Step 3: 通过弱标签训练密集检索器

1. 使用获取到的查询、段落和相关度分数来训练密集检索器。
2. 选择两个密集检索器：DPR和ColBERT。

- 训练密集检索器

- **DPR**：使用双编码器架构，通过两个独立的BERT编码器将问题和段落映射到嵌入空间。
  - 训练方式：in-batch negative training，使用top 1的段落作为正样本，top 2-n的作为负样本。
  - 损失函数：\[ \text{loss} = -\log \frac{\exp(\alpha \cdot \text{sim}(q, s_1))}{\sum_{i=1}^n \exp(\alpha \cdot \text{sim}(q, s_i))} \]

- **ColBERT**：使用双编码器架构，通过共享的BERT模型独立编码问题和段落。
  - 训练数据构造：使用positive sample和hard negative sample。
  - 损失函数：\[ \text{loss} = -\log \frac{\max(\text{sim}(q, s_p))}{\max(\text{sim}(q, s_p)) + \max(\text{sim}(q, s_n))} \]

#### 三、实验设计与结果

- 实验设计
  - **数据集**：MSMARCO、QnA v2.1、NQ、SQuAD、WebQ，每个数据集选取5000个QA对和500,000个段落。
  - **模型**：
    - Generator: Llama3-8B-Instruct
    - Retriever: DPR (bert-base-uncased、Yibin-Lei/ReContriever)，ColBERT（bert-base-uncased）
  - **Baseline**：
    - RAG效果对比：Naive（直接用llama3作答）、GroundTruth（将ground-truth文档插入到prompt中作答）
    - 检索效果对比：无监督模型（BM25、ColBERT，Contriever，ReContrever）、基于GroundTruth训练的模型（DPR、ColBERT）
  - **评估指标**：
    - 检索：recall
    - 生成：F1、Rouge-L、BLEU-1
- 实验结果
  - **提升效果**：相比于naive方法，W-RAG在检索和问答上都有显著提升，接近于ground-truth方法。
  - **BM25与LLM的排序能力**：BM25在排序能力上与llama3-8B有显著差距。

#### 四、论文创新点

- **弱监督数据生成方法**
  - **背景**：传统的密集检索（Dense Retrieval）微调需要大量标注数据，这不仅耗费大量人力，而且成本高昂。
  - **创新点**：提出了一种利用大型语言模型（LLM）的重排能力来生成弱标记数据的方法。这种方法不需要人工标注，而是通过模型自动生成标注数据，大大降低了数据标注的成本和工作量。
- 1. **W-RAG框架**
  - **背景**：现有的RAG系统在开放域问答中面临检索和生成的挑战，尤其是在处理复杂问题时，检索的准确性和生成的答案质量有待提高。
  - **创新点**：提出了W-RAG（Weakly Supervised Dense Retrieval in RAG for Open-domain Question Answering），这是一个数据构造方法，通过三个阶段（检索、生成弱标签、训练密集检索器）来提升检索和生成的性能。具体步骤如下：
    1. **通过BM25从证据语料库中检索相关段落**：利用传统的BM25算法快速检索与问题相关的段落。
    2. **使用LLM生成弱标签**：将查询、段落、指令和答案组装成提示（prompt），通过LLM生成每个段落生成ground_truth_answer的概率，作为弱标签。
    3. **通过弱标签训练密集检索器**：使用获取到的查询、段落和相关度分数来训练密集检索器，提升检索的准确性和效率。

#### 五、论文总结

开放域问答中的弱监督密集检索技术，利用大型语言模型的排序能力为训练密集检索器创建弱标注数据。通过评估大型语言模型基于问题和每个段落生成正确答案的概率，对通过 BM25 检索到的前 K 个段落进行重新排序。排名最高的段落随后被用作密集检索的正训练示例。


## 致谢

* 参考：[https://mp.weixin.qq.com/s/JqT1wteHC43h2cPlXmPOFg](https://mp.weixin.qq.com/s/JqT1wteHC43h2cPlXmPOFg)
