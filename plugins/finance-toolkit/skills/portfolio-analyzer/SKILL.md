---
name: portfolio-analyzer
description: >
  Comprehensive portfolio intelligence skill using Zerodha Kite MCP. Trigger when the user asks for
  "analyze my portfolio", "portfolio review", "should I sell/hold", "portfolio health check",
  "stock recommendations", "mutual fund review", "rebalancing advice", "early warning on my holdings",
  "portfolio report", "what to do with my investments", or any variation of reviewing their stocks
  or mutual fund investments. Fetches live holdings, positions, and MF data from Kite, conducts 
  market + company research, and produces a structured markdown report with exit/stop-loss alerts,
  rebalancing suggestions, sector concentration warnings, and tax-loss harvesting opportunities.
  Deep-dives on flagged instruments only; quick health check for the rest.
---

# Portfolio Analyzer Skill

Generate a comprehensive, actionable portfolio intelligence report using live Zerodha Kite data
combined with real-time market research.

---

## Workflow Overview

1. **Authenticate** — Ensure Kite session is active
2. **Fetch Portfolio Data** — Holdings, MF holdings, positions, margins
3. **Enrich & Classify** — Get live prices, compute P&L, flag instruments needing attention
4. **Market Research** — Quick health check for all; deep dive for flagged ones
5. **Generate Report** — Structured markdown with prioritized recommendations

---

## Step 1: Authenticate with Kite

Call `kite:get_profile` first to confirm the session is live.
- If session error → call `kite:login` and present the link to the user before proceeding.
- Greet the user by name from the profile response.

---

## Step 2: Fetch All Portfolio Data (Parallel)

Execute all of these simultaneously:

### 2a. Stock Holdings
```
kite:get_holdings
→ Returns: tradingsymbol, exchange, quantity, average_price, last_price, pnl, day_change, day_change_percentage
```

### 2b. Mutual Fund Holdings
```
kite:get_mf_holdings
→ Returns: tradingsymbol (scheme name), quantity, average_price, last_price, pnl
```

### 2c. Open Positions (Intraday / F&O)
```
kite:get_positions
→ Only include if non-zero; flag high-risk open positions separately
```

### 2d. Available Margins / Cash
```
kite:get_margins
→ Used for rebalancing suggestions (how much dry powder is available)
```

### 2e. Recent Orders
```
kite:get_orders (limit: 20)
→ Used to understand recent activity and avoid duplicate suggestions
```

---

## Step 3: Enrich with Live Prices & Compute Metrics

For each stock holding, call `kite:get_quotes` in batches of up to 50:
```
Format: ["NSE:RELIANCE", "NSE:INFY", ...]
```

### 3a. Per-Instrument Calculations (compute ALL of these — every number must appear in the report)

| Metric | Formula | Example |
|---|---|---|
| Invested Value (₹) | `avg_price × quantity` | ₹14,280 |
| Current Value (₹) | `last_price × quantity` | ₹21,300 |
| Unrealized P&L (₹) | `current_value − invested_value` | +₹7,020 |
| Unrealized P&L (%) | `(last_price − avg_price) / avg_price × 100` | +49.2% |
| Day Change (₹) | `day_change_per_unit × quantity` | −₹412 |
| Day Change (%) | From quote / holdings data | −1.9% |
| Portfolio Weight (%) | `current_value / total_equity_current_value × 100` | 18.3% |
| 52W High proximity (%) | `last_price / week52_high × 100` | 74% of 52W high |
| From 52W Low (%) | `(last_price − week52_low) / week52_low × 100` | +22% above 52W low |

### 3b. Mutual Fund Calculations

| Metric | Formula | Example |
|---|---|---|
| Invested Value (₹) | `avg_nav × units` | ₹4,48,000 |
| Current Value (₹) | `current_nav × units` | ₹8,68,000 |
| Unrealized P&L (₹) | `current_value − invested_value` | +₹4,20,000 |
| Unrealized P&L (%) | `(current_nav − avg_nav) / avg_nav × 100` | +93.8% |
| MF Portfolio Weight (%) | `current_value / total_mf_current_value × 100` | 34.2% |

### 3c. Portfolio-Level Aggregates

Compute and display these totals explicitly:
- **Total Equity Invested (₹)** = sum of all stock invested values
- **Total Equity Current Value (₹)** = sum of all stock current values
- **Total Equity P&L (₹ and %)** 
- **Total MF Invested (₹)** = sum of all MF invested values
- **Total MF Current Value (₹)** = sum of all MF current values
- **Total MF P&L (₹ and %)**
- **Grand Total Invested (₹)** = equity + MF invested
- **Grand Total Current Value (₹)** = equity + MF current
- **Grand Total P&L (₹ and %)**
- **Today's Total Portfolio Change (₹)** = sum of all day_change × quantity across stocks
- **Available Cash/Margin (₹)** = from `kite:get_margins`

---

## Step 4: Flagging Logic

### 🚨 FLAG for Deep Dive (any one condition triggers)

**Exit / Stop-Loss Alerts:**
- Unrealized loss > 15%
- Day drop > 5% in a single session
- Price < 10% above 52-week low (stock near multi-year bottom)
- Momentum reversal: price dropped > 20% from 52-week high

**Rebalancing Triggers:**
- Single stock > 20% of total equity portfolio
- Single sector > 35% of total equity portfolio
- Cash / margin significantly high (> 30% of portfolio) — under-deployed capital

**Tax-Loss Harvesting Candidates:**
- Unrealized loss > 10% AND holding period < 12 months (short-term capital loss)
- Unrealized loss > 10% AND holding period > 12 months (long-term capital loss for offset)

**MF Flags:**
- Scheme underperforming its benchmark/category average (research needed)
- Duplicate schemes: same category held in multiple schemes (redundancy)
- NFO / new fund with < 3 years track record

**Sector Concentration:**
- Compute sector weights across all stocks; flag if any sector > 35%

---

## Step 5: Research Phase

### 5a. Quick Health Check (ALL instruments)

For every stock, search:
```
"[COMPANY NAME] stock news 2025" 
"[COMPANY NAME] quarterly results"
```

Capture:
- Latest earnings trend (beat/miss/in-line)
- Any major corporate actions (buyback, bonus, rights, merger)
- Management changes or promoter pledging news
- Analyst consensus (buy/hold/sell) if available

For every MF scheme, search:
```
"[SCHEME NAME] performance 2025"
"[SCHEME NAME] vs benchmark"
```

Capture:
- 1Y / 3Y / 5Y CAGR vs category average
- AUM trend (significant outflow = warning signal)
- Fund manager changes

### 5b. Deep Dive (FLAGGED instruments only)

For flagged stocks, additionally research:
```
"[COMPANY] fundamental analysis 2025"
"[COMPANY] debt equity ratio"
"[COMPANY] promoter holding change"
"[COMPANY] ROCE ROE 2025"
"[COMPANY] management commentary"
"[COMPANY] competition threat"
"[COMPANY] target price analyst"
```

Capture:
- Revenue / profit growth trajectory (last 4 quarters)
- Debt levels and interest coverage
- Promoter holding trend (rising = bullish, falling = warning)
- Competitive positioning changes
- Analyst target price vs current price (upside/downside)
- Any governance concerns or regulatory issues

For flagged MFs, additionally research:
```
"[SCHEME] fund manager strategy 2025"
"[SCHEME] portfolio overlap"
"[CATEGORY] top performing funds 2025"
```

Capture:
- Portfolio concentration (top 10 holdings %)
- Fund manager tenure and track record
- Expense ratio vs peers
- Whether better alternatives exist in same category

---

## Step 6: Generate the Report

Output a **structured markdown report** with the following sections in exact order:

---

```markdown
# 📊 Portfolio Intelligence Report
**Generated:** [Date & Time IST]  
**Account:** [User Name] | [User ID]

---

## 🔢 Portfolio Snapshot

| Category | Invested (₹) | Current Value (₹) | P&L (₹) | P&L % | Today's Change (₹) |
|---|---|---|---|---|---|
| Stocks | ₹X,XX,XXX | ₹X,XX,XXX | ±₹X,XXX | ±X.X% | ±₹X,XXX |
| Mutual Funds | ₹X,XX,XXX | ₹X,XX,XXX | ±₹X,XXX | ±X.X% | — |
| **Grand Total** | **₹X,XX,XXX** | **₹X,XX,XXX** | **±₹X,XXX** | **±X.X%** | **±₹X,XXX** |

**Available Cash/Margin:** ₹X,XXX
> 💡 Note: Numbers are computed from Kite holdings data. Avg price × qty = invested; LTP × qty = current value.

---

## 🚨 Priority Alerts (Act on These First)

> Instruments requiring immediate attention based on technical, fundamental, or risk criteria.

### ⛔ Exit / Stop-Loss Alerts

For each flagged stock, always show full financial details:

#### [STOCK NAME] ([SYMBOL]) — [ALERT TYPE e.g. LOSS >15% / NEAR 52W LOW]
| Detail | Value |
|---|---|
| Quantity | X shares |
| Avg Buy Price | ₹X |
| Current Price (LTP) | ₹X |
| Invested Amount | ₹X,XXX |
| Current Value | ₹X,XXX |
| Unrealized P&L | ₹X,XXX (X%) |
| Today's Change | ₹X (X%) |
| Portfolio Weight | X% of equity portfolio |
| 52W High / Low | ₹X,XXX / ₹XXX |

- **Alert Reason:** [e.g. "Down 54% from avg buy; revenue fell 19% YoY; losing market share"]
- **Research Finding:** [2-3 line summary of deep dive findings with specific data — revenue, profit trend, competition]
- **Recommendation:** 🔴 EXIT / 🟡 SET STOP-LOSS at ₹X / 🟠 REDUCE by X shares (₹X,XXX worth)
- **If Sold, Approximate Proceeds:** ₹X,XXX | **Loss to Book:** ₹X,XXX (STCL/LTCL)

---

### 📊 Rebalancing Required

#### Overweight Positions
| Stock | Invested (₹) | Current Value (₹) | Current Weight | Recommended Max | Excess (₹) to Trim |
|---|---|---|---|---|---|
| [Stock] | ₹X,XXX | ₹X,XXX | X% | 20% | ₹X,XXX worth |

#### Sector Concentration
| Sector | Holdings | Total Current Value (₹) | Portfolio Weight | Max Recommended | Status |
|---|---|---|---|---|---|
| [Sector] | [Stock A, Stock B] | ₹X,XX,XXX | X% | 35% | ⚠️ Over |

---

### 💸 Tax-Loss Harvesting Opportunities

> Book losses to offset capital gains. Always verify with your CA before acting.

| Stock | Qty | Invested (₹) | Current Value (₹) | Unrealized Loss (₹) | Loss % | Holding Type | Potential Tax Saving |
|---|---|---|---|---|---|---|---|
| [Stock] | X | ₹X,XXX | ₹X,XXX | ₹X,XXX | X% | STCL (< 1Y) | ~₹X,XXX @ 20% STCG |
| [Stock] | X | ₹X,XXX | ₹X,XXX | ₹X,XXX | X% | LTCL (> 1Y) | ~₹X,XXX @ 12.5% LTCG |

**Total Losses Available to Harvest:** ₹X,XXX  
**Estimated Max Tax Saving:** ~₹X,XXX (assuming losses offset equivalent gains)

---

## ✅ Portfolio Health Check — Stocks (All Holdings)

> Every stock must appear here with complete financial figures. No stock should be mentioned without its numbers.

| # | Stock | Qty | Avg Price (₹) | LTP (₹) | Invested (₹) | Current Value (₹) | P&L (₹) | P&L% | Day Change | Weight | Signal |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | RELIANCE | 15 | ₹1,295 | ₹1,420 | ₹19,428 | ₹21,300 | +₹1,872 | +9.6% | +₹139 (+0.66%) | 12.3% | 🟢 HOLD |
| 2 | OLAELEC | 500 | ₹58.33 | ₹26.58 | ₹29,165 | ₹13,290 | -₹15,875 | -54.4% | -₹470 (-3.4%) | 7.7% | 🔴 EXIT |

**Equity Sub-total:** Invested ₹X,XX,XXX | Current ₹X,XX,XXX | P&L ₹±X,XXX (±X%)

**Signal Key:** 🟢 HOLD | 🔵 ACCUMULATE | 🟡 WATCH | 🟠 REDUCE | 🔴 EXIT

---

## ✅ Portfolio Health Check — Mutual Funds (All Holdings)

> Every MF scheme must appear with complete financial figures.

| # | Scheme (Short Name) | Units | Avg NAV (₹) | Current NAV (₹) | Invested (₹) | Current Value (₹) | P&L (₹) | P&L% | MF Weight | Signal |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | UTI Nifty 50 Index | 4,736.9 | ₹118.64 | ₹177.98 | ₹5,61,945 | ₹8,43,268 | +₹2,81,323 | +50.1% | 28.4% | 🟢 HOLD |
| 2 | Motilal Gold+Silver FOF | 7,971.6 | ₹33.49 | ₹31.89 | ₹2,66,959 | ₹2,54,180 | -₹12,779 | -4.8% | 8.6% | 🟡 HOLD |

**MF Sub-total:** Invested ₹X,XX,XXX | Current ₹X,XX,XXX | P&L ₹±X,XXX (±X%)

---

## 🗺️ Sector Allocation Analysis (Equity Only)

| Sector | Holdings | Invested (₹) | Current Value (₹) | Weight | Trend | Risk Level |
|---|---|---|---|---|---|---|
| Renewable Energy | ADANIGREEN, IREDA | ₹X,XXX | ₹X,XXX | X% | ↑ | 🟡 Moderate |
| Consumer Tech / Food | SWIGGY | ₹X,XXX | ₹X,XXX | X% | ↓ | 🟡 Moderate |
| Fintech | PAYTM, JIOFIN | ₹X,XXX | ₹X,XXX | X% | ↑ | 🟡 Moderate |
| Conglomerate | RELIANCE | ₹X,XXX | ₹X,XXX | X% | → | 🟢 Low |
| EV / Auto | OLAELEC | ₹X,XXX | ₹X,XXX | X% | ↓↓ | 🔴 High |
| Jewellery | PNGJL | ₹X,XXX | ₹X,XXX | X% | ↑ | 🟢 Low |
| Banking (ETF) | BANKIETF | ₹X,XXX | ₹X,XXX | X% | → | 🟢 Low |
| Gold / Fixed Income | SGBs, 755GJ31-SG | ₹X,XXX | ₹X,XXX | X% | ↑ | 🟢 Low |

**Observation:** [1-2 lines on concentration risk, overweight sectors, and macro commentary]

---

## 💡 Strategic Recommendations

> Prioritized action list — ordered by urgency and ₹ impact. Work top-to-bottom.

1. **[ACTION — INSTRUMENT]** `[URGENT / SOON / MONITOR]`
   - What: [Exact action, e.g. "Sell 500 shares of OLAELEC at market price"]
   - Why: [2–3 bullet reasons with specific data]
   - Expected outcome: [e.g. "Frees ₹13,290; books ₹15,875 STCL for tax offset"]

2. **[ACTION — INSTRUMENT]** `[SOON]`
   - What: ...
   - Why: ...
   - Expected outcome: ...

---

## 📈 Market Context

| Parameter | Status | Relevance to Your Portfolio |
|---|---|---|
| Nifty 50 | [Level, ±% from ATH] | [Impact on your index funds] |
| Sensex | [Level, trend] | — |
| FII Activity | [₹ bought/sold MTD] | [Headwind/tailwind for your holdings] |
| DII Activity | [₹ bought/sold MTD] | [Support level for markets] |
| RBI Repo Rate | [Current rate, last move] | [Impact on IREDA, Banking ETF, JIOFIN] |
| Gold (MCX) | [₹/10g, trend] | [Impact on SGB + Gold-Silver FOF] |
| Sector: Renewable | [Outlook] | [Impact on ADANIGREEN, IREDA] |
| Sector: Fintech | [Outlook] | [Impact on PAYTM, JIOFIN, SWIGGY] |
| Sector: EV/Auto | [Outlook] | [Impact on OLAELEC] |

---

## ⚠️ Disclaimer

This report is AI-generated for informational purposes only and does not constitute financial advice.
Always consult a SEBI-registered financial advisor before making investment decisions.
Tax-loss harvesting calculations are indicative — verify with a CA.
```

---

## Output Quality Rules

### 🔢 Numbers are MANDATORY — the most critical rule
- **Every holding must show ALL SIX key numbers**: Qty, Avg Price, LTP, Invested ₹, Current Value ₹, P&L ₹ (and %). No exceptions.
- **Never mention a stock without its rupee P&L** — saying "IREDA is down 12%" without saying "that's -₹884 on an investment of ₹7,216" loses the real context.
- **Portfolio weights must always be in ₹ AND %** — "15% weight" is incomplete without "₹21,300 current value out of ₹1,42,000 equity portfolio."
- **Tax-loss harvesting must show rupee loss amounts**, not just percentages. ₹15,875 loss on OLAELEC is more actionable than "-54%".
- **Rebalancing suggestions must say "sell ₹X,XXX worth"**, not just "trim by 10%".
- **MF holdings must show units × NAV = ₹ value** for both invested and current.

### 📋 Format is MANDATORY — no prose paragraphs anywhere
- **Zero prose paragraphs** in the final report. Every insight, finding, recommendation, and observation must be expressed as a bullet point or table row — never as flowing text.
- **Research findings** for flagged instruments must be bullet points, e.g.:
  - ❌ Wrong: "Ola Electric's Q3 FY25 results showed that revenue fell sharply while losses widened significantly due to multiple headwinds..."
  - ✅ Right:
    - Revenue: ₹1,045 Cr (−19% YoY)
    - Net loss: ₹564 Cr (widened from ₹376 Cr)
    - Market share: dropped from 35% → 25.5%
    - CCPA probe active; SEBI warning issued Jan 2025
- **Observations and conclusions** under each section must be 2–4 crisp bullet points, not sentences stitched into a paragraph.
- **Market context section** must be a clean table or bulleted list — not a narrative.
- **Strategic recommendations** must be a numbered list with sub-bullets for rationale — not paragraphs.
- **Quick health check notes** in tables must be ≤ 10 words per cell (e.g. "Strong Q3; analyst target ₹1,720; HOLD").

### General rules
- **Be specific** — Always name the instrument, give exact prices, quantities, and rupee amounts. Never use placeholder "X" in the final report.
- **Prioritize ruthlessly** — If there are 3+ exit alerts, sort by absolute rupee loss (largest loss first), not just percentage.
- **Research-backed** — Every REVIEW/EXIT signal must cite at least one specific data point (e.g. "revenue fell 19% YoY to ₹1,045 crore").
- **Avoid generic advice** — "Sell ₹15,875 worth of OLAELEC (500 shares at ₹26.58)" beats "consider reducing EV exposure".
- **Flag uncertainty** — If research data is conflicting, say so rather than picking a side.
- **Respect risk** — Never recommend leverage, F&O, or speculative calls. Keep advice conservative.
- **Tax sensitivity** — For loss-booking, note STCL vs LTCL, show ₹ amount, and remind user to verify with CA.
- **MF patience** — Don't recommend switching funds on < 1 year underperformance. Show 3Y CAGR context.

---

## Error Handling

| Situation | Handling |
|---|---|
| Kite session expired | Call `kite:login`, present auth link, stop and wait |
| Empty holdings | Report "No holdings found" and ask if user wants to check a different account |
| Quote API fails for a stock | Note "Price data unavailable" for that instrument and skip its metrics |
| Research returns no results | Note "Limited public data available" and flag for manual check |
| Positions with large open F&O | Add a separate "⚡ Open Positions" section before Priority Alerts with MTM P&L |

---

## Trigger Examples

These phrases should trigger this skill:
- "Analyze my portfolio"
- "Give me a portfolio report"
- "Should I sell any stocks?"
- "Am I too concentrated in IT?"
- "Which stocks are in loss?"
- "Review my mutual funds"
- "Portfolio health check"
- "Any tax loss harvesting opportunities?"
- "What's the early warning in my holdings?"
- "Is my portfolio well diversified?"
