---
name: repo-to-video-idea
description: Analyze a project repository to suggest YouTube video ideas and generate video context. Activate when user says "turn this into a video", "video ideas for this repo", "I want to demo this", "create a video about this project", or wants to create video content from an existing codebase. Works with n8n workflows, Claude Code skills, Python scripts, JavaScript projects, and other demo-able projects. Outputs to demo-video/ folder in the project.
---

# Repo to Video Idea Generator

Analyze a project repo, suggest video ideas, and create `video-context.md` for YouTube video production.

## Workflow

### Step 1: Analyze the Project

Detect project type and understand what was built.

**Detection order:**
1. Check for `*.json` files with n8n workflow structure (has `nodes` and `connections` arrays)
2. Check for `SKILL.md` (Claude Code skill)
3. Check for `pyproject.toml` or `requirements.txt` (Python)
4. Check for `package.json` (JavaScript/Node)
5. Read `CLAUDE.md`, `README.md` for general context

**For each type, extract:**
- What does it do? (core functionality)
- What problem does it solve?
- What tools/services does it integrate?
- What are the interesting parts to demo?

See `references/project-type-patterns.md` for type-specific analysis.

### Step 2: Generate Video Ideas

Create 5-10 video ideas. For each idea:

```markdown
### Idea N: [Catchy Title]
- **Audience:** Who would watch this
- **Value prop:** What they'll learn/gain
- **Key demo moments:** 2-3 things to show
- **Length:** Short (5min) / Medium (10-15min) / Deep dive (20+min)
```

See `references/video-idea-templates.md` for idea types and examples.

### Step 3: User Selection

Present ideas and ask:
> "Which idea would you like to develop? Pick a number, or describe your own angle."

### Step 4: Gather Context

After user picks an idea, ask these questions (batch where possible):

**Core:**
1. Who exactly is this video for? (specific persona)
2. What pain point does this solve for them?
3. What's the #1 takeaway for viewers?

**Demo:**
4. What scenarios to demo? (flagship + edge cases)
5. Assumptions viewers should know upfront?
6. What could go wrong during demo?

**Expanded:**
7. Tools needed? Costs/free tiers to mention?
8. Prerequisites for viewers?
9. Customization options to highlight?
10. Include CTA for custom builds/services?

### Step 5: Generate Output

Create `demo-video/` folder in project with:

**`demo-video/video-ideas.md`** - The ideas list from Step 2

**`demo-video/video-context.md`** - Full context:

```markdown
# Video Context: [Title]

## Problem Statement
[Pain point from Q2]

## Solution Overview
[What viewer learns - from analysis + Q3]

## Target Audience
[From Q1 - be specific]

## Tools & Technologies
| Tool | Purpose | Pricing |
|------|---------|---------|
| [tool] | [what it does] | [free tier info] |

## Prerequisites
[From Q8 - what viewer needs before starting]

## Workflow/Process
[High-level flow from project analysis]
Step 1 → Step 2 → Step 3...

## Demo Scenarios
1. **Flagship:** [main scenario from Q4]
2. **Secondary:** [variation from Q4]
3. **Edge case:** [what could fail from Q6]

## Key Value Propositions
- [benefit 1]
- [benefit 2]
- [benefit 3]

## Assumptions
[From Q5]

## Customization Options
[From Q9 - what viewers might want to change]

## Call-to-Action
[From Q10 - custom build offer, links, etc.]
```

## Notes

- If project has existing `demo-video/` folder, check if context exists before overwriting
- For n8n workflows, use n8n-mcp if available to get richer node details
- Ask clarifying questions if project type is unclear
- Keep video ideas varied (different lengths, angles, audiences)
