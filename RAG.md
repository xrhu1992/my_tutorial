# RAG
> [RAG 工作机制详解——一个高质量知识库背后的技术全流程](https://www.bilibili.com/video/BV1JLN2z4EZQ/?spm_id_from=333.1387.homepage.video_card.click&vd_source=50f856c7eacb227ad5ea84420a6b423b)  
> [BiliBili GPT中英字幕 《检索增强生成|RAG》 吴恩达 coursera课程](https://www.bilibili.com/video/BV1Zg4dzTEdm?spm_id_from=333.788.videopod.episodes&vd_source=50f856c7eacb227ad5ea84420a6b423b&p=12)  

**RAG(Retrieval-Augmented Generation) 检索-增强生成**，是一种结合了信息检索技术与语言生成模型的人工智能技术。通过**从外部知识库中检索相关信息，并将其作为Prompt输入给LLMs，以增强模型处理知识密集型任务的能力**，如知识库、智能客服等。


<center>
<img src="pic/RAG/RAG_flow.png" width = "700">
<img src="pic/RAG/RAG_before_quiz.png" width = "700">
<img src="pic/RAG/RAG_after_quiz.png" width = "700">
<br>
RAG的流程
</center>

> [!NOTE]
> 与一般的LLM的问答不同的是，RAG将输入给LLM的提示词分为**用户问题/任务 **（用户输入）和**系统提示词**（限制词和其它模型生成的提示词），二者合并输入给LLM以提高其对某一类问题的命中率，并减少LLM幻觉（一本正经胡说八道）的概率。 系统提示词可以是：
> - 模型角色
> - 运行规则
> - 环境信息
> - 其它 ... 

> [!WARNING]
> **与Agent的区别**  
> Agent是使用LLM思考和推理（相当于大脑），再根据LLM思考的结果去调用相应的工具（相当于手脚）执行特定的任务。 

## 1. 检索器（Retriever）

### 1.1 关键词检索（Keyword Search）
关键词匹配的速度快，比较适合在线搜索（比如搜索Internet），但可能会漏掉语义相近的关键词（例如happy和glad），且多义词（例如python既可以表示编程语言，又可以表示蛇）也会干扰搜索，导致检索范围受限或不准确。常用的关键词检索算法有：
  * TF-IDF(Term Frequency-Inverse Document Frequency, 词频-逆文件频率)
  * BM25(Best Matching 25) 

### 1.2 语义检索（Semantic Search）
语义搜索需要大量计算资源，一般会预先将搜索内容片段化（Chunking）和向量化（Embedding），并存储到向量数据库（Vector Database），以加快搜索速度降低延迟。语义检索也可能会检索到其它领域不相关内容，导致检索范围过大。
* 知识库Chunking，得到片段（Chunk），Chunking可以按段落、字数、页数、文章等方式
* 将Chunk向量化，以便于查找与用户问题Chunk相关的知识库Chunk
* 使用Embedding模型把Chunk向量化后，存入Vector Database（存储了向量和对应的Chunk原文）
* 相似度计算：欧式距离、余玄角度、点积（考虑距离和角度的结合）

> [!NOTE]
> **评估指标**
> - Accuracy 准确率（正确率）
> ```math 
> Accuracy=\frac{所有预测正确的样本}{总样本}=\frac{TP+TN}{TP+FN+FP+TN}
> ```
> - Precision 精确率（查准率）
> ```math 
> Precision=\frac{将正类的预测为正类}{预测的正类}=\frac{TP}{TP+FP}
> ```
> - Recall 召回率（查全率）
> ```math 
> Recall=\frac{将正类的预测为正类}{原本的正类}=\frac{TP}{TP+FN}
> ```
> - AP(Average Precision) 平均精度  
>   AP 是在不同的召回率阈值下计算的精度的平均值。通过绘制 Precision-Recall（P-R）曲线，计算出 P-R 曲线下的面积作为 AP 的值。简单来说，AP 是对模型在某一类别下的检测能力的衡量。AP 值越高，表示模型在不同召回率下的精度表现越好。
> - mAP(Mean Average Precision) 平均精度均值  
>   mAP 是在多个类别上的 AP 的平均值，用于衡量模型在整个数据集上的检测性能
>   ```math
>   mAP=\frac{1}{N}\sum^{N}_{i=1}AP_i
>   ```
>  ---
> - **例如**：假设共有100个Chunk，其中10个与Prompt是相关的，Retriever检索到12个结果，其中有8个是相关的（剩下4个不相关）  
>   **召回率（是否有遗漏）** $Recall = \frac{8}{10}$  
>   **精确率（是否正确）** $Precision = \frac{8}{12}$
> ---

> [!WARNING]
> 词向量的分割和选取有一定的碎片化，这会导致上下文语义的缺失（只有局部信息，缺乏全局和关联信息）

### 1.3 混合检索（Hybrid Search）
关键词检索和语义检索的结合
<center>
<img src="pic/RAG/retriever_1.png" width="800">
<br>混合检索
</center>

## 2. 向量数据库（Vector Database）
### 2.1 向量搜索（Vector Retrieval）


## 3. 重排序（Reranking）
Retrivever检索速度快，一般能保证较高的召回率，但是准确率较低，将Retriever检索的Chunk再经过Reranking Model处理后，可以进一步排除不相关Chunk，提高精确率。



## 工具
* [PandaWiki](https://pandawiki.docs.baizhi.cloud/)  
  AI 驱动的开源知识库搭建系统，帮助你快速构建智能化产品文档、技术文档、FAQ，提供智能问答，智能搜索，智能客服等能力。
  - 智能对话（Chat）、向量（Embedding）和重排序（Rerank）模型。推荐使用deepseek-chat作为对话模型，bge-m3作为向量模型，bge-reranker-v2-m3作为重排序模型

