# Video Idea Templates

**Purpose:** Types of video ideas and creative patterns to inspire generation.

When generating video ideas, consider these different angles and formats.

## Idea Types

### 1. Full Walkthrough
End-to-end demonstration of the entire project.

**Best for:** Complex workflows, multi-step processes
**Length:** Medium to Deep dive (15-30 min)
**Structure:** Setup → Step-by-step execution → Results

**Example:**
```markdown
### Idea: Automate Invoice Processing End-to-End with n8n + AI
- **Audience:** Small business owners, accounting teams tired of manual data entry
- **Value prop:** See a complete invoice automation from email to spreadsheet
- **Key demo moments:** Gmail trigger, AI extraction, Google Sheets logging, Slack alerts
- **Length:** Deep dive (25min)
- **Code Status:** 🟢 Fully Built

**What exists:**
- ✅ Complete n8n workflow with all nodes configured
- ✅ AI extraction logic implemented
- ✅ Google Sheets integration setup

**What needs to be built:**
- None

**Dev estimate:** None - Just needs sample invoices for demo
```

---

### 2. Feature Focus
Zoom in on one specific capability or technique.

**Best for:** Projects with multiple interesting features worth separate videos
**Length:** Short to Medium (5-15 min)
**Structure:** Problem → Feature explanation → Demo → Use cases

**Example:**
```markdown
### Idea: Smart Duplicate Detection in n8n Workflows
- **Audience:** n8n users building data pipelines who need deduplication
- **Value prop:** Learn a reusable pattern for preventing duplicate processing
- **Key demo moments:** The detection logic, how it compares records, handling edge cases
- **Length:** Medium (12min)
- **Code Status:** 🟢 Fully Built

**What exists:**
- ✅ Duplicate detection logic in workflow
- ✅ Comparison function implemented
- ✅ Edge case handling

**What needs to be built:**
- None

**Dev estimate:** None
```

---

### 3. Problem-Solution
Start with a pain point, end with the fix.

**Best for:** Relatable problems with clear solutions
**Length:** Medium (10-15 min)
**Structure:** Pain point → Why it's hard → Solution overview → Demo

**Example:**
```markdown
### Idea: Stop Manually Downloading Email Attachments Forever
- **Audience:** Anyone drowning in email attachments they need to organize
- **Value prop:** Automate the tedious task of saving and organizing email files
- **Key demo moments:** The before (manual pain), the after (automated bliss)
- **Length:** Medium (10min)
```

---

### 4. Quick Tip
One specific trick, pattern, or technique.

**Best for:** Shareable nuggets, algorithm-friendly short content
**Length:** Short (3-7 min)
**Structure:** Hook → Tip → Quick demo → Takeaway

**Example:**
```markdown
### Idea: Save 40% on AI API Costs with Pre-Filtering
- **Audience:** Developers using AI APIs who want to reduce costs
- **Value prop:** Simple technique to avoid unnecessary API calls
- **Key demo moments:** The filter logic, before/after cost comparison
- **Length:** Short (5min)
```

---

### 5. How to Install/Use
Getting started guide for tools or skills.

**Best for:** Skills, plugins, tools that need onboarding
**Length:** Short to Medium (5-10 min)
**Structure:** What it is → Installation → Basic usage → Next steps

**Example:**
```markdown
### Idea: Install and Use the Gemini Image Generation Skill
- **Audience:** Claude Code users who want AI image generation
- **Value prop:** Add image generation to any project in 60 seconds
- **Key demo moments:** npx install, API key setup, first image generation
- **Length:** Short (7min)
```

---

### 6. Comparison
This vs That, or multiple options evaluated.

**Best for:** Helping viewers choose between alternatives
**Length:** Medium (10-20 min)
**Structure:** Options overview → Criteria → Comparison → Recommendation

**Example:**
```markdown
### Idea: LlamaCloud vs OpenAI for Document Extraction
- **Audience:** Developers choosing an AI document processing service
- **Value prop:** See both in action on the same documents
- **Key demo moments:** Same invoice through both, accuracy comparison, pricing
- **Length:** Medium (15min)
- **Code Status:** 🟡 Partial - Comparison script needed

**What exists:**
- ✅ LlamaCloud extraction script
- ✅ OpenAI extraction script
- ✅ Both can process same documents

**What needs to be built:**
- ❌ scripts/compare_extraction_results.py - Side-by-side comparison
- ❌ Accuracy scoring/metrics calculation
- ❌ Cost comparison table generator

**Dev estimate:** 3-4 hours
```

---

### 7. Build-Along
Step-by-step creation from scratch.

**Best for:** Teaching how to build, not just use
**Length:** Deep dive (20-45 min)
**Structure:** Goal → Setup → Build step by step → Test → Polish

**Example:**
```markdown
### Idea: Build an Email-to-Drive Automation from Scratch
- **Audience:** n8n beginners who want to learn by building
- **Value prop:** Build a real automation while learning n8n fundamentals
- **Key demo moments:** Creating each node, connecting them, testing, debugging
- **Length:** Deep dive (30min)
```

---

## Idea Generation Checklist

When creating ideas for a project, ensure variety:

- [ ] At least one full walkthrough (if project is complex enough)
- [ ] At least one feature focus (pick the most interesting part)
- [ ] At least one problem-solution (lead with pain point)
- [ ] At least one quick tip (shareable, algorithm-friendly)
- [ ] Consider a how-to-install if it's a tool/skill
- [ ] Consider comparison if alternatives exist

## Title Patterns

**Problem-first:**
- "Stop [Pain Point] with [Solution]"
- "Never [Bad Thing] Again"

**Benefit-first:**
- "Automate [Task] in [Timeframe]"
- "Save [Resource] with [Technique]"

**How-to:**
- "How to [Action] with [Tool]"
- "Build [Thing] from Scratch"

**Curiosity:**
- "The [Technique] That [Impressive Result]"
- "Why I [Action] and You Should Too"

## Length Guidelines

| Type | Length | When to Use |
|------|--------|-------------|
| Short (3-7 min) | Quick tips, installs, single features | High volume, shareable |
| Medium (10-15 min) | Problem-solution, feature focus | Balanced depth |
| Deep dive (20-30+ min) | Full walkthroughs, build-alongs | Comprehensive teaching |

---

## Summary

Use these idea types as inspiration. Mix different types to create variety in your video ideas. For exact output format and complete examples, see `video-ideas-output-template.md`.
