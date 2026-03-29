---
name: salary-recon
description: "Research salary ranges and total compensation for specific roles at target companies. Use when user asks about 'salary at [company]', 'compensation range', 'what does [role] pay', 'market rate for', or needs data for negotiation prep."
---

# Salary Recon Skill

## Purpose

Gather comprehensive compensation intelligence for a target role/company to inform expectations and negotiation strategy. Focus on total compensation including base, equity, bonus, and benefits.

## Trigger Phrases

- "What's the salary range at [company]?"
- "How much does [company] pay for [role]?"
- "Market rate for [role]"
- "Compensation research for [company]"
- "What should I expect for [title] in [location]?"

## Required Inputs

1. **Company Name** (required)
2. **Role/Title** (required)
3. **Location** (required - affects comp significantly)
4. **Level** (helpful - VP, Director, Senior Director, etc.)

## Research Process

### Step 1: Direct Company Data

**Web Search Queries**:
```
1. site:levels.fyi "[Company]" "[Role/Level]"
2. site:glassdoor.com "[Company]" salaries "[Role]"
3. site:teamblind.com "[Company]" compensation "[Level]"
4. "[Company]" salary "[Role]" "[Location]"
5. "[Company]" total compensation engineering leadership
```

**If public company, also search**:
```
6. "[Company]" proxy statement executive compensation
7. site:sec.gov "[Company]" DEF 14A
```

### Step 2: Data Extraction

For each source found, extract:

| Source | Base Range | Equity/RSU | Bonus | Total Comp | Level | Date |
|--------|-----------|------------|-------|------------|-------|------|
| Levels.fyi | $X-Y | $A-B | C% | $Total | L8 | 2024 |
| Glassdoor | ... | ... | ... | ... | ... | ... |
| Blind | ... | ... | ... | ... | ... | ... |

**Important**:
- Note the date of data (salary data older than 18 months is less reliable)
- Distinguish between base, equity, and total comp
- Note if data is for different locations

### Step 3: Level Mapping

Different companies use different leveling. Map to understand comparisons:

| Company | Their Level | Equivalent | Typical Scope |
|---------|-------------|------------|---------------|
| Google | L8/Director | VP Eng (startup) | 50-150 reports |
| Meta | E7/Director | VP Eng | 30-100 reports |
| Amazon | L8/Director | VP Eng | 40-120 reports |
| Startup | VP Eng | Director (FAANG) | 10-40 reports |

### Step 4: Location Adjustment

**Base location multipliers** (approximate, varies by company):

| Location | Multiplier | Notes |
|----------|------------|-------|
| SF Bay Area | 1.0x | Baseline |
| NYC | 0.95-1.0x | Similar to SF |
| Seattle | 0.90-0.95x | Slightly lower |
| Austin | 0.80-0.85x | Growing market |
| Denver | 0.80-0.85x | Tech hub growth |
| Remote (US) | 0.80-0.95x | Varies by company |
| India (Mumbai) | 0.30-0.40x | Varies significantly |
| London | 0.75-0.85x | GBP considerations |

### Step 5: Company Stage Adjustment

| Stage | Equity Characteristics | Base Characteristics |
|-------|----------------------|---------------------|
| Seed | High risk, high upside, illiquid | Below market base |
| Series A | High risk, options-heavy | Slightly below market |
| Series B-C | Moderate risk, better liquidity outlook | Market rate |
| Series D+ | Lower risk, more RSU-like | Market to above |
| Pre-IPO | Liquidity imminent, equity valuable | At market |
| Public | Liquid RSUs, predictable | At or above market |

### Step 6: Compensation Structure Analysis

**For target company, determine**:

1. **Equity Type**
   - Stock Options (ISOs/NSOs): Need strike price, vesting schedule
   - RSUs: More straightforward value
   - Equity Value: Current valuation / shares outstanding

2. **Vesting Schedule**
   - Standard: 4 years, 1-year cliff
   - Variations: 3-year, backloaded, monthly

3. **Bonus Structure**
   - Target percentage
   - Performance multipliers
   - Sign-on bonus norms

4. **Refresh Grants**
   - Annual equity refresh policy
   - How it affects total comp over time

### Step 7: Market Synthesis

Combine all data into ranges:

```
Role: VP Engineering
Company: [Target]
Location: [City]

CONSERVATIVE ESTIMATE (25th percentile):
- Base: $X
- Equity: $Y/year
- Bonus: $Z
- Total: $Total

MARKET RATE (50th percentile):
- Base: $X
- Equity: $Y/year
- Bonus: $Z
- Total: $Total

STRONG OFFER (75th percentile):
- Base: $X
- Equity: $Y/year
- Bonus: $Z
- Total: $Total
```

## Output Format

### Deliverable: Salary Intelligence Report (.md)

```markdown
# Compensation Intelligence: [Role] at [Company]

**Prepared**: [Date]
**Location**: [City]
**Data Freshness**: [Most recent data point date]

---

## Executive Summary

| Component | Low | Market | Strong |
|-----------|-----|--------|--------|
| Base | $X | $Y | $Z |
| Equity (annual) | $A | $B | $C |
| Bonus Target | D% | E% | F% |
| **Total Comp** | $Total | $Total | $Total |

---

## Detailed Findings

### Direct Company Data

**Source: Levels.fyi**
[Specific data points with dates]

**Source: Glassdoor**
[Specific data points with dates]

**Source: Blind**
[Anonymized reports if available]

### Comparable Companies

| Company | Role | Base | Equity | Total | Notes |
|---------|------|------|--------|-------|-------|
| [Comp 1] | VP Eng | $X | $Y | $Z | [Context] |
| [Comp 2] | ... | ... | ... | ... | ... |

---

## Equity Deep Dive

**Company Stage**: [Seed/Series X/Public]
**Equity Type**: [Options/RSUs]
**Vesting**: [Schedule]
**Current Valuation**: [If known]

### Equity Value Scenarios

| Scenario | Assumption | 4-Year Value |
|----------|------------|--------------|
| Conservative | Current valuation stays flat | $X |
| Base Case | 2x growth over 4 years | $Y |
| Optimistic | 5x growth, successful exit | $Z |

---

## Location Analysis

**Target Location**: [City]
**Adjustment vs SF**: [X%]

If remote: [Company's remote compensation policy]

---

## Negotiation Anchors

Based on this research:

**Your Target** (aim for 75th percentile):
- Base: $X
- Equity: $Y total / 4 years
- Sign-on: $Z
- Total First Year: $Total

**Your Floor** (walk away below this):
- Base: $X
- Total Comp: $Y

**Negotiation Levers**:
1. [Lever 1 with context]
2. [Lever 2 with context]
3. [Lever 3 with context]

---

## Data Confidence

| Component | Confidence | Notes |
|-----------|------------|-------|
| Base Range | High/Medium/Low | [Why] |
| Equity Range | High/Medium/Low | [Why] |
| Bonus | High/Medium/Low | [Why] |

---

## Sources

1. [Source 1 with date]
2. [Source 2 with date]
...

---

*Note: Compensation varies significantly based on individual negotiation, 
specific experience match, and company circumstances. Use as directional guidance.*
```

## Special Cases

### When Data is Scarce (Startups/Private)

1. **Use comparable companies**
   - Similar stage
   - Similar domain
   - Similar location

2. **Estimate from funding**
   - Series A VP Eng: Often $200-280K base + 0.5-1.5% equity
   - Series B VP Eng: Often $250-320K base + 0.25-0.75% equity
   - Series C+ VP Eng: Often $280-380K base + 0.1-0.3% equity

3. **Check founder backgrounds**
   - Ex-FAANG founders often pay closer to market
   - First-time founders may have unrealistic expectations

### For International Roles

1. **Research local market rates**
2. **Determine if US pay parity or local rates**
3. **Factor in cost of living differences**
4. **Consider tax implications**

### For Public Companies

1. **Check SEC filings** for executive comp
2. **Look at stock performance** for equity value
3. **Research refresh grant policies**

## Anti-Patterns (Never Do)

- ❌ Present single data point as definitive range
- ❌ Ignore data recency
- ❌ Conflate different job levels
- ❌ Forget location adjustments
- ❌ Treat equity as guaranteed value
- ❌ Make up data when search fails

## Example Invocation

**User**: "What's the salary range for VP Engineering at Framer AI in San Francisco?"

**Claude**:
1. Search Levels.fyi, Glassdoor, Blind for Framer AI data
2. Search for comparable companies (Figma, Notion, Canva)
3. Research Framer's funding stage and equity structure
4. Apply SF location baseline
5. Generate compensation report with ranges
6. Provide negotiation anchors
