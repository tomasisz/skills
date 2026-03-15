# Financial Reporting Templates (金融报告模板) V1.0

> 本文档定义了各类金融文书的结构规范，确保输出格式符合国际金融机构 (如 GS, JPM, MS) 的标准。

---

## 1. 项目简介 (Investment Teaser)
*   **文件名建议**：Project_[Codename]_Teaser.md
*   **结构**：
    1.  **Executive Summary**：交易亮点 (3-5 点)。
    2.  **Company Overview**：业务描述、成立时间、总部。
    3.  **Market Opportunity**：行业规模 (TAM/SAM)、竞争优势。
    4.  **Key Financials**：营收趋势、EBITDA Margin (3 年历史 + 1 年预测)。
    5.  **Investment Highlights**：核心投资逻辑。
    6.  **Contact Info**：联系方式 (Placeholder)。

## 2. 投资委员会备忘录 (IC Memo)
*   **文件名建议**：Project_[Codename]_IC_Memo.md
*   **结构**：
    1.  **Investment Recommendation**：明确的投资结论 (Buy/Pass) 及核心理由。
    2.  **Deal Overview**：交易结构、对价、融资计划。
    3.  **Financial Analysis**：深度拆解历史业绩、QofE (盈余质量) 分析。
    4.  **Valuation Methodology**：DCF、LBO、Comps 分析结论。
    5.  **Strategic Rationale**：为何投资？协同效应在哪里？
    6.  **Key Risks & Mitigants**：识别核心风险并提出对冲方案。
    7.  **Exit Strategy**：退出路径 (IPO, Trade Sale, Buyback)。

## 3. 股票研究报告 (Equity Research - Initiating Coverage)
*   **文件名建议**：Company_[Ticker]_Initiation.md
*   **结构**：
    1.  **Investment Summary**：投资评级 (Overweight/Equal-weight/Underweight) 和目标价。
    2.  **Investment Thesis**：3 个核心看好理由。
    3.  **Key Catalysts**：未来 6-12 个月内可能触发股价变动的事件。
    4.  **Company Description**：详细业务拆解。
    5.  **Valuation & Risks**：目标价计算过程及风险提示。
    6.  **Financial Appendix**：预测模型概览。

## 4. 业绩点评报告 (Earnings Update)
*   **结构**：
    1.  **Summary Table**：实际业绩 vs 市场预期 (Beat/Miss)。
    2.  **Quick Take**：一句话总结财报表现。
    3.  **Earnings Highlights**：关键业务亮点。
    4.  **Guidance Update**：公司对未来的指引变动。
    5.  **Revised Outlook**：调整后的估值和目标价。

---

## 5. 输出格式规范
*   **金融单位**：统一使用 [Currency] [Value] [Multiplier] (如 USD 150m, CNY 2.5bn)。
*   **图表描述**：AI 在输出时应描述图表内容 (如："[Chart: Revenue Growth Trend, 2020-2025E]")，方便后续可视化工具接入。
*   **缩写规范**：首次使用缩写必须全称，后续使用缩写 (如：Enterprise Value -> EV)。
