
# 🧪 A/B测试与营销效果评估

[![Python](https://img.shields.io/badge/Python-3.10-blue)](https://www.python.org/)
[![Statsmodels](https://img.shields.io/badge/Statsmodels-0.14+-green)](https://www.statsmodels.org/)
[![Scipy](https://img.shields.io/badge/Scipy-1.11+-blue)](https://scipy.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> 对约29万用户执行的Landing Page A/B测试进行全流程统计推断，通过实验质量检查→假设检验→效应量→功效分析四步，得出"新页面未显著提升转化率"的严谨结论。

## 📊 项目概览

扮演公司数据科学家，对新旧两版Landing Page的A/B测试结果做**完整的统计推断**。不满足于"跑个t检验"，而是从实验执行质量检查开始，到假设检验、置信区间、效应量、功效分析，最后给出是否上线的决策建议——展示数据驱动决策的全闭环。

## ❓ 回答的核心问题

| 序号 | 分析步骤 | 回答的问题 |
|------|----------|-----------|
| 1 | 实验质量检查 | 实验执行是否有污染？随机分配是否均匀？ |
| 2 | 转化率对比 | 新旧页面转化率差多少？ |
| 3 | 假设检验 | 差异是真实的还是随机波动？ |
| 4 | 置信区间 | 真实效应可能在什么范围？ |
| 5 | 效应量分析 | 即使显著，有实际商业价值吗？ |
| 6 | 功效分析 | 样本量够不够？如果真有提升能检测到吗？ |
| 7 | 深层分析 | 效应在不同时间/用户群中一致吗？ |

## 🔍 核心发现

1. **实验存在1.3%的执行污染**：约3,900条记录的分组与实际看到页面不一致，需清洗
2. **两组转化率几乎一致**：Control 12.04% vs Treatment 12.06%，差异仅0.02个百分点
3. **z检验不显著**：p-value > 0.05，无法拒绝"新页面没有提升"的零假设
4. **95%置信区间包含0**：差异的95% CI为[-0.15%, +0.19%]，真实效应可能为正、为负或为零
5. **效应量极小**：Cohen's h < 0.01，属于"微小"级别——即使显著也无商业价值
6. **统计功效>99.9%**：样本量足够大，如果真有改进我们早该检测到了

## 🛠 技术栈

- **数据清洗**: Pandas, NumPy
- **统计检验**: Scipy, Statsmodels (proportions_ztest, proportion_confint, NormalIndPower)
- **效应量**: Cohen's h（自实现）
- **可视化**: Matplotlib, Seaborn

## 📁 项目结构
ab-test-marketing-evaluation/
├── README.md
├── requirements.txt
├── data/
│ └── ab_data.csv
├── notebooks/
│ └── ab_test_analysis.ipynb # 完整分析过程
├── images/
│ ├── randomization_check.png
│ ├── conversion_comparison.png
│ ├── confidence_intervals.png
│ ├── daily_conversion_trend.png
│ └── cohort_analysis.png
└── report/
└── AB测试与营销效果评估报告.md


## 🚀 快速复现

```bash
# 1. 克隆仓库
git clone https://github.com/Wanyiyi1991/ab-test-marketing-evaluation
cd ab-test-marketing-evaluation

# 2. 安装依赖
pip install -r requirements.txt

# 3. 下载数据
# 从 Kaggle 搜索 "A/B Testing Dataset" 下载 ab_data.csv
# 放入 data/ 文件夹

# 4. 启动 Jupyter
jupyter notebook notebooks/ab_test_analysis.ipynb

关键可视化
统计推断可视化——置信区间
[https://images/confidence_intervals.png](https://github.com/Wanyiyi1991/ab-test-marketing-evaluation/blob/main/images/confidence_intervals.png)

左：两组转化率的95%置信区间高度重叠。右：差异的置信区间包含0——无法排除"新页面反而更差"的可能性。

实验质量检查——每日分组比例
[https://images/randomization_check.png](https://github.com/Wanyiyi1991/ab-test-marketing-evaluation/blob/main/images/randomization_check.png)

每日实验组比例稳定在50%±0.5%，证明随机化执行良好。如果随机化失败，后续所有分析都不可信。

💡 决策建议
最终建议：不建议上线新Landing Page
维度      	结果	             解读
观察到的差异	+0.02百分点	    微不足道
p-value	    >0.05	        无法拒绝H₀
95% CI	 [-0.15%, +0.19%]	包含0
效应量(Cohen's h) <0.01	    微小
统计功效	>    99.9%	        样本充足

理由：
统计上无显著差异
置信区间包含0，无法排除新页面"更差"
效应量极小，无商业价值
上线需要工程成本，预期收益≈0
如果有真实改进，近29万的样本量早就检测到了
下一步方向：尝试多变量测试(A/B/n)，或关注长期指标（7日留存、复购率）。

👤 关于我
[一个数据分析探索者、爱好者！
QQ：783899056
Email：wanyiyi1991@gmail.com]

⭐ 如果这个项目对你有帮助，欢迎给个Star！
