### Nano-GraphRAG【轻装上阵】
> **轻装上阵**：像个轻装上阵的运动员，把繁复的装备都简化了，但保留了核心能力。
>

* 发表时间：2024.07.25
* Github 项目：[https://github.com/gusye1234/nano-graphrag](https://github.com/gusye1234/nano-graphrag)

#### 一、论文动机

- **背景**：微软提出的GraphRAG非常有效，但官方实现复杂，不易修改和定制。nano-graphrag是一个更简洁、易用且高度可定制的版本，保留了核心功能，同时提供了更友好的用户体验。

#### 二、论文思路

- **特点**：
  - **简洁性**：代码量仅为1100行（不包括测试和提示），是官方实现的紧凑高效替代品。
  - **易用性**：设计为轻量级、异步和完全类型化，适合希望将GraphRAG集成到项目中而不增加复杂性的开发者。
  - **可定制性**：提供了丰富的自定义选项，可以替换默认组件，如LLM函数、嵌入函数和存储组件。

#### 三、安装与使用
- **安装**：
  - 从PyPi安装：
    ```bash
    pip install nano-graphrag
    ```
  - 从源代码安装以获取最新功能：
    ```bash
    git clone https://github.com/yourusername/nano-graphrag.git
    cd nano-graphrag
    pip install -r requirements.txt
    pip install .
    ```

- **使用示例**：
  - **全局搜索**：
    ```python
    from nano_graphrag import GraphRAG, QueryParam

    graph_func = GraphRAG(working_dir="./dickens")
    with open("./book.txt") as f:
        graph_func.insert(f.read())

    # Perform global graphrag search
    print(graph_func.query("What are the top themes in this story?"))
    ```
  - **局部搜索**：
    ```python
    # Perform local graphrag search (I think is better and more scalable one)
    print(graph_func.query("What are the top themes in this story?", param=QueryParam(mode="local")))
    ```
  - **批量插入**：
    ```python
    graph_func.insert(["TEXT1", "TEXT2", ...])
    ```
  - **增量插入**：
    ```python
    with open("./book.txt") as f:
        book = f.read()
        half_len = len(book) // 2
        graph_func.insert(book[:half_len])
        graph_func.insert(book[half_len:])
    ```

#### 四、高级功能
- **自定义选项**：
  - **替换LLM函数**：可以自定义LLM函数，以使用不同的语言模型。
  - **替换嵌入函数**：可以自定义嵌入函数，以使用不同的嵌入技术。
  - **替换存储组件**：可以自定义存储组件，以使用不同的存储系统。

#### 五、结论
nano-graphrag通过其简洁性、易用性和可定制性，提供了一个高效、灵活的GraphRAG实现，适用于各种知识密集型任务和应用场景。开发团队将继续优化和扩展其功能，使其成为一个更强大的工具。

## 致谢

* 参考：[https://mp.weixin.qq.com/s/pnyhz0jA4jgLndMUM9IU1g](https://mp.weixin.qq.com/s/pnyhz0jA4jgLndMUM9IU1g)