### RAGChecker【质检员】
> **质检员**：不只简单地判断答案对错，而是会深入检查整个回答过程中的每个环节，从资料查找到最终答案生成，就像一个严格的考官，既给出详细的评分报告，还会指出具体哪里需要改进。
>

* 发表时间：2024.08.15
* 论文名称：[RAGChecker: A Fine-grained Framework for Diagnosing Retrieval-Augmented Generation](https://arxiv.org/abs/2408.08067)
* 论文地址：[https://arxiv.org/abs/2408.08067](https://arxiv.org/abs/2408.08067)
* Github 地址：[https://github.com/amazon-science/RAGChecker](https://github.com/amazon-science/RAGChecker)

#### 一、论文动机

- **RAG技术的重要性**：RAG技术通过将外部知识库和大型语言模型（LLM）内部知识无缝整合，大幅提升了AI系统的准确性和可靠性。
- **评估挑战**：现有的评估方法难以全面反映RAG系统的复杂性和实际表现，通常只能提供最终打分报告，缺乏细粒度的诊断信息。

#### 二、论文思路

- **目的**：RAGChecker为RAG系统提供细粒度、全面、可靠的诊断报告，并为进一步提升性能提供可操作的方向。
- **主要特点**：
  1. **细粒度评估**：采用基于声明（claim）级别的蕴含关系检查，而非简单的回复级别评估，提供更详细的系统性能分析。
  2. **全面的指标体系**：涵盖RAG系统各个方面性能的指标，包括忠实度、上下文利用率、噪声敏感度和幻觉等。
  3. **经过验证的有效性**：评估结果与人类判断有很强的相关性，表现超过其他现有评估指标，保证了评估结果的可信度和实用性。
  4. **可操作的洞察**：提供的诊断指标为改进RAG系统提供明确的方向指导，帮助研究人员和实践者开发更有效和可靠的AI应用。

#### 三、实验设计与结果

- **整体指标**：
  - **Precision（精确率）**：模型回答中正确陈述的比例。
  - **Recall（召回率）**：模型回答中包含的标准答案中陈述的比例。
  - **F1 score（F1分数）**：精确率和召回率的调和平均数，提供平衡的性能度量。
- **检索模块指标**：
  - **Context Precision（上下文精确率）**：在所有检索块中，包含至少一个标准答案陈述的块的比例。
  - **Claim Recall（陈述召回率）**：被检索块覆盖的标准答案陈述的比例。
- **生成模块指标**：
  - **Context Utilization（上下文利用率）**：评估生成模块如何有效利用从检索块中获取的相关信息来产生正确的陈述。
  - **Noise Sensitivity（噪音敏感度）**：衡量生成模块在回答中包含来自检索块的错误信息的倾向。
  - **Hallucination（幻觉）**：测量模型生成既不存在于检索块也不在标准答案中的信息的频率。
  - **Self-knowledge（模型内部知识）**：评估模型在未从检索块获得信息的情况下，正确回答问题的频率。
  - **Faithfulness（忠实度）**：衡量生成模块的响应与检索块提供的信息的一致程度。

#### 四、使用RAGChecker

- **环境设置**：安装RAGChecker及其依赖。
  ```bash
  pip install ragchecker
  python -m spacy download en_core_web_sm
  ```
- **准备数据**：将RAG系统的输出准备成特定的JSON格式，包括查询、标准答案、模型回答和检索的上下文。
- **运行评估**：
  - 使用命令行：
    ```bash
    ragchecker-cli \
        --input_path=examples/checking_inputs.json \
        --output_path=examples/checking_outputs.json
    ```
  - 使用Python代码：
    ```python
    from ragchecker import RAGResults, RAGChecker
    from ragchecker.metrics import all_metrics

    # 从JSON初始化RAGResults
    with open("examples/checking_inputs.json") as fp:
        rag_results = RAGResults.from_json(fp.read())

    # 设置评估器
    evaluator = RAGChecker()

    # 评估结果
    evaluator.evaluate(rag_results, all_metrics)
    print(rag_results)
    ```
- **分析结果**：RAGChecker输出json格式的文件，展示评估指标，帮助开发者了解RAG系统的各个方面表现。

#### 五、论文总结

RAGChecker 的诊断工具为 RAG 系统提供细粒度、全面、可靠的诊断报告，并为进一步提升性能，提供可操作的方向。它不仅能评估系统的整体表现，还能深入分析检索和生成两大核心模块的性能。


## 致谢

* 参考：[https://mp.weixin.qq.com/s/x4o7BinnwvTsOa2_hegcrQ](https://mp.weixin.qq.com/s/x4o7BinnwvTsOa2_hegcrQ)
