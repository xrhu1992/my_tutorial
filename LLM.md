
# 大模型基础(Foundation of Large Language Models)

> 参考资源: 
> [大模型基础-毛玉仁](doc/大模型基础%20完整版.pdf)
> [Hands-On-Large-Language-Models](doc/图解大模型生成式AI原理与实战%20([沙特]%20杰伊·阿拉马尔(Jay%20Alammar)%20etc.)%20(Z-Library).pdf)

## 1. 自然语言处理(Natural Language Processing, NLP)
### 1.1 自然语言处理常见任务
<p align="center">
<img src="https://ai-studio-static-online.cdn.bcebos.com/fc24714f601549068c2aa9255555f50aa706398d42eb47528590026d25df621b" height="250">
<br>自然语言处理常见任务<br>
</p>

### 1.2 词向量(Word Embedding)
* 如何把词转换成向量
  <p align="center">
  <img src="https://ai-studio-static-online.cdn.bcebos.com/2145ed77e5b24e0b9b33a7c8451b52cdc68f38b651494b51afdd264724392fe3" height="200">
  <br>张量计算示意图<br>
  </p>





## 2. 语言模型基础
* **分词（tokenization）**：将句子拆分成单个词或子词（词元，token）
* **词汇表（vocabulary）**：所有可能的词元集合（不重复）
* token: 词元，不可再拆分的最小语义单位
* LM (Language Model): 语言模型，预测下一个 token 的概率分布，语言模型的概率预测与<mark>上下文</mark>和<mark>语料库</mark>息息相关

* 条件概率链式法则  
  假设词元序列为 $( w_1, w_2, ..., w_n )$ ，则该序列的联合概率可以表示为：
  ```math 
  P(w_1, w_2, ..., w_n) = P(w_1)P(w_2|w_1)P(w_3|w_1,w_2)...P(w_n|w_1,w_2,...,w_{n-1})
  ```

* n-阶马尔可夫假设  
  为了简化条件概率的计算，假设当前词元只与前面n个词元相关
  ```math
  P(w_n|w_1,w_2,...,w_{n-1}) \approx P(w_n|w_{n-n},w_{n-(n-1)},...,w_{n-1})
  ```

* N-gram 模型
  - 通过假设当前词元只与前面 $N-1$ 个词元相关，简化条件概率的计算
  - 例如，二元模型 (Bigram) 假设 $P(w_n|w_1,w_2,...,w_{n-1}) \approx P(w_n|w_{n-1})$ ，则联合概率可表示为：
  ```math
  P(w_1, w_2, ..., w_n) \approx P(w_1)P(w_2|w_1)P(w_3|w_2)...P(w_n|w_{n-1})
  ``` 

## 3. Prompt工程（Prompt Engineering）
### 3.1 prompt的基本元素
* **任务说明**：向模型明确提出具体的任务要求
* **问题**：向模型具体描述需要解决的问题或任务
* **上下文**：向模型提供相关的背景信息、先验知识或约束条件，帮助模型更好地理解任务和生成符合要求的输出
* **输出格式**：期望模型给出回答的展现形式，如JSON格式 

### 3.2 上下文学习（In-Context Learning, ICL）
* **上下文学习**：通过在prompt中提供示例或指导，帮助模型理解任务要求和生成更准确的输出 
  -  零样本学习（Zero-Shot Learning）：模型在没有任何示例的情况下，根据任务说明和问题生成输出
  - 少样本学习（Few-Shot Learning）：在prompt中提供少量示例，帮助模型理解任务要求和生成更准确的输出，性能更好
* **示例选择的主要依据**：
  - 相似性：选择与当前任务或问题相似的示例
  - 多样性：选择涵盖不同方面或变体的示例，以提高模型的泛化能力

### 3.3 思维链（Chain-of-Thought, CoT）
* **思维链**：通过在提示词中<mark>嵌入一系列中间推理步骤</mark>，引导模型逐步解决复杂任务，提升模型处理System2类型问题的能力
  - 逐步推理：引导模型分解复杂任务为多个简单步骤，逐步解决问题
  - 自我反思：鼓励模型在生成输出前进行自我检查和评估，确保输出的准确性和合理性
  - 多样化思维链：提供多种不同的思维链示例，帮助模型学习不同的推理路径和策略
* **Zero-Shot CoT**：通过在prompt中添加类似“让我们一步一步来思考(Let's think step by step)”这样的指令，促使模型生成中间推理步骤，从而提升其解决复杂任务的能力。(会消耗更多的计算资源)
*  **Auto-CoT**：自动生成思维链示例，减少人工设计提示词的工作量
  - 使用预训练模型生成高质量的思维链示例
  - 选择具有代表性的示例，以覆盖不同类型的任务和问题

### 3.4 提示词调优（Prompt Tuning）



## 4. 应用案例
### 4.1 果蔬采摘机器人
通过输入果蔬的RGB和深度图，利用VLM技术完成多模态语义感知与跨模态推理，精准输出目标果蔬类型、遮挡状态、最佳操作区域等关键信息；具身决策模块则基于这些信息完成任务规划与手臂动作分配，最终实现精准执行。
<p align="center">
<img src="https://mmbiz.qpic.cn/sz_mmbiz_png/baIibQrtYGWRrYCRHNCzq2jq946rnYOXWPfYApc1ib1BlO1FphXp54hpeGOibBGR3I91ibrMGO2Ws517AKbX54ViawA/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=6" width="600">
<img src="https://mmbiz.qpic.cn/sz_mmbiz_png/baIibQrtYGWRrYCRHNCzq2jq946rnYOXW2XexEdiaYFwymTcaUILJucTsJ9RUsSibKWLgcKuRwib3tcC1AbH2sDxibg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=7" width="600">
<br>集萃智造采摘机器人<br>
</p>