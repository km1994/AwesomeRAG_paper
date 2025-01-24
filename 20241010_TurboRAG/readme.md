### TurboRAG【速记高手】
> **速记高手**：提前把功课做好，把答案都记在小本本里。像个考前突击的学霸，不是临场抱佛脚，而是把常考题提前整理成错题本。需要的时候直接翻出来用，省得每次都要现场推导一遍。
>

* 发表时间：2024.10.10
* 论文名称：[TurboRAG: Accelerating Retrieval-Augmented Generation with Precomputed KV Caches for Chunked Text](https://arxiv.org/abs/2410.07590)
* 论文地址：[https://arxiv.org/abs/2410.07590](https://arxiv.org/abs/2410.07590)
* Github 地址：[https://github.com/MooreThreads/TurboRAG](https://github.com/MooreThreads/TurboRAG)

#### 一、论文动机

检索增强生成（RAG）系统通过从文档集合中检索相关信息并结合生成模型来生成响应，但面临的主要问题是首次令牌时间（TTFT）的高延迟。这种延迟主要由以下因素导致：

- 处理和连接多个检索到的文档块需要大量计算。
- 检索到的文档的键值（KV）缓存的重复计算。

#### 二、论文思路

为了解决上述问题，Moore Threads AI的研究人员提出了 TurboRAG 方法。TurboRAG通过以下机制优化RAG系统的推理过程：

- 离线预计算KV缓存：计算并存储文档块的KV缓存，减少在线推理阶段的计算量。
- 在线检索预填充：
  - 检索预先计算的KV缓存，并将其与用户查询结合生成响应。
  - 使用独立的注意力掩码，防止跨文档的不必要注意力。
  - 采用相对位置嵌入，保持文档中位置关系的完整性。

这种方法显著减少了计算开销，加快了响应时间，同时保持了生成结果的准确性。

#### 三、实验设计与结果

实验表明，TurboRAG在降低TTFT方面表现出色：

- **延迟降低**：与传统RAG系统相比，TurboRAG的TTFT降低了高达9.4倍，平均加速为8.6倍。
- **准确性保持**：在多个基准测试中，TurboRAG的准确性与传统RAG方法相当。
- **计算资源优化**：KV缓存计算成本降低了98%以上，支持更大的批处理大小和更高的吞吐量。
- **微调实验**：即使在嘈杂的检索环境中，TurboRAG也能保持模型的准确性。

#### 四、论文总结

TurboRAG通过将KV缓存生成与在线推理过程分离，解决了RAG系统固有的延迟问题。它通过利用预先计算的KV缓存和调整注意力机制，在保持准确性的同时显著提高了响应速度和效率。这些改进使TurboRAG成为延迟敏感型应用中部署RAG的有力选择，有望扩大RAG在实时和大规模场景中的应用范围。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/lanZ8cIEnIt12tFt4d-xzw](https://mp.weixin.qq.com/s/lanZ8cIEnIt12tFt4d-xzw)
