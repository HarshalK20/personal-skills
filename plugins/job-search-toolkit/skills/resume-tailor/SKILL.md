---
name: resume-tailor
description: "Tailor resumes for specific job descriptions with ATS optimization. Use when user provides a JD and wants their resume customized for that specific role. Triggers: 'tailor my resume', 'customize resume for', 'apply to [company]', 'resume for [job title]', any JD paste with resume request."
---

# Resume Tailor Skill

## Purpose

Transform the user's master resume into a targeted, ATS-optimized version for a specific job description. Focus on VP Engineering and senior technical leadership roles.

## Trigger Phrases

- "Tailor my resume for [company/role]"
- "Customize my resume for this JD"
- "Apply to [company]"
- "Optimize resume for [position]"
- User pastes a JD and asks for resume help

## Required Inputs

1. **Job Description** (required)
   - Can be pasted directly
   - Or provide company name + role for web search

2. **Master Resume** (required)
   - Should be uploaded to project
   - Located in project files as resume.pdf or resume.docx

3. **Target Format** (optional)
   - Default: Word document (.docx)
   - Alternative: Markdown for review

## Process

### Step 1: JD Analysis

Extract and categorize from the job description:

```
REQUIRED_SKILLS: [list exact phrases]
PREFERRED_SKILLS: [list exact phrases]
LEADERSHIP_SIGNALS: [team size, scope, reports to whom]
DOMAIN_KEYWORDS: [industry-specific terms]
TECH_STACK: [specific technologies mentioned]
SOFT_SKILLS: [communication, culture fit indicators]
RED_FLAGS: [unrealistic expectations, unclear scope]
```

### Step 2: Gap Analysis

Compare JD requirements against user's experience:

| JD Requirement | User's Experience | Match Level | Positioning Strategy |
|----------------|-------------------|-------------|---------------------|
| [requirement]  | [relevant exp]    | Direct/Adjacent/Gap | [how to frame] |

### Step 3: Keyword Mapping

Create 1:1 mappings for ATS optimization:

| JD Phrase (exact) | Resume Phrase (use this) |
|-------------------|-------------------------|
| "cross-functional collaboration" | "cross-functional collaboration" |
| "AI/ML pipelines" | "AI/ML pipelines" |

**Rule**: Use JD's EXACT phrasing when the user has equivalent experience.

### Step 4: Resume Restructuring

#### Professional Summary (3-4 lines)
- Lead with years of experience + highest-impact title
- Include 2-3 JD keywords naturally
- Mention scale (users, revenue, team size)
- End with what you bring to THIS role

**Template**:
```
[X]+ years [domain] engineering leader with expertise in [JD keyword 1], 
[JD keyword 2], and [JD keyword 3]. Led [team size] engineers to deliver 
[measurable outcome]. Seeking to [specific value to target company].
```

#### Experience Section
For each role, structure as:

**[Title] | [Company] | [Duration]**
[One-line company context if not well-known]

- **[JD Keyword]**: [Action verb] + [what you did] + [quantified result]
- **[Another JD Keyword]**: [Action verb] + [what you did] + [quantified result]

**Rules**:
- Lead each bullet with a JD keyword or close synonym
- Every bullet needs a metric (%, $, scale, time saved)
- Maximum 5 bullets per role
- Most recent 2-3 roles get most detail

#### Skills Section
Structure as:

**Technical**: [Match JD tech stack exactly where applicable]
**Leadership**: [Match JD leadership terms]
**Domain**: [Match industry-specific terms]

### Step 5: ATS Optimization Checklist

Before finalizing, verify:

- [ ] No tables, columns, or graphics (ATS can't parse)
- [ ] Standard section headers (Experience, Education, Skills)
- [ ] No headers/footers (ATS often ignores)
- [ ] Contact info at top, not in header
- [ ] File saved as .docx (not .pdf for ATS systems)
- [ ] Font: Arial, Calibri, or Times New Roman
- [ ] Font size: 10-12pt body, 14-16pt headers
- [ ] Margins: 0.5" to 1"
- [ ] Length: 2 pages max for VP-level

### Step 6: Generate Output

Create the tailored resume as a Word document using the docx skill.

**File naming**: `resume_[company]_[role]_[YYYYMMDD].docx`

## Output Format

### Deliverables

1. **Tailored Resume** (.docx)
   - ATS-optimized format
   - Ready to submit

2. **Tailoring Summary** (in chat)
   ```
   ## Resume Tailoring Summary
   
   **Target**: [Company] - [Role]
   
   ### Key Optimizations Made
   - [Change 1]
   - [Change 2]
   
   ### Keyword Coverage
   - Required skills matched: X/Y
   - Preferred skills matched: X/Y
   
   ### Gaps to Address in Cover Letter
   - [Gap 1]: Suggest mentioning [adjacent experience]
   
   ### Interview Prep Flags
   - Be ready to discuss: [topic they'll likely probe]
   ```

## Special Cases

### When JD is Vague
- Search company's other job postings for context
- Research company's tech blog/engineering culture
- Make reasonable inferences, flag assumptions

### When User Has Gaps
- Emphasize adjacent/transferable experience
- Use functional resume elements strategically
- Suggest upskilling resources if major gaps

### For Startup vs Enterprise Roles
- **Startups**: Emphasize breadth, scrappiness, wearing multiple hats
- **Enterprise**: Emphasize scale, process, cross-team coordination

## Anti-Patterns (Never Do)

- ❌ Lie or exaggerate experience
- ❌ Use generic buzzwords without substance
- ❌ Include every skill regardless of relevance
- ❌ Exceed 2 pages
- ❌ Use first person ("I led...")
- ❌ Include references or "References available"
- ❌ Add photos or fancy formatting

## Example Invocation

**User**: "Tailor my resume for this VP Engineering role at Framer AI"
[pastes JD]

**Claude**:
1. Analyze JD → extract requirements
2. Read user's master resume from project files
3. Perform gap analysis
4. Create keyword mapping
5. Generate tailored .docx
6. Provide summary with optimization notes
