---
name: engineering-expert
description: 专业级 engineering 任务处理专家。集成了原 Anthropic 知识工作流，并适配了 Google Workspace 工具链。
---

# engineering Expert Mode

## 领域知识: SKILL.md
---
name: documentation
description: Write and maintain technical documentation. Trigger with "write docs for", "document this", "create a README", "write a runbook", "onboarding guide", or when the user needs help with any form of technical writing — API docs, architecture docs, or operational runbooks.
---

# Technical Documentation

Write clear, maintainable technical documentation for different audiences and purposes.

## Document Types

### README
- What this is and why it exists
- Quick start (< 5 minutes to first success)
- Configuration and usage
- Contributing guide

### API Documentation
- Endpoint reference with request/response examples
- Authentication and error codes
- Rate limits and pagination
- SDK examples

### Runbook
- When to use this runbook
- Prerequisites and access needed
- Step-by-step procedure
- Rollback steps
- Escalation path

### Architecture Doc
- Context and goals
- High-level design with diagrams
- Key decisions and trade-offs
- Data flow and integration points

### Onboarding Guide
- Environment setup
- Key systems and how they connect
- Common tasks with walkthroughs
- Who to ask for what

## Principles

1. **Write for the reader** — Who is reading this and what do they need?
2. **Start with the most useful information** — Don't bury the lede
3. **Show, don't tell** — Code examples, commands, screenshots
4. **Keep it current** — Outdated docs are worse than no docs
5. **Link, don't duplicate** — Reference other docs instead of copying
---
name: incident-response
description: Triage and manage production incidents. Trigger with "we have an incident", "production is down", "something is broken", "there's an outage", "SEV1", or when the user describes a production issue needing immediate response.
---

# Incident Response

Guide incident response from detection through resolution and postmortem.

## Severity Classification

| Level | Criteria | Response Time |
|-------|----------|---------------|
| SEV1 | Service down, all users affected | Immediate, all-hands |
| SEV2 | Major feature degraded, many users affected | Within 15 min |
| SEV3 | Minor feature issue, some users affected | Within 1 hour |
| SEV4 | Cosmetic or low-impact issue | Next business day |

## Response Framework

1. **Triage**: Classify severity, identify scope, assign incident commander
2. **Communicate**: Status page, internal updates, customer comms if needed
3. **Mitigate**: Stop the bleeding first, root cause later
4. **Resolve**: Implement fix, verify, confirm resolution
5. **Postmortem**: Blameless review, 5 whys, action items

## Communication Templates

Provide clear, factual updates at regular cadence. Include: what's happening, who's affected, what we're doing, when the next update is.

## Postmortem Format

Blameless. Focus on systems and processes. Include timeline, root cause analysis (5 whys), what went well, what went poorly, and action items with owners and due dates.
---
name: code-review
description: Review code for bugs, security vulnerabilities, performance issues, and maintainability. Trigger with "review this code", "check this PR", "look at this diff", "is this code safe?", or when the user shares code and asks for feedback.
---

# Code Review

Structured code review covering security, performance, correctness, and maintainability. Works on diffs, PRs, files, or pasted code snippets.

## Review Dimensions

### Security
- SQL injection, XSS, CSRF
- Authentication and authorization flaws
- Secrets or credentials in code
- Insecure deserialization
- Path traversal
- SSRF

### Performance
- N+1 queries
- Unnecessary memory allocations
- Algorithmic complexity (O(n²) in hot paths)
- Missing database indexes
- Unbounded queries or loops
- Resource leaks

### Correctness
- Edge cases (empty input, null, overflow)
- Race conditions and concurrency issues
- Error handling and propagation
- Off-by-one errors
- Type safety

### Maintainability
- Naming clarity
- Single responsibility
- Duplication
- Test coverage
- Documentation for non-obvious logic

## Output Format

Rate each dimension and provide specific, actionable findings with file and line references. Prioritize critical issues first. Always include positive observations alongside issues.
---
name: tech-debt
description: Identify, categorize, and prioritize technical debt. Trigger with "tech debt", "technical debt audit", "what should we refactor", "code health", or when the user asks about code quality, refactoring priorities, or maintenance backlog.
---

# Tech Debt Management

Systematically identify, categorize, and prioritize technical debt.

## Categories

| Type | Examples | Risk |
|------|----------|------|
| **Code debt** | Duplicated logic, poor abstractions, magic numbers | Bugs, slow development |
| **Architecture debt** | Monolith that should be split, wrong data store | Scaling limits |
| **Test debt** | Low coverage, flaky tests, missing integration tests | Regressions ship |
| **Dependency debt** | Outdated libraries, unmaintained dependencies | Security vulns |
| **Documentation debt** | Missing runbooks, outdated READMEs, tribal knowledge | Onboarding pain |
| **Infrastructure debt** | Manual deploys, no monitoring, no IaC | Incidents, slow recovery |

## Prioritization Framework

Score each item on:
- **Impact**: How much does it slow the team down? (1-5)
- **Risk**: What happens if we don't fix it? (1-5)
- **Effort**: How hard is the fix? (1-5, inverted — lower effort = higher priority)

Priority = (Impact + Risk) x (6 - Effort)

## Output

Produce a prioritized list with estimated effort, business justification for each item, and a phased remediation plan that can be done alongside feature work.
---
name: testing-strategy
description: Design test strategies and test plans. Trigger with "how should we test", "test strategy for", "write tests for", "test plan", "what tests do we need", or when the user needs help with testing approaches, coverage, or test architecture.
---

# Testing Strategy

Design effective testing strategies balancing coverage, speed, and maintenance.

## Testing Pyramid

```
        /  E2E  \         Few, slow, high confidence
       / Integration \     Some, medium speed
      /    Unit Tests  \   Many, fast, focused
```

## Strategy by Component Type

- **API endpoints**: Unit tests for business logic, integration tests for HTTP layer, contract tests for consumers
- **Data pipelines**: Input validation, transformation correctness, idempotency tests
- **Frontend**: Component tests, interaction tests, visual regression, accessibility
- **Infrastructure**: Smoke tests, chaos engineering, load tests

## What to Cover

Focus on: business-critical paths, error handling, edge cases, security boundaries, data integrity.

Skip: trivial getters/setters, framework code, one-off scripts.

## Output

Produce a test plan with: what to test, test type for each area, coverage targets, and example test cases. Identify gaps in existing coverage.
---
name: system-design
description: Design systems, services, and architectures. Trigger with "design a system for", "how should we architect", "system design for", "what's the right architecture for", or when the user needs help with API design, data modeling, or service boundaries.
---

# System Design

Help design systems and evaluate architectural decisions.

## Framework

### 1. Requirements Gathering
- Functional requirements (what it does)
- Non-functional requirements (scale, latency, availability, cost)
- Constraints (team size, timeline, existing tech stack)

### 2. High-Level Design
- Component diagram
- Data flow
- API contracts
- Storage choices

### 3. Deep Dive
- Data model design
- API endpoint design (REST, GraphQL, gRPC)
- Caching strategy
- Queue/event design
- Error handling and retry logic

### 4. Scale and Reliability
- Load estimation
- Horizontal vs. vertical scaling
- Failover and redundancy
- Monitoring and alerting

### 5. Trade-off Analysis
- Every decision has trade-offs. Make them explicit.
- Consider: complexity, cost, team familiarity, time to market, maintainability

## Output

Produce clear, structured design documents with diagrams (ASCII or described), explicit assumptions, and trade-off analysis. Always identify what you'd revisit as the system grows.
