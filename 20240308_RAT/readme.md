# RAT【思考者】

> **思考者**：像个善于反思的导师，不是一次性得出结论，而是先有初步想法，然后利用检索到的相关信息，不断审视和完善每一步推理过程，让思维链条更加严密可靠。
>

* 发表时间：2024.03.08
* 论文名称：[RAT: Retrieval Augmented Thoughts Elicit Context-Aware Reasoning in Long-Horizon Generation](https://arxiv.org/abs/2403.05313)
* 论文地址：https://arxiv.org/abs/2403.05313
* Github 项目：[https://github.com/CraftJarvis/RAT](https://github.com/CraftJarvis/RAT)

## 一、论文动机

- **幻觉问题**：在生成式AI应用中，语言模型常常会产生幻觉，即生成与事实不符的内容，影响输出的准确性.
- **效率与准确性的平衡**：应用开发者需要在效率和准确性之间找到平衡点，RAT提供了一种解决方法，能够在不牺牲太多效率的情况下提高准确性.

## 二、论文思路

- **结合CoT和RAG**：RAT是检索增强型思考的简称，通过结合思维链提示和检索增强生成，解决长视野推理和生成任务.
- **工作流程**：
  1. **第一步**：由大型语言模型（LLM）生成初始的Zero-Shot思维链提示，将每个中间思考步骤作为查询进行信息检索，根据检索到的信息修正或细化CoT步骤.
  2. **第二步**：使用修改后的CoT步骤和检索到的上下文生成最终响应或解决方案，提供全面且事实上准确的答案.
- **逐步推理**：RAT是一种渐进的方法，LLM会根据CoT逐步产生响应，类似于人类的推理过程.

## 三、论文创新点

- **Long-Horizon推理**：RAT在复杂的预测建模和规划算法中表现出色，能够模拟和预测不同行动方案在未来较长时期内的后果，处理不确定性并适应变化.
- **任务表现**：在挑战性代码生成、数学推理、任务规划以及创意写作等方面，RAT均取得了显著的成果，超过了传统的CoT提示、RAG以及其他基线方法.
- **优势**：作为一种Zero-Shot提示方法，RAT能够在不进行额外训练的情况下提高生成内容的准确性和可靠性，减少幻觉现象.

## 四、论文总结

RAT（Retrieval-Augmented Thoughts）通过结合思维链提示和检索增强生成，提供了一种有效的方法来解决生成式AI中的幻觉问题，提高输出内容的准确性和可靠性.

## 致谢

* 参考：[https://mp.weixin.qq.com/s/TqmY4ouDuloE2v-iSJB_-Q](https://mp.weixin.qq.com/s/TqmY4ouDuloE2v-iSJB_-Q)