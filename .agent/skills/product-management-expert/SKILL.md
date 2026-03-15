---
name: product-management-expert
description: 专业级 product-management 任务处理专家。集成了原 Anthropic 知识工作流，并适配了 Google Workspace 工具链。
---

# product-management Expert Mode

## 领域知识: SKILL.md
---
name: metrics-tracking
description: Define, track, and analyze product metrics with frameworks for goal setting and dashboard design. Use when setting up OKRs, building metrics dashboards, running weekly metrics reviews, identifying trends, or choosing the right metrics for a product area.
---

# Metrics Tracking Skill

You are an expert at product metrics — defining, tracking, analyzing, and acting on product metrics. You help product managers build metrics frameworks, set goals, run reviews, and design dashboards that drive decisions.

## Product Metrics Hierarchy

### North Star Metric
The single metric that best captures the core value your product delivers to users. It should be:

- **Value-aligned**: Moves when users get more value from the product
- **Leading**: Predicts long-term business success (revenue, retention)
- **Actionable**: The product team can influence it through their work
- **Understandable**: Everyone in the company can understand what it means and why it matters

**Examples by product type**:
- Collaboration tool: Weekly active teams with 3+ members contributing
- Marketplace: Weekly transactions completed
- SaaS platform: Weekly active users completing core workflow
- Content platform: Weekly engaged reading/viewing time
- Developer tool: Weekly deployments using the tool

### L1 Metrics (Health Indicators)
The 5-7 metrics that together paint a complete picture of product health. These map to the key stages of the user lifecycle:

**Acquisition**: Are new users finding the product?
- New signups or trial starts (volume and trend)
- Signup conversion rate (visitors to signups)
- Channel mix (where are new users coming from)
- Cost per acquisition (for paid channels)

**Activation**: Are new users reaching the value moment?
- Activation rate: % of new users who complete the key action that predicts retention
- Time to activate: how long from signup to activation
- Setup completion rate: % who complete onboarding steps
- First value moment: when users first experience the core product value

**Engagement**: Are active users getting value?
- DAU / WAU / MAU: active users at different timeframes
- DAU/MAU ratio (stickiness): what fraction of monthly users come back daily
- Core action frequency: how often users do the thing that matters most
- Session depth: how much users do per session
- Feature adoption: % of users using key features

**Retention**: Are users coming back?
- D1, D7, D30 retention: % of users who return after 1 day, 7 days, 30 days
- Cohort retention curves: how retention evolves for each signup cohort
- Churn rate: % of users or revenue lost per period
- Resurrection rate: % of churned users who come back

**Monetization**: Is value translating to revenue?
- Conversion rate: free to paid (for freemium)
- MRR / ARR: monthly or annual recurring revenue
- ARPU / ARPA: average revenue per user or account
- Expansion revenue: revenue growth from existing customers
- Net revenue retention: revenue retention including expansion and contraction

**Satisfaction**: How do users feel about the product?
- NPS: Net Promoter Score
- CSAT: Customer Satisfaction Score
- Support ticket volume and resolution time
- App store ratings and review sentiment

### L2 Metrics (Diagnostic)
Detailed metrics used to investigate changes in L1 metrics:

- Funnel conversion at each step
- Feature-level usage and adoption
- Segment-specific breakdowns (by plan, company size, geography, user role)
- Performance metrics (page load time, error rate, API latency)
- Content-specific engagement (which features, pages, or content types drive engagement)

## Common Product Metrics

### DAU / WAU / MAU
**What they measure**: Unique users who perform a qualifying action in a day, week, or month.

**Key decisions**:
- What counts as "active"? A login? A page view? A core action? Define this carefully — different definitions tell different stories.
- Which timeframe matters most? DAU for daily-use products (messaging, email). WAU for weekly-use products (project management). MAU for less frequent products (tax software, travel booking).

**How to use them**:
- DAU/MAU ratio (stickiness): values above 0.5 indicate a daily habit. Below 0.2 suggests infrequent usage.
- Trend matters more than absolute number. Is active usage growing, flat, or declining?
- Segment by user type. Power users and casual users behave very differently.

### Retention
**What it measures**: Of users who started in period X, what % are still active in period Y?

**Common retention timeframes**:
- D1 (next day): Was the first experience good enough to come back?
- D7 (one week): Did the user establish a habit?
- D30 (one month): Is the user retained long-term?
- D90 (three months): Is this a durable user?

**How to use retention**:
- Plot retention curves by cohort. Look for: initial drop-off (activation problem), steady decline (engagement problem), or flattening (good — you have a stable retained base).
- Compare cohorts over time. Are newer cohorts retaining better than older ones? That means product improvements are working.
- Segment retention by activation behavior. Users who completed onboarding vs those who did not. Users who used feature X vs those who did not.

### Conversion
**What it measures**: % of users who move from one stage to the next.

**Common conversion funnels**:
- Visitor to signup
- Signup to activation (key value moment)
- Free to paid (trial conversion)
- Trial to paid subscription
- Monthly to annual plan

**How to use conversion**:
- Map the full funnel and measure conversion at each step
- Identify the biggest drop-off points — these are your highest-leverage improvement opportunities
- Segment conversion by source, plan, user type. Different segments convert very differently.
- Track conversion over time. Is it improving as you iterate on the experience?

### Activation
**What it measures**: % of new users who reach the moment where they first experience the product's core value.

**Defining activation**:
- Look at retained users vs churned users. What actions did retained users take that churned users did not?
- The activation event should be strongly predictive of long-term retention
- It should be achievable within the first session or first few days
- Examples: created first project, invited a teammate, completed first workflow, connected an integration

**How to use activation**:
- Track activation rate for every signup cohort
- Measure time to activate — faster is almost always better
- Build onboarding flows that guide users to the activation moment
- A/B test activation flows and measure impact on retention, not just activation rate

## Goal Setting Frameworks

### OKRs (Objectives and Key Results)

**Objectives**: Qualitative, aspirational goals that describe what you want to achieve.
- Inspiring and memorable
- Time-bound (quarterly or annually)
- Directional, not metric-specific

**Key Results**: Quantitative measures that tell you if you achieved the objective.
- Specific and measurable
- Time-bound with a clear target
- Outcome-based, not output-based
- 2-4 Key Results per Objective

**Example**:
```
Objective: Make our product indispensable for daily workflows

Key Results:
- Increase DAU/MAU ratio from 0.35 to 0.50
- Increase D30 retention for new users from 40% to 55%
- 3 core workflows with >80% task completion rate
```

### OKR Best Practices
- Set OKRs that are ambitious but achievable. 70% completion is the target for stretch OKRs.
- Key Results should measure outcomes (user behavior, business results), not outputs (features shipped, tasks completed).
- Do not have too many OKRs. 2-3 objectives with 2-4 KRs each is plenty.
- OKRs should be uncomfortable. If you are confident you will hit all of them, they are not ambitious enough.
- Review OKRs at mid-period. Adjust effort allocation if some KRs are clearly off track.
- Grade OKRs honestly at end of period. 0.0-0.3 = missed, 0.4-0.6 = progress, 0.7-1.0 = achieved.

### Setting Metric Targets
- **Baseline**: What is the current value? You need a reliable baseline before setting a target.
- **Benchmark**: What do comparable products achieve? Industry benchmarks provide context.
- **Trajectory**: What is the current trend? If the metric is already improving at 5% per month, a 6% target is not ambitious.
- **Effort**: How much investment are you putting behind this? Bigger bets warrant more ambitious targets.
- **Confidence**: How confident are you in hitting the target? Set a "commit" (high confidence) and a "stretch" (ambitious).

## Metric Review Cadences

### Weekly Metrics Check
**Purpose**: Catch issues quickly, monitor experiments, stay in touch with product health.
**Duration**: 15-30 minutes.
**Attendees**: Product manager, maybe engineering lead.

**What to review**:
- North Star metric: current value, week-over-week change
- Key L1 metrics: any notable movements
- Active experiments: results and statistical significance
- Anomalies: any unexpected spikes or drops
- Alerts: anything that triggered a monitoring alert

**Action**: If something looks off, investigate. Otherwise, note it and move on.

### Monthly Metrics Review
**Purpose**: Deeper analysis of trends, progress against goals, strategic implications.
**Duration**: 30-60 minutes.
**Attendees**: Product team, key stakeholders.

**What to review**:
- Full L1 metric scorecard with month-over-month trends
- Progress against quarterly OKR targets
- Cohort analysis: are newer cohorts performing better?
- Feature adoption: how are recent launches performing?
- Segment analysis: any divergence between user segments?

**Action**: Identify 1-3 areas to investigate or invest in. Update priorities if metrics reveal new information.

### Quarterly Business Review
**Purpose**: Strategic assessment of product performance, goal-setting for next quarter.
**Duration**: 60-90 minutes.
**Attendees**: Product, engineering, design, leadership.

**What to review**:
- OKR scoring for the quarter
- Trend analysis for all L1 metrics over the quarter
- Year-over-year comparisons
- Competitive context: market changes and competitor movements
- What worked and what did not

**Action**: Set OKRs for next quarter. Adjust product strategy based on what the data shows.

## Dashboard Design Principles

### Effective Product Dashboards
A good dashboard answers the question "How is the product doing?" at a glance.

**Principles**:

1. **Start with the question, not the data**. What decisions does this dashboard support? Design backwards from the decision.

2. **Hierarchy of information**. The most important metric should be the most visually prominent. North Star at the top, L1 metrics next, L2 metrics available on drill-down.

3. **Context over numbers**. A number without context is meaningless. Always show: current value, comparison (previous period, target, benchmark), trend direction.

4. **Fewer metrics, more insight**. A dashboard with 50 metrics helps no one. Focus on 5-10 that matter. Put everything else in a detailed report.

5. **Consistent time periods**. Use the same time period for all metrics on a dashboard. Mixing daily and monthly metrics creates confusion.

6. **Visual status indicators**. Use color to indicate health at a glance:
   - Green: on track or improving
   - Yellow: needs attention or flat
   - Red: off track or declining

7. **Actionability**. Every metric on the dashboard should be something the team can influence. If you cannot act on it, it does not belong on the product dashboard.

### Dashboard Layout

**Top row**: North Star metric with trend line and target.

**Second row**: L1 metrics scorecard — current value, change, target, status for each key metric.

**Third row**: Key funnels or conversion metrics — visual funnel showing drop-off at each stage.

**Fourth row**: Recent experiments and launches — active A/B tests, recent feature launches with early metrics.

**Bottom / drill-down**: L2 metrics, segment breakdowns, and detailed time series for investigation.

### Dashboard Anti-Patterns
- **Vanity metrics**: Metrics that always go up but do not indicate health (total signups ever, total page views)
- **Too many metrics**: Dashboards that require scrolling to see. If it does not fit on one screen, cut metrics.
- **No comparison**: Raw numbers without context (current value with no previous period or target)
- **Stale dashboards**: Metrics that have not been updated or reviewed in months
- **Output dashboards**: Measuring team activity (tickets closed, PRs merged) instead of user and business outcomes
- **One dashboard for all audiences**: Executives, PMs, and engineers need different views. One size does not fit all.

### Alerting
Set alerts for metrics that require immediate attention:

- **Threshold alerts**: Metric drops below or rises above a critical threshold (error rate > 1%, conversion < 5%)
- **Trend alerts**: Metric shows sustained decline over multiple days/weeks
- **Anomaly alerts**: Metric deviates significantly from expected range

**Alert hygiene**:
- Every alert should be actionable. If you cannot do anything about it, do not alert on it.
- Review and tune alerts regularly. Too many false positives and people ignore all alerts.
- Define an owner for each alert. Who responds when it fires?
- Set appropriate severity levels. Not everything is P0.
---
name: stakeholder-comms
description: Draft stakeholder updates tailored to audience — executives, engineering, customers, or cross-functional partners. Use when writing weekly status updates, monthly reports, launch announcements, risk communications, or decision documentation.
---

# Stakeholder Communications Skill

You are an expert at product management communications — status updates, stakeholder management, risk communication, decision documentation, and meeting facilitation. You help product managers communicate clearly and effectively with diverse audiences.

## Update Templates by Audience

### Executive / Leadership Update
Executives want: strategic context, progress against goals, risks that need their help, decisions that need their input.

**Format**:
```
Status: [Green / Yellow / Red]

TL;DR: [One sentence — the most important thing to know]

Progress:
- [Outcome achieved, tied to goal/OKR]
- [Milestone reached, with impact]
- [Key metric movement]

Risks:
- [Risk]: [Mitigation plan]. [Ask if needed].

Decisions needed:
- [Decision]: [Options with recommendation]. Need by [date].

Next milestones:
- [Milestone] — [Date]
```

**Tips for executive updates**:
- Lead with the conclusion, not the journey. Executives want "we shipped X and it moved Y metric" not "we had 14 standups and resolved 23 tickets."
- Keep it under 200 words. If they want more, they will ask.
- Status color should reflect YOUR genuine assessment, not what you think they want to hear. Yellow is not a failure — it is good risk management.
- Only include risks you want help with. Do not list risks you are already handling unless they need to know.
- Asks must be specific: "Decision on X by Friday" not "support needed."

### Engineering Team Update
Engineers want: clear priorities, technical context, blockers resolved, decisions that affect their work.

**Format**:
```
Shipped:
- [Feature/fix] — [Link to PR/ticket]. [Impact if notable].

In progress:
- [Item] — [Owner]. [Expected completion]. [Blockers if any].

Decisions:
- [Decision made]: [Rationale]. [Link to ADR if exists].
- [Decision needed]: [Context]. [Options]. [Recommendation].

Priority changes:
- [What changed and why]

Coming up:
- [Next items] — [Context on why these are next]
```

**Tips for engineering updates**:
- Link to specific tickets, PRs, and documents. Engineers want to click through for details.
- When priorities change, explain why. Engineers are more bought in when they understand the reason.
- Be explicit about what is blocking them and what you are doing to unblock it.
- Do not waste their time with information that does not affect their work.

### Cross-Functional Partner Update
Partners (design, marketing, sales, support) want: what is coming that affects them, what they need to prepare for, how to give input.

**Format**:
```
What's coming:
- [Feature/launch] — [Date]. [What this means for your team].

What we need from you:
- [Specific ask] — [Context]. By [date].

Decisions made:
- [Decision] — [How it affects your team].

Open for input:
- [Topic we'd love feedback on] — [How to provide it].
```

### Customer / External Update
Customers want: what is new, what is coming, how it benefits them, how to get started.

**Format**:
```
What's new:
- [Feature] — [Benefit in customer terms]. [How to use it / link].

Coming soon:
- [Feature] — [Expected timing]. [Why it matters to you].

Known issues:
- [Issue] — [Status]. [Workaround if available].

Feedback:
- [How to share feedback or request features]
```

**Tips for customer updates**:
- No internal jargon. No ticket numbers. No technical implementation details.
- Frame everything in terms of what the customer can now DO, not what you built.
- Be honest about timelines but do not overcommit. "Later this quarter" is better than a date you might miss.
- Only mention known issues if they are customer-impacting and you have a resolution plan.

## Status Reporting Framework

### Green / Yellow / Red Status

**Green** (On Track):
- Progressing as planned
- No significant risks or blockers
- On track to meet commitments and deadlines
- Use Green when things are genuinely going well — not as a default

**Yellow** (At Risk):
- Progress is slower than planned, or a risk has materialized
- Mitigation is underway but outcome is uncertain
- May miss commitments without intervention or scope adjustment
- Use Yellow proactively — the earlier you flag risk, the more options you have

**Red** (Off Track):
- Significantly behind plan
- Major blocker or risk without clear mitigation
- Will miss commitments without significant intervention (scope cut, resource addition, timeline extension)
- Use Red when you genuinely need help. Do not wait until it is too late.

### When to Change Status
- Move to Yellow at the FIRST sign of risk, not when you are sure things are bad
- Move to Red when you have exhausted your own options and need escalation
- Move back to Green only when the risk is genuinely resolved, not just paused
- Document what changed when you change status — "Moved to Yellow because [reason]"

## Risk Communication

### ROAM Framework for Risk Management
- **Resolved**: Risk is no longer a concern. Document how it was resolved.
- **Owned**: Risk is acknowledged and someone is actively managing it. State the owner and the mitigation plan.
- **Accepted**: Risk is known but we are choosing to proceed without mitigation. Document the rationale.
- **Mitigated**: Actions have reduced the risk to an acceptable level. Document what was done.

### Communicating Risks Effectively
1. **State the risk clearly**: "There is a risk that [thing] happens because [reason]"
2. **Quantify the impact**: "If this happens, the consequence is [impact]"
3. **State the likelihood**: "This is [likely/possible/unlikely] because [evidence]"
4. **Present the mitigation**: "We are managing this by [actions]"
5. **Make the ask**: "We need [specific help] to further reduce this risk"

### Common Mistakes in Risk Communication
- Burying risks in good news. Lead with risks when they are important.
- Being vague: "There might be some delays" — specify what, how long, and why.
- Presenting risks without mitigations. Every risk should come with a plan.
- Waiting too long. A risk communicated early is a planning input. A risk communicated late is a fire drill.

## Decision Documentation (ADRs)

### Architecture Decision Record Format
Document important decisions for future reference:

```
# [Decision Title]

## Status
[Proposed / Accepted / Deprecated / Superseded by ADR-XXX]

## Context
What is the situation that requires a decision? What forces are at play?

## Decision
What did we decide? State the decision clearly and directly.

## Consequences
What are the implications of this decision?
- Positive consequences
- Negative consequences or tradeoffs accepted
- What this enables or prevents in the future

## Alternatives Considered
What other options were evaluated?
For each: what was it, why was it rejected?
```

### When to Write an ADR
- Strategic product decisions (which market segment to target, which platform to support)
- Significant technical decisions (architecture choices, vendor selection, build vs buy)
- Controversial decisions where people disagreed (document the rationale for future reference)
- Decisions that constrain future options (choosing a technology, signing a partnership)
- Decisions you expect people to question later (capture the context while it is fresh)

### Tips for Decision Documentation
- Write ADRs close to when the decision is made, not weeks later
- Include who was involved in the decision and who made the final call
- Document the context generously — future readers will not have today's context
- It is okay to document decisions that were wrong in hindsight — add a "superseded by" link
- Keep them short. One page is better than five.

## Meeting Facilitation

### Stand-up / Daily Sync
**Purpose**: Surface blockers, coordinate work, maintain momentum.
**Format**: Each person shares:
- What they accomplished since last sync
- What they are working on next
- What is blocking them

**Facilitation tips**:
- Keep it to 15 minutes. If discussions emerge, take them offline.
- Focus on blockers — this is the highest-value part of standup
- Track blockers and follow up on resolution
- Cancel standup if there is nothing to sync on. Respect people's time.

### Sprint / Iteration Planning
**Purpose**: Commit to work for the next sprint. Align on priorities and scope.
**Format**:
1. Review: what shipped last sprint, what carried over, what was cut
2. Priorities: what are the most important things to accomplish this sprint
3. Capacity: how much can the team take on (account for PTO, on-call, meetings)
4. Commitment: select items from the backlog that fit capacity and priorities
5. Dependencies: flag any cross-team or external dependencies

**Facilitation tips**:
- Come with a proposed priority order. Do not ask the team to prioritize from scratch.
- Push back on overcommitment. It is better to commit to less and deliver reliably.
- Ensure every item has a clear owner and clear acceptance criteria.
- Flag items that are underscoped or have hidden complexity.

### Retrospective
**Purpose**: Reflect on what went well, what did not, and what to change.
**Format**:
1. Set the stage: remind the team of the goal and create psychological safety
2. Gather data: what went well, what did not go well, what was confusing
3. Generate insights: identify patterns and root causes
4. Decide actions: pick 1-3 specific improvements to try next sprint
5. Close: thank people for honest feedback

**Facilitation tips**:
- Create psychological safety. People must feel safe to be honest.
- Focus on systems and processes, not individuals.
- Limit to 1-3 action items. More than that and nothing changes.
- Follow up on previous retro action items. If you never follow up, people stop engaging.
- Vary the retro format occasionally to prevent staleness.

### Stakeholder Review / Demo
**Purpose**: Show progress, gather feedback, build alignment.
**Format**:
1. Context: remind stakeholders of the goal and what they saw last time
2. Demo: show what was built. Use real product, not slides.
3. Metrics: share any early data or feedback
4. Feedback: structured time for questions and input
5. Next steps: what is coming next and when the next review will be

**Facilitation tips**:
- Demo the real product whenever possible. Slides are not demos.
- Frame feedback collection: "What feedback do you have on X?" is better than "Any thoughts?"
- Capture feedback visibly and commit to addressing it (or explaining why not)
- Set expectations about what kind of feedback is actionable at this stage
---
name: roadmap-management
description: Plan and prioritize product roadmaps using frameworks like RICE, MoSCoW, and ICE. Use when creating a roadmap, reprioritizing features, mapping dependencies, choosing between Now/Next/Later or quarterly formats, or presenting roadmap tradeoffs to stakeholders.
---

# Roadmap Management Skill

You are an expert at product roadmap planning, prioritization, and communication. You help product managers build roadmaps that are strategic, realistic, and useful for decision-making.

## Roadmap Frameworks

### Now / Next / Later
The simplest and often most effective roadmap format:

- **Now** (current sprint/month): Committed work. High confidence in scope and timeline. These are the things the team is actively building.
- **Next** (next 1-3 months): Planned work. Good confidence in what, less confidence in exactly when. Scoped and prioritized but not yet started.
- **Later** (3-6+ months): Directional. These are strategic bets and opportunities we intend to pursue, but scope and timing are flexible.

When to use: Most teams, most of the time. Especially good for communicating externally or to leadership because it avoids false precision on dates.

### Quarterly Themes
Organize the roadmap around 2-3 themes per quarter:

- Each theme represents a strategic area of investment (e.g., "Enterprise readiness", "Activation improvements", "Platform extensibility")
- Under each theme, list the specific initiatives planned
- Themes should map to company or team OKRs
- This format makes it easy to explain WHY you are building what you are building

When to use: When you need to show strategic alignment. Good for planning meetings and executive communication.

### OKR-Aligned Roadmap
Map roadmap items directly to Objectives and Key Results:

- Start with the team's OKRs for the period
- Under each Key Result, list the initiatives that will move that metric
- Include the expected impact of each initiative on the Key Result
- This creates clear accountability between what you build and what you measure

When to use: Organizations that run on OKRs. Good for ensuring every initiative has a clear "why" tied to measurable outcomes.

### Timeline / Gantt View
Calendar-based view with items on a timeline:

- Shows start dates, end dates, and durations
- Visualizes parallelism and sequencing
- Good for identifying resource conflicts
- Shows dependencies between items

When to use: Execution planning with engineering. Identifying scheduling conflicts. NOT good for communicating externally (creates false precision expectations).

## Prioritization Frameworks

### RICE Score
Score each initiative on four dimensions, then calculate RICE = (Reach x Impact x Confidence) / Effort

- **Reach**: How many users/customers will this affect in a given time period? Use concrete numbers (e.g., "500 users per quarter").
- **Impact**: How much will this move the needle for each person reached? Score on a scale: 3 = massive, 2 = high, 1 = medium, 0.5 = low, 0.25 = minimal.
- **Confidence**: How confident are we in the reach and impact estimates? 100% = high confidence (backed by data), 80% = medium (some evidence), 50% = low (gut feel).
- **Effort**: How many person-months of work? Include engineering, design, and any other functions.

When to use: When you need a quantitative, defensible prioritization. Good for comparing a large backlog of initiatives. Less good for strategic bets where impact is hard to estimate.

### MoSCoW
Categorize items into Must have, Should have, Could have, Won't have:

- **Must have**: The roadmap is a failure without these. Non-negotiable commitments.
- **Should have**: Important and expected, but delivery is viable without them.
- **Could have**: Desirable but clearly lower priority. Include only if capacity allows.
- **Won't have**: Explicitly out of scope for this period. Important to list for clarity.

When to use: Scoping a release or quarter. Negotiating with stakeholders about what fits. Good for forcing prioritization conversations.

### ICE Score
Simpler than RICE. Score each item 1-10 on three dimensions:

- **Impact**: How much will this move the target metric?
- **Confidence**: How confident are we in the impact estimate?
- **Ease**: How easy is this to implement? (Inverse of effort — higher = easier)

ICE Score = Impact x Confidence x Ease

When to use: Quick prioritization of a feature backlog. Good for early-stage products or when you do not have enough data for RICE.

### Value vs Effort Matrix
Plot initiatives on a 2x2 matrix:

- **High value, Low effort** (Quick wins): Do these first.
- **High value, High effort** (Big bets): Plan these carefully. Worth the investment but need proper scoping.
- **Low value, Low effort** (Fill-ins): Do these when you have spare capacity.
- **Low value, High effort** (Money pits): Do not do these. Remove from the backlog.

When to use: Visual prioritization in team planning sessions. Good for building shared understanding of tradeoffs.

## Dependency Mapping

### Identifying Dependencies
Look for dependencies across these categories:

- **Technical dependencies**: Feature B requires infrastructure work from Feature A
- **Team dependencies**: Feature requires work from another team (design, platform, data)
- **External dependencies**: Waiting on a vendor, partner, or third-party integration
- **Knowledge dependencies**: Need research or investigation results before starting
- **Sequential dependencies**: Must ship Feature A before starting Feature B (shared code, user flow)

### Managing Dependencies
- List all dependencies explicitly in the roadmap
- Assign an owner to each dependency (who is responsible for resolving it)
- Set a "need by" date: when does the depending item need this resolved
- Build buffer around dependencies — they are the highest-risk items on any roadmap
- Flag dependencies that cross team boundaries early — these require coordination
- Have a contingency plan: what do you do if the dependency slips?

### Reducing Dependencies
- Can you build a simpler version that avoids the dependency?
- Can you parallelize by using an interface contract or mock?
- Can you sequence differently to move the dependency earlier?
- Can you absorb the work into your team to remove the cross-team coordination?

## Capacity Planning

### Estimating Capacity
- Start with the number of engineers and the time period
- Subtract known overhead: meetings, on-call rotations, interviews, holidays, PTO
- A common rule of thumb: engineers spend 60-70% of time on planned feature work
- Factor in team ramp time for new members

### Allocating Capacity
A healthy allocation for most product teams:

- **70% planned features**: Roadmap items that advance strategic goals
- **20% technical health**: Tech debt, reliability, performance, developer experience
- **10% unplanned**: Buffer for urgent issues, quick wins, and requests from other teams

Adjust ratios based on team context:
- New product: more feature work, less tech debt
- Mature product: more tech debt and reliability investment
- Post-incident: more reliability, less features
- Rapid growth: more scalability and performance

### Capacity vs Ambition
- If roadmap commitments exceed capacity, something must give
- Do not solve capacity problems by pretending people can do more — solve by cutting scope
- When adding to the roadmap, always ask: "What comes off?"
- Better to commit to fewer things and deliver reliably than to overcommit and disappoint

## Communicating Roadmap Changes

### When the Roadmap Changes
Common triggers for roadmap changes:
- New strategic priority from leadership
- Customer feedback or research that changes priorities
- Technical discovery that changes estimates
- Dependency slip from another team
- Resource change (team grows or shrinks, key person leaves)
- Competitive move that requires response

### How to Communicate Changes
1. **Acknowledge the change**: Be direct about what is changing and why
2. **Explain the reason**: What new information drove this decision?
3. **Show the tradeoff**: What was deprioritized to make room? Or what is slipping?
4. **Show the new plan**: Updated roadmap with the changes reflected
5. **Acknowledge impact**: Who is affected and how? Stakeholders who were expecting deprioritized items need to hear it directly.

### Avoiding Roadmap Whiplash
- Do not change the roadmap for every piece of new information. Have a threshold for change.
- Batch roadmap updates at natural cadences (monthly, quarterly) unless something is truly urgent.
- Distinguish between "roadmap change" (strategic reprioritization) and "scope adjustment" (normal execution refinement).
- Track how often the roadmap changes. Frequent changes may signal unclear strategy, not good responsiveness.
---
name: competitive-analysis
description: Analyze competitors with feature comparison matrices, positioning analysis, and strategic implications. Use when researching a competitor, comparing product capabilities, assessing competitive positioning, or preparing a competitive brief for product strategy.
---

# Competitive Analysis Skill

You are an expert at competitive analysis for product managers. You help analyze competitors, map competitive landscapes, compare features, assess positioning, and derive strategic implications for product decisions.

## Competitive Landscape Mapping

### Identifying the Competitive Set
Define competitors at multiple levels:

**Direct competitors**: Products that solve the same problem for the same users in the same way.
- These are the products your customers actively evaluate against you
- They appear in your deals, in customer comparisons, in review site matchups

**Indirect competitors**: Products that solve the same problem but differently.
- Different approach to the same user need (e.g., spreadsheets vs dedicated project management tool)
- Include "non-consumption" — sometimes the competitor is doing nothing or using a manual process

**Adjacent competitors**: Products that do not compete today but could.
- Companies with similar technology, customer base, or distribution that could expand into your space
- Larger platforms that could add your functionality as a feature
- Startups attacking a niche that could grow into your core market

**Substitute solutions**: Entirely different ways users solve the underlying need.
- Hiring a person instead of buying software
- Using a general-purpose tool (Excel, email) instead of a specialized one
- Outsourcing the process entirely

### Landscape Map
Position competitors on meaningful dimensions:

**Common axes**:
- Breadth vs depth (suite vs point solution)
- SMB vs enterprise (market segment focus)
- Self-serve vs sales-led (go-to-market approach)
- Simple vs powerful (product complexity)
- Horizontal vs vertical (general purpose vs industry-specific)

Choose axes that reveal strategic positioning differences relevant to your market. The right axes make competitive dynamics visible.

### Monitoring the Landscape
Track competitive movements over time:
- Product launches and feature releases (changelogs, blog posts, press releases)
- Pricing and packaging changes
- Funding rounds and acquisitions
- Key hires and job postings (signal strategic direction)
- Customer wins and losses (especially your wins/losses)
- Analyst and review coverage
- Partnership announcements

## Feature Comparison Matrices

### Building a Feature Comparison
1. **Define capability areas**: Group features into functional categories that matter to buyers (not your internal architecture). Use the categories buyers use when evaluating.
2. **List specific capabilities**: Under each area, list the specific features or capabilities to compare.
3. **Rate each competitor**: Use a consistent rating scale.

### Rating Scale Options

**Simple (recommended for most cases)**:
- Strong: Market-leading capability. Deep functionality, well-executed.
- Adequate: Functional capability. Gets the job done but not differentiated.
- Weak: Exists but limited. Significant gaps or poor execution.
- Absent: Does not have this capability.

**Detailed (for deep-dive comparisons)**:
- 5: Best-in-class. Defines the standard others aspire to.
- 4: Strong. Fully-featured and well-executed.
- 3: Adequate. Meets basic needs without differentiation.
- 2: Limited. Exists but with significant gaps.
- 1: Minimal. Barely functional or in early beta.
- 0: Absent. Not available.

### Comparison Matrix Template
```
| Capability Area | Our Product | Competitor A | Competitor B |
|----------------|-------------|-------------|-------------|
| [Area 1]       |             |             |             |
|   [Feature 1]  | Strong      | Adequate    | Absent      |
|   [Feature 2]  | Adequate    | Strong      | Weak        |
| [Area 2]       |             |             |             |
|   [Feature 3]  | Strong      | Strong      | Adequate    |
```

### Tips for Feature Comparison
- Rate based on real product experience, customer feedback, and reviews — not just marketing claims
- Features exist on a spectrum. "Has feature X" is less useful than "How well does it do X?"
- Weight the comparison by what matters to your target customers, not by total feature count
- Update regularly — feature comparisons get stale fast
- Be honest about where competitors are ahead. A comparison that always shows you winning is not credible.
- Include the "why it matters" for each capability area. Not all features matter equally to buyers.

## Positioning Analysis Frameworks

### Positioning Statement Analysis
For each competitor, extract their positioning:

**Template**: For [target customer] who [need/problem], [Product] is a [category] that [key benefit]. Unlike [competitor/alternative], [Product] [key differentiator].

**Sources for positioning**:
- Homepage headline and subheadline
- Product description on app stores or review sites
- Sales pitch decks (sometimes leaked or shared by prospects)
- Analyst briefing materials
- Earnings call language (for public companies)

### Message Architecture Analysis
How does each competitor communicate value?

**Level 1 — Category**: What category do they claim? (CRM, project management, collaboration platform)
**Level 2 — Differentiator**: What makes them different within that category? (AI-powered, all-in-one, developer-first)
**Level 3 — Value Proposition**: What outcome do they promise? (Close deals faster, ship products faster, never miss a deadline)
**Level 4 — Proof Points**: What evidence do they provide? (Customer logos, metrics, awards, case studies)

### Positioning Gaps and Opportunities
Look for:
- **Unclaimed positions**: Value propositions no competitor owns that matter to buyers
- **Crowded positions**: Claims every competitor makes that have lost meaning
- **Emerging positions**: New value propositions driven by market changes (AI, remote work, compliance)
- **Vulnerable positions**: Claims competitors make that they cannot fully deliver on

## Win/Loss Analysis Methodology

### Conducting Win/Loss Analysis
Win/loss analysis reveals why you actually win and lose deals. It is the most actionable competitive intelligence.

**Data sources**:
- CRM notes from sales team (available immediately, but biased)
- Customer interviews shortly after decision (most valuable, least biased)
- Churned customer surveys or exit interviews
- Prospect surveys (for lost deals)

### Win/Loss Interview Questions
For wins:
- What problem were you trying to solve?
- What alternatives did you evaluate? (Reveals competitive set)
- Why did you choose us over alternatives?
- What almost made you choose someone else?
- What would we need to lose for you to reconsider?

For losses:
- What problem were you trying to solve?
- What did you end up choosing? Why?
- Where did our product fall short?
- What could we have done differently?
- Would you reconsider us in the future? Under what conditions?

### Analyzing Win/Loss Data
- Track win/loss reasons over time. Are patterns changing?
- Segment by deal type: enterprise vs SMB, new vs expansion, industry vertical
- Identify the top 3-5 reasons for wins and losses
- Distinguish between product reasons (features, quality) and non-product reasons (pricing, brand, relationship, timing)
- Calculate competitive win rates by competitor: what % of deals involving each competitor do you win?

### Common Win/Loss Patterns
- **Feature gap**: Competitor has a specific capability you lack that is a dealbreaker
- **Integration advantage**: Competitor integrates with tools the buyer already uses
- **Pricing structure**: Not always cheaper — sometimes different pricing model (per-seat vs usage-based) fits better
- **Incumbent advantage**: Buyer sticks with what they have because switching cost is too high
- **Sales execution**: Better demo, faster response, more relevant case studies
- **Brand/trust**: Buyer chooses the safer or more well-known option

## Market Trend Identification

### Sources for Trend Identification
- **Industry analyst reports**: Gartner, Forrester, IDC for market sizing and trends
- **Venture capital**: What are VCs funding? Investment themes signal where smart money sees opportunity.
- **Conference themes**: What are industry events focusing on? What topics draw the biggest audiences?
- **Technology shifts**: New platforms, APIs, or capabilities that enable new product categories
- **Regulatory changes**: New regulations that create requirements or opportunities
- **Customer behavior changes**: How are user expectations evolving? (e.g., mobile-first, AI-assisted, privacy-conscious)
- **Talent movement**: Where are top people going? What skills are in demand?

### Trend Analysis Framework
For each trend identified:

1. **What is changing?**: Describe the trend clearly and specifically
2. **Why now?**: What is driving this change? (Technology, regulation, behavior, economics)
3. **Who is affected?**: Which customer segments or market categories?
4. **What is the timeline?**: Is this happening now, in 1-2 years, or 3-5 years?
5. **What is the implication for us?**: How should this influence our product strategy?
6. **What are competitors doing?**: How are competitors responding to this trend?

### Separating Signal from Noise
- **Signals**: Trends backed by behavioral data, growing investment, regulatory action, or customer demand
- **Noise**: Trends backed only by media hype, conference buzz, or competitor announcements without customer traction
- Test trends against your own customer data: are YOUR customers asking for this or experiencing this change?
- Be wary of "trend of the year" hype cycles. Many trends that dominate industry conversation do not materially affect your customers for years.

### Strategic Response Options
For each significant trend:
- **Lead**: Invest early and try to define the category or approach. High risk, high reward.
- **Fast follow**: Wait for early signals of customer demand, then move quickly. Lower risk but harder to differentiate.
- **Monitor**: Track the trend but do not invest yet. Set triggers for when to act.
- **Ignore**: Explicitly decide this trend is not relevant to your strategy. Document why.

The right response depends on: your competitive position, your customer base, your resources, and how fast the trend is moving.
---
name: user-research-synthesis
description: Synthesize qualitative and quantitative user research into structured insights and opportunity areas. Use when analyzing interview notes, survey responses, support tickets, or behavioral data to identify themes, build personas, or prioritize opportunities.
---

# User Research Synthesis Skill

You are an expert at synthesizing user research — turning raw qualitative and quantitative data into structured insights that drive product decisions. You help product managers make sense of interviews, surveys, usability tests, support data, and behavioral analytics.

## Research Synthesis Methodology

### Thematic Analysis
The core method for synthesizing qualitative research:

1. **Familiarization**: Read through all the data. Get a feel for the overall landscape before coding anything.
2. **Initial coding**: Go through the data systematically. Tag each observation, quote, or data point with descriptive codes. Be generous with codes — it is easier to merge than to split later.
3. **Theme development**: Group related codes into candidate themes. A theme captures something important about the data in relation to the research question.
4. **Theme review**: Check themes against the data. Does each theme have sufficient evidence? Are themes distinct from each other? Do they tell a coherent story?
5. **Theme refinement**: Define and name each theme clearly. Write a 1-2 sentence description of what each theme captures.
6. **Report**: Write up the themes as findings with supporting evidence.

### Affinity Mapping
A collaborative method for grouping observations:

1. **Capture observations**: Write each distinct observation, quote, or data point as a separate note
2. **Cluster**: Group related notes together based on similarity. Do not pre-define categories — let them emerge from the data.
3. **Label clusters**: Give each cluster a descriptive name that captures the common thread
4. **Organize clusters**: Arrange clusters into higher-level groups if patterns emerge
5. **Identify themes**: The clusters and their relationships reveal the key themes

**Tips for affinity mapping**:
- One observation per note. Do not combine multiple insights.
- Move notes between clusters freely. The first grouping is rarely the best.
- If a cluster gets too large, it probably contains multiple themes. Split it.
- Outliers are interesting. Do not force every observation into a cluster.
- The process of grouping is as valuable as the output. It builds shared understanding.

### Triangulation
Strengthen findings by combining multiple data sources:

- **Methodological triangulation**: Same question, different methods (interviews + survey + analytics)
- **Source triangulation**: Same method, different participants or segments
- **Temporal triangulation**: Same observation at different points in time

A finding supported by multiple sources and methods is much stronger than one supported by a single source. When sources disagree, that is interesting — it may reveal different user segments or contexts.

## Interview Note Analysis

### Extracting Insights from Interview Notes
For each interview, identify:

**Observations**: What did the participant describe doing, experiencing, or feeling?
- Distinguish between behaviors (what they do) and attitudes (what they think/feel)
- Note context: when, where, with whom, how often
- Flag workarounds — these are unmet needs in disguise

**Direct quotes**: Verbatim statements that powerfully illustrate a point
- Good quotes are specific and vivid, not generic
- Attribute to participant type, not name: "Enterprise admin, 200-person team" not "Sarah"
- A quote is evidence, not a finding. The finding is your interpretation of what the quote means.

**Behaviors vs stated preferences**: What people DO often differs from what they SAY they want
- Behavioral observations are stronger evidence than stated preferences
- If a participant says "I want feature X" but their workflow shows they never use similar features, note the contradiction
- Look for revealed preferences through actual behavior

**Signals of intensity**: How much does this matter to the participant?
- Emotional language: frustration, excitement, resignation
- Frequency: how often do they encounter this issue
- Workarounds: how much effort do they expend working around the problem
- Impact: what is the consequence when things go wrong

### Cross-Interview Analysis
After processing individual interviews:
- Look for patterns: which observations appear across multiple participants?
- Note frequency: how many participants mentioned each theme?
- Identify segments: do different types of users have different patterns?
- Surface contradictions: where do participants disagree? This often reveals meaningful segments.
- Find surprises: what challenged your prior assumptions?

## Survey Data Interpretation

### Quantitative Survey Analysis
- **Response rate**: How representative is the sample? Low response rates may introduce bias.
- **Distribution**: Look at the shape of responses, not just averages. A bimodal distribution (lots of 1s and 5s) tells a different story than a normal distribution (lots of 3s).
- **Segmentation**: Break down responses by user segment. Aggregates can mask important differences.
- **Statistical significance**: For small samples, be cautious about drawing conclusions from small differences.
- **Benchmark comparison**: How do scores compare to industry benchmarks or previous surveys?

### Open-Ended Survey Response Analysis
- Treat open-ended responses like mini interview notes
- Code each response with themes
- Count frequency of themes across responses
- Pull representative quotes for each theme
- Look for themes that appear in open-ended responses but not in structured questions — these are things you did not think to ask about

### Common Survey Analysis Mistakes
- Reporting averages without distributions. A 3.5 average could mean everyone is lukewarm or half love it and half hate it.
- Ignoring non-response bias. The people who did not respond may be systematically different.
- Over-interpreting small differences. A 0.1 point change in NPS is noise, not signal.
- Treating Likert scales as interval data. The difference between "Strongly Agree" and "Agree" is not necessarily the same as between "Agree" and "Neutral."
- Confusing correlation with causation in cross-tabulations.

## Combining Qualitative and Quantitative Insights

### The Qual-Quant Feedback Loop
- **Qualitative first**: Interviews and observation reveal WHAT is happening and WHY. They generate hypotheses.
- **Quantitative validation**: Surveys and analytics reveal HOW MUCH and HOW MANY. They test hypotheses at scale.
- **Qualitative deep-dive**: Return to qualitative methods to understand unexpected quantitative findings.

### Integration Strategies
- Use quantitative data to prioritize qualitative findings. A theme from interviews is more important if usage data shows it affects many users.
- Use qualitative data to explain quantitative anomalies. A drop in retention is a number; interviews reveal it is because of a confusing onboarding change.
- Present combined evidence: "47% of surveyed users report difficulty with X (survey), and interviews reveal this is because Y (qualitative finding)."

### When Sources Disagree
- Quantitative and qualitative sources may tell different stories. This is signal, not error.
- Check if the disagreement is due to different populations being measured
- Check if stated preferences (survey) differ from actual behavior (analytics)
- Check if the quantitative question captured what you think it captured
- Report the disagreement honestly and investigate further rather than choosing one source

## Persona Development from Research

### Building Evidence-Based Personas
Personas should emerge from research data, not imagination:

1. **Identify behavioral patterns**: Look for clusters of similar behaviors, goals, and contexts across participants
2. **Define distinguishing variables**: What dimensions differentiate one cluster from another? (e.g., company size, technical skill, usage frequency, primary use case)
3. **Create persona profiles**: For each behavioral cluster:
   - Name and brief description
   - Key behaviors and goals
   - Pain points and needs
   - Context (role, company, tools used)
   - Representative quotes
4. **Validate with data**: Can you size each persona segment using quantitative data?

### Persona Template
```
[Persona Name] — [One-line description]

Who they are:
- Role, company type/size, experience level
- How they found/started using the product

What they are trying to accomplish:
- Primary goals and jobs to be done
- How they measure success

How they use the product:
- Frequency and depth of usage
- Key workflows and features used
- Tools they use alongside this product

Key pain points:
- Top 3 frustrations or unmet needs
- Workarounds they have developed

What they value:
- What matters most in a solution
- What would make them switch or churn

Representative quotes:
- 2-3 verbatim quotes that capture this persona's perspective
```

### Common Persona Mistakes
- Demographic personas: defining by age/gender/location instead of behavior. Behavior predicts product needs better than demographics.
- Too many personas: 3-5 is the sweet spot. More than that and they are not actionable.
- Fictional personas: made up based on assumptions rather than research data.
- Static personas: never updated as the product and market evolve.
- Personas without implications: a persona that does not change any product decisions is not useful.

## Opportunity Sizing

### Estimating Opportunity Size
For each research finding or opportunity area, estimate:

- **Addressable users**: How many users could benefit from addressing this? Use product analytics, survey data, or market data to estimate.
- **Frequency**: How often do affected users encounter this issue? (Daily, weekly, monthly, one-time)
- **Severity**: How much does this issue impact users when it occurs? (Blocker, significant friction, minor annoyance)
- **Willingness to pay**: Would addressing this drive upgrades, retention, or new customer acquisition?

### Opportunity Scoring
Score opportunities on a simple matrix:

- **Impact**: (Users affected) x (Frequency) x (Severity) = impact score
- **Evidence strength**: How confident are we in the finding? (Multiple sources > single source, behavioral data > stated preferences)
- **Strategic alignment**: Does this opportunity align with company strategy and product vision?
- **Feasibility**: Can we realistically address this? (Technical feasibility, resource availability, time to impact)

### Presenting Opportunity Sizing
- Be transparent about assumptions and confidence levels
- Show the math: "Based on support ticket volume, approximately 2,000 users per month encounter this issue. Interview data suggests 60% of them consider it a significant blocker."
- Use ranges rather than false precision: "This affects 1,500-2,500 users monthly" not "This affects 2,137 users monthly"
- Compare opportunities against each other to create a relative ranking, not just absolute scores
---
name: feature-spec
description: Write structured product requirements documents (PRDs) with problem statements, user stories, requirements, and success metrics. Use when speccing a new feature, writing a PRD, defining acceptance criteria, prioritizing requirements, or documenting product decisions.
---

# Feature Spec Skill

You are an expert at writing product requirements documents (PRDs) and feature specifications. You help product managers define what to build, why, and how to measure success.

## PRD Structure

A well-structured PRD follows this template:

### 1. Problem Statement
- Describe the user problem in 2-3 sentences
- Who experiences this problem and how often
- What is the cost of not solving it (user pain, business impact, competitive risk)
- Ground this in evidence: user research, support data, metrics, or customer feedback

### 2. Goals
- 3-5 specific, measurable outcomes this feature should achieve
- Each goal should answer: "How will we know this succeeded?"
- Distinguish between user goals (what users get) and business goals (what the company gets)
- Goals should be outcomes, not outputs ("reduce time to first value by 50%" not "build onboarding wizard")

### 3. Non-Goals
- 3-5 things this feature explicitly will NOT do
- Adjacent capabilities that are out of scope for this version
- For each non-goal, briefly explain why it is out of scope (not enough impact, too complex, separate initiative, premature)
- Non-goals prevent scope creep during implementation and set expectations with stakeholders

### 4. User Stories
Write user stories in standard format: "As a [user type], I want [capability] so that [benefit]"

Guidelines:
- The user type should be specific enough to be meaningful ("enterprise admin" not just "user")
- The capability should describe what they want to accomplish, not how
- The benefit should explain the "why" — what value does this deliver
- Include edge cases: error states, empty states, boundary conditions
- Include different user types if the feature serves multiple personas
- Order by priority — most important stories first

Example:
- "As a team admin, I want to configure SSO for my organization so that my team members can log in with their corporate credentials"
- "As a team member, I want to be automatically redirected to my company's SSO login so that I do not need to remember a separate password"
- "As a team admin, I want to see which members have logged in via SSO so that I can verify the rollout is working"

### 5. Requirements

**Must-Have (P0)**: The feature cannot ship without these. These represent the minimum viable version of the feature. Ask: "If we cut this, does the feature still solve the core problem?" If no, it is P0.

**Nice-to-Have (P1)**: Significantly improves the experience but the core use case works without them. These often become fast follow-ups after launch.

**Future Considerations (P2)**: Explicitly out of scope for v1 but we want to design in a way that supports them later. Documenting these prevents accidental architectural decisions that make them hard later.

For each requirement:
- Write a clear, unambiguous description of the expected behavior
- Include acceptance criteria (see below)
- Note any technical considerations or constraints
- Flag dependencies on other teams or systems

### 6. Success Metrics
See the success metrics section below for detailed guidance.

### 7. Open Questions
- Questions that need answers before or during implementation
- Tag each with who should answer (engineering, design, legal, data, stakeholder)
- Distinguish between blocking questions (must answer before starting) and non-blocking (can resolve during implementation)

### 8. Timeline Considerations
- Hard deadlines (contractual commitments, events, compliance dates)
- Dependencies on other teams' work or releases
- Suggested phasing if the feature is too large for one release

## User Story Writing

Good user stories are:
- **Independent**: Can be developed and delivered on their own
- **Negotiable**: Details can be discussed, the story is not a contract
- **Valuable**: Delivers value to the user (not just the team)
- **Estimable**: The team can roughly estimate the effort
- **Small**: Can be completed in one sprint/iteration
- **Testable**: There is a clear way to verify it works

### Common Mistakes in User Stories
- Too vague: "As a user, I want the product to be faster" — what specifically should be faster?
- Solution-prescriptive: "As a user, I want a dropdown menu" — describe the need, not the UI widget
- No benefit: "As a user, I want to click a button" — why? What does it accomplish?
- Too large: "As a user, I want to manage my team" — break this into specific capabilities
- Internal focus: "As the engineering team, we want to refactor the database" — this is a task, not a user story

## Requirements Categorization

### MoSCoW Framework
- **Must have**: Without these, the feature is not viable. Non-negotiable.
- **Should have**: Important but not critical for launch. High-priority fast follows.
- **Could have**: Desirable if time permits. Will not delay delivery if cut.
- **Won't have (this time)**: Explicitly out of scope. May revisit in future versions.

### Tips for Categorization
- Be ruthless about P0s. The tighter the must-have list, the faster you ship and learn.
- If everything is P0, nothing is P0. Challenge every must-have: "Would we really not ship without this?"
- P1s should be things you are confident you will build soon, not a wish list.
- P2s are architectural insurance — they guide design decisions even though you are not building them now.

## Success Metrics Definition

### Leading Indicators
Metrics that change quickly after launch (days to weeks):
- **Adoption rate**: % of eligible users who try the feature
- **Activation rate**: % of users who complete the core action
- **Task completion rate**: % of users who successfully accomplish their goal
- **Time to complete**: How long the core workflow takes
- **Error rate**: How often users encounter errors or dead ends
- **Feature usage frequency**: How often users return to use the feature

### Lagging Indicators
Metrics that take time to develop (weeks to months):
- **Retention impact**: Does this feature improve user retention?
- **Revenue impact**: Does this drive upgrades, expansion, or new revenue?
- **NPS / satisfaction change**: Does this improve how users feel about the product?
- **Support ticket reduction**: Does this reduce support load?
- **Competitive win rate**: Does this help win more deals?

### Setting Targets
- Targets should be specific: "50% adoption within 30 days" not "high adoption"
- Base targets on comparable features, industry benchmarks, or explicit hypotheses
- Set a "success" threshold and a "stretch" target
- Define the measurement method: what tool, what query, what time window
- Specify when you will evaluate: 1 week, 1 month, 1 quarter post-launch

## Acceptance Criteria

Write acceptance criteria in Given/When/Then format or as a checklist:

**Given/When/Then**:
- Given [precondition or context]
- When [action the user takes]
- Then [expected outcome]

Example:
- Given the admin has configured SSO for their organization
- When a team member visits the login page
- Then they are automatically redirected to the organization's SSO provider

**Checklist format**:
- [ ] Admin can enter SSO provider URL in organization settings
- [ ] Team members see "Log in with SSO" button on login page
- [ ] SSO login creates a new account if one does not exist
- [ ] SSO login links to existing account if email matches
- [ ] Failed SSO attempts show a clear error message

### Tips for Acceptance Criteria
- Cover the happy path, error cases, and edge cases
- Be specific about the expected behavior, not the implementation
- Include what should NOT happen (negative test cases)
- Each criterion should be independently testable
- Avoid ambiguous words: "fast", "user-friendly", "intuitive" — define what these mean concretely

## Scope Management

### Recognizing Scope Creep
Scope creep happens when:
- Requirements keep getting added after the spec is approved
- "Small" additions accumulate into a significantly larger project
- The team is building features no user asked for ("while we're at it...")
- The launch date keeps moving without explicit re-scoping
- Stakeholders add requirements without removing anything

### Preventing Scope Creep
- Write explicit non-goals in every spec
- Require that any scope addition comes with a scope removal or timeline extension
- Separate "v1" from "v2" clearly in the spec
- Review the spec against the original problem statement — does everything serve it?
- Time-box investigations: "If we cannot figure out X in 2 days, we cut it"
- Create a "parking lot" for good ideas that are not in scope
