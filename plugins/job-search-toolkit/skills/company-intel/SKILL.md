---
name: company-intel
description: "Deep-dive company research for job applications. Provides company overview, recent activity, tech stack, culture signals, key people, and strategic insights. Use when user asks to 'research [company]', 'tell me about [company]', 'company deep dive', or before interviews."
---

# Company Intel Skill

## Purpose

Gather comprehensive intelligence about a target company to inform job applications, interview prep, and salary negotiations. Combines web research with any user-provided information.

## Trigger Phrases

- "Research [company name]"
- "Tell me about [company]"
- "Deep dive on [company]"
- "What should I know about [company]?"
- "Company brief for [company]"

## Required Inputs

1. **Company Name** (required)
2. **Role Context** (optional but helpful)
   - What position is the user targeting?
3. **User-Provided Info** (optional)
   - Any insider knowledge, articles, or notes to incorporate

## Research Process

### Step 1: Core Company Profile

**Web Search Queries** (execute in sequence):
```
1. "[Company] about" OR "[Company] overview"
2. "[Company] founding story" OR "[Company] history"
3. "[Company] funding" OR "[Company] valuation" OR "[Company] IPO"
4. "[Company] revenue" OR "[Company] business model"
5. "[Company] headquarters" OR "[Company] offices locations"
```

**Extract**:
- Founded: [Year]
- Headquarters: [Location]
- Company Stage: [Seed/Series A/B/C/Public/etc.]
- Valuation/Market Cap: [Amount if available]
- Employee Count: [Number, with engineering estimate if possible]
- Business Model: [How they make money]
- Core Product(s): [What they sell/offer]

### Step 2: Recent Activity (Last 6 Months Priority)

**Web Search Queries**:
```
1. "[Company] news" (filter: past 6 months)
2. "[Company] announcement" OR "[Company] launch"
3. "[Company] funding round 2025" OR "[Company] acquisition"
4. "[Company] layoffs" OR "[Company] hiring" (recent)
5. "[Company] CEO interview" OR "[Company] leadership"
```

**Categorize Findings**:
- 🚀 **Growth Signals**: New funding, hiring, product launches
- ⚠️ **Risk Signals**: Layoffs, pivots, leadership changes
- 📰 **Neutral News**: General coverage, industry mentions

### Step 3: Tech Stack & Engineering Culture

**Web Search Queries**:
```
1. "[Company] tech stack" OR "[Company] engineering blog"
2. "[Company] engineering culture" OR "[Company] developers"
3. site:github.com/[company]
4. site:stackshare.io "[Company]"
5. "[Company] tech talks" OR "[Company] conference"
```

**Extract**:
- Languages: [Primary languages used]
- Frameworks: [Frontend/Backend frameworks]
- Infrastructure: [Cloud provider, key services]
- Data/ML: [If applicable]
- Engineering Blog: [URL if exists]
- Open Source: [Notable projects]

### Step 4: Leadership & Key People

**Web Search Queries**:
```
1. "[Company] CEO" OR "[Company] founder"
2. "[Company] VP Engineering" OR "[Company] CTO"
3. site:linkedin.com "[Company]" "VP Engineering"
4. "[CEO Name] interview" OR "[CEO Name] podcast"
```

**For each key leader, extract**:
- Name & Title
- Background (previous companies)
- Public statements/philosophy (if available)
- LinkedIn URL

**Special focus on**:
- Who the role reports to
- Who might interview the user
- Engineering leadership structure

### Step 5: Culture & Values

**Web Search Queries**:
```
1. "[Company] culture" OR "[Company] values"
2. "[Company] Glassdoor" OR "[Company] reviews"
3. "[Company] interview process" OR "[Company] hiring"
4. "[Company] remote work" OR "[Company] office policy"
5. "[Company] diversity" OR "[Company] ERG"
```

**Extract**:
- Stated Values: [From website/careers page]
- Work Style: [Remote/Hybrid/In-office]
- Interview Process: [Rounds, timeline, known patterns]
- Glassdoor Rating: [Score + key themes]
- Red Flags: [Concerning patterns in reviews]

### Step 6: Competitive Landscape

**Web Search Queries**:
```
1. "[Company] competitors"
2. "[Company] vs [Competitor]"
3. "[Company] market position" OR "[Company] market share"
```

**Extract**:
- Main Competitors: [2-4 companies]
- Competitive Advantages: [What differentiates them]
- Market Position: [Leader/Challenger/Niche]

### Step 7: Strategic Insights

Synthesize findings into actionable intelligence:

1. **Why This Company Now?**
   - What's their current trajectory?
   - What challenges are they likely facing?

2. **How User Can Add Value**
   - Match user's background to company needs
   - Identify pain points user can solve

3. **Potential Concerns**
   - Any red flags to investigate further?
   - Questions to ask in interviews

4. **Culture Fit Assessment**
   - Alignment with user's preferences
   - Potential friction points

## Output Format

### Deliverable: Company Brief (.md)

```markdown
# [Company Name] - Intelligence Brief

**Prepared**: [Date]
**Target Role**: [Role if specified]

---

## Company Overview

| Attribute | Details |
|-----------|---------|
| Founded | [Year] |
| Stage | [Funding stage] |
| Valuation | [Amount] |
| Employees | [Count] |
| HQ | [Location] |

**What They Do**: [2-3 sentence description]

**Business Model**: [How they make money]

---

## Recent Activity (Last 6 Months)

### 🚀 Growth Signals
- [Item with date and source]

### ⚠️ Watch Items
- [Item with date and source]

---

## Tech Stack

**Languages**: [List]
**Infrastructure**: [Cloud/services]
**Notable**: [Interesting technical choices]
**Eng Blog**: [URL]

---

## Key People

### [CEO/Founder Name]
- **Background**: [Previous roles]
- **Notable**: [Relevant quote or philosophy]

### [VP Eng/CTO Name] ← *Your potential manager*
- **Background**: [Previous roles]
- **Notable**: [Relevant info]

---

## Culture & Interview Process

**Values**: [Stated values]
**Work Style**: [Remote/Hybrid/Office]
**Glassdoor**: [Rating] - [Key themes]

**Known Interview Process**:
1. [Round 1]
2. [Round 2]
...

---

## Competitive Landscape

- **Main Competitors**: [List]
- **Differentiation**: [What makes them unique]

---

## Strategic Insights

### Why Join Now
[Analysis of company trajectory and timing]

### How You Can Add Value
- [Specific way user's background matches needs]
- [Pain point user can address]

### Questions to Ask Them
1. [Strategic question about company direction]
2. [Question about engineering challenges]
3. [Question about team/culture]

### Red Flags to Monitor
- [Any concerns from research]

---

*Sources: [List key sources used]*
```

## Hybrid Mode (Web + User Input)

When user provides additional context:

1. **Start with web research** (steps 1-6)
2. **Incorporate user intel**:
   - "You mentioned [X]. This aligns with/contradicts..."
   - Flag any discrepancies between public info and insider knowledge
3. **Weight user's info highly** for recent/internal matters
4. **Use web to verify/expand** on user's points

## Special Cases

### For Startups (Seed/Series A)
- Limited public info expected
- Focus on founders' backgrounds
- Look for TechCrunch, Product Hunt launches
- Check AngelList/Crunchbase

### For Public Companies
- Add stock performance
- Check earnings calls/investor presentations
- Look for SEC filings (10-K) for strategy

### For Stealth/Early Stage
- Focus on founders
- Check what problem they're solving
- Look for adjacent company info

## Anti-Patterns (Never Do)

- ❌ Present unverified rumors as fact
- ❌ Access paywalled content without permission
- ❌ Make up information when search fails
- ❌ Ignore red flags to paint rosy picture
- ❌ Include confidential information

## Example Invocation

**User**: "Research Framer AI for me - I'm applying for VP Engineering"

**Claude**:
1. Execute web searches for company info
2. Compile findings into structured brief
3. Tailor insights to VP Engineering context
4. Highlight what user's background offers
5. Save as company_brief_framerAI_[date].md
