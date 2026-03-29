---
name: interview-prep
description: "Create customized interview study plans and preparation materials tailored to specific companies and roles. Use when user asks to 'prepare for interview', 'interview prep', 'study plan for [company]', 'what questions will [company] ask', or mentions an upcoming interview."
---

# Interview Prep Skill

## Purpose

Generate a comprehensive, tailored interview preparation plan based on the target company, role, user's background, and known interview patterns. Focus on VP Engineering and senior technical leadership interviews.

## Trigger Phrases

- "Prepare me for [company] interview"
- "Interview prep for [role] at [company]"
- "What should I study for [company]?"
- "Mock interview for [company]"
- "I have an interview at [company] on [date]"

## Required Inputs

1. **Company Name** (required)
2. **Role/JD** (required or fetchable)
3. **Interview Date** (optional - affects urgency/timeline)
4. **Known Interview Format** (optional)
   - Number of rounds
   - Types of interviews (system design, behavioral, etc.)
5. **User's Background** (from project files)

## Preparation Process

### Step 1: Gather Interview Intelligence

**Web Search Queries**:
```
1. "[Company] interview process VP Engineering"
2. "[Company] engineering interview questions"
3. site:glassdoor.com "[Company]" "interview"
4. site:leetcode.com/discuss "[Company]"
5. site:teamblind.com "[Company]" interview
6. "[Company] system design interview"
7. "[Company] leadership interview"
```

**Extract**:
- Number of rounds
- Types of interviews
- Common questions reported
- Timeline/duration
- Key interviewers (if patterns emerge)

### Step 2: Interview Format Analysis

For VP/Director Engineering roles, expect:

| Round | Type | Duration | Interviewers |
|-------|------|----------|--------------|
| 1 | Recruiter Screen | 30 min | Recruiter |
| 2 | Hiring Manager | 45-60 min | VP Eng/CTO |
| 3 | Technical Deep Dive | 60 min | Senior Engineers |
| 4 | System Design | 60-90 min | Staff+ Engineers |
| 5 | Executive/Culture | 45 min | CEO/Founders |
| 6 | Team Meet | 30-45 min | Direct Reports |

**Customize based on company stage**:
- **Startups**: More founder involvement, broader scope questions
- **Enterprise**: More structured, competency-based

### Step 3: Question Bank Generation

#### Category A: Leadership & Management (40% of prep)

**Questions to prepare**:

1. **Team Building**
   - "How do you build and scale an engineering team?"
   - "Tell me about a time you made a critical hire."
   - "How do you handle underperformers?"

2. **Strategy & Vision**
   - "How do you set technical direction?"
   - "How do you balance technical debt vs features?"
   - "How do you align engineering with business goals?"

3. **Execution & Delivery**
   - "How do you handle missed deadlines?"
   - "Tell me about a project that failed. What did you learn?"
   - "How do you manage competing priorities?"

4. **Cross-Functional**
   - "How do you work with Product?"
   - "Tell me about a conflict with another team."
   - "How do you communicate technical decisions to non-technical stakeholders?"

5. **Culture & Values**
   - "What engineering culture do you want to build?"
   - "How do you foster innovation?"
   - "How do you handle disagreements with your team?"

#### Category B: Technical Depth (30% of prep)

**Tailored to JD requirements**:

1. **Architecture & Scale**
   - System design for company's domain
   - Scaling challenges relevant to their product
   - Technology choices and tradeoffs

2. **Domain-Specific** (for AI/Media tech):
   - Video processing pipelines
   - ML infrastructure
   - Content delivery at scale
   - Real-time systems

3. **Technical Decision Making**
   - "Walk me through a significant technical decision."
   - "How do you evaluate build vs buy?"
   - "How do you approach technical migrations?"

#### Category C: Company-Specific (20% of prep)

**Generated from Company Intel**:

1. **Why Us**
   - "Why [Company]?"
   - "What interests you about our product?"
   - "Where do you see us in 5 years?"

2. **Current Challenges**
   - Based on recent news/activity
   - Engineering scaling questions
   - Product direction questions

3. **Your Value Add**
   - How your background solves their problems
   - Specific examples from your experience

#### Category D: Logistics & Fit (10% of prep)

1. **Compensation**
   - "What are your salary expectations?"
   - See Negotiation Playbook for handling

2. **Timeline**
   - "When can you start?"
   - "Other offers/processes?"

3. **Reverse Interview**
   - Questions to ask them
   - Red flags to probe

### Step 4: STAR Story Bank

For each major theme, prepare structured stories:

**Template**:
```
### Story: [Short Title]

**Use for**: [Question types this answers]

**Situation** (2-3 sentences):
[Context and challenge]

**Task** (1-2 sentences):
[Your specific responsibility]

**Action** (3-4 sentences):
[What YOU did - be specific]

**Result** (2-3 sentences):
[Quantified outcome + learnings]

**Variations**:
- [Shorter version for quick follow-ups]
- [Technical angle if needed]
```

**Required Stories** (prepare 8-10):
1. Team building/hiring success
2. Difficult performance conversation
3. Major technical decision
4. Project failure and recovery
5. Cross-functional conflict resolution
6. Scaling challenge solved
7. Innovation/improvement initiative
8. Mentorship/developing others
9. Handling ambiguity/change
10. Delivering under pressure

### Step 5: System Design Prep

**For VP-level, focus on**:
- Explaining tradeoffs at a high level
- Asking clarifying questions
- Discussing organizational/team implications
- Knowing when to dive deep vs stay high level

**Prepare 2-3 designs relevant to company**:

Example for media/AI company:
1. Video processing pipeline at scale
2. Content recommendation system
3. Real-time collaborative editing system

**Framework**:
```
1. Clarify requirements (5 min)
2. High-level design (10 min)
3. Deep dive on critical components (15 min)
4. Scaling considerations (5 min)
5. Trade-offs and alternatives (5 min)
6. Organizational implications (5 min)
```

### Step 6: Generate Study Plan

Based on interview date and format:

**If interview in < 1 week**:
- Focus on company-specific prep
- Polish 5 best STAR stories
- Review likely questions only

**If interview in 1-2 weeks**:
- Full question bank review
- 2-3 mock interviews
- System design practice
- Company deep dive

**If interview in 2+ weeks**:
- Comprehensive preparation
- Fill any technical gaps
- Multiple mock interviews
- Relationship building (LinkedIn research)

## Output Format

### Deliverable: Interview Prep Plan (.docx)

```
# [Company] Interview Preparation Plan

**Role**: [Title]
**Interview Date**: [Date if known]
**Prepared**: [Today's date]

---

## Interview Format Intelligence

[What we know about their process]

| Round | Type | What to Expect | Key Prep |
|-------|------|----------------|----------|
| 1 | ... | ... | ... |

---

## Your Top 5 STAR Stories

[Pre-filled with user's experiences mapped to company needs]

### Story 1: [Title]
[Full STAR format]

...

---

## Technical Prep Checklist

### System Design Topics
- [ ] [Topic 1]: [Resources]
- [ ] [Topic 2]: [Resources]

### Domain Knowledge
- [ ] [Company's tech stack]
- [ ] [Industry-specific concepts]

---

## Company-Specific Questions

### Likely to Be Asked
1. [Question] → [Your angle]
2. ...

### Questions to Ask Them
1. [Strategic question]
2. [Team/culture question]
3. [Growth question]

---

## Daily Study Schedule

### Day 1-3: Foundation
- [ ] Review all STAR stories
- [ ] Company deep dive
- [ ] Technical fundamentals

### Day 4-5: Practice
- [ ] Mock behavioral interview
- [ ] System design walkthrough

### Day 6-7: Polish
- [ ] Final story refinement
- [ ] Logistics prep
- [ ] Rest and confidence building

---

## Interview Day Checklist

### Before
- [ ] Review company brief
- [ ] Re-read job description
- [ ] Check interviewer LinkedIn profiles
- [ ] Prepare questions to ask
- [ ] Test tech setup (if virtual)

### During
- [ ] Take brief notes
- [ ] Ask clarifying questions
- [ ] Use STAR structure
- [ ] Watch for buying signals

### After
- [ ] Send thank you notes (within 24h)
- [ ] Document questions asked
- [ ] Note any concerns to address
```

## Mock Interview Mode

When user requests mock interview:

1. **Select interview type** (behavioral, technical, system design)
2. **Ask 3-5 realistic questions** from question bank
3. **Provide structured feedback**:
   - What worked
   - What to improve
   - Suggested rephrasing
4. **Score on rubric** (if requested):
   - Clarity: /5
   - Specificity: /5
   - Relevance: /5
   - Impact demonstration: /5

## Anti-Patterns (Never Do)

- ❌ Encourage dishonesty or exaggeration
- ❌ Provide answers that don't match user's real experience
- ❌ Over-prepare to the point of seeming rehearsed
- ❌ Ignore company culture fit concerns
- ❌ Skip the "questions to ask them" preparation

## Example Invocation

**User**: "Help me prepare for my VP Engineering interview at Framer AI next Tuesday"

**Claude**:
1. Gather Framer AI interview intelligence (web search)
2. Cross-reference with Company Intel (if previously generated)
3. Map user's background to likely questions
4. Generate STAR stories from user's experience
5. Create compressed 5-day study plan
6. Generate Interview Prep Plan document
7. Offer mock interview practice
