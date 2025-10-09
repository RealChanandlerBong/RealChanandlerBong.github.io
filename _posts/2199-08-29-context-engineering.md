---
title: '关于Context Engineering的一点思考'
date: 2199-08-29
permalink: /posts/2025/08/context-engineering
tags:
  - think
  - category1
---

大模型时代，概念、范式层出不穷。先有Prompt Engineering、RAG(Retrieval Augment Generation)，后有Context Engineering，其本质都是对模型上下文的管理。这种管理方法论更偏工程导向，通过精心设计维护一个必要的上下文窗口，使大模型具备所需的上下文输入，优化其在垂直领域的表现。

上下文可根据长中短期来分类管理。以多轮对话为例：

- **短期**：对话记录。当对话条数变多时，可参考LangGraph定义Reducer函数的做法，进行过滤保留（如保留最新的5条记录）。

- **中期**：可以是总结摘要、事实提取等形式。其中后者是指，将对话内容进行事实性的提取、陈述。随着对话轮数增多，可定义摘要的存储范式与更新频率。以下是一个简单的示例。

    摘要更新操作（大模型输出）
    ```json
    [
        {
            "type": "CREATE",
            "content": "呆老师喜欢在上路打架"
        },
        {
            "type": "EDIT",
            "id": "some-id-0",
            "content": "呆老师在9月离开了美团",
        }
    ]
    ```

    已有摘要：
    ```json
    [
        {
            "id": "some-id-0",
            "content": "呆老师23年入职美团",
            "status": "CREATED"
        }
    ]
    ```
    更新后：
    ```json
    [
        {
            "id": "some-id-0",
            "content": "呆老师在23年入职美团，并在25年9月离开",
            "history": ["呆老师23年入职美团", "呆老师在9月离开了美团"],
            "status": "UPDATED"
        },
        {
            "id": "some-id-1",
            "content": "呆老师喜欢在上路打架",
            "status": "CREATED"
        }
    ]
    ```

- **长期**：持久化、可召回。如向量存储、数据库存储。目的是为了刻画用户画像，以及存储更长期的记忆。


