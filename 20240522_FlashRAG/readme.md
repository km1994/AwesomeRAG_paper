# FlashRAG【百宝箱】
> **百宝箱**：把各路RAG神器打包成一个工具包，让研究者像挑选积木一样，随心所欲地搭建自己的检索模型。
>

* 发表时间：2024.05.22
* 论文名称：[FlashRAG: A Modular Toolkit for Efficient Retrieval-Augmented Generation Research](https://arxiv.org/abs/2405.13576)
* 论文地址：[https://arxiv.org/abs/2405.13576](https://arxiv.org/abs/2405.13576)
* Github 项目：[https://github.com/RUC-NLPIR/FlashRAG](https://github.com/RUC-NLPIR/FlashRAG)

## 一、论文动机

- **RAG技术**：检索增强生成（RAG）技术通过利用外部知识库来缓解大型语言模型（LLM）中的幻觉问题，但缺乏标准化的实现框架，使得研究人员难以比较和评估不同的RAG方法.
- **现有工具包的局限性**：现有的RAG工具包如LangChain和LlamaIndex通常比较重量级且难以满足研究人员的个性化需求.

## 二、论文思路

![](20240522_FlashRAG/img/v2-f282e2c53a094312974f774a64c54f1b_1440w.png)

- **三个模块**：FlashRAG由环境模块、组件模块和管道模块组成.
  - **环境模块**：提供必要的数据集、超参数和评估指标.
  - **组件模块**：包括五个主要组件：判断器、检索器、排序器、精炼器和生成器.
  - **管道模块**：将各种组件组合在一起以实现完整的RAG过程，提供了多种预设的管道，方便用户快速搭建RAG流程.
- **组件模块详解**：
  1. **判断器（Judger）**：确定是否需要检索.
  2. **检索器（Retriever）**：支持多种检索方式，如稀疏检索和稠密检索，并支持自定义预取结果.
  3. **排序器（Reranker）**：优化检索结果的顺序，支持多种跨编码模型.
  4. **精炼器（Refiner）**：减少生成器的输入文本量并降低噪声，提供四种类型的精炼器供选择.
  5. **生成器（Generator）**：支持多种主流LLM加速库和编码解码模型.

## 三、实验设计与结果

![](20240522_FlashRAG/img/微信截图_20250109180254.png)

- **基准数据集**：收集并预处理了32个基准数据集，涵盖了RAG工作中使用的大部分数据集，所有数据集都已格式化为统一的JSONL结构.
- **语料库**：提供了方便的脚本来自动下载和预处理所需的Wikipedia版本，还提供了DPR提供的广泛使用的2018年12月20日的Wikipedia转储作为基础资源.
- **评估指标**：支持多种检索和生成方面的评估指标，包括召回率@k、精确度@k、F1@k、平均精度（MAP）、词级别F1分数、准确率、BLEU和ROUGE-L等.
- **实验设置**：使用最新的LLAMA3-8B-instruct作为生成器，E5-base-v2作为检索器，2018年12月的Wikipedia数据作为检索语料库，在六个常见数据集上进行实验.
- **主要结果**：与直接生成的基线相比，RAG方法有显著的改进。使用先进的检索器和生成器的标准RAG是一个强大的基线，在六个数据集上都表现良好.

![](20240522_FlashRAG/img/微信截图_20250109180406.png)

- **不同方法的比较分析**：
  - **精炼器优化方法**：在多跳数据集上表现尤其出色，因为复杂问题导致文档检索的准确性降低，需要精炼器优化.
  - **生成器优化方法**：Ret-Robust使用带有lora模块的Llama2-13B模型，大大增强了生成器对检索文档的理解，优于其他无需训练的方法.
  - **适应性检索方法**：在需要多步推理的复杂数据集上比基线有显著的改进，但在简单任务上可能会带来更高的成本，但收益有限.

## 四、论文创新点

- **广泛且可定制的模块化RAG框架**：提供了丰富的组件和预设的管道，方便用户快速搭建RAG流程.
- **预实现的先进RAG算法**：目前已实现12个先进的RAG方法.
- **全面的基准数据集**：目前收录32个基准数据集.
- **高效的RAG辅助脚本**：如下载维基百科、构建索引等.

## 五、论文总结

FlashRAG是一个高效且模块化的开源工具包，旨在帮助研究人员在统一框架内重现现有的RAG方法并开发他们自己的RAG算法。我们的工具包实现了12种先进的RAG方法，并收集和整理了32个基准数据集。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/vvOdcARaU1LD6KgcdShhoA](https://mp.weixin.qq.com/s/vvOdcARaU1LD6KgcdShhoA)

