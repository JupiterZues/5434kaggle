# GROUP10 · COMP5434 项目作品集

## 项目概览

本项目完成两个 Kaggle 机器学习任务：

| 任务 | 任务类型 | 最终 Public 成绩 |
|---|---|---:|
| Task 1 | 四类天气分类 / Macro-F1 | **0.92488** |
| Task 2 | Amazon 评论评分预测 / RMSE | **0.46326** |

## 技术栈

- Task 1：StratifiedKFold、OOF、nested selection、LightGBM/CatBoost/XGBoost/RandomForest/ExtraTrees、FT-Transformer、TabICLv2、TabM、RealMLP-TD、TabPFN-3.5、specialist/OVR、class quota、closed-cycle calibration。
- Task 2：Amazon Reviews 2023 source matching、clean-label 修复、Apache Spark 分布式关系特征、DeBERTa-v3-large、BF16、gradient checkpointing、Ridge/LightGBM/CatBoost/XGBoost side stack、nested six-stream simplex blend、exact-star bounded postprocessing。
- 工程方法：固定 fold、OOF-safe validation、cross-fitting、防泄漏、提交格式与 SHA-256 校验、可复现命令。

## 我负责的技术重点

Task 2 技术链路：clean labels → Spark relational features → DeBERTa-v3-large → cross-fitted side stack → six-stream nested blend → exact-star postprocessing。

## 关键发现

- Task 1 的 Public Macro-F1 0.92488 是旧的 top-10 boundary 0.92456 之上的结果；最终改动是保持 825/825/825/825 的四行闭环。
- Task 2 原始训练标签只有约 80% 与匹配 source rating 一致，source-label RMSE 约 1.155；标签修复比单纯增大模型更关键。
- Task 2 测试 source rating 不进入训练、特征或权重选择；测试侧 source matching 只用于商品 ID join，source proxy 仅用于事后诊断。

## 风险说明

Task 1 的 public/private 差异和 Task 2 的外部数据政策是主要风险。外部 Amazon Reviews 2023 数据的使用方式需要在课程规则下向老师/TA确认；本作品集不把外部数据或模型 checkpoint 重新分发。Task 2 的 Spark、DeBERTa 训练和 transformer 推理时间是局部阶段时间，不构成统一总离线时间。

## 文件说明

- `documents/`：两份报告、两份 PPT、技术手册、全项目技术总结和演讲稿。
- `diagrams/`：总体架构和两条任务技术路线图。
- `evidence/`：最终指标和两个任务的 final submission。
- `code/GROUP10_DELIVERY.zip`：不包含报告/PPT的代码交付包。

## English summary

This is the GROUP10 portfolio for COMP5434. It demonstrates two end-to-end Kaggle workflows: a balanced tabular classification system (Task 1, Public Macro-F1 0.92488) and a review rating regression system (Task 2, Public RMSE 0.46326). The main engineering themes are leakage-safe OOF validation, nested ensembling, source-label repair, Spark relational features, DeBERTa-v3-large, cross-fitted side stacking and reproducible submission auditing.
