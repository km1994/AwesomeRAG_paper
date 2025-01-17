### Medical-Graph-RAG【数字医生】
> **数字医生**：像个经验丰富的医学顾问，用图谱把复杂的医疗知识整理得清清楚楚，诊断建议不是凭空想象，而是有理有据，让医生和患者都能看明白每个诊断背后的依据。
>

* 发表时间：2024.08.08
* 论文名称：[Medical Graph RAG: Towards Safe Medical Large Language Model via Graph Retrieval-Augmented Generation](https://arxiv.org/abs/2408.04187)
* 论文地址：[https://arxiv.org/abs/2408.04187](https://arxiv.org/abs/2408.04187)
* Github 地址：[https://github.com/SuperMedIntel/Medical-Graph-RAG](https://github.com/SuperMedIntel/Medical-Graph-RAG)

#### 一、论文动机

- **研究问题**：如何在医学领域中使用基于图的RAG框架来提高LLM生成基于证据的医疗响应的能力，特别是在处理私有医疗数据时的安全性和可靠性。
- **研究难点**：医学领域依赖庞大的知识库，这些知识难以适应LLM的有限上下文窗口；医学领域对术语系统的精确性和事实的确定性要求极高；验证医学响应的准确性对于非专家用户来说特别具有挑战性。

#### 二、论文思路

![](20240808_Medical-Graph-RAG/img/v2-e9ebf4771f4096168817e260e483511d_1440w.png)

- **三元组图谱构建**：提出了一种独特的三元组图构建方法，将用户RAG数据与可信的医疗来源和受控词汇表连接起来，生成三元组[RAG数据, 来源, 定义]以构建用户文档的综合图。
  - **语义文档分块**：将大医学文档分割成符合LLM上下文限制的数据块，采用字符分离和主题语义分区的混合方法。
  - **实体提取**：从每个块中提取实体，生成包含名称、类型和上下文的结构化输出。
  - **三元组链接**：构建仓库图（RepoGraph），将用户RAG文档与可信来源和专业定义连接起来。
  - **关系链接**：识别RAG实体之间的关系，生成简洁的关系短语，指定源和目标实体及其关系描述。
- **U-Retrieval策略**：提出了一种独特的U-Retrieval策略，结合自上而下的精确检索和自下而上的响应细化，平衡全局上下文意识和检索效率。
  - **图标签化**：使用预定义的医学标签总结每个Meta-MedGraph，并迭代生成更抽象的标签摘要。
  - **U-Retrieval**：首先生成用户查询的标签摘要，并使用自上而下的方法检索最相关的图，然后自下而上地逐步整合更高层次的标签，直到生成最终答案。

#### 三、实验设计与结果

- 实验设计
  - **数据集**：使用了多个数据集，包括MIMIC-IV电子健康记录数据集、MedC-K生物医学学术论文和教科书数据集、FakeHealth和PubHealth公共卫生事实验证数据集，以及一个收集的多层次健康问答数据集DiverseHealth。
  - **实验设置**：比较了不同RAG方法在6种语言模型上的表现，包括Llama2、Llama3、Gemini-pro和GPT-4。使用Llama3-70B构建图，文本嵌入使用OpenAI的text-embedding-3-large模型。模型比较使用5次响应集成进行评估。
- 结果与分析
  - **多选题评估**：MedGraphRAG在健康和医学问答基准测试中显著提高了LLM的性能。与没有检索的基线相比，MedGraphRAG在事实检查和医学问答基准测试中分别平均提高了近10%和8%。与使用GraphRAG的基线相比，分别提高了约8%和5%。特别是在较小的LLMs（如Llama2-13B和Llama2-70B）中，MedGraphRAG表现出更显著的改进。
  - **长形式生成评估**：人类评估显示，MedGraphRAG在所有指标上均获得了更高的评分。特别是在引用精度（CP）、引用召回率（CR）和可理解性（Und.）方面，MedGraphRAG表现出显著优势，表明其响应更有可能得到准确来源的支持，并且更容易被理解和接受。
  - **消融研究**：通过消融研究验证了所提出模块的有效性。逐步添加Med-MetaGraph、三元组图构建和U-Retrieval模块后，性能逐渐提高。特别是将GraphRAG的图构建替换为三元组图构建后，性能显著提高。

#### 四、论文创新点

- **首次提出**：首次提出了专门应用于医学领域的基于图检索增强生成（RAG）框架，命名为MedGraphRAG。
- **独特的三元组图构建和U检索技术**：开发了独特的三元组图构建和U检索方法，使LLMs能够高效生成基于证据的响应。
- **超越现有方法**：在广泛的医学问答基准测试中，MedGraphRAG的表现优于现有的标准RAG和GraphRAG模型，并在多个医学语料库上设立了新的最先进（SOTA）水平。
- **人类评估验证**：通过人类评估验证，MedGraphRAG能够提供更可理解和基于证据的响应，特别是在复杂医学推理方面。
- **全面的比较**：在多个基准测试中，MedGraphRAG显著提高了LLMs的性能，特别是在健康事实检查和医学问答任务中。

#### 五、论文总结

- **性能提升**：MedGraphRAG通过其基于图的RAG框架，使用三元组图谱构建和U-Retrieval方法，增强了基于证据、上下文感知的响应。其在基准测试和人类评估中的强大表现表明了其确保复杂医学推理准确性的能力。
- **未来工作**：未来的工作将集中在实时数据更新和在实际临床数据上的验证，以确保MedGraphRAG能够利用最新的医学数据和研究成果，并在真实世界应用场景中发挥更大的作用。

#### 六、不足与反思
- **实时数据更新**：未来的工作将集中在实时数据更新和在实际临床数据上的验证，以确保MedGraphRAG能够利用最新的医学数据和研究成果，并在真实世界应用场景中发挥更大的作用。

#### 七、关键问题及回答
- **问题1**：MedGraphRAG在图谱构建方面有哪些独特的设计，这些设计如何提高其在医学领域的应用效果？
  - **三元组图构建**：通过生成三元组[RAG数据, 来源, 定义]来构建用户文档的综合图谱，确保生成的响应能够追溯到其来源和定义，提高了响应的可信度和可解释性。
  - **U-Retrieval**：结合自上而下的精确检索和自下而上的响应细化，平衡全局上下文意识和检索效率，使得LLM能够在保持高效的同时，获取全面的上下文信息，从而生成更准确和可靠的响应。
- **问题2**：MedGraphRAG在实验中表现如何，与其他方法相比有哪些优势？
  - **多选题评估**：在健康和医学问答基准测试中，MedGraphRAG显著提高了LLM的性能，特别是在较小的LLMs中表现出更显著的改进。
  - **长形式生成评估**：人类评估显示，MedGraphRAG在所有指标上均获得了更高的评分，特别是在引用精度、引用召回率和可理解性方面表现出显著优势。
  - **消融研究**：通过消融研究验证了所提出模块的有效性，逐步添加模块后性能逐渐提高。
- **问题3**：MedGraphRAG的未来工作方向是什么？
  - **实时数据更新**：未来的工作将集中在实时数据更新上，以确保MedGraphRAG能够利用最新的医学数据和研究成果。
  - **实际临床数据验证**：研究将在实际临床数据上进行验证，以进一步评估MedGraphRAG在真实世界应用场景中的性能和可靠性。

通过这些改进，MedGraphRAG有望在医学领域发挥更大的作用，提供更高质量和更可靠的医疗响应，从而改善患者的诊疗体验。
## 致谢

* 参考：[https://mp.weixin.qq.com/s/c5-0dCWI0bIa2zHagM1w0w](https://mp.weixin.qq.com/s/c5-0dCWI0bIa2zHagM1w0w)