# 论文CCL-2025 “目标自适应的可解释立场检测：新任务及大模型实验”的中文立场检测数据集与大模型实验结果

## 数据集描述

### 事件主题
数据集包含五个热点事件的评论文本：
1. **巴以冲突**
2. **央视记者采访燕郊爆炸被驱离**
3. **胡锡进谈虐猫事件**
4. **新闻学教授怒骂张雪峰**
5. **姜萍数学竞赛违规事件**

### 数据规模与划分
- 总数据量：**10,513条**
- 训练集：**8,386条**（占比80%）
- 测试集：**2,127条**（占比20%）
- 划分训练集、测试集原则：
  - 每个主题按 **8:2** 比例划分
  - 立场保证 **1:1** 均衡

### 数据结构
每条数据包含以下字段：
| 字段名 | 说明 |
|--------|------|
| `topic` | 事件主题 |
| `background` | 事件背景 |
| `content` | 评论文本 |
| `target` | 立场目标 |
| `opinion` | 观点 |
| `stance` | 立场标签（支持/反对/中立） |

### 数据文件
- 训练集：`train.xlsx`
- 测试集：`test.xlsx`

---

## 实验模型
评测涵盖以下10个大语言模型：
1. **GPT-4o** 
2. **GPT-3.5 Turbo** 
3. **DeepSeek-R1** 
4. **DeepSeek-V3** 
5. **Qwen2.5-72B-Instruct** 
6. **Qwen2.5-32B-Instruct** 
7. **Qwen2.5-7B-Instruct** 
8. **Gemini-1.5-Pro** 
9. **GLM-4-32B** 
10. **GLM-4-9B** 

---

## 实验结果
### 模型输出
每个模型对测试集生成以下预测结果：
- `predict_target`：预测的目标
- `predict_opinion`：预测的观点
- `predict_stance`：预测的立场标签

### 评估指标
包含各模型在测试集上每条数据的完整评估指标得分，包括：
- 目标识别的完全匹配率EM值、N-gram相似度BLEU值、深度语义相似度BERTScore、大模型评分和综合得分（target_em、target_bleu、target_bertscore、target_llm_score、target_score）
- 观点生成的N-gram相似度BLEU值、深度语义相似度BERTSCORE、大模型评分和综合得分（opinion_bleu、opinion_bertscore、opinion_llm_score、opinion_score）
- 立场是否正确（is_stance_correct）
