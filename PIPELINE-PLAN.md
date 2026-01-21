# YouTube Video Production Skills Pipeline

## Purpose

This document defines the artifact pipeline for producing YouTube videos using AI agent skills. Each skill transforms one artifact into another, creating a chain from initial idea to published video.

---

## Pipeline Overview

```
Project Repo (something you built)
    │
    ▼
┌─────────────────────────────────────┐
│  Skill: repo-to-video-idea          │
│  Input:  Project codebase           │
│  Output: demo-video/video-ideas.md  │
│          demo-video/video-context.md│
└─────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────┐
│  Skill: youtube-script-generator    │
│  Input:  video-context.md           │
│  Output: script.md                  │
└─────────────────────────────────────┘
    │
    ├───────────────────────────────────────────────┐
    │                                               │
    ▼                                               ▼
┌─────────────────────────────────────┐   ┌─────────────────────────────────────┐
│  Skill: youtube-slide-prompts       │   │  Skill: youtube-thumbnail-prompt    │
│  Input:  script.md                  │   │  Input:  script.md + title          │
│  Output: slide-prompts/*.md         │   │  Output: thumbnail-prompt.md        │
└─────────────────────────────────────┘   └─────────────────────────────────────┘
    │                                               │
    ▼                                               ▼
┌─────────────────────────────────────┐   ┌─────────────────────────────────────┐
│  Skill: gemini-image-generation     │   │  Skill: gemini-image-generation     │
│  Input:  slide-prompts/*.md         │   │  Input:  thumbnail-prompt.md        │
│  Output: slides/*.png               │   │  Output: thumbnail.png              │
└─────────────────────────────────────┘   └─────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────┐
│  [MANUAL] You Record the Video      │
│  Output: recording/*.mp4            │
│  Output: srt/*.srt (transcript)     │
└─────────────────────────────────────┘
    │
    ├───────────────────────────────────────────────┐
    │                                               │
    ▼                                               ▼
┌─────────────────────────────────────┐   ┌─────────────────────────────────────┐
│  Skill: youtube-title-generator     │   │  Skill: youtube-description-gen     │
│  Input:  srt/*.srt + context        │   │  Input:  srt/*.srt + script + tools │
│  Output: title-variations.md        │   │  Output: description.md             │
└─────────────────────────────────────┘   └─────────────────────────────────────┘
```

---

## Artifact Definitions

### 1. `demo-video/video-context.md`
**Created by:** `repo-to-video-idea` skill
**Consumed by:** `youtube-script-generator`, `youtube-title-generator`, `youtube-description-generator`
**Location:** Lives in the project repo alongside the code being demoed

Structure:
```markdown
# Video Context: [Title]

## Problem Statement
What pain point does this video address?

## Solution Overview
What does the viewer learn/build?

## Target Audience
Who is this video for? (specific persona)

## Tools & Technologies
| Tool | Purpose | Pricing |
|------|---------|---------|
| Tool 1 | [what it does] | [free tier info] |

## Prerequisites
What viewer needs before starting

## Workflow/Process
High-level flow: Step 1 → Step 2 → Step 3

## Demo Scenarios
1. **Flagship:** [main scenario]
2. **Secondary:** [variation]
3. **Edge case:** [what could fail]

## Key Value Propositions
- Benefit 1
- Benefit 2

## Assumptions
- Assumption 1
- Assumption 2

## Customization Options
What viewers might want to change

## Call-to-Action
Custom build offer, links, etc.
```

---

### 2. `script.md`
**Created by:** `youtube-script-generator` skill
**Consumed by:** `youtube-slide-prompts`, `youtube-thumbnail-prompt`, recording reference

Structure:
```markdown
# YouTube Video Script: [Title]

## [Section Name | Visual: Visual Type]

[Narration text that will be spoken]

## [Next Section | Visual: Visual Type]

[Narration text...]
```

Visual types:
- `Talking Head Only`
- `Static Visual with Voiceover`
- `Screen Recording with Voiceover`

---

### 3. `slide-prompts/*.md`
**Created by:** `youtube-slide-prompts` skill
**Consumed by:** Image generation skill (e.g., `gemini-image-generation`)

One file per section that needs a static visual. Contains:
- Design system (colors, typography, layout)
- Global context (what the video is about)
- Script narration for that section
- Visual requirements

---

### 4. `thumbnail-prompt.md`
**Created by:** `youtube-thumbnail-prompt` skill
**Consumed by:** Image generation skill

Contains:
- Video title and value proposition
- Visual approach (icons, process flow, benefit focus, etc.)
- Text overlay content
- Color scheme
- Brand/logo requirements

---

### 5. `title-variations.md`
**Created by:** `youtube-title-generator` skill
**Consumed by:** You (final selection)

Contains:
- 3-5 title variations with different approaches
- Rationale for each
- SEO keywords targeted
- Recommended title with explanation

---

### 6. `description.md`
**Created by:** `youtube-description-generator` skill
**Consumed by:** YouTube upload

Structure:
```markdown
[High-level intro - 3-4 lines]

🔧 Tools Used
- Tool 1 - link - brief description
- Tool 2 - link - brief description

📋 Chapters
0:00 - Introduction
2:15 - Section Name
...

[Call to Action - contact info, download links]
```

---

## Project Folder Structure (Per Video)

The `demo-video/` folder lives INSIDE the project repo being demoed:

```
my-project-repo/                    # Your actual project (n8n workflow, skill, etc.)
├── [project files]                 # The code/workflow being demoed
│   ├── workflow.json
│   ├── src/
│   └── ...
│
├── demo-video/                     # Created by skills, contains all video production files
│   ├── video-ideas.md              # Initial ideas list (repo-to-video-idea output)
│   ├── video-context.md            # Full context (repo-to-video-idea output)
│   ├── script.md                   # Video script (youtube-script-generator output)
│   │
│   ├── visuals/
│   │   ├── slide-prompts/          # Image generation prompts
│   │   │   ├── 02-what-you-will-learn.md
│   │   │   └── ...
│   │   ├── slides/                 # Generated slide images
│   │   │   └── ...
│   │   ├── thumbnail-prompt.md
│   │   └── thumbnail.png
│   │
│   ├── recording/
│   │   ├── raw/                    # Your video files
│   │   └── srt/
│   │       └── final.srt
│   │
│   └── metadata/
│       ├── title-variations.md
│       └── description.md
│
└── CLAUDE.md                       # Project memory
```

---

## Skills Inventory

| Skill | Status | Input Artifact | Output Artifact |
|-------|--------|----------------|-----------------|
| `repo-to-video-idea` | **Created** | Project codebase | `demo-video/video-ideas.md`, `demo-video/video-context.md` |
| `youtube-script-generator` | Planned | `video-context.md` | `script.md` |
| `youtube-slide-prompts` | Planned | `script.md` | `slide-prompts/*.md` |
| `youtube-thumbnail-prompt` | Planned | `script.md` + title | `thumbnail-prompt.md` |
| `youtube-title-generator` | Planned | SRT + context | `title-variations.md` |
| `youtube-description-generator` | Planned | SRT + script + tools | `description.md` |
| `gemini-image-generation` | Exists | Image prompt | Generated image |

---

## Skill Dependencies (Tools)

| Skill | Optional Tools | Purpose |
|-------|---------------|---------|
| `video-context-builder` | n8n-mcp | Analyze workflow JSON structure |
| `video-context-builder` | yt-dlp | Extract transcript from reference videos |
| `youtube-title-generator` | WebSearch | SEO research for keywords |
| Image generation | Gemini API | Generate slide/thumbnail images |

---

## Design Principles

1. **One skill = One artifact transformation**
   - Each skill takes a defined input and produces a defined output
   - No mega-skills that do everything

2. **File-based handoff**
   - Skills read/write files in the project folder
   - User can review/edit between steps

3. **Skills suggest upstream skills**
   - If input artifact missing, skill suggests which skill creates it
   - "I need video-context.md. Use `video-context-builder` skill first, or create it manually."

4. **Defined contracts**
   - Each artifact has a known structure
   - Skills can rely on that structure

5. **Agent-agnostic**
   - Skills work with any AI agent that supports skills
   - Installable via `npx skills add`

---

## Next Steps

1. [x] Build `repo-to-video-idea` skill (the foundation) - **DONE**
2. [ ] Build `youtube-script-generator` skill
3. [ ] Build `youtube-slide-prompts` skill
4. [ ] Build `youtube-thumbnail-prompt` skill
5. [ ] Build `youtube-title-generator` skill
6. [ ] Build `youtube-description-generator` skill
7. [ ] Test full pipeline on a real video project

---

## Iteration Log

### Session 1
- Defined initial pipeline structure
- Identified 6 skills needed
- Documented artifact formats
- Created project folder structure

### Session 2 (Current)
- Renamed first skill from `video-context-builder` to `repo-to-video-idea`
- Key insight: Start from a project repo, not raw ideas (you build first, then demo)
- Created `repo-to-video-idea` skill with:
  - SKILL.md (main workflow)
  - references/project-type-patterns.md (detection logic)
  - references/video-idea-templates.md (idea formats)
- Output location changed to `demo-video/` folder inside project repo
- Added comprehensive context gathering (10 questions)

*Add notes here as we iterate on the pipeline design*
