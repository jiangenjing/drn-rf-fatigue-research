# 控制室操作员疲劳识别｜DRN-RF 论文展示

**Integrating DRN-RF with computer vision for detection of control room operator’s mental fatigue**

PLOS ONE 20(4), e0320780 (2025) · [正式论文](https://doi.org/10.1371/journal.pone.0320780)

## 研究目标

将面部视觉特征与主观疲劳标签结合，探索操作员疲劳状态的分类方法，为工业场景中的状态监测提供研究依据。它不是医疗诊断系统，也不是已上线的安全控制产品。

## 方法结构

1. 使用 KSS 量表形成疲劳标签，整理样本。
2. 基于 Dlib 的人脸检测与 68 点关键点定位得到面部几何信息。HOG 用于检测流程，不能简单说“HOG 直接输出 68 点”。
3. 进行 3σ 异常处理与 Min-Max 归一化。
4. 结合 Monte Carlo 与 RFECV 选择特征。
5. 以 DRN 与 RF 形成两层 Stacking，并与 ANN、GBM、KNN、RF 等基线比较。

Stacking 的关键是使用折外预测训练第二层，不能把第一层对自身训练样本的拟合结果直接当作可靠验证表现。预处理与特征选择也应仅在训练折拟合；跨人泛化需要按受试者划分验证，不能只看随机帧划分的高分。

## 结果与本人贡献

论文报告最终模型准确率 **94.2%**、结果偏差 **0.004**。这是论文实验结论，不是仓库当前重跑结果；偏差不在这里擅自改写为置信区间或标准差。

Enjing Jiang 是论文第三位作者。公开 CRediT 包括 Conceptualization、Data curation、Project administration、Visualization、Writing – original draft；不据此宣称独立实现了全部模型。

## 展示页与可用材料

打开 `index.html` 可交互阅读方法流程。附带的混淆矩阵计算器仅使用明确标注的**教学示例计数**，用于理解 Precision / Recall / F1 / Accuracy，不是论文原始混淆矩阵。

目前未取得原训练源码、权重和完整环境，因此不提供伪装成原实现的摄像头识别 Demo。

找回了出版社提供的 [S1 Supporting Information](https://doi.org/10.1371/journal.pone.0320780.s001)。应先检查其中的数据结构、使用条件和被试隐私，再确定能复现哪些实验；附件存在不等于本仓库已完成下载、训练或复现。

## 后续复现验收

- 核对样本单位、受试者 ID、KSS 到类别的映射。
- 明确按受试者划分还是按样本划分，防止同人信息泄漏。
- 在每个训练折内拟合归一化、异常处理及特征选择。
- 保存折外预测、随机种子、每折指标及模型配置。
- 报告类别不均衡下的宏平均 F1、召回率及混淆矩阵，而不只报告准确率。

## 引用

Ji Z, Xie X, Jiang E, Wang Y, Min B, Yang S, et al. (2025). 上述论文. PLOS ONE 20(4): e0320780. https://doi.org/10.1371/journal.pone.0320780 。论文为开放获取；本仓库页面是方法解读，不是论文源码。
