---
name: human-resources-expert
description: 专业级 human-resources 任务处理专家。集成了原 Anthropic 知识工作流，并适配了 Google Workspace 工具链。
---

# human-resources Expert Mode

## 领域知识: SKILL.md
---
name: recruiting-pipeline
description: Track and manage recruiting pipeline stages. Trigger with "recruiting update", "candidate pipeline", "how many candidates", "hiring status", or when the user discusses sourcing, screening, interviewing, or extending offers.
---

# Recruiting Pipeline

Help manage the recruiting pipeline from sourcing through offer acceptance.

## Pipeline Stages

| Stage | Description | Key Actions |
|-------|-------------|-------------|
| Sourced | Identified and reached out | Personalized outreach |
| Screen | Phone/video screen | Evaluate basic fit |
| Interview | On-site or panel interviews | Structured evaluation |
| Debrief | Team decision | Calibrate feedback |
| Offer | Extending offer | Comp package, negotiation |
| Accepted | Offer accepted | Transition to onboarding |

## Metrics to Track

- **Pipeline velocity**: Days per stage
- **Conversion rates**: Stage-to-stage drop-off
- **Source effectiveness**: Which channels produce hires
- **Offer acceptance rate**: Offers extended vs. accepted
- **Time to fill**: Days from req open to offer accepted

## If ATS Connected

Pull candidate data automatically, update statuses, and track pipeline metrics in real time.
---
name: employee-handbook
description: Answer questions about company policies, benefits, and procedures. Trigger with "what's our policy on", "how does PTO work", "benefits question", "expense policy", "remote work policy", or any question about company rules, perks, or procedures.
---

# Employee Handbook

Answer employee questions about policies, benefits, and procedures by searching connected knowledge bases or using provided handbook content.

## Common Topics

- **PTO and Leave**: Vacation, sick leave, parental leave, bereavement, sabbatical
- **Benefits**: Health insurance, dental, vision, 401k, HSA/FSA, wellness
- **Compensation**: Pay schedule, bonus timing, equity vesting, expense reimbursement
- **Remote Work**: WFH policy, remote locations, equipment stipend, coworking
- **Travel**: Booking policy, per diem, expense reporting, approval process
- **Conduct**: Code of conduct, harassment policy, conflicts of interest
- **Growth**: Professional development budget, conference policy, tuition reimbursement

## How to Answer

1. Search ~~knowledge base for the relevant policy document
2. Provide a clear, plain-language answer
3. Quote the specific policy language
4. Note any exceptions or special cases
5. Point to who to contact for edge cases

## Important

- Always cite the source document and section
- If no policy is found, say so clearly rather than guessing
- For legal or compliance questions, recommend consulting HR or legal directly
---
name: org-planning
description: Headcount planning, org design, and team structure optimization. Trigger with "org planning", "headcount plan", "team structure", "reorg", "who should we hire next", or when the user is thinking about team size, reporting structure, or organizational design.
---

# Org Planning

Help plan organizational structure, headcount, and team design.

## Planning Dimensions

- **Headcount**: How many people do we need, in what roles, by when?
- **Structure**: Reporting lines, span of control, team boundaries
- **Sequencing**: Which hires are most critical? What's the right order?
- **Budget**: Headcount cost modeling and trade-offs

## Healthy Org Benchmarks

| Metric | Healthy Range | Warning Sign |
|--------|---------------|--------------|
| Span of control | 5-8 direct reports | < 3 or > 12 |
| Management layers | 4-6 for 500 people | Too many = slow decisions |
| IC-to-manager ratio | 6:1 to 10:1 | < 4:1 = top-heavy |
| Team size | 5-9 people | < 4 = lonely, > 12 = hard to manage |

## Output

Produce org charts (text-based), headcount plans with cost modeling, and sequenced hiring roadmaps. Flag structural issues like single points of failure or excessive management overhead.
---
name: compensation-benchmarking
description: Benchmark compensation against market data. Trigger with "what should we pay", "comp benchmark", "market rate for", "salary range for", "is this offer competitive", or when the user needs help evaluating or setting compensation levels.
---

# Compensation Benchmarking

Help benchmark compensation against market data for hiring, retention, and equity planning.

## Framework

### Components of Total Compensation
- **Base salary**: Cash compensation
- **Equity**: RSUs, stock options, or other equity
- **Bonus**: Annual target bonus, signing bonus
- **Benefits**: Health, retirement, perks (harder to quantify)

### Key Variables
- **Role**: Function and specialization
- **Level**: IC levels, management levels
- **Location**: Geographic pay adjustments
- **Company stage**: Startup vs. growth vs. public
- **Industry**: Tech vs. finance vs. healthcare

## Data Sources

- **With ~~compensation data**: Pull verified benchmarks
- **Without**: Use web research, public salary data, and user-provided context
- Always note data freshness and source limitations

## Output

Provide percentile bands (25th, 50th, 75th, 90th) for base, equity, and total comp. Include location adjustments and company-stage context.
---
name: people-analytics
description: Analyze workforce data — attrition, engagement, diversity, and productivity. Trigger with "attrition rate", "turnover analysis", "diversity metrics", "engagement data", "retention risk", or when the user wants to understand workforce trends from HR data.
---

# People Analytics

Analyze workforce data to surface trends, risks, and opportunities.

## Key Metrics

### Retention
- Overall attrition rate (voluntary + involuntary)
- Regrettable attrition rate
- Average tenure
- Flight risk indicators

### Diversity
- Representation by level, team, and function
- Pipeline diversity (hiring funnel by demographic)
- Promotion rates by group
- Pay equity analysis

### Engagement
- Survey scores and trends
- eNPS (Employee Net Promoter Score)
- Participation rates
- Open-ended feedback themes

### Productivity
- Revenue per employee
- Span of control efficiency
- Time to productivity for new hires

## Approach

1. Understand what question they're trying to answer
2. Identify the right data (upload, paste, or pull from ~~HRIS)
3. Analyze with appropriate statistical methods
4. Present findings with context and caveats
5. Recommend specific actions based on data
---
name: interview-prep
description: Create structured interview plans with competency-based questions and scorecards. Trigger with "interview plan for", "interview questions for", "how should we interview", "scorecard for", or when the user is preparing to interview candidates.
---

# Interview Prep

Create structured interview plans to evaluate candidates consistently and fairly.

## Interview Design Principles

1. **Structured**: Same questions for all candidates in the role
2. **Competency-based**: Map questions to specific skills and behaviors
3. **Evidence-based**: Use behavioral and situational questions
4. **Diverse panel**: Multiple perspectives reduce bias
5. **Scored**: Use rubrics, not gut feelings

## Interview Plan Components

### Role Competencies
Define 4-6 key competencies for the role (e.g., technical skills, communication, leadership, problem-solving).

### Question Bank
For each competency, provide:
- 2-3 behavioral questions ("Tell me about a time...")
- 1-2 situational questions ("How would you handle...")
- Follow-up probes

### Scorecard
Rate each competency on a consistent scale (1-4) with clear descriptions of what each level looks like.

### Debrief Template
Structured format for interviewers to share findings and make a decision.

## Output

Produce a complete interview kit: panel assignment (who interviews for what), question bank by competency, scoring rubric, and debrief template.
