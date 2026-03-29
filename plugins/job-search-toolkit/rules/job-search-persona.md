---
description: Provides persona context, skill workflow, and best practices for the Job Search Command Center plugin.
alwaysApply: true
---

# Job Search Command Center — Persona & Context

## User Persona

- **Target Role Level**: VP Engineering, Director of Engineering, Head of Engineering, Senior Staff Engineer, Member of Technical Staff
- **Industry Focus**: AI/ML, Media Technology, Content Platforms, Video Processing
- **Experience Level**: 8+ years in engineering, transitioning from IC to leadership
- **Key Strengths**:
  - AI-powered content platforms
  - Video processing at scale (FFMPEG, HLS/DASH)
  - Microservices architecture
  - Cloud-native systems (AWS/GCP)
  - Cross-functional team leadership

## Skill Interaction Flow

When a job opportunity arises, skills should be invoked in this order:

1. **Company Intel** → research the company first
2. **Resume Tailor** → customize resume using research insights
3. **Salary Recon** → gather compensation data
4. **Interview Prep** → build study plan using company + salary context
5. **Negotiation Playbook** → prepare scripts using all prior intelligence

## Quick Command Triggers

| Command Pattern | Skill |
|---|---|
| "Tailor my resume for [company/JD]" | resume-tailor |
| "Research [company name]" | company-intel |
| "What's the salary range at [company]?" | salary-recon |
| "Prepare me for [company] interview" | interview-prep |
| "Help me negotiate with [company]" | negotiation-playbook |

## Best Practices

### Resume Tailoring
- Extract EXACT keywords from the JD
- Map experience to JD requirements
- Quantify impact wherever possible
- Maximum 2 pages for executive roles

### Company Research
- Prioritize recent news (last 6 months)
- Identify company challenges the user can solve
- Note key decision-makers and their backgrounds

### Salary Research
- Use multiple sources (Levels.fyi, Glassdoor, Blind)
- Consider company stage (startup vs public)
- Factor in total comp (base + equity + bonus)

### Interview Prep
- Focus on STAR format for behavioral questions
- Prepare system design scenarios relevant to the company
- Research interviewers if known

### Negotiation
- Never give a number first
- Research company's typical offer structure
- Identify non-salary levers (equity, signing bonus, title)

## Output Naming Convention

```
resume_[company]_[role]_[YYYYMMDD].docx
company_brief_[company]_[YYYYMMDD].md
salary_report_[company]_[role]_[YYYYMMDD].md
interview_plan_[company]_[YYYYMMDD].docx
negotiation_playbook_[company]_[YYYYMMDD].md
```
