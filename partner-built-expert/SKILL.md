---
name: partner-built-expert
description: 专业级 partner-built 任务处理专家。集成了原 Anthropic 知识工作流，并适配了 Google Workspace 工具链。
---

# partner-built Expert Mode

## 领域知识: SKILL.md
---
name: brand-voice-enforcement
description: >
  This skill applies brand guidelines to content creation. It should be used when
  the user asks to "write an email", "draft a proposal", "create a pitch deck",
  "write a LinkedIn post", "draft a presentation", "write a Slack message",
  "draft sales content", or any content creation request where brand voice should
  be applied. Also triggers on "on-brand", "brand voice", "enforce voice",
  "apply brand guidelines", "brand-aligned content", "write in our voice",
  "use our brand tone", "make this sound like us", "rewrite this in our tone",
  or "this doesn't sound on-brand". Not for generating guidelines from scratch
  (use guideline-generation) or discovering brand materials (use discover-brand).
---

# Brand Voice Enforcement

Apply existing brand guidelines to all sales and marketing content generation. Load the user's brand guidelines, apply voice constants and tone flexes to the content request, validate output, and explain brand choices.

## Loading Brand Guidelines

Find the user's brand guidelines using this sequence. Stop as soon as you find them:

1. **Session context** — Check if brand guidelines were generated earlier in this session (via `/brand-voice:generate-guidelines`). If so, they are already in the conversation. Use them directly. Session-generated guidelines are the freshest and reflect the user's most recent intent.

2. **Local guidelines file** — Check for `.claude/brand-voice-guidelines.md` inside the user's working folder. Do NOT use a relative path from the agent's current working directory — in Cowork, the agent runs from a plugin cache directory, not the user's project. Resolve the path relative to the user's working folder. If no working folder is set, skip this step.

3. **Ask the user** — If none of the above found guidelines, tell the user:
   "I couldn't find your brand guidelines. You can:
   - Run `/brand-voice:discover-brand` to find brand materials across your platforms
   - Run `/brand-voice:generate-guidelines` to create guidelines from documents or transcripts
   - Paste guidelines directly into this chat or point me to a file"

   Wait for the user to provide guidelines before proceeding.

Also read `.claude/brand-voice.local.md` for enforcement settings (even if guidelines came from another source):
- `strictness`: strict | balanced | flexible
- `always-explain`: whether to always explain brand choices

## Enforcement Workflow

### 1. Analyze the Content Request

Before writing, identify:
- **Content type**: email, presentation, proposal, social post, message, etc.
- **Target audience**: role, seniority, industry, company stage
- **Key messages needed**: which message pillars apply
- **Specific requirements**: length, format, tone overrides

### 2. Apply Voice Constants

Voice is the brand's personality — it stays constant across all content:
- Apply "We Are / We Are Not" attributes from guidelines
- Use brand personality consistently
- Incorporate approved terminology; reject prohibited terms
- Follow messaging framework and value propositions

Refer to `references/voice-constant-tone-flexes.md` for the "voice constant, tone flexes" model.

### 3. Flex Tone for Context

Tone adapts by content type and audience. Use the tone-by-context matrix from guidelines to set:
- **Formality**: How formal or casual should this be?
- **Energy**: How much urgency or enthusiasm?
- **Technical depth**: How detailed or accessible?

### 4. Generate Content

Create content that:
- Matches brand voice attributes throughout
- Follows tone guidelines for this specific content type
- Incorporates key messages naturally (not forced)
- Uses preferred terminology
- Mirrors the quality and style of guideline examples

For complex or long-form content, delegate to the content-generation agent (defined in `agents/content-generation.md`).
For high-stakes content, delegate to the quality-assurance agent (defined in `agents/quality-assurance.md`) for validation.

### 5. Validate and Explain

After generating content:
- Briefly highlight which brand guidelines were applied
- Explain key voice and tone decisions
- Note any areas where guidelines were adapted for context
- Offer to refine based on feedback

When `always-explain` is true in settings, include brand application notes with every response.

## Handling Conflicts

When the user's request conflicts with brand guidelines:
1. Explain the conflict clearly
2. Provide a recommendation
3. Offer options: follow guidelines strictly, adapt for context, or override

Default to adapting guidelines with an explanation of the tradeoff.

## Open Questions Awareness

Open questions are unresolved brand positioning decisions flagged during guideline generation, stored in the guidelines under an "Open Questions" section. When generating content, check if the brand guidelines contain open questions:
- If content touches an unresolved open question, note it
- Apply the agent's recommendation from the open question unless the user specifies otherwise
- Suggest resolving the question if it significantly impacts the content

## Reference Files

- **`references/voice-constant-tone-flexes.md`** — The "voice constant, tone flexes" mental model, "We Are / We Are Not" table structure, and tone-by-context matrix explanation
- **`references/before-after-examples.md`** — Before/after content examples per content type showing enforcement in practice
---
name: discover-brand
description: >
  This skill orchestrates autonomous discovery of brand materials across enterprise
  platforms (Notion, Confluence, Google Drive, Box, SharePoint, Figma, Gong, Granola, Slack).
  It should be used when the user asks to "discover brand materials",
  "find brand documents", "search for brand guidelines", "audit brand content",
  "what brand materials do we have", "find our style guide", "where are our brand docs",
  "do we have a style guide", "discover brand voice", "brand content audit",
  or "find brand assets".
---

# Brand Discovery

Orchestrate autonomous discovery of brand materials across enterprise platforms. This skill coordinates the discover-brand agent to search connected platforms (Notion, Confluence, Google Drive, Box, Microsoft 365, Figma, Gong, Granola, Slack), triage sources, and produce a structured discovery report with open questions.

## Discovery Workflow

### 0. Orient the User

Before starting, briefly explain what's about to happen so the user knows what to expect:

"Here's how brand discovery works:

1. **Search** — I'll search your connected platforms (Notion, Google Drive, Slack, etc.) for brand-related materials: style guides, pitch decks, templates, transcripts, and more.
2. **Analyze** — I'll categorize and rank what I find, pull the best sources, and produce a discovery report with what I found, any conflicts, and open questions.
3. **Generate guidelines** — Once you've reviewed the report, I can generate a structured brand voice guideline document from the results.
4. **Save** — Guidelines are saved to `.claude/brand-voice-guidelines.md` in your working folder once you approve them. Nothing is written until that step.

The search usually takes a few minutes depending on how many platforms are connected. Ready to get started?"

Wait for the user to confirm before proceeding. If they have questions about the process, answer them first.

### 1. Check Settings

Read `.claude/brand-voice.local.md` if it exists. Extract:
- Company name
- Which platforms are enabled (notion, confluence, google-drive, box, microsoft-365, figma, gong, granola, slack)
- Search depth preference (standard or deep)
- Max sources limit
- Any known brand material locations listed under "Known Brand Materials"

If no settings file exists, proceed with all connected platforms and standard search depth.

### 2. Validate Platform Coverage

Before confirming scope, check which platforms are actually connected and classify them:

**Document platforms** (where brand guidelines, style guides, templates, and decks live):
- Notion, Confluence, Google Drive, Box, Microsoft 365 (SharePoint/OneDrive)

**Supplementary platforms** (valuable for patterns, but not where brand docs are stored):
- Slack, Gong, Granola, Figma

Apply these rules:

1. **If zero document platforms are connected**: **Stop.** Tell the user: "You don't have any document storage platforms connected (Google Drive, SharePoint, Notion, Confluence, or Box). Brand guidelines and style guides almost always live on one of these. Please connect at least one before running discovery. Gong/Granola/Slack transcripts are valuable supplements but unlikely to contain formal brand documents."

2. **If no Google Drive AND no Microsoft 365 AND no Box**: **Warn** (but proceed): "None of your primary file storage platforms (Google Drive, SharePoint, Box) are connected. Brand documents frequently live on these platforms. Discovery will proceed with [connected platforms], but results may have significant gaps. Consider connecting Google Drive or SharePoint."

3. **If only one platform total is connected**: **Warn** (but proceed): "Only [platform] is connected. Discovery works best with 2+ platforms for cross-source validation. Results from a single platform will have lower confidence scores."

### 3. Confirm Scope with User

Before launching discovery, confirm:
- Which platforms to search (default: all connected)
- Whether to include conversation transcripts (Gong, Granola) or just documents
- Any known locations to prioritize

Keep this brief — one question, not a questionnaire.

### 4. Delegate to Discover-Brand Agent

Launch the discover-brand agent via the Task tool. Provide:
- Company name (from settings or user input)
- Enabled platforms
- Search depth
- Any known URLs or locations to check first

The agent executes the 4-phase discovery algorithm autonomously:
1. **Broad Discovery** — parallel searches across platforms
2. **Source Triage** — categorize and rank sources
3. **Deep Fetch** — retrieve and extract from top sources
4. **Discovery Report** — structured output with open questions

### 5. Present Discovery Report

When the agent returns, present the report to the user with a summary:
- Total sources found and analyzed
- Key brand elements discovered
- Any conflicts between sources
- Open questions requiring team input

### 6. Offer Next Steps

After presenting the report, offer:
1. **Generate guidelines now** — chain to `/brand-voice:generate-guidelines` using discovery report as input
2. **Resolve open questions first** — work through high-priority questions before generating
3. **Save report** — store the discovery report to Notion or as a local file
4. **Expand search** — search additional platforms or deeper if coverage is low

## Open Questions

Open questions arise when the discovery agent encounters ambiguity it cannot resolve:
- Conflicting documents (e.g., 2023 style guide vs. 2024 brand update)
- Missing critical sections (e.g., no social media guidelines found)
- Inconsistent terminology across platforms

Every open question includes an agent recommendation. Present questions as "confirm or override" — not dead ends.

## Integration with Other Skills

- **Guideline Generation**: The discovery report is returned by the discover-brand agent via the Task tool. Pass it directly to the guideline-generation skill as structured input, replacing the need for users to manually gather sources.
- **Brand Voice Enforcement**: Once guidelines are generated from discovery, enforcement uses them automatically.

## Error Handling

- If zero platforms are connected, inform the user which platforms the plugin supports and how to connect them.
- If all searches return empty results, flag the discovery as "low coverage" and suggest the user provide documents manually or check platform connections.
- If a platform is connected but returns permission errors, note the gap and continue with other platforms.

## Reference Files

For detailed discovery patterns and algorithms, consult:

- **`references/search-strategies.md`** — Platform-specific search queries, query patterns by platform, and tips for maximizing discovery coverage
- **`references/source-ranking.md`** — Source category definitions, ranking algorithm weights, and triage decision criteria
---
name: guideline-generation
description: >
  This skill generates, creates, or builds brand voice guidelines from source
  materials. It should be used when the user asks to "generate brand guidelines",
  "create a style guide", "extract brand voice", "create guidelines from calls",
  "consolidate brand materials", "analyze my sales calls for brand voice",
  "build a brand playbook from documents", "synthesize a voice and tone guide",
  or uploads brand documents, transcripts, or meeting recordings for brand
  analysis. Also triggers when the user has a discovery report and wants to
  convert it into actionable guidelines.
---

# Guideline Generation

Generate comprehensive, LLM-ready brand voice guidelines from any combination of sources — brand documents, sales call transcripts, discovery reports, or direct user input. Transform raw materials into structured, enforceable guidelines with confidence scoring and open questions.

## Inputs

Accept any combination of:
- **Discovery report** from the discover-brand skill (structured, pre-triaged)
- **Brand documents** uploaded or from connected platforms (PDF, PPTX, DOCX, MD, TXT)
- **Conversation transcripts** from Gong, Granola, manual uploads, or Notion meeting notes
- **Direct user input** about their brand voice and values

When a discovery report is provided, use it as the primary input — sources are already triaged and ranked. Supplement with additional analysis as needed.

## Generation Workflow

### 1. Identify and Classify Sources

Determine what the user has provided. If no sources are available:
- Check if a discovery report exists from a previous `/brand-voice:discover-brand` run
- Check `.claude/brand-voice.local.md` for known brand material locations
- Suggest running discovery first: `/brand-voice:discover-brand`

### 2. Process Sources

**For documents:** Delegate to the document-analysis agent for heavy parsing. Extract voice attributes, messaging themes, terminology, tone guidance, and examples.

**For transcripts:** Delegate to the conversation-analysis agent for pattern recognition. Extract implicit voice attributes, successful language patterns, tone by context, and anti-patterns.

**For discovery reports:** Extract pre-triaged sources, conflicts, and gaps. Use the ranked sources directly.

### 3. Synthesize Into Guidelines

Merge all findings into a unified guideline document following the template in `references/guideline-template.md`. Key sections:

**"We Are / We Are Not" Table** — The core brand identity anchor:

| We Are | We Are Not |
|--------|------------|
| [Attribute — e.g., "Confident"] | [Counter — e.g., "Arrogant"] |
| [Attribute — e.g., "Approachable"] | [Counter — e.g., "Casual or sloppy"] |

Derive attributes from the most consistent patterns across sources. Each row should have supporting evidence.

**Voice Constants vs. Tone Flexes** — Clarify what stays fixed and what adapts:
- **Voice** = personality, values, "We Are / We Are Not" — constant across all content
- **Tone** = formality, energy, technical depth — flexes by context

**Tone-by-Context Matrix:**

| Context | Formality | Energy | Technical Depth | Example |
|---------|-----------|--------|-----------------|---------|
| Cold outreach | Medium | High | Low | "[example phrase]" |
| Enterprise proposal | High | Medium | High | "[example phrase]" |
| Social media | Low | High | Low | "[example phrase]" |

### 4. Assign Confidence Scores

Score each section using the methodology in `references/confidence-scoring.md`:
- **High confidence**: 3+ corroborating sources, explicit guidance found
- **Medium confidence**: 1-2 sources, or inferred from patterns
- **Low confidence**: Single source, inferred, or conflicting data

### 5. Surface Open Questions

Generate open questions for any ambiguity that cannot be resolved:

```markdown
## Open Questions for Team Discussion

### High Priority (blocks guideline completion)
1. **[Question Title]**
   - What was found: [conflicting or incomplete info]
   - Agent recommendation: [suggested resolution with reasoning]
   - Need from you: [specific decision or confirmation needed]
```

Every open question MUST include an agent recommendation. Turn ambiguity into "confirm or override" — never a dead end.

### 6. Quality Check

Before presenting, verify via the quality-assurance agent (defined in `agents/quality-assurance.md`):
- All major sections populated (including Brand Personality and Content Examples if sources support them)
- At least 3 voice attributes with evidence
- "We Are / We Are Not" table has 4+ rows
- Tone matrix covers at least 3 contexts
- Confidence scores assigned per section
- Source attribution for all extracted elements
- No PII exposed
- Open questions include recommendations

### 7. Present and Offer Next Steps

Summarize key findings:
- Total sections generated with confidence breakdown
- Strongest voice attribute and most effective message
- Number of open questions (if any)

### 8. Save for Future Sessions

The default save location is `.claude/brand-voice-guidelines.md` inside the user's working folder.

**Important:** The agent's working directory may not be the user's project root (especially in Cowork, where plugins run from a plugin cache directory). Always resolve the path relative to the user's working folder, not the current working directory. If no working folder is set, skip the file save and tell the user guidelines will only be available in this conversation.

1. **Resolve the save path.** The file MUST be saved to `.claude/brand-voice-guidelines.md` inside the user's working folder. Confirm the working folder path before writing.
2. **Check if guidelines already exist** at that path
3. **If they exist, archive the previous version:** Rename the existing file to `brand-voice-guidelines-YYYY-MM-DD.md` in the same directory (using today's date)
4. **Save new guidelines** to `.claude/brand-voice-guidelines.md` inside the working folder
5. **Confirm to the user** with the full absolute path: "Guidelines saved to `<full-path>`. `/brand-voice:enforce-voice` will find them automatically in future sessions."

The guidelines are also present in this conversation, so `/brand-voice:enforce-voice` can use them immediately without loading from file.

After saving, offer:
1. Walk through the guidelines section by section
2. Start creating content with `/brand-voice:enforce-voice`
3. Resolve open questions

## Privacy and Security

Enforce these privacy constraints throughout the entire generation workflow, not only at output time:
- Redact customer names and contact information from all examples
- Anonymize company names in transcript excerpts if requested
- Flag any sensitive information detected during processing

## Reference Files

- **`references/guideline-template.md`** — Complete output template with all sections, field definitions, and formatting guidance
- **`references/confidence-scoring.md`** — Confidence scoring methodology, thresholds, and examples
---
name: prospect
description: "Full ICP-to-leads pipeline. Describe your ideal customer in plain English and get a ranked table of enriched decision-maker leads with emails and phone numbers."
user-invocable: true
argument-hint: "[describe your ideal customer]"
---

# Prospect

Go from an ICP description to a ranked, enriched lead list in one shot. The user describes their ideal customer via "$ARGUMENTS".

## Examples

- `/apollo:prospect VP of Engineering at Series B+ SaaS companies in the US, 200-1000 employees`
- `/apollo:prospect heads of marketing at e-commerce companies in Europe`
- `/apollo:prospect CTOs at fintech startups, 50-500 employees, New York`
- `/apollo:prospect procurement managers at manufacturing companies with 1000+ employees`
- `/apollo:prospect SDR leaders at companies using Salesforce and Outreach`

## Step 1 — Parse the ICP

Extract structured filters from the natural language description in "$ARGUMENTS":

**Company filters:**
- Industry/vertical keywords → `q_organization_keyword_tags`
- Employee count ranges → `organization_num_employees_ranges`
- Company locations → `organization_locations`
- Specific domains → `q_organization_domains_list`

**Person filters:**
- Job titles → `person_titles`
- Seniority levels → `person_seniorities`
- Person locations → `person_locations`

If the ICP is vague, ask 1-2 clarifying questions before proceeding. At minimum, you need a title/role and an industry or company size.

## Step 2 — Search for Companies

Use `mcp__claude_ai_Apollo_MCP__apollo_mixed_companies_search` with the company filters:
- `q_organization_keyword_tags` for industry/vertical
- `organization_num_employees_ranges` for size
- `organization_locations` for geography
- Set `per_page` to 25

## Step 3 — Enrich Top Companies

Use `mcp__claude_ai_Apollo_MCP__apollo_organizations_bulk_enrich` with the domains from the top 10 results. This reveals revenue, funding, headcount, and firmographic data to help rank companies.

## Step 4 — Find Decision Makers

Use `mcp__claude_ai_Apollo_MCP__apollo_mixed_people_api_search` with:
- `person_titles` and `person_seniorities` from the ICP
- `q_organization_domains_list` scoped to the enriched company domains
- `per_page` set to 25

## Step 5 — Enrich Top Leads

> **Credit warning**: Tell the user exactly how many credits will be consumed before proceeding.

Use `mcp__claude_ai_Apollo_MCP__apollo_people_bulk_match` to enrich up to 10 leads per call with:
- `first_name`, `last_name`, `domain` for each person
- `reveal_personal_emails` set to `true`

If more than 10 leads, batch into multiple calls.

## Step 6 — Present the Lead Table

Show results in a ranked table:

### Leads matching: [ICP Summary]

| # | Name | Title | Company | Employees | Revenue | Email | Phone | ICP Fit |
|---|---|---|---|---|---|---|---|---|

**ICP Fit** scoring:
- **Strong** — title, seniority, company size, and industry all match
- **Good** — 3 of 4 criteria match
- **Partial** — 2 of 4 criteria match

**Summary**: Found X leads across Y companies. Z credits consumed.

## Step 7 — Offer Next Actions

Ask the user:

1. **Save all to Apollo** — Bulk-create contacts via `mcp__claude_ai_Apollo_MCP__apollo_contacts_create` with `run_dedupe: true` for each lead
2. **Load into a sequence** — Ask which sequence and run the sequence-load flow for these contacts
3. **Deep-dive a company** — Run `/apollo:company-intel` on any company from the list
4. **Refine the search** — Adjust filters and re-run
5. **Export** — Format leads as a CSV-style table for easy copy-paste
---
name: enrich-lead
description: "Instant lead enrichment. Drop a name, company, LinkedIn URL, or email and get the full contact card with email, phone, title, company intel, and next actions."
user-invocable: true
argument-hint: "[name, company, LinkedIn URL, or email]"
---

# Enrich Lead

Turn any identifier into a full contact dossier. The user provides identifying info via "$ARGUMENTS".

## Examples

- `/apollo:enrich-lead Tim Zheng at Apollo`
- `/apollo:enrich-lead https://www.linkedin.com/in/timzheng`
- `/apollo:enrich-lead sarah@stripe.com`
- `/apollo:enrich-lead Jane Smith, VP Engineering, Notion`
- `/apollo:enrich-lead CEO of Figma`

## Step 1 — Parse Input

From "$ARGUMENTS", extract every identifier available:
- First name, last name
- Company name or domain
- LinkedIn URL
- Email address
- Job title (use as a matching hint)

If the input is ambiguous (e.g. just "CEO of Figma"), first use `mcp__claude_ai_Apollo_MCP__apollo_mixed_people_api_search` with relevant title and domain filters to identify the person, then proceed to enrichment.

## Step 2 — Enrich the Person

> **Credit warning**: Tell the user enrichment consumes 1 Apollo credit before calling.

Use `mcp__claude_ai_Apollo_MCP__apollo_people_match` with all available identifiers:
- `first_name`, `last_name` if name is known
- `domain` or `organization_name` if company is known
- `linkedin_url` if LinkedIn is provided
- `email` if email is provided
- Set `reveal_personal_emails` to `true`

If the match fails, try `mcp__claude_ai_Apollo_MCP__apollo_mixed_people_api_search` with looser filters and present the top 3 candidates. Ask the user to pick one, then re-enrich.

## Step 3 — Enrich Their Company

Use `mcp__claude_ai_Apollo_MCP__apollo_organizations_enrich` with the person's company domain to pull firmographic context.

## Step 4 — Present the Contact Card

Format the output exactly like this:

---

**[Full Name]** | [Title]
[Company Name] · [Industry] · [Employee Count] employees

| Field | Detail |
|---|---|
| Email (work) | ... |
| Email (personal) | ... (if revealed) |
| Phone (direct) | ... |
| Phone (mobile) | ... |
| Phone (corporate) | ... |
| Location | City, State, Country |
| LinkedIn | URL |
| Company Domain | ... |
| Company Revenue | Range |
| Company Funding | Total raised |
| Company HQ | Location |

---

## Step 5 — Offer Next Actions

Ask the user which action to take:

1. **Save to Apollo** — Create this person as a contact via `mcp__claude_ai_Apollo_MCP__apollo_contacts_create` with `run_dedupe: true`
2. **Add to a sequence** — Ask which sequence, then run the sequence-load flow
3. **Find colleagues** — Search for more people at the same company using `mcp__claude_ai_Apollo_MCP__apollo_mixed_people_api_search` with `q_organization_domains_list` set to this company
4. **Find similar people** — Search for people with the same title/seniority at other companies
---
name: sequence-load
description: "Find leads matching criteria and bulk-add them to an Apollo outreach sequence. Handles enrichment, contact creation, deduplication, and enrollment in one flow."
user-invocable: true
argument-hint: "[targeting criteria + sequence name]"
---

# Sequence Load

Find, enrich, and load contacts into an outreach sequence — end to end. The user provides targeting criteria and a sequence name via "$ARGUMENTS".

## Examples

- `/apollo:sequence-load add 20 VP Sales at SaaS companies to my "Q1 Outbound" sequence`
- `/apollo:sequence-load SDR managers at fintech startups → Cold Outreach v2`
- `/apollo:sequence-load list sequences` (shows all available sequences)
- `/apollo:sequence-load directors of engineering, 500+ employees, US → Demo Follow-up`
- `/apollo:sequence-load reload 15 more leads into "Enterprise Pipeline"`

## Step 1 — Parse Input

From "$ARGUMENTS", extract:

**Targeting criteria:**
- Job titles → `person_titles`
- Seniority levels → `person_seniorities`
- Industry keywords → `q_organization_keyword_tags`
- Company size → `organization_num_employees_ranges`
- Locations → `person_locations` or `organization_locations`

**Sequence info:**
- Sequence name (text after "to", "into", or "→")
- Volume — how many contacts to add (default: 10 if not specified)

If the user just says "list sequences", skip to Step 2 and show all available sequences.

## Step 2 — Find the Sequence

Use `mcp__claude_ai_Apollo_MCP__apollo_emailer_campaigns_search` to find the target sequence:
- Set `q_name` to the sequence name from input

If no match or multiple matches:
- Show all available sequences in a table: | Name | ID | Status |
- Ask the user to pick one

## Step 3 — Get Email Account

Use `mcp__claude_ai_Apollo_MCP__apollo_email_accounts_index` to list linked email accounts.

- If one account → use automatically
- If multiple → show them and ask which to send from

## Step 4 — Find Matching People

Use `mcp__claude_ai_Apollo_MCP__apollo_mixed_people_api_search` with the targeting criteria.
- Set `per_page` to the requested volume (or 10 by default)

Present the candidates in a preview table:

| # | Name | Title | Company | Location |
|---|---|---|---|---|

Ask: **"Add these [N] contacts to [Sequence Name]? This will consume [N] Apollo credits for enrichment."**

Wait for confirmation before proceeding.

## Step 5 — Enrich and Create Contacts

For each approved lead:

1. **Enrich** — Use `mcp__claude_ai_Apollo_MCP__apollo_people_bulk_match` (batch up to 10 per call) with:
   - `first_name`, `last_name`, `domain` for each person
   - `reveal_personal_emails` set to `true`

2. **Create contacts** — For each enriched person, use `mcp__claude_ai_Apollo_MCP__apollo_contacts_create` with:
   - `first_name`, `last_name`, `email`, `title`, `organization_name`
   - `direct_phone` or `mobile_phone` if available
   - `run_dedupe` set to `true`

Collect all created contact IDs.

## Step 6 — Add to Sequence

Use `mcp__claude_ai_Apollo_MCP__apollo_emailer_campaigns_add_contact_ids` with:
- `id`: the sequence ID
- `emailer_campaign_id`: same sequence ID
- `contact_ids`: array of created contact IDs
- `send_email_from_email_account_id`: the chosen email account ID
- `sequence_active_in_other_campaigns`: `false` (safe default)

## Step 7 — Confirm Enrollment

Show a summary:

---

**Sequence loaded successfully**

| Field | Value |
|---|---|
| Sequence | [Name] |
| Contacts added | [count] |
| Sending from | [email address] |
| Credits used | [count] |

**Contacts enrolled:**

| Name | Title | Company | Email |
|---|---|---|---|

---

## Step 8 — Offer Next Actions

Ask the user:

1. **Load more** — Find and add another batch of leads
2. **Review sequence** — Show sequence details and all enrolled contacts
3. **Remove a contact** — Use `mcp__claude_ai_Apollo_MCP__apollo_emailer_campaigns_remove_or_stop_contact_ids` to remove specific contacts
4. **Pause a contact** — Re-add with `status: "paused"` and an `auto_unpause_at` date
---
name: slack-messaging
description: Guidance for composing well-formatted, effective Slack messages using mrkdwn syntax
---

# Slack Messaging Best Practices

This skill provides guidance for composing well-formatted, effective Slack messages.

## When to Use

Apply this skill whenever composing, drafting, or helping the user write a Slack message — including when using `slack_send_message`, `slack_send_message_draft`, or `slack_create_canvas`.

## Slack Formatting (mrkdwn)

Slack uses its own markup syntax called **mrkdwn**, which differs from standard Markdown. Always use mrkdwn when composing Slack messages:

| Format | Syntax | Notes |
|--------|--------|-------|
| Bold | `*text*` | Single asterisks, NOT double |
| Italic | `_text_` | Underscores |
| Strikethrough | `~text~` | Tildes |
| Code (inline) | `` `code` `` | Backticks |
| Code block | `` ```code``` `` | Triple backticks |
| Quote | `> text` | Angle bracket |
| Link | `<url\|display text>` | Pipe-separated in angle brackets |
| User mention | `<@U123456>` | User ID in angle brackets |
| Channel mention | `<#C123456>` | Channel ID in angle brackets |
| Bulleted list | `- item` or `• item` | Dash or bullet character |
| Numbered list | `1. item` | Number followed by period |

### Common Mistakes to Avoid

- Do NOT use `**bold**` (double asterisks) — Slack uses `*bold*` (single asterisks)
- Do NOT use `## headers` — Slack does not support Markdown headers. Use `*bold text*` on its own line instead.
- Do NOT use `[text](url)` for links — Slack uses `<url|text>` format
- Do NOT use `---` for horizontal rules — Slack does not render these

## Message Structure Guidelines

- **Lead with the point.** Put the most important information in the first line. Many people read Slack on mobile or in notifications where only the first line shows.
- **Keep it short.** Aim for 1-3 short paragraphs. If the message is long, consider using a Canvas instead.
- **Use line breaks generously.** Walls of text are hard to read. Separate distinct thoughts with blank lines.
- **Use bullet points for lists.** Anything with 3+ items should be a list, not a run-on sentence.
- **Bold key information.** Use `*bold*` for names, dates, deadlines, and action items so they stand out when scanning.

## Thread vs. Channel Etiquette

- **Reply in threads** when responding to a specific message to keep the main channel clean.
- **Use `reply_broadcast`** (also post to channel) only when the reply contains information everyone needs to see.
- **Post in the channel** (not a thread) when starting a new topic, making an announcement, or asking a question to the whole group.
- **Don't start a new thread** to continue an existing conversation — find and reply to the original message.

## Tone and Audience

- Match the tone to the channel — `#general` is usually more formal than `#random`.
- Use emoji reactions instead of reply messages for simple acknowledgments (though note: the MCP tools can't add reactions, so suggest the user do this manually if appropriate).
- When writing announcements, use a clear structure: context, key info, call to action.
---
name: slack-search
description: Guidance for effectively searching Slack to find messages, files, channels, and people
---

# Slack Search

This skill provides guidance for effectively searching Slack to find messages, files, and information.

## When to Use

Apply this skill whenever you need to find information in Slack — including when a user asks you to locate messages, conversations, files, or people, or when you need to gather context before answering a question about what's happening in Slack.

## Search Tools Overview

| Tool | Use When |
|------|----------|
| `slack_search_public` | Searching public channels only. Does not require user consent. |
| `slack_search_public_and_private` | Searching all channels including private, DMs, and group DMs. Requires user consent. |
| `slack_search_channels` | Finding channels by name or description. |
| `slack_search_users` | Finding people by name, email, or role. |

## Search Strategy

### Start Broad, Then Narrow

1. Begin with a simple keyword or natural language question.
2. If too many results, add filters (`in:`, `from:`, date ranges).
3. If too few results, remove filters and try synonyms or related terms.

### Choose the Right Search Mode

- **Natural language questions** (e.g., "What is the deadline for project X?") — Best for fuzzy, conceptual searches where you don't know exact keywords.
- **Keyword search** (e.g., `project X deadline`) — Best for finding specific, exact content.

### Use Multiple Searches

Don't rely on a single search. Break complex questions into smaller searches:
- Search for the topic first
- Then search for specific people's contributions
- Then search in specific channels

## Search Modifiers Reference

### Location Filters
- `in:channel-name` — Search within a specific channel
- `in:<#C123456>` — Search in channel by ID
- `-in:channel-name` — Exclude a channel
- `in:<@U123456>` — Search in DMs with a user

### User Filters
- `from:<@U123456>` — Messages from a specific user (by ID)
- `from:username` — Messages from a user (by Slack username)
- `to:me` — Messages sent directly to you

### Content Filters
- `is:thread` — Only threaded messages
- `has:pin` — Pinned messages
- `has:link` — Messages containing links
- `has:file` — Messages with file attachments
- `has::emoji:` — Messages with a specific reaction

### Date Filters
- `before:YYYY-MM-DD` — Messages before a date
- `after:YYYY-MM-DD` — Messages after a date
- `on:YYYY-MM-DD` — Messages on a specific date
- `during:month` — Messages during a specific month (e.g., `during:january`)

### Text Matching
- `"exact phrase"` — Match an exact phrase
- `-word` — Exclude messages containing a word
- `wild*` — Wildcard matching (minimum 3 characters before `*`)

## File Search

To search for files, use the `content_types="files"` parameter with type filters:
- `type:images` — Image files
- `type:documents` — Document files
- `type:pdfs` — PDF files
- `type:spreadsheets` — Spreadsheet files
- `type:canvases` — Slack Canvases

Example: `content_types="files" type:pdfs budget after:2025-01-01`

## Following Up on Results

After finding relevant messages:
- Use `slack_read_thread` to get the full thread context for any threaded message.
- Use `slack_read_channel` with `oldest`/`latest` timestamps to read surrounding messages for context.
- Use `slack_read_user_profile` to identify who a user is when their ID appears in results.

## Common Pitfalls

- **Boolean operators don't work.** `AND`, `OR`, `NOT` are not supported. Use spaces (implicit AND) and `-` for exclusion.
- **Parentheses don't work.** Don't try to group search terms with `()`.
- **Search is not real-time.** Very recent messages (last few seconds) may not appear in search results. Use `slack_read_channel` for the most recent messages.
- **Private channel access.** Use `slack_search_public_and_private` when you need to include private channels, but note this requires user consent.
---
name: contact-research
description: "Research a specific person using Common Room data. Triggers on 'who is [name]', 'look up [email]', 'research [contact]', 'is [name] a warm lead', or any contact-level question."
---

# Contact Research

Retrieve a comprehensive contact profile from Common Room. Supports lookup by email, social handle, or name + company. Returns enriched data including activity history, Spark, scores, website visits, and CRM fields.

## Step 1: Locate the Contact

Common Room supports multiple lookup methods — use whichever the user has provided:

| What the user gives | Lookup method |
|---------------------|--------------|
| Email address | Look up by email (most reliable) |
| LinkedIn, Twitter/X, or GitHub handle | Look up by social handle — specify handle type explicitly |
| Name + company | Identity resolution by name + org domain; present matches if ambiguous |
| Name only | Search by name; if multiple matches, show a brief list and ask the user to confirm |

If no match is found, respond: "Common Room doesn't have a record for this person." Do not speculate or fabricate profile data.

## Step 2: Fetch Contact Fields

Use the Common Room object catalog to see available field groups and their contents. For full profiles, request all groups. For targeted questions, request only what's relevant.

**Key field groups to know about:**
- **Scores** — always return as raw values or percentiles, never labels
- **Recent activity** — use `Contact Initiated` filter (last 60 days) for their actions, not your team's
- **Website visits** — total count + specific pages (last 12 weeks)
- **Spark** — retrieve all Sparks when tracking engagement evolution over time

## Step 3: Run Spark Enrichment (If Available)

If Spark is available, use it. Spark provides:
- Professional background and job history
- Social presence and influence signals
- Persona classification: Champion, Economic Buyer, Technical Evaluator, End User, or Gatekeeper
- Inferred role in the buying process

If Spark is unavailable but real activity data exists (recent actions, website visits, community engagement), infer a persona from those signals. If neither Spark nor activity data is available, classify as Unknown — do not guess a persona from title alone.

Retrieve **all Sparks** (not just the most recent) when the user wants to understand how this contact's engagement has evolved over time.

## Step 4: Assess Account Context

Pull an abbreviated account snapshot for this contact's parent company. Note:
- Open opportunities, expansion signals, or churn risk at the account level
- Whether other contacts at this company are also active
- How this person's engagement compares to their colleagues

## Step 5: Identify Conversation Angles

Based on activity and signals, surface the strongest 2–3 hooks:
- A recent `Contact Initiated` activity (community post, product event, support ticket)
- A specific web page they visited recently — especially if it signals evaluation intent
- A job change, promotion, or company news
- Their Spark persona and what that suggests about communication style
- Their role in a known active deal

## Output Format

Only include sections where data was actually returned. Omit sections with no data rather than filling them with guesses.

**When data is rich:**

```
## [Contact Name] — Profile

**Overview**
[2 sentences: who they are, their role, and relationship status]

**Details**
- Title: [title]
- Company: [company]
- Email: [email]
- LinkedIn: [URL]
- Other profiles: [Twitter/X, GitHub, CRM link if available]

**Scores** [If scores returned]
[All scores as raw values or percentiles]

**Recent Activity** (last 60 days) [If activity returned]
[3–5 bullets with dates]

**Website Visits** (last 12 weeks) [If visit data exists]
[Total visit count + list of pages visited]

**Spark Profile** [If Spark data is non-null]
[Persona type, background summary, influence signals]

**Segments** [If segments returned]
[List of segment names this contact belongs to]

**Account Context**
[1–2 sentences on their company's status]

**Conversation Starters**
[2–3 specific, signal-backed openers]
```

**When data is sparse (e.g., only name, title, email, tags returned; sparkSummary is null):**

```
## [Contact Name] — Profile (Limited Data)

**Data available:** [List exactly what Common Room returned]

[Present only the returned fields]

**Web Search**
[Any findings from searching their name + company]

**Note:** Common Room has limited data on this contact. No activity history, scores, or Spark profile available. I can run deeper web searches or look up their company for additional context.
```

Do not generate conversation starters, persona inferences, or engagement assessments from sparse data. These require real signals.

## Quality Standards

- Lookup must use the correct method for the input type — don't guess on email vs. handle
- Scores as raw/percentile only — never labels
- `Contact Initiated` activity (last 60 days) is the primary engagement signal — lead with it
- If Spark is unavailable, say so — don't fabricate a persona from title alone
- Flag any contact where the most recent activity is older than 30 days

## Reference Files

- **`references/contact-signals-guide.md`** — full field descriptions, Spark persona guide, and conversation starter principles
---
name: prospect
description: "Build targeted account or contact lists using Common Room's Prospector. Triggers on 'find companies that match [criteria]', 'build a prospect list', 'find contacts at [type of company]', 'show me companies hiring [role]', or any list-building request."
---

# Prospecting

Build targeted account and contact lists using Common Room's Prospector. Supports iterative refinement through natural conversation, intent-based discovery, and both net-new prospecting and signal-based queries against existing accounts.

## Critical Distinction: Two Object Types

Common Room's Prospector operates against two fundamentally different object types. Always clarify which one is in play before running a query:

**`ProspectorOrganization`** — Companies **not yet in Common Room**
- Net-new companies that match specified criteria
- Available fields are firmographic only: name, domain, size, industry, capital raised, annual revenue, location
- Fewer filter options — no signal-based filters, no scores, no activity history
- Use when: building a brand-new target list, territory planning, top-of-funnel expansion

**`Organization`** (in Common Room) — Companies **already in your CR workspace**
- Full signal data available: product usage, community activity, CRM fields, scores, custom fields
- Much richer filter set — includes signal-based, score-based, segment-based, and firmographic filters
- Use when: finding warm accounts to prioritize, identifying expansion candidates, surfacing intent signals within existing pipeline

When a user's request could apply to both (e.g., "Show companies hiring AI engineers this month"), clarify:
> "Are you looking for net-new companies not yet in Common Room, or filtering accounts already in your workspace?"

The catalog should make this distinction explicit so the LLM can select the right Prospector endpoint.

## Step 0: Load User Context (Me)

Fetch the `Me` object to get the user's segments. When prospecting against `Organization` records (accounts already in CR), default to filtering within "My Segments" unless the user asks for a broader search.

## Step 1: Gather Targeting Criteria

If criteria are already provided, proceed. Otherwise ask:

> "What kind of accounts or contacts are you looking for? For example: company size, industry, job titles, signals like recent product activity or community engagement, geographic region, or specific intent signals like recent funding or job postings."

Use the Common Room object catalog to see available filters for each object type. The key distinction:
- **ProspectorOrganization** — firmographic and technographic filters only (industry, size, geography, funding, tech stack)
- **Organization** — all firmographic filters plus signal-based, score-based, segment-based, and CRM filters

**Lookalike search:** If the user asks to "find companies like [X]", first look up the reference company in Common Room (or via web search if not in CR). Extract its key attributes — industry, employee range, tech stack, funding stage, geography — and propose those as filter criteria. Present the derived criteria to the user for confirmation before running the search, since lookalike targeting works best when the user can refine which attributes matter most.

## Step 2: Support Iterative Refinement

Prospecting is conversational. Support multi-turn refinement naturally:

1. Run initial query with provided criteria
2. If results are large (50+), summarize and offer: "I found [N] results. Want to narrow by [suggested filter]?"
3. If results are too few (< 5), suggest: "Only [N] results with those filters — I can broaden by relaxing [specific criterion]."
4. Apply each refinement as a follow-up query, not a new search from scratch

Example flow:
- Rep: "Find cybersecurity companies in California." → 500 results
- Rep: "Only show ones over 300 employees using AWS." → 47 results
- Rep: "Focus on the ones with recent hiring activity." → 12 results ✓

## Step 3: Run the Query and Present Results

Execute the Prospector query with confirmed criteria. Sort by signal strength or fit score where available (not alphabetically).

**For `ProspectorOrganization` (net-new) results:**

| Company | Domain | Industry | Size | Capital Raised | Revenue | Location |
|---------|--------|----------|------|---------------|---------|----------|

**For `Organization` (in CR) results:**

| Company | Industry | Size | Top Signal | Signal Date | Score | CRM Stage |
|---------|----------|------|-----------|-------------|-------|-----------|

Flag any results where data is thin or the most recent signal is older than 90 days.

## Step 3.5: Enrich Net-New Results with Web Search

For `ProspectorOrganization` results (net-new companies not in CR), run a quick web search on the top 3–5 companies to add context beyond firmographics. CR has no behavioral signals for these companies, so web search fills the gap — look for recent funding, product launches, leadership changes, or news coverage. Include findings as brief annotations next to each company in the results.

## Step 4: Offer Next Steps

- "Want me to draft outreach for the top 3–5 prospects?"
- "Should I run a full account brief on any of these?"
- "Want to refine the criteria or add another filter?"
- "I can format this as a CSV if you'd like to export it."
- "For any net-new companies here, I can add them to Common Room for enrichment." *(future capability)*

## Quality Standards

- Always confirm which object type (ProspectorOrg vs Organization) before running the query
- Default to "My Segments" when querying Organization records, unless user specifies otherwise
- Support iterative refinement — treat each follow-up as a filter adjustment, not a fresh start
- Never mix result fields from ProspectorOrganization and Organization in the same list
- Fewer high-quality results beat a long unqualified list
- **Only show data the query returned** — leave blank or "—" for missing fields, don't invent values

## Reference Files

- **`references/prospect-guide.md`** — filter types, signal-based sorting, object type distinctions, and list-building strategies
---
name: compose-outreach
description: "Generate personalized outreach messages using Common Room signals. Triggers on 'draft outreach to [person]', 'write an email to [name]', 'compose a message for [contact]', or any outreach drafting request."
---

# Compose Outreach

Generate three personalized outreach formats — email, call script, and LinkedIn message — grounded in Common Room signals for a specific company or contact.

## Outreach Process

### Step 1: Look Up the Target

Use Common Room MCP tools to find and retrieve data for the target (company and/or specific contact). Pull:
- Recent product activity and engagement signals
- Community activity (posts, questions, reactions)
- 3rd-party intent signals (job postings, news, funding)
- Relationship history (prior contact, meetings, email opens)

If the user specified a person, run contact-level research. If only a company was given, identify the best contact to target based on title, engagement, and role.

### Step 2: Web Search for External Hooks (If CR Signals Are Thin)

If CR returned strong signals (recent activity, engagement, product usage), those should drive personalization — skip web search. If CR signals are thin or the prospect has little CR activity, run a web search for external hooks:

**What to search:**
- `"[company name]" funding OR acquisition OR launch OR announcement` — last 30 days
- `"[contact full name]" "[company name]"` — look for recent articles, interviews, LinkedIn posts, or conference talks

**Prioritize external hooks that are:**
- Very recent (< 2 weeks) — the prospect is likely still thinking about it
- Publicly visible — they know you could have seen it
- Change-signaling — growth, new role, new product, new market

If the user explicitly asks for web search or external hooks, run it regardless of CR signal richness.

### Step 3: Spark Enrichment (If Available)

If Spark is available, run enrichment on the target contact to get persona classification, background, and influence signals. Use this to calibrate tone and message angle.

### Step 4: Identify the Best Hooks

From the signal data, identify the 1–3 strongest personalization hooks. Rank by:
1. **Recency** — happened in the last 7–14 days
2. **Specificity** — a concrete action they took, not a general trend
3. **Relevance** — connects directly to a value your product delivers

Good hooks: posted a question in the community about X, just hired 5 engineers, recently started using [feature], company just raised Series B, trial nearing expiration, champion just changed jobs.

Bad hooks: "I noticed you're a customer" or generic industry trends.

### Step 5: Generate All Three Formats

Use the strongest hooks to write all three formats. Each format has different constraints and conventions — follow the format-specific guidelines in `references/outreach-formats-guide.md`.

Always produce all three, clearly labeled.

When the user's company context is available (see `references/my-company-context.md`), ground the value bridge and pitch in the user's specific product and positioning.

### Step 6: Annotate Your Choices

After the three drafts, include a brief note (2–4 sentences) explaining:
- Which signals were used and why they were chosen
- Any assumptions made (e.g., inferred call objective)
- Alternative angles if the primary hook doesn't land

## Output Format

```
## Outreach for [Name / Company]

### 📧 Email

**Subject:** [Subject line]

[Email body — 3–5 sentences]

---

### 📞 Call Script

**Opening:**
[Opening line — conversational, 1–2 sentences]

**Value Bridge:**
[Why you're calling and why now — 2–3 sentences tied to a signal]

**Ask:**
[Single, low-friction ask — e.g., 15-minute call, specific question]

---

### 💼 LinkedIn Message

[Under 300 characters. Warm, personal, no pitch.]

---

### Signal Notes
[2–4 sentences: which signals were used, why, and any alternative angles]
```

## When Signal Data Is Sparse

If Common Room returns minimal data on the target (e.g., just name, title, tags — no activity, no scores, no Spark):

1. **Do not draft outreach from thin air.** Outreach grounded in fabricated signals is worse than no outreach.
2. **Run web search first** — this becomes your primary personalization source. Look for recent news, LinkedIn posts, conference talks, company announcements.
3. **If web search also returns little**, present what you have honestly and ask the user for context:

```
## Outreach for [Name / Company] — Limited Data

**What I found:**
[Only the real data from CR and web search]

**I don't have enough signal to draft personalized outreach yet.** To write something strong, I'd need:
- Recent activity or engagement signals
- Context you have from prior conversations
- A specific reason for reaching out now

Can you share any of the above?
```

## Quality Standards

- Every message must reference something specific — generic outreach is not acceptable output
- Match tone to context: warm and conversational for inbound/community signals; more formal for cold/executive outreach
- The LinkedIn message must be under 300 characters — no exceptions
- The call script must be speakable naturally — read it aloud mentally to check rhythm
- **Never fabricate signals** — only reference data retrieved from Common Room or web search

## Reference Files

- **`references/outreach-formats-guide.md`** — detailed format rules, examples, and tone guidelines for each channel
---
name: account-research
description: "Research a company using Common Room data. Triggers on 'research [company]', 'tell me about [domain]', 'pull up signals for [account]', 'what's going on with [company]', or any account-level question."
---

# Account Research

Retrieve and synthesize account information from Common Room. Handles four interaction patterns: full overviews, targeted field questions, sparse data situations, and combined MCP data + LLM reasoning.

## Step 0: Load User Context (Me)

Before researching any account, fetch the `Me` object from Common Room. This provides:
- The user's profile, title, role, and Persona in CR
- The user's segments ("My Segments")

Default all queries to the user's own segments unless the user explicitly asks for a broader view. This keeps results scoped to their territory.

## Step 1: Identify the Interaction Pattern

Determine what the user actually needs before deciding how much data to fetch:

**Pattern 1 — Full Overview:** "Tell me about Datadog" / "Summarize cloudflare.com"
→ Fetch the full field set and produce a structured briefing.

**Pattern 2 — Targeted Question:** "Who owns the Snowflake account?" / "Is acme.io showing buying signals?" / "What's the employee count for notion.so?"
→ Fetch only the relevant field(s). Return a direct, concise answer — do not produce a full brief for a simple question.

**Pattern 3 — Sparse Data:** "Tell me about tiny-startup.io"
→ If Common Room has limited data for an account, say so honestly: "There is limited information available for this account." Never speculate or fill gaps with generic statements.

**Pattern 4 — Combined Reasoning:** Fetch structured MCP data, then layer in LLM analysis — e.g., "Stripe has 8,000 employees and is hiring heavily for AI roles. Based on your ICP of 1k–10k fintech companies, this is a strong fit."

## Step 2: Look Up the Account

Search Common Room for the account by domain or company name. Exact match first; if no result, try partial match and confirm with the user before proceeding.

## Step 3: Fetch the Right Fields

Use the Common Room object catalog to see available field groups and their contents. For full overviews, request all field groups. For targeted questions, request only what's relevant.

**Key field groups to know about:**
- **Scores** — always return as raw values or percentiles, never labels
- **Summary research** — RoomieAI output; often the richest qualitative signal
- **Top contacts** — sorted by score desc; use communityMemberID for full lookups

**Choosing what to fetch:**

| User query type | Fields to request |
|-----------------|------------------|
| Full account overview | All field groups |
| "Who owns this account?" | Company profiles & links, CRM fields |
| "Is this company a good fit?" | Key fields, scores, about |
| "What signals is this account showing?" | Scores, summary research, CRM fields |
| "Who are the top contacts?" | Top contacts |
| "What does RoomieAI say about them?" | Summary research, all research |
| "Find engineers at this account" | Prospects (with title filter) |

## Step 4: Web Search (Sparse Data Only)

Common Room is the primary data source. Do not run web search when CR returns rich data.

When CR data is sparse (Pattern 3 — few fields returned, no activity, no scores), run a targeted web search to fill gaps:
- `"[company name]" news` — scoped to the last 30 days
- Look for: funding rounds, acquisitions, product launches, executive changes, press coverage

If the user explicitly asks for external context or recent news, run web search regardless of data richness.

## Step 5: Apply Reasoning (Pattern 4)

When the user's question invites synthesis — not just data retrieval — layer in analysis:
- Compare account data to known ICP criteria from session context
- Identify fit signals (size, industry, tech stack, hiring patterns)
- Note timing signals (funding, trial status, recent activity spike)
- Frame insights as clearly derived from data, not assumed

When the user's company context is available (see `references/my-company-context.md`), position findings relative to the user's value proposition and ICP.

## Step 6: Produce Output

Only include sections where Common Room returned actual data. Omit sections entirely rather than filling them with guesses.

**Full overview (when data is rich):**

```
## [Company Name] — Account Overview

**Snapshot**
[2–3 sentences: what they do, plan/stage, relationship status]

**Key Details**
[Employee count, industry, location, domain, funding — from key fields]

**CRM & Ownership** [If CRM fields returned]
[Owner, opp stage, ARR]

**Scores** [If scores returned]
[All available scores as raw values or percentiles]

**Signal Highlights** [If activity/signals exist]
[3–5 most important signals with dates]

**Top Contacts** [If contacts returned]
[Name | Title | Score — top 5 sorted by score desc]

**RoomieAI Research** [If summary research is non-null]
[Summary research output; list all available research topic names]

**Recommended Next Steps**
[2–3 specific, signal-backed actions]
```

**Targeted question:** 1–3 sentence direct answer. No full brief needed.

**Sparse data (few fields returned, most sections would be empty):**

```
## [Company Name] — Account Overview (Limited Data)

**Data available:** [List exactly what Common Room returned]

[Present only the returned fields]

**Web Search**
[Findings from web search — or "No significant recent news found"]

**Note:** Common Room has limited data on this account. The account may need enrichment in Common Room.
```

## Quality Standards

- Scores must always be raw values or percentiles — never categorical labels
- For targeted questions, answer precisely and don't over-deliver
- Be explicit when data is missing or stale — don't speculate
- Keep full briefings readable in 2–3 minutes
- **Every fact must trace to a tool call** — don't include data not returned by Common Room

## Reference Files

- **`references/signals-guide.md`** — signal type taxonomy and interpretation guide

---
name: weekly-prep-brief
description: "Generate a comprehensive weekly briefing for all external calls in the next 7 days. Triggers on 'weekly prep brief', 'prepare my week', 'what calls do I have this week', 'Monday prep', or any weekly planning request."
---

# Weekly Prep Brief

Generate a single comprehensive weekly briefing that covers every external customer or prospect call in the next 7 days, with per-meeting account and contact research from Common Room.

## Briefing Process

### Step 1: Get the Week's External Meetings

**Option A — Calendar connected:**
Use the `~~calendar` connector to fetch all meetings scheduled in the next 7 days (or a user-specified range). Filter to keep only external meetings — those with attendees from outside your organization. Discard internal-only meetings, one-on-ones with colleagues, and recurring internal syncs.

Identify for each external meeting:
- Company name
- Meeting date and time
- External attendee names and email addresses

**Option B — No calendar connected:**
Ask the user: "To build your weekly prep brief, I'll need your upcoming external calls. Please list them: company name, date/time, and attendee names."

Accept freeform input and parse it into a structured list before proceeding.

### Step 2: Confirm the Meeting List

Present the identified meetings to the user for confirmation before beginning research:

> "Here are the external calls I found for this week. Let me know if anything's missing or should be excluded:
> - [Company] — [Day], [Time] — [Attendees]
> - ..."

This prevents wasted research on cancelled or incorrect meetings.

### Step 3: Research Each Meeting

For each confirmed external meeting, run in parallel where possible:
1. **Account research** — full account snapshot using the account-research skill
2. **Contact research** — profile for each external attendee using the contact-research skill

Common Room data is the primary source. After CR research, run a quick **recency check** for each company — this is supplementary, not primary:
- Search `"[company name]" news` scoped to the last 7 days
- For executive attendees, search their name for recent public posts or interviews
- Only include findings that are genuinely noteworthy (funding, leadership changes, major press). Don't pad the brief with generic news.

Depth calibration:
- For high-priority accounts (large accounts, open opportunities, renewal risk), produce full depth research
- For lower-priority or short meetings, produce abbreviated snapshots (3–4 bullets each)

### Step 4: Synthesize the Weekly Brief

Compile all per-meeting research into a single structured document, sorted by meeting date/time.

Open with a brief week-level overview that flags:
- Any accounts with urgent signals (at-risk, trial expiring, expansion opportunity)
- Any meetings that need special preparation or executive involvement
- Total external call count and estimated time commitment

## Output Format

```
# Weekly Prep Brief — Week of [Date]

## Week Overview
[2–4 bullets: key themes, flagged priorities, call count]

---

## [Monday / Tuesday / etc.]

### [Company Name] — [Time]
**Attendees:** [Names and titles]
**Meeting type:** [Discovery / QBR / Renewal / Expansion / etc. — inferred if possible]

**Company Snapshot**
[4–5 bullets: account status, top signals, recent activity]

**Attendee Profiles**
- **[Name]** ([Title]): [2–3 bullets on their signals, persona, conversation angle]
- [Repeat per attendee]

**Top Signals This Week**
[2–3 most relevant signals for this specific call]

**This Week's News** [If notable news found]
[Only genuinely noteworthy findings — funding, leadership changes, major press]

**Recommended Objectives**
[1–2 sentences: what to accomplish in this meeting]

---

[Repeat per meeting, sorted by date/time]
```

## When a Meeting Has Sparse Data

If Common Room returns limited data for a particular meeting's account or attendees, use a compressed format for that meeting instead of the full template:

```
### [Company Name] — [Time] ⚠️ Limited Data
**Attendees:** [Names and titles if known]
**Data available:** [What Common Room actually returned]

**Web Search Results**
[Findings from web search — company news, attendee LinkedIn profiles]

**Note:** Common Room has limited data on this account. The rep may want to check directly in CR or gather context from colleagues before this call.
```

Do not generate a full meeting prep section (company snapshot, signal highlights, talking points, recommended objectives) from sparse data. A short honest section is more useful than a fabricated full one.

## Quality Standards

- Keep each meeting section scannable — reps read these in the morning, often on mobile
- Always sort by date/time ascending
- Flag urgent situations prominently (risk, trial expiration, open opps) — don't bury them
- If a meeting has very thin Common Room data, use the sparse-data format above — never fill the full template with guesses
- Total brief should be readable in 10–15 minutes for a week with 4–6 meetings
- **Every fact must come from a tool call** — no invented deal context, activity, or signals

## Reference Files

- **`references/briefing-guide.md`** — guidelines for structuring briefings, prioritization logic, and how to handle edge cases (cancelled meetings, new accounts with no data, etc.)
---
name: call-prep
description: "Prepare for a customer or prospect call using Common Room signals. Triggers on 'prep me for my call with [company]', 'prepare for a meeting with [company]', 'what should I know before talking to [company]', or any call preparation request."
---

# Call Prep

Produce a complete, scannable call prep brief by combining account research, contact research, and signal synthesis from Common Room.

## Prep Process

### Step 1: Identify the Account and Attendees

Parse what the user has provided:
- **Company name** — required; look up the account in Common Room
- **Attendee names** — optional; if provided, research each one

**Calendar lookup:** If a `~~calendar` connector is available, search for upcoming meetings with the named company to automatically surface attendee names, meeting time, and any meeting notes or agenda. Use this to fill gaps the user didn't provide.

If neither attendees nor a calendar match can be found, ask: "Who will be on the call from [Company]? I can research each attendee to make your prep more useful."

### Step 2: Run Account Research

Use the account-research skill process to build a full account snapshot. For call prep, prioritize:
- Recent product signals (what are they doing in the product right now?)
- Open opportunities or renewal timeline
- Any risk signals (declining usage, support tickets, churned seats)
- Key recent events (funding, executive change, new hire)

When reviewing activity history, prioritize Gong and call recording activities — these provide direct context about previous conversations. Do not filter out call recordings by activity origin.

### Step 3: Run Contact Research for Each Attendee

For each external attendee, use the contact-research skill process. For call prep, focus on:
- Role and influence in the buying process
- Their personal activity and engagement history
- Any recent signals that suggest their current mood/priorities
- Spark persona classification if available

### Step 4: Synthesize Talking Points and Objectives

Based on the combined account and contact research:
- Identify the **call objective** (e.g., discovery, demo, expansion conversation, renewal, QBR)
- Generate **3–5 tailored talking points** grounded in specific signal data
- Anticipate **2–3 likely objections or topics** the customer may raise
- Suggest a **recommended outcome** for the call

When the user's company context is available (see `references/my-company-context.md`), tailor talking points to the user's product and value proposition.

### Step 5: Recency Check (Web Search)

After gathering all Common Room data, run a quick recency check to catch anything that happened since the last CR data sync. This is supplementary — CR data drives the prep; web search only adds recency.

**Company news:** Search `"[company name]" news` filtered to the last 14 days. Look for funding announcements, product launches, leadership changes, layoffs, partnerships, or press coverage.

**Attendee presence:** For each external attendee, search `"[full name]" "[company name]"` — look for recent articles, LinkedIn posts, conference talks, podcasts, or published opinions.

If a company news item is significant (e.g., just raised a round, announced a major hire), flag it in Signal Highlights. Otherwise, include findings briefly — don't let web search results overshadow CR signals.

## Output Format

The output adapts to how much data Common Room returned. Only include sections where you have real data. Never fill a section with invented details.

### When data is rich (multiple field groups returned, activity history, scores, signals):

```
## Call Prep: [Company] — [Date/Time if known]

**Meeting Context**
[Attendees, meeting type, and any known agenda]

---

### Company Snapshot
[4–6 bullets: key account status, signals, and recent activity]

---

### Attendee Profiles

**[Attendee Name] — [Title]**
[3–4 bullets: role, recent activity, Spark persona if available, personal hook]

[Repeat for each attendee]

---

### Signal Highlights
[Top 3 signals most relevant to this specific call]

---

### Talking Points
1. [Point tied to a specific signal]
2. [Point tied to a specific signal]
3. [Point tied to a specific signal]

### Likely Topics / Objections to Prepare For
- [Topic or objection + suggested response]
- [Topic or objection + suggested response]

### Recommended Call Outcome
[1–2 sentences: what success looks like for this meeting]
```

### When data is sparse (few fields returned, no activity, null sparkSummary):

```
## Call Prep: [Company] — [Date/Time if known]

**Data available:** [List exactly what Common Room returned — e.g., "Name, title, email, two tags. No activity history, no scores, no Spark data."]

### What I Found
[Only the fields actually returned, presented as-is]

### Web Search Results
[Findings from web search on the company and attendees — or "No significant results"]

### Suggested Next Steps
- I can pull [specific field groups] from Common Room if available
- I can run deeper web searches on [specific topics]
- You may want to check Common Room directly for [what's missing]
```

Do not generate a full call prep brief from sparse data. A short honest output is always better than a long fabricated one.

## Quality Standards

- Ground every talking point in a real signal — no generic filler
- Keep the brief tight — it should be readable in 5 minutes or less
- Flag unknowns explicitly — if attendee research is thin, say so
- Time-box the research — don't over-research at the expense of speed
- **Never invent deal context** — no fabricated proposals, competitor comparisons, pricing, trial terms, or objections not returned by a tool call

## Reference Files

- **`references/call-types-guide.md`** — guidance for different call types (discovery, expansion, renewal, QBR) and how to tailor prep accordingly
