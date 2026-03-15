# Financial Modeling Standards (财务建模标准) V1.0

> 本文档定义了在财务建模过程中必须遵循的勾稽关系 (Linkages)、逻辑检查 (Checks) 和计算规范。

---

## 1. 三张表勾稽逻辑 (3-Statement Linkages)

在构建 3-Statement 模型时，必须确保以下联动逻辑准确无误：

### 1.1 损益表 (IS) -> 现金流量表 (CFS)
*   **Net Income (净利润)**：从损益表底部链接到现金流量表顶部（间接法起点）。
*   **D&A (折旧与摊销)**：在现金流量表中作为非现金支出加回 (Add back)。

### 1.2 现金流量表 (CFS) -> 资产负债表 (BS)
*   **Δ Cash (现金变动额)**：期末现金 = 期初现金 + 经营活动净额 + 投资活动净额 + 筹资活动净额。
*   **Closing Cash (期末现金)**：链接回资产负债表中的“货币资金 (Cash & Cash Equivalents)”。

### 1.3 损益表 (IS) -> 资产负债表 (BS)
*   **Retained Earnings (留存收益)**：期末留存收益 = 期初留存收益 + 本期净利润 - 本期分红。

---

## 2. 估值模型核心逻辑 (Valuation Logic)

### 2.1 DCF (现金流折现) 标准
1.  **预测期 (Projection Period)**：通常为 5-10 年。
2.  **Unlevered FCF** = EBIT * (1 - Tax Rate) + D&A - CapEx - ΔNWC。
3.  **WACC 计算**：
    *   Cost of Equity (Ke) = Rf + Beta * (Rm - Rf) + Size Premium。
    *   WACC = [E/(D+E) * Ke] + [D/(D+E) * Kd * (1 - Tax Rate)]。
4.  **敏感度测试 (Sensitivity Analysis)**：必须测试关键变量对企业价值的影响，如 WACC 和 永续增长率 (g)。

### 2.2 LBO (杠杆收购) 标准
1.  **Entry Multiple (入门倍数)**：基于 EV/EBITDA 或 历史交易。
2.  **Debt Structure (债务结构)**：定义 Senior Debt, Mezzanine Debt 的优先级及利率。
3.  **Exit Multiple (退出倍数)**：通常假设与 Entry Multiple 一致或根据行业趋势下调 (Multiple Compression)。
4.  **Target IRR (目标收益率)**：通常设定在 20%-25%+。

---

## 3. 核心质量检查 (Model Integrity Checks)

| 检查项 | 逻辑要求 |
| :--- | :--- |
| **Balance Sheet Match** | Total Assets - (Total Liabilities + Equity) = 0 |
| **Cash Flow Reconciliation** | CFS 期末现金必须等于 BS 期末现金 |
| **Debt Paydown Logic** | 强制性本金偿还 (Mandatory Amortization) 不得超过可用现金流 |
| **Operating Margin Trend** | 预测期的营业利润率变化应有明确的业务逻辑支撑 (如规模效应、成本优化) |

---

## 4. 关键金融公式参考 (Formula Library)

*   **ROE (净资产收益率)** = Net Income / Shareholder's Equity.
*   **ROIC (投入资本回报率)** = NOPAT / Invested Capital.
*   **EBITDA Margin** = EBITDA / Total Revenue.
*   **Net Debt** = Total Debt - Cash & Equivalents.
*   **Beta (Unlevered)** = Levered Beta / [1 + (1 - Tax Rate) * (Debt/Equity)].
