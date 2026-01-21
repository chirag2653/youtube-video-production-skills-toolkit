---
name: video-idea-to-context
description: Transforms a video idea into comprehensive production context by deeply analyzing the codebase, planning demo scenarios, and gathering user input. Creates video-context.md that contains everything needed for script generation. Use when building context for YouTube tutorial videos, analyzing projects for demos, or preparing technical documentation for video production.
---

# Video Idea to Context Builder

This skill transforms a video idea into comprehensive production context by analyzing your codebase, planning concrete demo scenarios, and gathering essential user input. It creates `demo-video/video-context.md` that provides everything a script writer needs without re-scanning the repo.

## Core Capabilities

- Works with or without existing `video-ideas.md` file
- Deep codebase analysis to understand application workflows
- Identifies features, integrations, and code paths
- Plans specific, executable demo scenarios with test data
- Maps external dependencies with pricing information
- Gathers user context (target audience, pain points, CTAs)
- Generates comprehensive context file ready for script generation

## Workflow Overview

The skill follows this sequence:

```
1. Tool Availability Check → Verify required tools, check for optional MCPs
2. Input Discovery → Look for video-ideas.md or ask basic questions
3. Project Detection → Identify tech stack and project type
4. Deep Analysis → Trace code paths, map workflows, identify features
5. Demo Planning → Design concrete scenarios with specific test data
6. Tool Inventory → Document dependencies with pricing (using WebSearch if available)
7. User Context → Ask targeted questions about audience, pain points, CTAs
8. Generate Output → Create video-context.md with all gathered information
```

## Phase 0: Tool Availability Check

**CRITICAL: No Hallucination Policy**

This skill NEVER makes up information it doesn't have access to. If a tool is needed but unavailable, it will stop and tell you how to configure it.

### Required Tools (Must Have)

Check for these built-in tools first:

```
✅ Read - Read files from codebase
✅ Write - Create video-context.md output
✅ Glob - Find files by pattern
✅ Grep - Search code for patterns
✅ SemanticSearch - Understand code concepts
✅ LS - Explore directory structures
```

If ANY are missing → Abort with error message:
```
❌ Required tool [TOOL_NAME] is not available.
This skill cannot proceed without core tools.
```

### Project-Specific MCP Tools

#### 1. n8n-mcp (HIGH priority for n8n workflows)

**Check when:** If `workflow.json` detected in project

**Server name:** `user-n8n-mcp`

**Key tools:**
- `n8n_get_workflow` - Parse workflow structure
- `n8n_validate_workflow` - Validate workflow
- `get_node` - Get node information

**If missing:**
```
⚠️  n8n workflow detected but n8n-mcp is not configured.

Install: npx @n8n/mcp-server
Configure in Cursor: Add to .cursor/mcp.json
Configure in Claude: Add to claude_desktop_config.json

Options:
A) I'll configure n8n-mcp now (recommended for accurate analysis)
B) Proceed with basic JSON parsing (less accurate)

Your choice: [A/B]
```

#### 2. WebSearch (MEDIUM priority for API pricing)

**Check when:** External APIs detected in code

**Tool name:** `WebSearch` (built-in in Cursor/Claude)

**Purpose:** Research tool pricing, free tiers, and setup requirements

**If missing:**
```
⚠️  External APIs detected: [List of APIs found]

I need web search to look up:
- Pricing and free tier limits
- Setup requirements
- API documentation

WebSearch tool is not available.

Options:
A) You'll provide pricing info manually (I'll ask later)
B) I'll mark pricing as "❓ Research required" (not recommended - incomplete context)

Your choice: [A/B]
```

**No Hallucination Rule:** If WebSearch unavailable and user doesn't provide info:
- Mark pricing as "Unknown - research required"
- Never guess or make up pricing information

#### 3. user-github (LOW priority - optional)

**Server name:** `user-github`

**Purpose:** Enhanced README/documentation context

**Fallback:** Read files directly with Read tool (no warning needed)

### Display Tool Status

After checking, display a clear status report:

```
🔍 Tool Availability Check

Required Tools:
✅ Read, Write, Glob, Grep, SemanticSearch, LS - Available

Project-Specific Tools:
✅ n8n-mcp - Available
⚠️  WebSearch - Not available (will ask you for pricing info)

Optional Enhancers:
ℹ️  user-github - Not available (will read files directly)

Proceeding with analysis...
```

## Phase 1: Input Discovery

Check if `demo-video/video-ideas.md` exists:

**If YES:**
1. Read the file
2. Display ideas to user
3. Ask user to select one idea
4. Extract idea details (title, type, features)
5. Note: Will still need user context later

**If NO:**
1. Ask minimal questions:
   - What type of video? (Tutorial / Feature Demo / Workflow / Integration)
   - Any specific features to highlight? (optional)
2. Continue to repo analysis
3. Will ask detailed questions after understanding the project

## Phase 2: Project Type Detection

Analyze the project structure to understand what we're working with.

### 1. Find Project Indicators

Use Glob to find key files:

```
Package files: "package.json", "requirements.txt", "pyproject.toml", "go.mod"
Entry points: "main.py", "app.py", "index.js", "server.js", "workflow.json"
Config files: "config.*", ".env.example", "settings.*"
```

### 2. Identify Tech Stack

Use Grep to find frameworks:

```
Python: "from fastapi", "from flask", "from django", "import click"
Node.js: "express()", "require('koa')", "import { Hono }"
n8n: Check workflow.json structure
React/Vue: "import React", "import { createApp }"
```

### 3. Determine Demo Approach

Based on project type:
- **Has UI** → Screen recording required
- **CLI only** → Terminal recording approach
- **API/Backend** → Postman/curl demo approach
- **n8n workflow** → n8n interface demonstration

For detailed patterns, see [references/project-type-detection-patterns.md](references/project-type-detection-patterns.md)

## Phase 3: Deep Codebase Analysis

This is the most important phase. Use SemanticSearch extensively to understand how the application actually works.

### 1. Find Entry Points

Use Glob and Read:
- Main files (main.py, index.js, app.py, server.js)
- Route definitions (API endpoints)
- CLI commands
- n8n workflow nodes

### 2. Map Core Workflows

Use SemanticSearch with queries like:
- "How does user authentication flow work?"
- "What is the main data processing pipeline?"
- "How are external API calls handled?"
- "What is the workflow from input to output?"

Read the relevant files identified by search.

### 3. Identify Key Features

Use SemanticSearch:
- "What are the main user-facing features?"
- "How does [specific feature] work?"
- "What integrations exist with external services?"

Use Grep for specifics:
- API endpoints: `"@app.route"`, `"app.get"`, `"app.post"`
- Database models: `"class.*Model"`, `"Schema ="`
- External APIs: `"api_key"`, `"requests.get"`, `"fetch("`

### 4. Trace Feature Implementations

For each key feature:
1. Find relevant code files (SemanticSearch + Grep)
2. Understand dependencies (Read key files)
3. Identify configuration needs
4. Note setup requirements
5. Check for existing tests/examples

### 5. Identify Integration Points

Find external services:
- API calls to third parties
- Database connections
- File storage (S3, Drive, etc.)
- Communication tools (Slack, email, etc.)
- Authentication services

For each integration, note:
- What service (Stripe, OpenAI, SendGrid, etc.)
- How it's used
- Configuration required
- Any API keys/credentials needed

## Phase 4: Demo Scenario Planning

Design specific, concrete scenarios that demonstrate the value of the project.

### 1. Design Flagship Scenario

The main "happy path" demonstration:
- Primary use case (most common/valuable)
- Clear input → process → output
- Demonstrates core value proposition
- Should have a "wow" moment

### 2. Design Secondary Scenarios

Variations that show flexibility:
- Different input types
- Alternative configurations
- Integration demonstrations
- Different workflows

### 3. Consider Edge Cases

Show robust error handling:
- Validation examples
- Error handling demos
- Troubleshooting scenarios

### 4. For Each Scenario, Specify:

**Setup Requirements:**
- Configuration files needed
- Environment variables
- API keys/credentials (use mock/test values)
- Service dependencies

**Test Data:**
Be SPECIFIC - don't just say "provide sample data". Instead:
```
✅ GOOD:
- users.csv (3 rows):
  - Row 1: admin user (email: admin@example.com, role: admin)
  - Row 2: regular user (email: user@example.com, role: user)
  - Row 3: guest (email: guest@example.com, role: guest)

❌ BAD:
- Provide sample user data
```

**Execution Steps:**
Numbered, concrete steps:
```
1. Run: python main.py --input users.csv --config config.json
2. System reads CSV and validates users
3. Calls API endpoint for each user (src/api/client.py, line 45)
4. Processes responses and generates report
5. Outputs: report.html and summary.json
```

**Expected Outcomes:**
Specific results:
```
- Success message: "Processed 3 users in 2.3s"
- HTML report with user cards and status badges
- JSON summary with statistics
```

For templates and examples, see [references/demo-scenario-templates.md](references/demo-scenario-templates.md)

## Phase 5: Tool & Technology Inventory

Document all external dependencies with pricing information.

### For Each External Tool/Service:

1. **Tool Name**
2. **Purpose** - What role it plays in the workflow
3. **Pricing:**
   - If WebSearch available → Research current pricing
   - If WebSearch NOT available → Mark as "User to provide" and ask later
   - Never guess or hallucinate pricing information

4. **Setup Complexity** - Easy / Medium / Hard
5. **Alternatives** - Any substitutes available

### Pricing Research with WebSearch

If WebSearch is available, research each tool:

```
Search: "[Tool Name] pricing free tier 2026"
Search: "[Tool Name] API rate limits"
Search: "[Tool Name] setup requirements"
```

Extract:
- Free tier limits
- When payment is needed
- Approximate costs for typical usage

### If WebSearch Unavailable

Add to your user questions list (Phase 7):
```
I detected these external services:
- n8n
- LlamaCloud
- Stripe
- [etc.]

For the video context, I need pricing information.
Please provide for each:
- Free tier limits (if any)
- When viewers need to pay
- Typical costs

OR

Would you like me to mark pricing as "Research required" and you'll add it later?
```

## Phase 6: Gather User Context

**IMPORTANT:** Do this AFTER technical analysis, not before.

By now you understand the project technically, so you can ask smarter, context-aware questions.

### Questions to Ask

Use the AskQuestion tool if available, otherwise ask conversationally.

See [references/user-context-questions.md](references/user-context-questions.md) for the complete question set.

#### 1. Target Audience (Required)

```
I analyzed your project and found it [brief summary of what it does].

Who is this video for? (select all that apply)
- [ ] Beginners learning [technology/automation/etc.]
- [ ] Experienced developers exploring [specific tools]
- [ ] Business owners wanting to automate processes
- [ ] Freelancers/agencies looking for client solutions
- [ ] Other: [specify]

What's their main goal from watching this video?
[Free text input]
```

#### 2. Pain Point / Problem Statement (Required)

```
What frustrating manual process or problem does this solve?

Example: "Manual invoice data entry from PDFs takes hours and is error-prone"

Your answer:
[Free text input]
```

#### 3. Value Proposition / Hook (Required)

```
In one sentence, what's the main benefit viewers get?

I noticed your project [technical observation]. How would you pitch this?

Example: "Automatically extract invoice data with AI and organize files without any manual work"

Your answer:
[Free text input]
```

#### 4. Tool Pricing (If WebSearch was unavailable)

Ask about each external service detected.

#### 5. Call-to-Action (Required)

```
What should viewers do after watching?

Custom build service:
- [ ] Yes, I offer custom builds
  - Contact method: [email/link]
  - Message to show: [e.g., "I can customize this for your needs"]
- [ ] No

Consultation:
- [ ] Yes, I offer consultations
  - Calendar link: [URL]
  - Details: [e.g., "Book a 30-min setup call"]
- [ ] No

Download/Resources:
- Workflow/code location: [GitHub/website/description]
- Setup guide available: [Yes/No, link if yes]

Contact Info:
- Email: [address]
- Discord: [link]
- Twitter: [@handle]
- Other: [links]
```

#### 6. Video Preferences (Optional)

```
Video style preferences:

Tone: [ ] Casual [ ] Professional [ ] Friendly (default)
Technical depth: [ ] High [ ] Medium (default) [ ] Low
Target length: [ ] 5-10min [ ] 10-20min (default) [ ] 20+min
```

## Phase 7: Generate video-context.md

Create `demo-video/video-context.md` using the template from [references/video-context-output-template.md](references/video-context-output-template.md)

The file has two main sections:

### 1. USER-PROVIDED CONTEXT (Top Section)

Fill this with all the answers from user questions:
- Problem statement / Pain point
- Target audience definition
- Value proposition / Hook
- Video preferences
- Call-to-action details

### 2. AUTO-GENERATED CONTEXT (Bottom Section)

Fill this with all your technical findings:
- Solution overview (how it works)
- Tools & technologies table
- Prerequisites and setup
- Workflow/process description
- Demo scenarios (detailed)
- Technical deep dive notes
- Key value propositions
- Assumptions and limitations
- Customization options

## Output Location

Create the file at:
```
demo-video/video-context.md
```

If the `demo-video/` folder doesn't exist, create it.

## Success Criteria

Before finishing, verify:

- [ ] All sections of video-context.md are filled meaningfully
- [ ] At least 1 flagship demo scenario with specific test data
- [ ] External tools documented with pricing (or marked "Research required")
- [ ] User context gathered (audience, pain point, CTA)
- [ ] Code paths traced (specific file/function references included)
- [ ] Expected outcomes are concrete, not vague
- [ ] No hallucinated information (pricing, capabilities, etc.)

## Example Usage

```
User: "Create video context for this n8n invoice processing workflow"

Skill:
1. ✅ Checks tools → All required available, n8n-mcp found, WebSearch available
2. 📋 Checks for video-ideas.md → Not found
3. 🔍 Analyzes workflow.json → Invoice processing automation with AI extraction
4. 🎯 Plans demos → Basic processing, high-value invoice, duplicate detection
5. 💰 Researches pricing → n8n (free tier), LlamaCloud (free with limits), etc.
6. 💬 Asks user:
   - Audience: "Business owners wanting to automate invoice processing"
   - Pain point: "Manual data entry takes 10+ hours/week"
   - CTA: Custom build offered, email provided
7. 📝 Generates video-context.md with all context
8. ✅ File ready at demo-video/video-context.md
```

## Tips for Best Results

1. **Use SemanticSearch liberally** - It's your best tool for understanding code
2. **Be specific in demo scenarios** - Include actual commands, file names, data examples
3. **Reference actual code** - Include file paths and line numbers when relevant
4. **Ask user questions AFTER analysis** - Pre-fill with what you found
5. **Never guess** - If you don't know something (pricing, capability), say so
6. **Verify tool availability** - Don't assume MCPs are configured

## Troubleshooting

**"I can't find the main entry point"**
- Use SemanticSearch: "What is the main entry point of this application?"
- Check common patterns: main.py, app.py, index.js, server.js
- Look for workflow.json (n8n projects)

**"I'm not sure what this project does"**
- Read README.md first
- Use SemanticSearch: "What does this project do?"
- Look at package.json "description" field

**"The workflow is very complex"**
- Focus on the main happy path first
- Use SemanticSearch to understand overall flow
- Break it into smaller chunks
- Trace one feature end-to-end as an example

**"WebSearch not available and user doesn't provide pricing"**
- Mark pricing as "❓ Research required"
- Add note: "User will research pricing before script generation"
- Never make up pricing information

## Reference Files

- [references/project-type-detection-patterns.md](references/project-type-detection-patterns.md) - How to detect project types
- [references/demo-scenario-templates.md](references/demo-scenario-templates.md) - Demo scenario examples
- [references/user-context-questions.md](references/user-context-questions.md) - Complete question set
- [references/video-context-output-template.md](references/video-context-output-template.md) - Output file template
