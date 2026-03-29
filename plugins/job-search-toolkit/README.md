# Job Search Toolkit

A dual-compatible plugin (Cursor + Claude Code) for senior engineering leadership job searches. Provides specialized skills for resume optimization, company research, salary intelligence, interview preparation, and negotiation strategy.

## Skills

| Skill | Trigger | What It Does |
|---|---|---|
| `resume-tailor` | "Tailor my resume for [company/JD]" | ATS-optimized resume generation from a master resume and job description |
| `company-intel` | "Research [company name]" | Deep-dive company research: profile, news, tech stack, leadership, culture |
| `interview-prep` | "Prepare me for [company] interview" | Custom study plans, STAR stories, system design prep, mock interviews |
| `salary-recon` | "What's the salary at [company]?" | Market compensation intelligence with percentile ranges |
| `negotiation-playbook` | "Help me negotiate with [company]" | Offer analysis, counter-offer scripts, pushback responses |

## Workflow

```
Job Posted
    |
    v
Company Intel --> Resume Tailor
    |                 |
    v                 v
Salary Recon    Interview Prep
    |                 |
    +--------+--------+
             v
    Negotiation Playbook
```

## Output Formats

| Deliverable | Format | Rationale |
|---|---|---|
| Tailored Resume | `.docx` | ATS-compatible, editable |
| Company Brief | `.md` | Quick reference |
| Salary Report | `.md` | Easy to update |
| Interview Plan | `.docx` | Printable, structured |
| Negotiation Script | `.md` | Easy to rehearse |

## Setup

### Personal Files

The `templates/` directory contains placeholder templates. To use the plugin effectively, fill them in with your real data and save to `personal/` (which is gitignored):

```bash
cp templates/career_narrative_template.md personal/career_narrative.md
cp templates/compensation_template.md personal/compensation.md
```

You should also add these files to `personal/`:

- **Master Resume** (`resume.pdf` or `resume.docx`) -- your current comprehensive resume, used as the base for all tailored versions
- **Interview Log** (`interview_log.md`) -- past interview experiences, questions asked, what worked/didn't

Edit the files in `personal/` with your actual information. These files are excluded from git via the `**/personal/` pattern in `.gitignore`, so your data stays local.

When using the plugin, provide files from `personal/` as context for the skills to work with.

### Install in Cursor

```bash
# Option A: Symlink for local use
ln -s "$(pwd)" ~/.cursor/plugins/local/job-search-toolkit

# Option B: Add as marketplace
# Add this repo as a marketplace source in Cursor settings
```

### Install in Claude Code

```bash
# Option A: Direct plugin directory
claude --plugin-dir ./plugins/job-search-toolkit/

# Option B: Add as marketplace
# /plugin marketplace add ./
# /plugin install job-search-toolkit@personal-skills
```

## Rules

The `rules/job-search-persona.md` rule auto-loads persona context (target roles, industry focus, key strengths) and best practices into every conversation. This is auto-discovered by Cursor plugins.

## Privacy

All company research and salary data is gathered from public sources only. Your personal files in `personal/` are never committed to git.
