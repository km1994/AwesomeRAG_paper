### RuAG【炼金术士】
> **炼金术士**：像个炼金术士，能将海量数据提炼成清晰的逻辑规则，并用通俗易懂的语言表达出来，让AI在实际应用中更有智慧。
>

* 发表时间：2024.11.04
* 论文名称：[RuAG: Learned-rule-augmented Generation for Large Language Models](https://arxiv.org/abs/2411.03349)
* 论文地址：[https://arxiv.org/abs/2411.03349](https://arxiv.org/abs/2411.03349)
* Github 地址：

#### 一、论文动机

- **外部知识注入**：利用外部数据集增强预训练LLMs在下游任务中的性能是当前研究的热点。现有方法包括监督式微调（SFT）、上下文学习（ICL）、检索增强生成（RAG）和知识图谱（KGs）的使用，但这些方法存在计算成本高、依赖手工标注、上下文窗口有限或需要大量人工干预等挑战。
- **逻辑规则的优势**：逻辑规则因其高信息密度和可解释性，成为连接多样化数据和LLMs理解的桥梁。逻辑规则可以将复杂关系以简洁形式表达，并且易于翻译成自然语言，适合与LLMs结合。

#### 二、论文思路

RuAG框架包含三个关键阶段：

1. **LLM辅助的逻辑规则搜索公式化**：利用LLMs的常识自动定义逻辑规则中的目标谓词和主体谓词，减少人工干预。
2. **基于蒙特卡洛树搜索（MCTS）的逻辑规则搜索**：在LLMs定义的搜索空间中，利用MCTS高效发现逻辑规则。
3. **逻辑规则增强的生成**：将逻辑规则翻译成自然语言并注入LLMs的提示中，以增强其在下游任务中的推理能力。

- 方法细节

1. **逻辑规则搜索公式化**：
   1. **初始谓词定义**：将数据集的标签作为目标谓词，特征作为主体谓词。
   2. **去除无关谓词**：LLMs通过常识推理过滤掉与目标无关的谓词。
   3. **新目标谓词建议**：LLMs生成新的目标谓词以探索更多逻辑规则。
2. **基于MCTS的逻辑规则搜索**：
   1. **定义状态、动作和奖励**：状态是部分逻辑规则，动作是添加新谓词，奖励是规则的精度。
   2. **MCTS过程**：通过选择、扩展、模拟和回溯四个阶段，高效搜索逻辑规则。
3. **逻辑规则增强的生成**：
   1. **清理搜索到的规则**：去除低质量或重复的规则。
   2. **翻译规则为自然语言**：将逻辑规则翻译成自然语言句子，注入LLMs的提示中。
   3. **选择相关规则**：根据LLMs的上下文窗口大小，选择最相关的规则注入。

#### 三、实验设计与结果

作者在多个领域（自然语言处理、时间序列、决策制定和工业任务）评估了RuAG框架的有效性，包括关系抽取（DWIE数据集）、日志异常检测（HDFS数据集）和多人合作游戏（Alice&Bob）等任务。实验结果表明，RuAG在多个任务中显著优于现有方法，例如：

- 在关系抽取任务中，使用GPT-4的RuAG方法达到了60.42%的F1分数。
- 在日志异常检测任务中，RuAG达到了92.59%的F1分数。
- 在Alice&Bob游戏中，RuAG的平均胜率达到了70%。

#### 四、论文总结

RuAG（Learned-Rule-Augmented Generation） 的新型框架，旨在通过将离线数据自动提炼成可解释的一阶逻辑规则，并将其注入到大型语言模型（LLMs）中，以增强其推理能力。该框架通过结合逻辑规则和LLMs的生成能力，解决了现有方法（如上下文学习ICL、检索增强生成RAG等）在上下文窗口大小和信息注入效率上的限制。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/A4vjN1eJr7hJd75UH0kuXA](https://mp.weixin.qq.com/s/A4vjN1eJr7hJd75UH0kuXA)