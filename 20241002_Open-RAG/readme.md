### Open-RAG【智囊团】
> **智囊团**：把庞大的语言模型分解成专家小组，让它们既能独立思考又能协同工作，还特别会分辨真假信息，关键时刻知道该不该查资料，像个经验丰富的智囊团。
>

* 发表时间：2024.10.02
* 论文名称：[Open-RAG: Enhanced Retrieval-Augmented Reasoning with Open-Source Large Language Models](https://arxiv.org/abs/2410.01782)
* 论文地址：[https://arxiv.org/abs/2409.01782](https://arxiv.org/abs/2409.01782)
* Github 地址：[https://github.com/ShayekhBinIslam/openrag](https://github.com/ShayekhBinIslam/openrag)

#### 一、论文动机

- 现有的RAG方法在处理复杂查询（如多跳检索任务）时，推理能力有限。OpenRAG框架通过增强开源LLM的推理能力，解决了这一问题。

#### 二、论文思路

![](20241002_Open-RAG/img/v2-18bf579b07447508f85c497b644e7b77_1440w.png)

- **架构转换**：**OpenRAG将任意密集LLM转换为参数高效的稀疏专家混合（MoE）模型**，能够处理单跳和多跳查询等复杂推理任务。具体实现包括：
  - 路由器（R）从头开始训练。
  - 前馈网络（FFN）层保持冻结，并由基于并行适配器的专家（E）进行调整。
  - 其他层被复制。
- **训练过程**: 通过独特的训练方法，使模型能够导航看似相关但具有误导性的挑战性干扰因素。
  - 训练过程中，模型学习生成检索/不检索的反射标记，并评估检索内容的相关性、支持程度和实用性。
  - **OPEN-RAG训练数据准备**：涉及从每个原始对（q, y）生成四种新的训练实例的变化，每种都使用真实情况/LLM评论家和检索到的段落，结合不同的反射标记。OPEN-RAG不仅使LLM能够反思生成质量，还能够对比干扰项。
- **推理流程**：
  - **检索/不检索**：模型学会生成检索/不检索的标记，以指示是否需要检索来回答查询。
  - **相关性评估**：对于检索到的内容，模型生成相关性标记，指示内容是否与查询相关。
  - **生成答案**：根据预测的相关性、支持度和效用标记，对所有可能的答案进行排序，生成最终答案。

#### 三、实验设计与结果

- 在多种知识密集型的单跳/多跳短文/长文推理任务中，基于Llama2-7B的OpenRAG在事实准确性和推理能力方面显著优于现有的开源RAG模型，并且常常匹配或超越了最先进的专有LLMs及其RAG模型。
- OpenRAG在多个任务中超越了ChatGPT-RAG、Self-RAG、RAG 2.0和104B RAG-Command R+，树立了新的基准。
- OpenRAG结合CRAG（Corrective Retrieval Augmented Generation）方法，评估了模型对检索质量的鲁棒性。结果表明，OpenRAG在结合CRAG数据集时表现优于其他基线，显示出对高质量检索的潜在改进能力。

#### 四、论文总结

OpenRAG通过创新的架构和训练方法，显著提升了开源LLM在RAG任务中的推理能力，并在多个任务中超越了现有的先进模型。其自适应检索策略和鲁棒性分析进一步证明了其在实际应用中的潜力。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/H0_THczQ3UWCkSnnk-vveQ](https://mp.weixin.qq.com/s/H0_THczQ3UWCkSnnk-vveQ)
