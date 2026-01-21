# YouTube Video Production Skills Toolkit

## Purpose

This is the **design and development workspace** for building a suite of AI agent skills that automate YouTube video production workflows.

## What This Project Is

- A thinking ground for designing skills
- Where skills are developed and tested
- Skills are later moved to the appropriate distribution folder (e.g., `my-claude-code-plugins` or published to a skills repo)

## Key Document

**`PIPELINE-PLAN.md`** - The master plan defining:
- The artifact pipeline (idea → published video)
- Each skill's input/output contracts
- Project folder structure for video projects
- Skills inventory and status

Always read `PIPELINE-PLAN.md` first when returning to this project.

## Skills Being Developed

1. `video-context-builder` - Structures raw ideas into video-context.md
2. `youtube-script-generator` - Creates video scripts from context
3. `youtube-slide-prompts` - Generates image prompts for static visuals
4. `youtube-thumbnail-prompt` - Creates thumbnail generation prompts
5. `youtube-title-generator` - Generates SEO-optimized title variations
6. `youtube-description-generator` - Creates YouTube descriptions

## Reference Material

Existing templates and examples can be found in:
```
C:\Users\chira\Downloads\Local - HQ - Master\Coding\n8n email attachment automation to Google Drive\
├── video-script-templates\script-template-v2
├── video-script\youtube-video-script-version-2.md
├── prompt-template\youtube-title-generation-template.md
├── prompt-template\youtube-description-generation-template.md
├── images\image-prompts\prompt-template.md
└── images\thumbnail-prompt-template.md
```

## Workflow

1. Design skill in this folder
2. Test with real use cases
3. Move to distribution folder when ready
4. Update PIPELINE-PLAN.md with status
