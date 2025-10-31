# RAG
RAG(Retrieval-Augmented Generation) 检索-增强生成，是一种结合了信息检索技术与语言生成模型的人工智能技术。通过从外部知识库中检索相关信息，并将其作为Prompt输入给LLMs，以增强模型处理知识密集型任务的能力，如知识库、智能客服等。
> [RAG 工作机制详解——一个高质量知识库背后的技术全流程](https://www.bilibili.com/video/BV1JLN2z4EZQ/?spm_id_from=333.1387.homepage.video_card.click&vd_source=50f856c7eacb227ad5ea84420a6b423b)
> 

<center>
<img src="pic/RAG/RAG_before_quiz.png" width = "800">
<img src="pic/RAG/RAG_after_quiz.png" width = "800">
<br>
RAG的流程
</center>

## 向量（Embedding）

## 重排序（Reranking）

## 工具
* [PandaWiki](https://pandawiki.docs.baizhi.cloud/)  
  AI 驱动的开源知识库搭建系统，帮助你快速构建智能化产品文档、技术文档、FAQ，提供智能问答，智能搜索，智能客服等能力。
  - 智能对话（Chat）、向量（Embedding）和重排序（Rerank）模型。推荐使用deepseek-chat作为对话模型，bge-m3作为向量模型，bge-reranker-v2-m3作为重排序模型
