---
name: trigify-tools
description: MUST USE for ANY Trigify operation — searches, workflows, enrichment, X/Twitter, Jarvis, credits, testing, or anything involving social listening and workflow automation. This skill contains critical rules about testing procedures and search design that prevent common mistakes. Trigger this skill even for simple tasks like "test this workflow", "create a search", "check credits", or "send a test event". Also trigger when the user mentions social listening, keyword monitoring, track competitors, monitor brand, capture engagers, enrich profile, enrich company, post on X, signal detection — even if the task seems straightforward. Skipping this skill leads to fabricated test data and poorly designed searches.
---

# Trigify Tools Guide

Help users create effective social listening searches and automated workflows using Trigify.

## Core Philosophy

1. **Be a consultant, not an order taker.** Most users don't know what's possible with social listening. Guide them by suggesting signal types and use cases.
2. **Searches cast a broad net. Workflows extract specific signals.** Don't over-filter in the search — the AI agents in workflows do the precision work.
3. **Always look up examples first.** Before building a workflow, look up existing workflow examples to see proven patterns. Don't reinvent the wheel.
4. **Test with real data. NEVER fabricate test posts.** When testing workflows, ALWAYS pull actual posts from the attached search first, then use a real post as the test payload. Fabricated/dummy posts produce misleading test results.

---

## Capabilities at a Glance

| Category | Key Operations | When to Use |
|----------|---------------|-------------|
| **Searches** | Create, list, get results, update, delete | Setting up social listening for keywords or profiles |
| **Workflows** | Create, list examples, test, execute, modify | Automating actions on social listening data |
| **Enrichment** | Enrich profile, enrich company | Getting LinkedIn data (title, company, email) for a person or company |
| **X/Twitter** | Post, reply, like, repost, follow, DM, lookup user | Managing X accounts and engagement |
| **Jarvis AI** | Start conversation, send message, check task | Natural language workflow building |
| **Content** | Get post by URL, get comments, get profile posts | Analyzing specific posts or profiles |
| **Integrations** | List integrations, check health, get CRM fields | Checking connected tools (CRM, Slack, etc.) |
| **Credits** | Check balance, usage breakdown | Checking account usage and remaining credits |
| **Tracking** | Bulk track profiles, remove tracked profile | Monitoring specific LinkedIn/Twitter profiles |

---

## Part 1: Creating Effective Searches

A search is the foundation — it defines what content Trigify captures from social media. Getting this right determines everything downstream.

### Signal-Oriented Discovery

Before asking about keywords or platforms, understand the user's goal. Ask:

> "At a high level, are you looking to **generate leads/pipeline** or **gather market intelligence**?"

Then suggest specific signal types based on their answer.

**Sales/Growth signals:** Competitor Engagement Capture, Pain Point Discovery, Dissatisfied Customer Signals, High-Intent Topic Monitoring, Comparison Shopping, Funding Signals, Hiring Signals, Champion Movement Tracking.

**Marketing Intelligence signals:** Brand Mention Monitoring, Sentiment Shift Detection, Share of Voice, Content Trend Detection, Question Mining, Competitor Content Analysis, Feature Request Mining.

Once a signal type is chosen, explain:
> "I'll create a search that captures [category of content] broadly. Then we'll build a workflow with AI to extract [specific signal] from those results."

### Boolean Query Rules

**Read `references/search-guide.md` before creating any search** — it has the full Boolean query reference, platform-specific rules, and keyword strategy patterns. The critical rules summarized here:

- **6 keywords max** across OR + AND + NOT combined (except Instagram: 30 hashtags, OR only)
- **OR** = primary terms to capture (match any)
- **AND** = context to narrow (must also contain all)
- **NOT** = noise exclusion (exclude posts with any)
- **Don't over-filter** — use 2-3 OR terms, 1-2 AND for context, 1-2 NOT for noise
- **Split into multiple searches** when you need more precision (no downside — multiple searches can feed one workflow)

### Creating the Search

Key parameters when creating a search:
- `name` — descriptive name reflecting the signal type
- `keywords` — OR keywords (required for keyword searches)
- `keywordsAnd` — AND keywords (optional, for context)
- `keywordsNot` — NOT keywords (optional, for exclusion)
- `monitoringType` — platform + type (see reference for full list)
- `frequency` — how often to check (DAILY, WEEKLY, etc.)

**Keyword searches:** `linkedin-posts`, `twitter-posts`, `reddit-posts`, `youtube-videos`, `podcast-keywords`
**Profile monitoring:** `linkedin-profile`, `twitter-profile`, `youtube-channel`, `podcast-episodes`

### When to Use Profile vs Keyword Monitoring

- **Profile monitoring**: Track what a specific person/company posts ("monitor our CEO's LinkedIn")
- **Keyword monitoring**: Find posts about a topic across many authors ("find people talking about CRM pain points")
- **Brand monitoring**: Use BOTH — keyword search for what people say about you, profile search for your own posts

### Multi-Search Strategy

Proactively suggest splitting when:
- Tracking 2+ competitors → each gets its own focused search
- Need different context terms per topic
- Boolean logic needs > 6 keywords
- Different platforms need different keyword strategies

Frame it positively: "I'd recommend 2 searches — one for [X], one for [Y]. Both can feed the same workflow, but you'll get more targeted results."

---

## Part 2: Building Workflows

Workflows automate what happens when searches find content: enrich profiles, filter by ICP, send to CRM, notify Slack, etc.

### MANDATORY: Look Up Examples First

**Before creating any workflow, ALWAYS look up existing workflow examples.** This returns proven patterns you can adapt. Don't build from scratch when a tested example exists.

After reviewing examples, if building a custom workflow, look up all available action nodes to see what's possible.

### Workflow Patterns

**Read `references/workflow-patterns.md` before creating any workflow** — it has detailed patterns, decision trees, and examples. Quick reference:

| User Goal | Pattern | Key Components |
|-----------|---------|----------------|
| Enriched leads for outreach | Loop → Enrich → CRM | Loop, person enrichment, CRM action |
| Real-time alerts | Direct → Notify | Slack notification |
| Weekly summary | Scheduled → AI → Send | Fetch results, AI agent, Slack/email |
| Qualified leads only | Loop → Enrich → IF → CRM | Loop, enrichment, IF condition, CRM |
| Sentiment routing | Analyze → IF chain → Route | Sentiment agent, chained IF nodes |

### Trigger Selection

| User Intent | Trigger Type | Why |
|-------------|-------------|-----|
| Automate a single search | New Post | Simplest — fires per-post in real-time |
| Multiple searches, same logic | Multi-Post | Consolidation, deduplication |
| Batch summaries/digests | Scheduled | Use with fetch_search_results for date ranges |
| Chain workflows | Signal Created | Separate detection from action logic |
| External data | Webhook | CRM events, form submissions, Zapier/Make |

**Common mistake:** Using a real-time trigger for digests. "Summarize what competitors posted this week" = scheduled trigger + fetch, NOT a per-post trigger with AI on every post.

### Testing Workflows (CRITICAL)

**Always test before publishing. NEVER fabricate test data.**

#### For new-post triggered workflows (most common)

Every workflow with a new-post or multi-post trigger has a saved search attached to it. That search has already collected real posts. You MUST use one of those real posts as your test data. Here's the exact procedure:

1. **Get the workflow** to find which saved search is attached to it
2. **Get results from that saved search** to retrieve actual posts it has collected
3. **Pick a real post** from those results (ideally a recent one with engagement)
4. **Send that real post as the test payload** — pass the actual `text`, `authorUrl`, `postUrl`, `source`, `likes`, `comments`, `datePosted` fields from the real post
5. **Review the execution** to check each step passed with real data

**Why this matters:** Fabricated posts have fake author URLs that fail enrichment, fake text that produces meaningless AI analysis, and fake engagement numbers that skew filtering. Real posts test the entire pipeline end-to-end.

#### For scheduled workflows

Trigger the test normally — it simulates the scheduled execution and will pull its own data via fetch_search_results.

#### For webhook workflows

Provide a sample payload matching the expected schema.

#### After any test

Review the workflow execution to check each step's status. Verify enrichment returned data, AI analysis was meaningful, and outputs reached the destination.

### Credit-Saving Patterns

Credits matter — enrichment is where most get spent. Always filter BEFORE enriching:

**Bad:** Trigger → Person Enrichment → Email → IF (ICP check) → CRM
*(19 credits per post, even non-ICP contacts)*

**Good:** Trigger → Person Enrichment → IF (ICP check) → Email → CRM
*(4 credits for non-ICP, 19 only for qualified leads)*

**AI node selection:**
- Sentiment analysis → use the sentiment agent (2 credits, structured output)
- Custom analysis, scoring, summaries → use the general AI agent (variable credits)
- Always default to Claude Sonnet for AI agents — outperforms other options

---

## Part 3: Other Common Tasks

### Enrichment

- **Profile enrichment** — LinkedIn person data (name, title, company, location, email). Needs a LinkedIn URL.
- **Company enrichment** — Company data (size, industry, location). Needs a company name or domain.

### X/Twitter Management

Check connected accounts first. Then:
- Create posts, reply to tweets, like, repost, follow
- Send direct messages
- Look up user details by username

### Jarvis AI (Natural Language Workflows)

For users who prefer describing what they want in plain English:
1. Start a new Jarvis conversation
2. Describe the workflow in natural language
3. Poll for completion
4. Jarvis creates the search and/or workflow automatically

### Integration Health

Before building workflows that depend on integrations:
1. Check what's connected (list integrations)
2. Verify connections are working (health check)
3. Get field mappings for CRM fields, Slack channels, Notion databases, etc.

### Credits & Usage

- Check remaining credit balance
- View usage breakdown over time
- View per-feature breakdown
- 1 credit = 1 post monitored or 1 workflow action

---

## Reference Files (MUST READ when relevant)

These files are bundled with this skill. Read them before taking action — they contain critical details not covered above.

- **`references/search-guide.md`** — **Read before creating any search.** Contains Boolean query rules, platform-specific requirements (monitoring types, keyword limits, profile parameters), keyword strategy patterns per use case, and the multi-search splitting strategy.
- **`references/workflow-patterns.md`** — **Read before creating or modifying any workflow.** Contains decision trees for choosing triggers, enrichment nodes, AI nodes, and destinations. Includes full workflow pattern examples, signal-to-AI-prompt mapping, testing procedures, and the modification process for existing workflows.

---

# Search Creation Reference

## Boolean Field Structure

Each search has exactly THREE keyword fields. All keywords within a field are combined with that field's logic.

| Field | Logic | Purpose |
|-------|-------|---------|
| OR (`keywords`) | Match ANY | Primary terms to capture |
| AND (`keywordsAnd`) | Must ALSO contain ALL | Context to narrow results |
| NOT (`keywordsNot`) | Exclude ANY | Filter out noise |

**Total across all three fields: max 6 keywords** (except Instagram hashtags: 30, OR only).

You cannot have multiple AND groups or multiple OR groups. If you need more complex logic, split into multiple searches.

## Typical Keyword Structures

- 1 OR + 1 AND + 2 NOT = 4 keywords (focused, room to spare)
- 2 OR + 1 AND + 2 NOT = 5 keywords (good balance)
- 2 OR + 2 AND + 2 NOT = 6 keywords (maximum, fully used)

## Detecting Broad Keywords

**Red flags (too broad):**
- Single common words: "AI", "sales", "marketing", "growth", "tech", "data"
- Industry buzzwords without context: "automation", "cloud", "digital"
- Generic actions: "hiring", "looking for", "need help"
- Common words that are also brand names: "Clay", "Unify", "Notion"

**Good, specific keywords:**
- Unique brand names: "Trigify", "HubSpot", "Salesforce"
- Multi-word phrases: "sales enablement", "revenue operations"
- Specific use cases: "cold email templates", "LinkedIn automation"
- Problem statements: "CRM not syncing", "lead scoring broken"

**When keywords are broad:** Don't just create the search. Explain the issue and offer options:
1. User adds context keywords
2. Research the topic online and suggest keywords
3. Keep it broad (user accepts noise)

**Never assume context keywords.** If a keyword is generic (e.g., "Clay"), don't guess what AND/NOT terms to add. Ask the user.

## Boolean Strategy by Use Case

**Brand Monitoring:**
```
OR: ["CompanyName", "ProductName", "@handle"]
NOT: ["jobs", "hiring", "career"]
```

**Competitor Intelligence:**
```
OR: ["Competitor1", "Competitor2"]
AND: ["review", "alternative"]
NOT: ["jobs", "hiring"]
```

**Lead Generation (Pain Points):**
```
OR: ["struggling with", "hate my", "anyone recommend"]
AND: ["CRM", "sales tool"]
```

**Dissatisfied Competitor Customers:**
```
OR: ["CompetitorName"]
AND: ["alternative", "vs", "switched"]
NOT: ["jobs", "hiring"]
```
Note: Don't try to capture frustration with keywords like "hate" or "frustrated" — the AI agent in the workflow is better at detecting sentiment than Boolean logic.

**Industry Trends:**
```
OR: ["social listening", "social monitoring"]
AND: ["trends", "report"]
```

## Multi-Search Strategy

Splitting into multiple searches is almost always better. There is NO downside — multiple searches can feed into a single workflow via the Multi-Post trigger.

**When to split:**
- Tracking 2+ competitors (each gets focused AND/NOT terms)
- Brand monitoring + competitor tracking (separate concerns)
- Need > 6 keywords for precision
- Different context terms per topic

**Example — Competitor Tracking:**

Instead of one search: `OR: ["Competitor1", "Competitor2", "review", "alternative"]` (4 keywords, no room for NOT)

Create two:
- Search 1: `OR: ["Competitor1"] AND: ["review", "alternative"] NOT: ["jobs"]`
- Search 2: `OR: ["Competitor2"] AND: ["review", "alternative"] NOT: ["jobs"]`

Both trigger the same workflow. Result: more precise, less noise.

## Platform-Specific Rules

### Keyword Searches

| Platform | monitoring_type | Keyword Limit | Boolean |
|----------|-----------------|---------------|---------|
| LinkedIn Posts | `linkedin-posts` | 6 total | OR + AND + NOT |
| Twitter/X Posts | `twitter-posts` | 6 total | OR + AND + NOT |
| Reddit | `reddit-posts` | 6 total | OR + AND + NOT |
| YouTube Videos | `youtube-videos` | 6 total | OR + AND + NOT |
| Podcasts | `podcast-keywords` | 6 total | OR + AND + NOT |
| Instagram Hashtags | `instagram-hashtag` | 30 hashtags | OR only |

### Profile Monitoring

| Platform | monitoring_type | Key Parameter |
|----------|-----------------|---------------|
| LinkedIn Profile | `linkedin-profile` | `profileUrl` |
| Twitter Profile | `twitter-profile` | `twitterProfileUrl` or `twitterUserId` |
| YouTube Channel | `youtube-channel` | `channelUrl` |
| Podcast Episodes | `podcast-episodes` | `podcastId` |
| Instagram Profile | `instagram-profile` | `instagramUsername` |

### Common Options (All Platforms)

- `frequency` — DAILY, WEEKLY, MONTHLY, QUARTERLY
- `maxResults` — 1-100 (default 50)
- `timeFrame` — past-24h, past-week, past-month, all-time

### LinkedIn-Specific Options

- `jobTitles` — Filter by job title (array)
- `contentType` — "videos", "photos", "documents", etc.
- `linkedinSortBy` — "date_posted" or "relevance"

### Instagram-Specific Rules

- 30 hashtags maximum, OR logic only (no AND/NOT)
- Hashtags entered without the # symbol
- `instagramSortBy` — "top" or "recent"

## Profile vs Keyword: When to Use Which

**Profile monitoring** when:
- Track a specific person's or company's posts
- "Monitor what our CEO posts"
- "Track competitor's official account"
- Goal is "see everything they post"

**Keyword monitoring** when:
- Find posts ABOUT a topic across many authors
- Catch mentions by anyone
- Goal is content discovery

**Brand monitoring — two-search strategy:**
One keyword search to catch what people say about the brand, plus one profile search to track the brand's own posts.

---

# Workflow Patterns Reference

## Table of Contents

1. [Trigger Decision Tree](#trigger-decision-tree)
2. [Enrichment Decision Tree](#enrichment-decision-tree)
3. [AI Node Decision Tree](#ai-node-decision-tree)
4. [Destination Decision Tree](#destination-decision-tree)
5. [Common Workflow Patterns](#common-workflow-patterns)
6. [Signal Type to AI Prompt Mapping](#signal-type-to-ai-prompt-mapping)
7. [Testing Workflows](#testing-workflows)
8. [Modifying Existing Workflows](#modifying-existing-workflows)

---

## Trigger Decision Tree

```
Real-time, per-post processing?
  → New Post (single search) or Multi-Post (multiple searches, same logic)

Batch summaries, digests, periodic reports?
  → Scheduled trigger + fetch_search_results

Chain workflows (detection → action)?
  → Workflow A creates signal → Workflow B uses Signal Created trigger

Data from outside Trigify?
  → Webhook trigger

Multiple searches, DIFFERENT logic per search?
  → Separate workflows with New Post trigger each (NOT multi-post)
```

## Enrichment Decision Tree

```
Have a LinkedIn URL, need person details?
  → person_enrichment (4 credits)

Need company info before spending on person enrichment?
  → company_enrichment (10 credits) or surfe_enrich_company (2 credits, cheaper)

Need email for outreach?
  → surfe_enrich_email (3 credits, 6-provider waterfall, higher accuracy)
  → email_enrichment (15 credits, native single provider — only if user specifically requests)

Need to find people at a company (no profile URL yet)?
  → surfe_find_people (1 credit/person)

Need phone number?
  → surfe_enrich_phone (26 credits) — expensive, reserve for high-value targets
```

**Credit-saving order:** Always filter BEFORE enriching. Place cheapest filters first:
1. IF conditions (free)
2. Person enrichment (4 credits)
3. ICP check with IF (free)
4. Email enrichment (3-15 credits) — only for qualified leads

## AI Node Decision Tree

```
Simple positive/negative/neutral classification?
  → get_sentiment (2 credits) — structured output, plugs into IF conditions

Custom analysis, scoring, classification, summarization?
  → generic_agent (variable credits) — flexible, any output format

Quick outreach copy?
  → copy_writer (5 credits) — but most users prefer generic_agent for full control
```

**Model selection:** Always default to Claude Sonnet (anthropic/claude-sonnet-4.6). It outperforms other options even for simple tasks.

**Key insight:** For simple yes/no checks (e.g., "Is this a SaaS company?"), use generic_agent with boolean output + IF node. But don't use an agent when a plain IF on job title or company size works — that's wasted credits.

## Destination Decision Tree

```
Team visibility, immediate alerts?
  → Slack channel or Slack DM

Building a lead pipeline?
  → CRM: HubSpot or Attio (ask which they use)

Email outreach campaigns?
  → Instantly or Smartlead (requires email from enrichment)

LinkedIn outreach?
  → HeyReach (requires LinkedIn URL + firstName + lastName)

Multi-channel outreach?
  → La Growth Machine (requires both LinkedIn URL and email)

Internal typed alert for triage or chaining?
  → Signal (appears in Signals dashboard, can trigger other workflows)

Custom API / Clay / any system?
  → HTTP request (universal connector)

AI agent memory / cross-run context?
  → Save to DB (ONLY for agent memory, not business data)

Formal email / external recipients?
  → Gmail

Structured database for marketing ops?
  → Google Sheets, Airtable, or Notion (ask preference)
```

## Common Workflow Patterns

### Lead Gen / Engagement Tracking
```
Trigger: New post from search
→ Get post likers (linkedin_get_post_likes)
→ Loop through each liker
→ Enrich person (person_enrichment)
→ IF matches ICP (job title, company size, location)
  → TRUE: Get email → Push to CRM → Notify Slack
  → FALSE: Skip (loop continues)
→ Loop done: Exit
```

### Real-time Alerts
```
Trigger: New post from search
→ (Optional) Analyze sentiment
→ Send Slack message with post details
```

### Weekly Summary / Executive Report
```
Trigger: Scheduled (weekly)
→ Fetch recent posts (fetch_search_results, dateRange: week)
→ AI summarize the batch (generic_agent)
→ Send to Gmail and/or Slack
```

**Important:** Create SEPARATE reports per topic — brand mentions, competitor activity, and industry trends each get their own workflow. The AI produces better analysis when focused on one topic.

**Volume handling:** Under ~1,000 results/week → feed directly to agent. Thousands of results → use Loop + Agent Memory: loop processes each batch, agent saves to memory, then a final agent reads from memory to generate the consolidated report.

### Sentiment Router
```
Trigger: New post from search
→ Analyze sentiment
→ IF positive → Share to #wins channel
→ IF negative → Alert to #urgent channel
→ IF neutral → Log for trend analysis
```

### Qualified Lead Pipeline with Outreach
```
Trigger: New post from search
→ Loop through engagers
→ Person enrichment
→ IF ICP match
  → Email enrichment
  → IF email deliverable
    → Push to outreach tool (HeyReach/Instantly)
    → Notify sales rep via Slack DM
```

## Signal Type to AI Prompt Mapping

When the workflow includes an AI agent, the signal type determines the prompt:

### Sales/Growth Signals

| Signal Type | AI Prompt Focus |
|-------------|----------------|
| Competitor Engagement Capture | "Identify the person's role, company, and what the engagement suggests about their interest. Score as hot/warm/cold lead." |
| Pain Point Discovery | "Identify the specific pain point, severity (1-10), and whether our product could help. Extract the core frustration." |
| Dissatisfied Customer Signals | "Identify complaints, frustrations, or switching intent. Extract: what they're unhappy about, severity, alternatives mentioned." |
| High-Intent Topic Monitoring | "Identify if this is someone actively seeking recommendations. Extract: requirements, budget signals, timeline hints." |
| Comparison Shopping | "Identify which solutions they're comparing, what criteria matter, and any stated preferences." |

### Marketing Intelligence Signals

| Signal Type | AI Prompt Focus |
|-------------|----------------|
| Brand Mention Monitoring | "Classify sentiment (positive/neutral/negative). Extract: what they said, context, whether response is needed." |
| Sentiment Shift Detection | "Analyze sentiment vs typical baseline. Flag negative shifts with specific cause." |
| Content Trend Detection | "Identify if this represents an emerging trend. Extract: topic, velocity, who's talking about it." |
| Question Mining | "Extract the specific question, context, and whether we have content that answers it." |
| Feature Request Mining | "Identify the requested feature, use case behind it, and frequency signal." |

## Testing Workflows

### Before Testing

1. **Check integrations:** Verify all required integrations are connected and healthy
2. **Get integration data:** For Slack workflows, verify channels exist. For CRM, verify field mappings.

### Testing with Real Data (NEVER fabricate)

**For new-post triggered workflows — step by step:**

Every new-post/multi-post workflow has a saved search attached. That search has already collected real posts. Use them:

1. **Get the workflow details** to find which saved search is attached
2. **Get results from that saved search** to retrieve actual posts it has collected
3. **Pick a real post** from those results — one with engagement data (likes, comments, a real author URL)
4. **Send that real post as the test payload** passing the actual fields: `text`, `authorUrl`, `postUrl`, `source`, `likes`, `comments`, `datePosted`
5. **Review the execution** to verify each step worked with real data

**Why real data matters:** Fake posts have fake author URLs → enrichment fails or returns nothing. Fake text → AI analysis is meaningless. Fake engagement numbers → filtering logic isn't truly tested. The whole point of testing is to verify the pipeline works end-to-end with real content.

**For scheduled workflows:**
Trigger the test normally — it simulates the scheduled execution and pulls its own data.

**For webhook workflows:**
Provide a sample payload matching the expected schema.

### After Testing

1. Review the execution to see each step's status
2. Verify enrichment data came back correctly
3. Verify messages reached Slack/CRM/destination
4. Check credits consumed vs expected

## Modifying Existing Workflows

When a user wants to change an existing workflow:

1. **Fetch the current workflow** to see the live definition
2. **Check for existing drafts** — if a draft exists, base changes on it (it may have unsaved edits)
3. **Apply changes** to the workflow definition
4. **Save as a draft** before publishing
5. **Test the draft** (testing uses the draft automatically if one exists)
6. **Publish** after a successful test

**Key rules:**
- Always base changes on current workflow state — don't rebuild from scratch
- Preserve existing action IDs — changing them breaks version history
- Test after every modification before publishing
