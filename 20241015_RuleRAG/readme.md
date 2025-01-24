### RuleRAG【循规蹈矩】
> **循规蹈矩**：用规矩来教AI做事，就像带新人入职，先给本员工手册。不是漫无目的地学，而是像个严格的老师，先把规矩和范例都讲明白，然后再让学生自己动手。做多了，这些规矩就变成了肌肉记忆，下次遇到类似问题自然知道怎么处理。
>

* 发表时间：2024.10.15
* 论文名称：[RuleRAG: Rule-guided retrieval-augmented generation with language models for question answering](https://arxiv.org/abs/2410.22353)
* 论文地址：[https://arxiv.org/abs/2410.22353](https://arxiv.org/abs/2410.22353)
* Github 地址：[https://github.com/chenzhongwu20/RuleRAG_ICL_FT](https://github.com/chenzhongwu20/RuleRAG_ICL_FT)

#### 一、论文动机

大型语言模型（LLM）在上下文学习（ICL）方面表现出色，但在处理知识密集型任务时存在局限性。RAG框架通过将知识检索与答案生成解耦，显著提升了性能。

然而，**现有RAG框架在检索阶段无法保证检索信息与查询的强相关性，在生成阶段也未能明确指导LLM如何利用检索到的文档**。为此，本文提出RuleRAG，通过引入规则来解决这些问题。

#### 二、论文思路

![](20241015_RuleRAG/img/v2-9562de690b1c874c59f10629d8c0af17_1440w.png)

RuleRAG包括两个主要部分：无需训练的RuleRAG-ICL和经过微调的RuleRAG-FT。

- RuleRAG-ICL：通过在检索和生成阶段引入规则，指导检索器检索逻辑相关的文档，并指导生成器根据规则生成答案。具体流程如下：
  - 给定查询q，从规则库R中选择与q相关的规则Rq。
  - 将q与Rq中的规则r逐一结合，进行规则引导的检索，获取与规则相关的文档Drq。
  - 将所有规则的检索结果Drq组合成最终检索结果Dq。
  - 基于q、Rq和Dq生成最终答案a。
- RuleRAG-FT：通过规则引导的微调（RGFT）进一步提升模型性能。RGFT包括：
  - **规则引导的检索器微调（RGFT-retriever）**：通过对比学习优化检索器，使其能够更准确地检索与规则相关的文档。
  - **规则引导的生成器微调（RGFT-generator）**：通过监督学习优化生成器，使其能够根据规则更好地利用检索到的文档生成答案。

#### 三、实验设计与结果

- 实验设计：作者使用了多种检索器（如DPR、SimCSE、BM25）和生成器（如LLAMA2_7B、LLAMA2_13B、ChatGLM2_6B等），并对比了RuleRAG与标准RAG及其他基线方法的性能。
- 实验结果：RuleRAG在五个基准数据集上均显著优于标准RAG和其他基线方法：
  - RuleRAG-ICL在Recall@10和Exact Match（EM）等指标上平均提升了+89.2%和+103.1%。
  - RuleRAG-FT进一步提升了性能，尤其是在Recall@10和EM指标上，平均提升了+45.7%和+24.2%。

#### 四、论文总结

本文提出的RuleRAG通过引入规则显著提升了检索增强型生成模型在知识密集型问答任务中的性能。未来工作将探索RuleRAG在更复杂的查询场景下的表现，并进一步优化规则挖掘和利用机制。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/GNLvKG8ZgJzzNsWyVbSSig](https://mp.weixin.qq.com/s/GNLvKG8ZgJzzNsWyVbSSig)