### AutoRAG【调音师】
> **调音师**：一位经验丰富的调音师，不是靠猜测调音，而是通过科学测试找到最佳音效。它会自动尝试各种RAG组合，就像调音师测试不同的音响设备搭配，最终找到最和谐的"演奏方案"。
>

* 发表时间：2024.10.28
* 论文名称：[AutoRAG: Automated Framework for optimization of Retrieval Augmented Generation Pipeline](https://arxiv.org/abs/2410.20878)
* 论文地址：[https://arxiv.org/abs/2410.20878](https://arxiv.org/abs/2410.20878)
* Github 地址：[https://github.com/Marker-Inc-Korea/AutoRAG_ARAGOG_Paper](https://github.com/Marker-Inc-Korea/AutoRAG_ARAGOG_Paper)

#### 一、论文动机

在实际应用中，**选择适合特定数据和用例的RAG（检索增强生成）技术栈是一个复杂且耗时的任务**。市面上存在多种RAG模块和Pipeline，但缺乏一种简单的方法来评估和选择最适合的组合。

为此，研究者提出了 AutoRAG，这是一个自动化工具，能够自动评估多种RAG模块组合，并找到最适合特定用例的RAG Pipeline。

#### 二、AutoRAG的核心功能

![](20241028_AutoRAG/img/v2-a14c7b21af6d896ce425652dc6feec9e_1440w.png)

AutoRAG通过以下方式实现对RAG技术栈的优化：

- **支持多种模块**：
   1. **解析模块**：支持16种解析模块，包括PDFMiner，PDFPlumber，PyPDFium2，PyPDF，PyMuPDF，UnstructuredPDF，NaverClovaOCR，llama Parse，Upstage Document Parser，Directory，Unstructured，csv，json，unstructuredmarkdown，bshtml，unstructuredxml。
   2. **切块模块**：支持10种切块模块，如Token，SentenceTransformersToken，Character，RecursiveCharacter，Sentence，Konlpy ，Semantic_llama_index，SemanticDoubleMerging，SentenceWindow，SimpleFile。
   3. **重排**：UPR，Tart，MonoT5，Cohere reranker，RankGPT，Jina Reranker，Sentence Transformer Reranker，Colbert Reranker，Flag Embedding Reranker，Flag Embedding LLM Reranker，Time Reranker，OpenVINO Reranker，VoyageAI Reranker，MixedBread AI Reranker，Ko-reranker，pass_reranker
   4. **Query理解**：query_decompose，hyde，multi_query_expansion，pass_query_expansion
   5. **检索**：bm25，vectordb，hybrid_rrf，hybrid_cc
   6. **评价指标**：支持15种评价指标，如Precision，Recall，F1，MRR (Mean Reciprocal Rank)，MAP (Mean Average Precision)，NDCG (Normalized Discounted Cumulative Gain)，Token Precision，Token Recall，Token F1，BLEU，ROUGE，METEOR，Sem Score，G-Eval，Bert Score。

- **自动化评估**：
   1. 用户可以提供自己的 QA数据集 和 Corpus数据集，AutoRAG将自动评估不同的RAG模块组合。
   2. 通过设置YAML文件，用户可以定义评估的参数和目标。
   3. AutoRAG将运行评估流程，自动选择最佳的RAG Pipeline。

- 数据准备。为了优化RAG性能，需要准备两种类型的数据：
  1. **QA数据集**：用于准确可靠的评估和优化。
  2. **Corpus数据集**：用于RAG检索文档并生成答案。

- 优化步骤
  1. **设置YAML文件**：定义评估的参数和目标。
  2. **运行评估**：AutoRAG自动评估不同的RAG模块组合。
  3. **优化过程**：根据评估结果选择最佳的RAG Pipeline。
  4. **部署**：将优化后的RAG Pipeline部署到实际应用中。

#### 三、优势

AutoRAG的主要优势在于：

1. 自动化：简化了RAG模块选择和评估的过程，节省时间和精力。
2. 灵活性：支持多种RAG模块和评价指标，适应不同的数据和用例。
3. 高效性：通过自动化评估，快速找到最适合的RAG技术栈。

#### 四、论文总结

AutoRAG通过自动化评估多种RAG模块组合，帮助用户快速找到最适合特定数据和用例的RAG技术栈。它支持多种解析、切块、检索和评价模块，简化了优化流程，提高了RAG系统的性能和效率。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/96r6y3cNmLRL2Z0W78X1OQ](https://mp.weixin.qq.com/s/96r6y3cNmLRL2Z0W78X1OQ)