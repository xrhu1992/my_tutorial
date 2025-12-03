# AI服务商调研

> [!TIP]
> 搭建RAG服务，单次对话需要使用上百token 

## 腾讯云
> [腾讯云AI产品](https://cloud.tencent.com/act/pro/midyear1111-ai-2025?from=29020&Is=home)
* **大模型**  
  |云服务项目|单位|价格|首单价|有效期|
  |---------|----|---|------|-----|
  |图像风格化（图生图）|千次|90|29.9|三个月|
  |混元生图（文字生图）|千次|400|49|三个月|
  |模特换装|千次|400|99|三个月|
  |AI写真|千次|260|99|三个月|
  |DeepSeek-R1|千万token|380|152|无|
  |知识库容量扩容包（LLM+RAG）|千万次|720|1800|一年|
* **语音**  
  |云服务项目|单位|价格|首单价|有效期|
  |---------|----|---|------|-----|
  |语音识别(实时/异步)|30小时|90|14.9|一个月|
  |一句话识别|30千次|90|14.9|一个月|
  |语音合成|60万字符|30|14.9|一个月|

## Claude
> [Claude API Pricing](https://claude.com/pricing#api)
<center>
<img src="https://raysees-1384742255.cos.ap-shanghai.myqcloud.com/AI/claude_api_pricing.png" width = "900">
</center>

## Gemini


## RAG
### [PandaWiki](https://pandawiki.docs.baizhi.cloud/)  
  AI 驱动的开源知识库搭建系统，帮助你快速构建智能化产品文档、技术文档、FAQ，提供智能问答，智能搜索，智能客服等能力。
  - 智能对话（Chat）、向量（Embedding）和重排序（Rerank）模型。推荐使用deepseek-chat作为对话模型，bge-m3作为向量模型，bge-reranker-v2-m3作为重排序模型
