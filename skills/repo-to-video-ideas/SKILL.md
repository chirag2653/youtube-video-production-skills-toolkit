---
name: repo-to-video-ideas
description: Scan any code repository and generate in-depth YouTube/demo video ideas ranked by code readiness. Activate when user says "video ideas for this repo", "what videos can I make from this", "analyze this for demos", "suggest demo ideas", or wants video content ideas from a codebase. Works with any project type - n8n workflows, Claude Code skills, Python scripts, JavaScript apps, and more. Outputs comprehensive video-ideas.md to demo-video/ folder showing which ideas are ready to demo vs need development. Output can be used by downstream tools for video planning, content strategy, or production.
---

# Repo to Video Ideas

Scan a code repository and generate comprehensive video ideas with code readiness assessment.

## Workflow

### Step 1: Analyze the Project

Detect project type, understand functionality, **and assess code readiness**.

**1a. Detect Project Type**

Detection order:
1. Check for `*.json` files with n8n workflow structure (has `nodes` and `connections` arrays)
2. Check for `SKILL.md` (Claude Code skill)
3. Check for `pyproject.toml` or `requirements.txt` (Python)
4. Check for `package.json` (JavaScript/Node)
5. Read `CLAUDE.md`, `README.md` for general context

**1b. Extract Core Functionality**

For each type, extract:
- What does it do? (core functionality)
- What problem does it solve?
- What tools/services does it integrate?
- What are the interesting parts to demo?

See `references/project-type-patterns.md` for type-specific analysis.

**1c. Assess Code Readiness**

Identify what code exists to support potential video ideas:
- Search for CLI commands, scripts, main entry points
- Check for comparison scripts, benchmark scripts, visualization code
- Note what features are fully implemented vs. partially built
- Document findings for use in Step 2

See `references/code-assessment-patterns.md` for detailed assessment patterns.

### Step 2: Generate Video Ideas with Code Status

Create 5-10 video ideas with code readiness assessment.

**Quick format reference (see video-ideas-output-template.md for exact format):**

```markdown
### Idea N: [Catchy Title]
- **Audience:** Who would watch this
- **Value prop:** What they'll learn/gain
- **Key demo moments:** 2-3 things to show
- **Length:** Short (5min) / Medium (10-15min) / Deep dive (20+min)
- **Code Status:** 🟢 Fully Built | 🟡 Partial | 🔴 Needs Development

**What exists:**
- ✅ [Feature/script that exists]
- ✅ [Another existing component]

**What needs to be built:**
- ❌ [Missing code/script] (if any)

**Dev estimate:** [None | X hours | X days]
```

**Then group and rank ideas by readiness:**
- 🟢 Ready to Demo (just needs demo data)
- 🟡 Needs Minor Code Additions (1-3 files, 2-6 hours)
- 🔴 Requires Feature Development (significant work)

**Reference files:**
- `references/video-idea-templates.md` - Idea types and creative patterns
- `references/code-assessment-patterns.md` - How to assess code readiness
- `references/video-ideas-output-template.md` - Exact output format with examples (definitive)

### Step 3: Generate Output File

**3a. Prepare Output Location**

1. Check if `demo-video/` folder exists in the project root
2. If it doesn't exist, create it
3. If it exists, check if `video-ideas.md` file is already there
4. If `video-ideas.md` exists, ask user: "video-ideas.md already exists. Regenerate it with new analysis? (y/n)"
   - If yes, proceed to overwrite
   - If no, ask if they want to save with a timestamp: `video-ideas-2026-01-21.md`

**3b. Write Output File**

Write to `demo-video/video-ideas.md` (or timestamped variant if user chose that).

Use the exact format from `references/video-ideas-output-template.md` - that file is the definitive output format with complete examples.

**3c. Confirm to User**

Present the result:
> "✅ Generated `demo-video/video-ideas.md` with [N] ideas ranked by code readiness.
> 
> 🟢 [X] ideas are ready to demo
> 🟡 [Y] ideas need minor code additions
> 🔴 [Z] ideas require feature development
> 
> This file can be used for video planning, content strategy, or fed into downstream tools for production planning."

## Output

**Primary output:** `demo-video/video-ideas.md`

A comprehensive video ideas document ranked by code readiness. See `references/video-ideas-output-template.md` for format, usage, and complete examples.

## Notes

- Always create `demo-video/` folder if it doesn't exist - this is the standard location for video-related outputs
- For n8n workflows, use n8n-mcp if available to get richer node details
- Keep video ideas varied (different lengths, angles, audiences)
- This skill is focused on analysis and idea generation - it does NOT handle video production planning or context building
