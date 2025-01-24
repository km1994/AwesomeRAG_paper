### SimRAG【自学成才】
> **自学成才**：面对专业领域时，先自己提问再自己回答，通过不断练习来提升专业知识储备，就像学生通过反复做习题来熟悉专业知识一样。
>

* 发表时间：2024.10.23
* 论文名称：[SimRAG: Self-Improving Retrieval-Augmented Generation for Adapting Large Language Models to Specialized Domains](https://arxiv.org/abs/2410.17952)
* 论文地址：[https://arxiv.org/abs/2410.17952](https://arxiv.org/abs/2410.17952)
* Github 地址：

#### 一、论文动机

RAG通过检索相关文档来增强模型的回答能力，类似于人类在回答问题前查阅资料的过程。尽管RAG技术不断改进，但在专业领域的表现仍不理想，主要原因是模型可能无法正确利用检索到的专业文献。

#### 二、论文思路

![](20241023_SimRAG/img/v2-b3d8a6621382a21f426b84ca3f6f3e57_1440w.png)

SimRAG框架分为两个阶段：基础训练和自我提升。

- 基础训练

基础训练阶段的目标是让模型掌握基本能力：

1. **指令理解能力**：使用OpenAssistant、Dolly和SODA等数据集训练模型理解人类指令。
2. **问答能力**：使用Squad、DROP和NQ等问答数据集提升模型的解题能力。
3. **检索能力**：训练模型从文档中找到可能的答案，并根据文档和答案生成问题。

- 自我提升

自我提升阶段是SimRAG的核心，模型利用基础训练阶段学到的能力来自我提升：

1. **答案生成**：模型阅读专业文献，提取关键信息作为潜在答案。
2. **问题生成**：基于提取的答案，生成不同类型的问题（如填空题、多选题、判断题）。
3. **质量控制**：筛选生成的问题，确保答案在文档中可找到，且问题清晰合理。

#### 三、实验设计与结果

- 实验设计: SimRAG在三个专业领域进行了测试
  - 医疗领域：使用PubMedQA、BioASQ、MedQA等7个数据集。
  - 科学领域：使用ARC、SciQ、MMLU-sci等3个数据集。
  - 计算机科学领域：使用CS-Bench数据集。

- 实验结果：SimRAG在医疗、科学和计算机科学领域的表现如下
  - 医疗领域：SimRAG在多个数据集上超越了通用大模型和专业领域模型。
  - 科学领域：SimRAG在ARC、SciQ和MMLU-sci数据集上表现优异。
  - 计算机科学领域：SimRAG在CS-Bench数据集上取得了较好的成绩。

#### 四、论文总结

SimRAG通过让模型同时学会回答和提出问题，提升了LLM在专业领域的表现。其核心在于利用检索增强生成技术，结合自我提升策略，让模型更好地理解和应用专业知识。尽管存在一些局限性，但SimRAG为领域适应性模型的研究提供了新的思路。


## 致谢

* 参考：[https://mp.weixin.qq.com/s/pR-W_bQEA4nM86YsVTThtA](https://mp.weixin.qq.com/s/pR-W_bQEA4nM86YsVTThtA)