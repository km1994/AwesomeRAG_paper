### GraphRAG-Local-UI【改装师】
> **改装师**：把跑车改装成适合本地道路的实用车，加装了友好的仪表盘，让人人都能轻松驾驶。
>

* 发表时间：2024.07.14
* Github 项目：[https://github.com/severian42/GraphRAG-Local-UI](https://github.com/severian42/GraphRAG-Local-UI)

#### 一、论文动机

GraphRAG-Local-UI的工具，它是基于Microsoft的GraphRAG的本地化实现，提供了一个丰富的交互式用户界面生态系统。

#### 二、论文思路

![](20240714_GraphRAG-Local-UI/img/v2-5fb9eeead8d4b48f1dd358f869a9f49c_1440w.png)

- **功能亮点**：
  - **核心架构**：采用FastAPI构建的高效服务器（`api.py`），作为整个GraphRAG操作的大脑。
  - **索引与提示界面**：一个专为索引管理和提示调整设计的界面（`index_app.py`），基于Gradio，操作简便。
  - **本地模型集成**：支持本地大型语言模型（LM）和嵌入技术，与Ollama及OpenAI的API完美兼容。
  - **成本优化**：通过部署本地模型，摆脱对昂贵云服务模型的依赖，实现成本控制。
  - **用户交互体验**：设计友好的界面，简化数据管理、查询执行和结果可视化流程（主应用程序）。
  - **动态数据可视化**：利用Plotly技术，在二维或三维空间中动态展示您的知识图谱（主应用程序）。
  - **文件操作**：直接通过界面进行文件的上传、浏览、编辑和删除。
  - **设置定制**：通过用户界面轻松调整和管理GraphRAG配置。
  - **输出导航**：方便地浏览和检查索引结果和相关工件。
  - **日志跟踪**：实时记录日志，优化调试和监控过程。
  - **查询灵活性**：支持全局、局部和直接聊天查询，且可自定义参数（主应用程序）。
  - **可视化定制**：根据个人喜好调整图表布局、节点大小和颜色（主应用程序）。

- 功能详解

1. **核心架构**：
   - **FastAPI服务器**：作为整个GraphRAG操作的大脑，提供高效的API接口。

2. **索引与提示界面**：
   - **Gradio界面**：专为索引管理和提示调整设计，操作简便，用户可以轻松管理索引和调整提示。

3. **本地模型集成**：
   - **兼容性**：支持本地大型语言模型（LM）和嵌入技术，与Ollama及OpenAI的API完美兼容，减少对云服务的依赖。

4. **成本优化**：
   - **本地部署**：通过部署本地模型，实现成本控制，减少对昂贵云服务的依赖。

5. **用户交互体验**：
   - **友好界面**：设计友好的界面，简化数据管理、查询执行和结果可视化流程。

6. **动态数据可视化**：
   - **Plotly技术**：利用Plotly技术，在二维或三维空间中动态展示知识图谱。

7. **文件操作**：
   - **文件管理**：直接通过界面进行文件的上传、浏览、编辑和删除。

8. **设置定制**：
   - **配置管理**：通过用户界面轻松调整和管理GraphRAG配置。

9. **输出导航**：
   - **结果检查**：方便地浏览和检查索引结果和相关工件。

10. **日志跟踪**：
    - **实时记录**：实时记录日志，优化调试和监控过程。

11. **查询灵活性**：
    - **多种查询**：支持全局、局部和直接聊天查询，且可自定义参数。

12. **可视化定制**：
    - **个性化调整**：根据个人喜好调整图表布局、节点大小和颜色。

#### 三、论文总结

GraphRAG-Local-UI通过其丰富的交互式用户界面和本地模型集成，提供了一个高效、成本优化且用户友好的GraphRAG实现。开发团队正在不断改进和扩展其功能，使其成为一个更强大的工具，适用于各种知识密集型任务和应用场景.


## 致谢

* 参考：[https://mp.weixin.qq.com/s/DLvF7YpU3IfWvnu9ZyiBIA](https://mp.weixin.qq.com/s/DLvF7YpU3IfWvnu9ZyiBIA)