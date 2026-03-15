---
name: operations-expert
description: 专业级 operations 任务处理专家。集成了原 Anthropic 知识工作流，并适配了 Google Workspace 工具链。
---

# operations Expert Mode

## 领域知识: SKILL.md
---
name: process-optimization
description: Analyze and improve business processes. Trigger with "this process is slow", "how can we improve", "streamline this workflow", "too many steps", "bottleneck", or when the user describes an inefficient process they want to fix.
---

# Process Optimization

Analyze existing processes and recommend improvements.

## Analysis Framework

### 1. Map Current State
- Document every step, decision point, and handoff
- Identify who does what and how long each step takes
- Note manual steps, approvals, and waiting times

### 2. Identify Waste
- **Waiting**: Time spent in queues or waiting for approvals
- **Rework**: Steps that fail and need to be redone
- **Handoffs**: Each handoff is a potential point of failure or delay
- **Over-processing**: Steps that add no value
- **Manual work**: Tasks that could be automated

### 3. Design Future State
- Eliminate unnecessary steps
- Automate where possible
- Reduce handoffs
- Parallelize independent steps
- Add checkpoints (not gates)

### 4. Measure Impact
- Time saved per cycle
- Error rate reduction
- Cost savings
- Employee satisfaction improvement

## Output

Produce a before/after process comparison with specific improvement recommendations, estimated impact, and an implementation plan.
---
name: change-management
description: Plan and execute organizational or technical changes. Trigger with "we're changing", "rolling out", "migration plan", "how do we communicate this change", "change management plan", or when the user is planning a change that affects people, processes, or systems.
---

# Change Management

Help plan and execute changes that affect people, processes, or technology.

## Change Management Framework

### 1. Assess
- What is changing?
- Who is affected?
- How significant is the change? (Low / Medium / High)
- What resistance should we expect?

### 2. Plan
- Communication plan (who, what, when, how)
- Training plan (what skills are needed, how to deliver)
- Support plan (help desk, champions, FAQs)
- Timeline with milestones

### 3. Execute
- Announce and explain the "why"
- Train and support
- Monitor adoption
- Address resistance

### 4. Sustain
- Measure adoption and effectiveness
- Reinforce new behaviors
- Address lingering issues
- Document lessons learned

## Communication Principles

- Explain the **why** before the **what**
- Communicate early and often
- Use multiple channels
- Acknowledge what's being lost, not just what's being gained
- Provide a clear path for questions and concerns

## Output

Produce a change management plan with communication timeline, stakeholder impact analysis, training plan, and resistance mitigation strategies.
---
name: resource-planning
description: Plan and optimize resource allocation. Trigger with "resource planning", "capacity", "utilization", "staffing plan", "who should work on what", "we're stretched thin", or when the user needs help allocating people, budget, or time across projects and teams.
---

# Resource Planning

Help plan and optimize resource allocation across projects and teams.

## Planning Dimensions

### People
- Available headcount and skills
- Current allocation and utilization
- Planned hires and timeline
- Contractor and vendor capacity

### Budget
- Operating budget by category
- Project-specific budgets
- Variance tracking
- Forecast vs. actual

### Time
- Project timelines and dependencies
- Critical path analysis
- Buffer and contingency planning
- Deadline management

## Utilization Targets

| Role Type | Target Utilization | Notes |
|-----------|-------------------|-------|
| IC / Specialist | 75-80% | Leave room for reactive work and growth |
| Manager | 60-70% | Management overhead, meetings, 1:1s |
| On-call / Support | 50-60% | Interrupt-driven work is unpredictable |

## Common Pitfalls

- Planning to 100% utilization (no buffer for surprises)
- Ignoring meeting load and context-switching costs
- Not accounting for vacation, holidays, and sick time
- Treating all hours as equal (creative work ≠ admin work)

## Output

Produce allocation plans, utilization dashboards, scenario analyses (what if we hire / don't hire / deprioritize), and staffing recommendations.
---
name: compliance-tracking
description: Track compliance requirements and audit readiness. Trigger with "compliance", "audit prep", "SOC 2", "ISO 27001", "GDPR", "regulatory requirement", or when the user needs help tracking, preparing for, or documenting compliance activities.
---

# Compliance Tracking

Help track compliance requirements, prepare for audits, and maintain regulatory readiness.

## Common Frameworks

| Framework | Focus | Key Requirements |
|-----------|-------|-----------------|
| SOC 2 | Service organizations | Security, availability, processing integrity, confidentiality, privacy |
| ISO 27001 | Information security | Risk assessment, security controls, continuous improvement |
| GDPR | Data privacy (EU) | Consent, data rights, breach notification, DPO |
| HIPAA | Healthcare data (US) | PHI protection, access controls, audit trails |
| PCI DSS | Payment card data | Encryption, access control, vulnerability management |

## Compliance Tracking Components

### Control Inventory
- Map controls to framework requirements
- Document control owners and evidence
- Track control effectiveness

### Audit Calendar
- Upcoming audit dates and deadlines
- Evidence collection timelines
- Remediation deadlines

### Evidence Management
- What evidence is needed for each control
- Where evidence is stored
- When evidence was last collected

### Gap Analysis
- Requirements vs. current state
- Prioritized remediation plan
- Timeline to compliance

## Output

Produce compliance status dashboards, gap analyses, audit prep checklists, and evidence collection plans.
---
name: risk-assessment
description: Identify, assess, and mitigate operational risks. Trigger with "what are the risks", "risk assessment", "risk register", "what could go wrong", or when the user is evaluating risks associated with a project, vendor, process, or decision.
---

# Risk Assessment

Systematically identify, assess, and plan mitigations for operational risks.

## Risk Assessment Matrix

| | Low Impact | Medium Impact | High Impact |
|---|-----------|---------------|-------------|
| **High Likelihood** | Medium | High | Critical |
| **Medium Likelihood** | Low | Medium | High |
| **Low Likelihood** | Low | Low | Medium |

## Risk Categories

- **Operational**: Process failures, staffing gaps, system outages
- **Financial**: Budget overruns, vendor cost increases, revenue impact
- **Compliance**: Regulatory violations, audit findings, policy breaches
- **Strategic**: Market changes, competitive threats, technology shifts
- **Reputational**: Customer impact, public perception, partner relationships
- **Security**: Data breaches, access control failures, third-party vulnerabilities

## Risk Register Format

For each risk, document:
- **Description**: What could happen
- **Likelihood**: High / Medium / Low
- **Impact**: High / Medium / Low
- **Risk Level**: Critical / High / Medium / Low
- **Mitigation**: What we're doing to reduce likelihood or impact
- **Owner**: Who is responsible for managing this risk
- **Status**: Open / Mitigated / Accepted / Closed

## Output

Produce a prioritized risk register with specific, actionable mitigations. Focus on risks that are controllable and material.
---
name: vendor-management
description: Evaluate, compare, and manage vendor relationships. Trigger with "evaluate this vendor", "compare vendors", "vendor review", "should we renew", "RFP", or when the user is making procurement or vendor decisions.
---

# Vendor Management

Help evaluate, compare, and manage vendor relationships.

## Evaluation Framework

### Cost Analysis
- Total cost of ownership (not just license fees)
- Implementation and migration costs
- Training and onboarding costs
- Ongoing support and maintenance
- Exit costs (data migration, contract termination)

### Risk Assessment
- Vendor financial stability
- Security and compliance posture
- Concentration risk (single vendor dependency)
- Contract lock-in and exit terms
- Business continuity and disaster recovery

### Performance Metrics
- SLA compliance
- Support response times
- Uptime and reliability
- Feature delivery cadence
- Customer satisfaction

## Comparison Matrix

When comparing vendors, produce a side-by-side matrix covering: pricing, features, integrations, security, support, contract terms, and references.

## Output

Provide a clear recommendation with supporting evidence. Always flag risks and negotiation leverage points.
