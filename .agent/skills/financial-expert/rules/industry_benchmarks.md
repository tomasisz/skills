# Industry Benchmarks (行业基准与 KPI) V1.0

> 本文档定义了不同行业的核心绩效指标 (KPI) 和通用估值基准，用于 AI 在执行 `/er`, `/ib`, `/pe` 指令时的横向对比。

---

## 1. 软件与 SaaS (Software & SaaS)
*   **核心 KPI**：
    *   **Rule of 40**：(营收增长率 + 利润率) 应 > 40%。
    *   **Churn Rate (流失率)**：衡量客户粘性。
    *   **LTV/CAC**：应 > 3x。
    *   **Magic Number**：衡量销售效率 (> 0.75 为佳)。
*   **估值倍数**：EV/Revenue (NTM), EV/EBITDA.

## 2. 零售与消费品 (Retail & Consumer)
*   **核心 KPI**：
    *   **SSSG (Same-store sales growth)**：同店销售增长率。
    *   **Inventory Turnover**：存货周转率。
    *   **Gross Margin**：毛利率稳定性。
    *   **Customer Acquisition Cost (CAC)**：获客成本趋势。
*   **估值倍数**：P/E, EV/EBITDA, P/S (高增长品类)。

## 3. 工业与制造业 (Industrial & Manufacturing)
*   **核心 KPI**：
    *   **Capacity Utilization**：产能利用率。
    *   **Backlog Growth**：未完成订单增长情况。
    *   **ROIC (投入资本回报率)**：应高于 WACC。
    *   **Free Cash Flow Conversion**：净利润转化为现金流的能力。
*   **估值倍数**：EV/EBITDA, EV/IC.

## 4. 银行与金融服务 (Banking & Financials)
*   **核心 KPI**：
    *   **NIM (Net Interest Margin)**：净息差。
    *   **Cost-to-Income Ratio**：成本收入比。
    *   **NPL Ratio (Non-performing loan)**：不良贷款率。
    *   **Common Equity Tier 1 (CET1)**：核心一级资本充足率。
*   **估值倍数**：P/B (市净率), P/E.

## 5. 能源与大宗商品 (Energy & Commodities)
*   **核心 KPI**：
    *   **Reserve Replacement Ratio (RRR)**：储量替代率。
    *   **Lifting Cost / Break-even Price**：开采成本/盈亏平衡点。
    *   **Production Decline Rate**：产量衰减率。
*   **估值倍数**：P/NAV (净资产价值比), EV/EBITDA, EV/Daily Production.

---

## 6. 使用说明
在执行 `/fa:comps` 时，AI 必须根据目标公司所属行业，自动提取上述 KPI 进行横向对标分析。
