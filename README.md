# Credit Risk Analysis – 信贷违约风险分析

## 项目简介
本项目基于 Kaggle 的 **Credit Risk Dataset**（约 3.2 万条信贷记录），使用 **MySQL** 进行数据存储与查询，利用 **Python (pandas, matplotlib, seaborn, scikit-learn)** 完成数据分析与建模。主要工作包括：

- **单变量风险分析**：探索住房类型、贷款等级、债务收入比等特征与违约率的关系。展示了不同住房类型（租房、自有、按揭）的违约率，发现 **租房群体违约率最高**。
- **债务收入比（DTI）分箱**：将 DTI 分为四档，结果显示 **DTI ≥ 0.6 的群体违约率高达 85.5%**，表明高负债是极强的风险预警信号。
- **组合规则挖掘**：定义“租房 + 低贷款等级（D~G）+ 历史违约记录”的高风险客群，其违约率 **75.07%**，远高于整体违约率 21.82%，可直接用于自动拒绝策略。
- **双变量交互分析**：通过热力图展示 **收入 × DTI** 对违约率的交互影响，发现 **低收入 + 高负债** 人群违约率超过 85%，而高收入 + 低负债人群违约率低于 10%，证实了收入和负债的协同效应。
- **逻辑回归建模**：使用 8 个数值特征和 3 个分类特征，构建违约预测模型，**AUC 达到 0.8624**，准确率 86.36%。特征重要性分析显示：
  - **贷款等级 G、F、E、D** 的系数均为较大的正值，其中 `loan_grade_G` 系数高达 **+4.74**，是最强的违约驱动因素。
  - **自有房（OWN）** 的系数为 **-1.68**，是显著的保护因素。
  - `loan_percent_income`（贷款/收入比）系数为正，说明相对负债水平越高，风险越大。

## 数据集
- 来源：[Kaggle Credit Risk Dataset](https://www.kaggle.com/datasets/alexdister/credit-risk-dataset)
- 记录数：约 3.2 万条，29 个特征
- 目标变量：`loan_status`（1=违约，0=正常）

## 技术栈
- MySQL（数据存储与查询）
- Python（pandas, matplotlib, seaborn, scikit-learn）
- Jupyter Notebook

## 分析结果摘要
- 整体违约率：21.82%
- 高负债（DTI ≥ 0.6）违约率：85.5%
- 组合规则（租房 + 低等级 D~G + 历史违约）违约率：**75.07%**
- 逻辑回归模型 AUC = **0.8624**，准确率 86.36%
- 最重要的风险特征：`loan_grade_G`（+4.74），`loan_grade_F`（+3.41），自有房（-1.68）

## 图表展示
![住房类型违约率](images/default_rate_by_home_ownership.png)
![债务收入比违约率](images/default_rate_by_dti.png)
![收入与债务比热力图](images/heatmap_income_dti.png)
![Top10重要特征](images/top10_features.png)
![混淆矩阵](images/confusion_matrix.png)

## 项目结构
```text
credit-risk-analysis/
├── credit_risk_analysis.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── images/
    ├── default_rate_by_home_ownership.png
    ├── default_rate_by_dti.png
    ├── heatmap_income_dti.png
    ├── top10_features.png
    └── confusion_matrix.png
```

## 作者
GitHub: syfzln(https://github.com/sifzln/credit-risk-analysis)

## 许可证
本项目仅用于学习，数据集遵循 CC0 公共领域许可。
