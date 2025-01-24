### VisRAG【火眼金睛】
> **火眼金睛**：终于悟出文字不过是图像的一种特殊表现形式。像个开了天眼的阅读者，不再执着于逐字解析，而是直接"看"透全局。用照相机代替了OCR，懂得了"一图胜千言"的精髓。
>

* 发表时间：2024.10.14
* 论文名称：[VisRAG: Vision-based Retrieval-augmented Generation on Multi-modality Documents](https://arxiv.org/abs/2410.10594)
* 论文地址：[https://arxiv.org/abs/2410.10594](https://arxiv.org/abs/2410.10594)
* Github 地址：[https://github.com/openbmb/visrag](https://github.com/openbmb/visrag)

#### 一、论文动机

传统的RAG系统（TextRAG）主要依赖文本信息进行检索和生成，**但在处理多模态文档时，会因为解析过程（如OCR、布局识别等）引入错误，导致信息损失和性能下降**。

VisRAG旨在通过直接将文档作为图像嵌入并检索，避免解析过程中的信息损失，更全面地保留原始文档信息。

#### 二、论文思路

![](20241014_VisRAG/img/v2-76eba47553bbfd94f571efe9041b581e_1440w.png)

- VisRAG由两部分组成：
  - **VisRAG-Ret（检索阶段）**：使用视觉语言模型（VLM）将查询和文档图像映射到嵌入空间，通过位置加权平均池化处理VLM的最后一层隐藏状态，从而实现文档页面的检索。
  - **VisRAG-Gen（生成阶段）**：利用检索到的页面生成答案。由于多模态大模型通常只能处理单张图片，VisRAG提出了两种方案：页面合并（将检索到的页面水平合并为一张图片）和加权筛选（为每个页面生成答案并选择置信度最高的答案）。

#### 三、实验设计与结果

- 检索性能：
  - VisRAG-Ret在跨领域数据上显著超越了现有基线模型，包括文本和视觉模型。
  - 在跨领域环境中，VisRAG-Ret相比传统文本模型和视觉模型分别实现了15%和22%的性能提升。
  - VisRAG-Ret在内存效率上也优于其他模型，适合扩展到大规模文档集合。
- 生成性能：
  - VisRAG-Gen在处理真实文档图像时，显著优于仅依赖提取文本的TextRAG-Gen。
  - 在实际应用场景中，VisRAG-Gen在处理检索到的文档时持续超越TextRAG-Gen，尤其是在加权筛选方法下表现更优。
- 整体性能：
  - 在六个评估数据集中，VisRAG平均实现了39%的准确率提升。
  - 在InfographicsVQA数据集上，VisRAG的整体准确率从22.1%提升至42.7%，显示出其在多模态文档处理中的强大能力。

#### 四、论文总结

VisRAG通过直接利用文档图像进行检索和生成，有效避免了传统RAG系统中解析过程带来的信息损失，显著提升了检索和生成的性能。该系统不仅在训练数据上表现出色，还展现出强大的泛化能力，成为多模态文档RAG的理想选择。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/WB23pwJD-JV95ZlpB3bUew](https://mp.weixin.qq.com/s/WB23pwJD-JV95ZlpB3bUew)