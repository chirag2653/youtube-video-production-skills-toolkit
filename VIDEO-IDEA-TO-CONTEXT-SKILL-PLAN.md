# Video Idea to Context Skill - Design Plan

## Purpose

This document defines the design and workflow for the `video-idea-to-context` skill, which transforms a video idea into comprehensive production context by analyzing the codebase and planning demo scenarios.

---

## Skill Overview

**Name:** `video-idea-to-context`

**Input Artifacts:**
- `demo-video/video-ideas.md` (optional - if exists, user selects one idea)
- Project codebase (required - the repo being analyzed)

**Output Artifact:**
- `demo-video/video-context.md` (comprehensive context for script generation)

**Core Capabilities:**
1. Work with or without pre-existing video-ideas.md file
2. Deep codebase analysis to understand application flow
3. Identify key features, workflows, and integration points
4. Plan specific demo scenarios with test data
5. Map code paths to demonstrate value propositions
6. Generate comprehensive context for script writers

---

## Workflow Architecture

### Phase 0: Tool Availability Check (NEW!)
**Goal:** Verify required tools and check for optional enhancers

```
START
  │
  ├─ Check Required Tools (Read, Write, Glob, Grep, SemanticSearch, LS)
  │   └─ If ANY missing → ABORT with error message
  │
  ├─ Detect Project Type (quick scan)
  │   ├─ Check for workflow.json → n8n project
  │   ├─ Check for package.json → Node.js project
  │   ├─ Check for requirements.txt → Python project
  │   └─ Etc.
  │
  ├─ Check Project-Specific Tools
  │   │
  │   ├─ IF n8n project:
  │   │   ├─ Check for user-n8n-mcp server
  │   │   └─ If missing → Warn user, offer fallback
  │   │
  │   └─ Scan for external API usage (quick Grep)
  │       ├─ If external APIs found:
  │       ├─ Check for WebSearch tool
  │       └─ If missing → Warn user about pricing research limitation
  │
  ├─ Check Optional Enhancers
  │   ├─ user-github → If available, will use; if not, direct file reading
  │   └─ (Silent check, no warnings)
  │
  ├─ Display Tool Status Report
  │   (Show user what's available and any limitations)
  │
  └─ PROCEED TO PHASE 1
```

### Phase 1: Input Discovery & Validation
**Goal:** Determine if working from existing ideas or starting fresh

```
START
  │
  ├─ Check: Does demo-video/video-ideas.md exist?
  │   │
  │   ├─ YES → Present ideas, ask user to select one
  │   │   ├─ Extract selected idea details
  │   │   ├─ Extract any user-provided context (if present)
  │   │   └─ Note: Will still need to ask remaining questions later
  │   │
  │   └─ NO → Ask minimal questions to understand intent
  │       ├─ What type of video? (tutorial, feature demo, workflow, integration)
  │       ├─ Any specific features to highlight? (optional)
  │       └─ Note: Will ask detailed questions AFTER repo analysis
  │
  └─ PROCEED TO PHASE 2 (Repo Analysis)
     
     [Phases 2-4: Deep repo analysis happens here]
     
  └─ AFTER PHASE 4 → Gather User Context (NEW!)
      │
      ├─ Now that we understand the project technically,
      │  ask context-aware questions:
      │
      ├─ 1. Target Audience
      │   └─ "I found this workflow automates [X]. Who is this for?"
      │       Options based on what was found in code
      │
      ├─ 2. Pain Point
      │   └─ "What manual process does this replace?"
      │       Suggest based on code understanding
      │
      ├─ 3. Value Proposition
      │   └─ "What's the key benefit? I noticed it [does X]"
      │       Pre-fill with technical findings
      │
      ├─ 4. Tool Pricing (if WebSearch unavailable)
      │   └─ "I detected: [n8n, LlamaCloud]. Provide pricing or research manually?"
      │
      ├─ 5. Call-to-Action
      │   └─ "Do you offer custom builds? Provide contact info?"
      │
      └─ 6. Video Preferences
          └─ "Tone, depth, length preferences?"
```

**Key Change:** User context questions happen AFTER technical analysis, not before. This allows for smarter, context-aware questions.

### Phase 2: Project Type Detection
**Goal:** Understand what type of project we're working with

```
Analyze project structure:
  │
  ├─ Check for key indicators:
  │   ├─ n8n workflow (workflow.json)
  │   ├─ Python project (requirements.txt, setup.py, pyproject.toml)
  │   ├─ Node.js project (package.json, node_modules)
  │   ├─ Web app (HTML/CSS/JS, React, Vue, etc.)
  │   ├─ API/Backend (FastAPI, Express, Django, etc.)
  │   ├─ CLI tool (bin/, scripts/, main entry point)
  │   ├─ Library/Package (src/, lib/, module structure)
  │   └─ Mixed/Monorepo (multiple sub-projects)
  │
  ├─ Identify tech stack:
  │   ├─ Languages (Python, JavaScript, TypeScript, Go, etc.)
  │   ├─ Frameworks (React, FastAPI, Express, etc.)
  │   ├─ External services (APIs, databases, cloud services)
  │   └─ Key dependencies (significant libraries)
  │
  └─ Determine demo approach:
      ├─ Does it have a UI? → Screen recording required
      ├─ CLI only? → Terminal recording approach
      ├─ API? → Postman/curl demo approach
      └─ Workflow? → n8n interface or results demonstration
```

### Phase 3: Deep Codebase Analysis
**Goal:** Understand how the application actually works

```
Systematic code exploration:
  │
  ├─ 1. Find entry points:
  │   ├─ Main files (main.py, index.js, app.py, server.js)
  │   ├─ Route definitions (API endpoints)
  │   ├─ CLI commands (click, argparse, commander)
  │   └─ Workflow nodes (n8n JSON structure)
  │
  ├─ 2. Map core workflows:
  │   ├─ User-facing features (what users interact with)
  │   ├─ Data flow (input → processing → output)
  │   ├─ Integration points (external APIs, services)
  │   └─ State management (databases, sessions, storage)
  │
  ├─ 3. Identify key value propositions:
  │   ├─ What problem does it solve?
  │   ├─ What's unique or impressive?
  │   ├─ What saves time/money/effort?
  │   └─ What's the "wow" moment?
  │
  ├─ 4. Trace feature implementations:
  │   For each feature mentioned in video idea:
  │   ├─ Find relevant code files
  │   ├─ Understand dependencies
  │   ├─ Identify configuration needs
  │   ├─ Note any setup requirements
  │   └─ Check for existing tests/examples
  │
  └─ 5. Assess demo readiness:
      ├─ What works out of the box?
      ├─ What needs configuration?
      ├─ What requires test data?
      └─ Any broken/incomplete features?
```

### Phase 4: Demo Scenario Planning
**Goal:** Design specific, concrete scenarios to demonstrate in the video

```
For each key feature/workflow:
  │
  ├─ Design flagship scenario:
  │   ├─ Primary use case (most common/valuable)
  │   ├─ Clear input → process → output
  │   ├─ Demonstrates core value prop
  │   └─ Should have "wow" moment
  │
  ├─ Design secondary scenarios:
  │   ├─ Variations showing flexibility
  │   ├─ Different input types/configs
  │   ├─ Alternative workflows
  │   └─ Integration demonstrations
  │
  ├─ Consider edge cases:
  │   ├─ Error handling demos
  │   ├─ Validation examples
  │   ├─ Performance demonstrations
  │   └─ Troubleshooting scenarios
  │
  └─ For each scenario, define:
      ├─ Setup requirements:
      │   ├─ Configuration files needed
      │   ├─ API keys/credentials (mock if sensitive)
      │   ├─ Environment variables
      │   └─ Service dependencies
      │
      ├─ Test data:
      │   ├─ Sample input files
      │   ├─ Mock API responses
      │   ├─ Database seed data
      │   └─ Example configurations
      │
      ├─ Execution steps:
      │   ├─ Step-by-step user actions
      │   ├─ Commands to run
      │   ├─ UI interactions
      │   └─ Expected timing (for pacing)
      │
      └─ Expected outcomes:
          ├─ Success indicators
          ├─ Output examples
          ├─ Visual results
          └─ Performance metrics
```

### Phase 5: Tool & Technology Inventory
**Goal:** Document all tools/services viewers need to replicate

```
For each external dependency:
  │
  ├─ Tool/Service name
  ├─ Purpose (why it's needed)
  ├─ Pricing tier:
  │   ├─ Free tier limits
  │   ├─ Paid tier (if needed for demo)
  │   └─ Cost estimate for viewer
  ├─ Setup complexity (easy/medium/hard)
  ├─ Alternatives (if any)
  └─ Documentation links
```

### Phase 6: Context Document Generation
**Goal:** Synthesize all gathered information into video-context.md

```
Build structured output:
  │
  ├─ Video Title & Overview
  │   ├─ Working title (can be refined later)
  │   ├─ One-line hook
  │   └─ Estimated video length
  │
  ├─ Problem Statement
  │   ├─ What pain point addressed?
  │   ├─ Current bad solutions
  │   └─ Why it matters
  │
  ├─ Solution Overview
  │   ├─ What viewer will build/learn
  │   ├─ High-level approach
  │   └─ Key benefits
  │
  ├─ Target Audience
  │   ├─ Skill level required
  │   ├─ Prior knowledge needed
  │   └─ Persona description
  │
  ├─ Tools & Technologies Table
  │   (From Phase 5 analysis)
  │
  ├─ Prerequisites
  │   ├─ Required software/accounts
  │   ├─ Background knowledge
  │   └─ Time estimate
  │
  ├─ Workflow/Process
  │   ├─ High-level flow diagram (text)
  │   ├─ Step-by-step sequence
  │   └─ Decision points
  │
  ├─ Demo Scenarios (Detailed)
  │   ├─ Flagship scenario with full details
  │   ├─ Secondary scenarios
  │   ├─ Edge cases to show
  │   └─ For each: setup, data, steps, outcomes
  │
  ├─ Key Value Propositions
  │   ├─ Time saved
  │   ├─ Cost benefits
  │   ├─ Quality improvements
  │   └─ Unique capabilities
  │
  ├─ Technical Deep Dive Notes
  │   ├─ Code paths explained
  │   ├─ Architecture decisions
  │   ├─ Integration patterns
  │   └─ Performance considerations
  │
  ├─ Assumptions & Limitations
  │   ├─ What we assume viewer has
  │   ├─ What's out of scope
  │   └─ Known limitations to mention
  │
  ├─ Customization Options
  │   ├─ How viewers can adapt it
  │   ├─ Configuration options
  │   └─ Extension points
  │
  └─ Call-to-Action Ideas
      ├─ Custom build services
      ├─ Consultation offers
      ├─ Download links
      └─ Community/contact info
```

---

## Key Design Decisions

### 1. Flexible Input Handling
- **Design:** Skill works both with and without video-ideas.md
- **Rationale:** Users might want to create context directly, or ideas file might be elsewhere
- **Implementation:** Check for file first, then pivot to questions if not found

### 2. Deep vs. Shallow Analysis
- **Design:** Conduct thorough code analysis, not just surface-level
- **Rationale:** Script generator needs to understand actual implementation details
- **Implementation:** Trace code paths, read key files, map dependencies

### 3. Concrete Demo Planning
- **Design:** Create specific, executable demo scenarios (not vague suggestions)
- **Rationale:** Script writer needs exact steps, data, and outcomes
- **Implementation:** For each scenario, define setup, data, steps, and expected results

### 4. Test Data Specification
- **Design:** List exactly what test data is needed (but don't create it yet)
- **Rationale:** Keeps skill focused, but ensures nothing is forgotten
- **Implementation:** "Demo with: users.csv (3 rows: admin, regular user, guest), config.json (API key: test_key_123)"

### 5. Code-Aware Context
- **Design:** Include technical details (file paths, function names, endpoints)
- **Rationale:** Script generator might need to reference specific code
- **Implementation:** "The /api/process endpoint (in src/api/routes.py, process_request function) handles..."

---

## Tool Dependencies & "No Hallucination" Policy

### Phase 0: Tool Availability Check

**CRITICAL RULE:** The skill must NEVER hallucinate information it doesn't have access to. If a tool is needed but unavailable, the skill must:
1. Stop execution
2. Tell the user which tool is needed
3. Provide installation instructions
4. Wait for user to configure the tool

### Required Tools (Built-in - Must Have)

These are available in both Cursor and Claude Code Agents:

| Tool | Purpose | Failure Handling |
|------|---------|------------------|
| `Read` | Read files from codebase | Abort if unavailable |
| `Write` | Create video-context.md output | Abort if unavailable |
| `Glob` | Find files by pattern | Abort if unavailable |
| `Grep` | Search code for patterns | Abort if unavailable |
| `SemanticSearch` | Understand code concepts | Abort if unavailable |
| `LS` | Explore directory structures | Abort if unavailable |

**Check Method:**
```markdown
Try to use each tool. If any fail → Display error:
"❌ Required tool [TOOL_NAME] is not available. This skill cannot proceed."
```

### Optional MCP Tools (Project-Specific)

#### 1. n8n-mcp Server (Priority: HIGH for n8n projects)

**Server Name:** `user-n8n-mcp`

**Key Tools:**
- `n8n_get_workflow` - Parse workflow.json structure
- `n8n_validate_workflow` - Validate workflow integrity
- `get_node` - Get node type information
- `get_template` - Get workflow templates

**When Needed:** If `workflow.json` detected in project

**Check Method:**
```markdown
1. Check if workflow.json exists (using Glob)
2. If YES:
   - Check if user-n8n-mcp server is available
   - If NOT available → Stop and show message:
     
     "⚠️  n8n workflow detected but n8n-mcp is not configured.
     
     Options:
     1. Install n8n-mcp: `npx @n8n/mcp-server`
     2. Configure in Cursor: Add to .cursor/mcp.json
     3. Configure in Claude: Add to claude_desktop_config.json
     
     Cannot analyze workflow accurately without this tool.
     
     Proceed anyway with basic JSON parsing? (Y/N)"
```

**Fallback:** Basic JSON parsing (less accurate, warn user)

#### 2. WebSearch Tool (Priority: MEDIUM for API pricing research)

**Tool Name:** `WebSearch` (built-in) OR web search MCP

**When Needed:** When external APIs/services detected in code (Stripe, OpenAI, SendGrid, etc.)

**Check Method:**
```markdown
1. Detect external API usage (Grep for api_key, API calls, etc.)
2. If external APIs found:
   - Check if WebSearch tool is available
   - If NOT available → Stop and show message:
     
     "⚠️  External APIs detected: [Stripe, OpenAI, etc.]
     
     I need web search to look up:
     - Pricing/free tier limits
     - Setup requirements
     - API documentation
     
     No web search tool available.
     
     Options:
     1. If in Cursor/Claude with built-in WebSearch: Should be available
     2. Install web-search MCP server
     3. Proceed with generic assumptions (NOT RECOMMENDED - may be inaccurate)
     
     How would you like to proceed?"
```

**No Hallucination Rule:** If WebSearch unavailable and user doesn't provide info:
- Mark pricing as "Unknown (research required)"
- Add to Tools table: "Pricing: ❓ Research needed"
- DO NOT guess or make up pricing info

#### 3. user-github Server (Priority: LOW)

**Server Name:** `user-github`

**When Needed:** For enhanced README/documentation context

**Check Method:**
```markdown
- If available → Use to fetch README, repo description
- If NOT available → Read README.md directly with Read tool
- No warning needed (graceful fallback)
```

**Fallback:** Direct file reading (works fine)

### Tool Usage Patterns

#### Phase 2: Project Type Detection

**Glob:**
```
Find entry points: "*.py", "main*", "app.py", "server.js", "index.js", "workflow.json"
Locate config: "config.*", ".env.example", "settings.*"
Find package files: "package.json", "requirements.txt", "pyproject.toml", "go.mod"
```

**Grep:**
```
Find frameworks: 
  - Python: "from fastapi", "from flask", "from django"
  - Node: "express()", "require('koa')", "import { Hono }"
  - n8n: Look in workflow.json
```

#### Phase 3: Deep Codebase Analysis

**SemanticSearch:** (Most important tool for this phase!)
```
Understanding workflows:
  - query: "How does user authentication flow work?"
  - query: "What is the main data processing pipeline?"
  - query: "How are external API calls handled?"

Finding integrations:
  - query: "Where are external API calls made?"
  - query: "What databases or storage systems are used?"
  - query: "How does the application handle errors?"

Identifying features:
  - query: "What are the main user-facing features?"
  - query: "How does [specific feature] work?"
  - query: "What are the key configuration options?"
```

**Grep:**
```
Find API endpoints: "@app.route", "app.get", "app.post", "@router"
Locate models: "class.*Model", "Schema =", "interface.*{"
Find CLI commands: "@click.command", "commander.command", "argparse"
External APIs: "api_key", "API_KEY", "requests.get", "fetch("
```

**Read:**
```
Priority order:
1. README.md (project overview)
2. Main entry point (main.py, index.js, app.py)
3. Configuration examples (.env.example, config.sample.json)
4. Package files (requirements.txt, package.json)
5. Key implementation files (identified by SemanticSearch)
```

#### Phase 4: Demo Scenario Planning

**n8n-mcp (if n8n project):**
```
Use: n8n_get_workflow to understand node structure
Use: get_node to understand node capabilities
Use: n8n_validate_workflow to check if workflow is functional
```

**WebSearch (if external APIs detected):**
```
For each external API:
  query: "[API Name] pricing free tier 2026"
  query: "[API Name] API rate limits"
  query: "[API Name] setup requirements"
```

### Tool Check Output Example

When the skill starts, it should display:

```
🔍 Checking tool availability...

Required Tools:
✅ Read - Available
✅ Write - Available
✅ Glob - Available
✅ Grep - Available
✅ SemanticSearch - Available
✅ LS - Available

Project-Specific Tools:
✅ n8n-mcp - Available (workflow.json detected)
⚠️  WebSearch - Not available
   → External APIs detected: Stripe, OpenAI
   → Will mark pricing as "Unknown (research required)"
   → Recommend: Configure web search or provide pricing info manually

Optional Enhancers:
ℹ️  user-github - Not available (will read files directly)

Proceeding with analysis...
```

---

## Context Requirements Analysis (Reverse-Engineered from Real Script)

After analyzing a professional YouTube tutorial script, here's what context the script generator needs:

### Information Sources

#### 🤖 FROM REPO ANALYSIS (Automatic)
The skill can gather these by analyzing the codebase:

1. **Technical Implementation Details**
   - Workflow structure (n8n nodes, code modules, API calls)
   - Key features and capabilities
   - Integration points (external APIs, databases, services)
   - Configuration requirements (env vars, API keys, credentials)
   - Error handling and validation logic
   - Data flow (input → processing → output)
   - Code-level design decisions (thresholds, filters, logic)

2. **Tools & Technologies**
   - All tools/services detected in code
   - How each tool is used (purpose/role)
   - Integration patterns
   - Configuration needs

3. **Demo Scenario Design** (Code-Driven)
   - Flagship scenario (primary happy path)
   - Edge cases (error handling, validation)
   - Variations (different inputs/outputs)
   - Expected behavior (inferred from code logic)

4. **Customization Points**
   - Alternative tool options (if/else branches, modular structure)
   - Extension points (plugins, hooks, config options)
   - Swap-able components

5. **Workflow Assumptions**
   - Input format expectations (from validation logic)
   - Output format guarantees
   - Data structure requirements

#### 👤 FROM USER INPUT (Manual - Must Ask!)
The skill CANNOT gather these automatically:

1. **Target Audience Definition**
   - Who is this video for? (specific persona)
   - What do they want to accomplish? (goals)
   - Skill level? (beginner/intermediate/advanced)
   - Pain points they experience
   - Example from script:
     ```
     "This tutorial is perfect if you want to:
     - Automate invoice processing and eliminate manual data entry
     - Organize your invoice files automatically with smart naming
     - See what's possible with n8n and AI automation"
     ```

2. **Pain Point / Problem Statement**
   - What frustrating manual process does this solve?
   - Why does it matter?
   - Current bad solutions
   - Example: "Manual invoice data entry takes hours and is error-prone"

3. **Value Proposition / Hook**
   - Why should viewers watch this?
   - What's the "wow" factor?
   - Time/money/effort saved
   - Example: "Watches your Gmail inbox for invoice emails, uses AI to extract data, saves everything to Google Drive"

4. **Tool Pricing Information** ⚠️ REQUIRES WebSearch
   - Free tier limits
   - When you need to pay
   - Cost estimates
   - Example from script: "Always Free (with limits) | When you exceed free tier execution limits"
   - **If WebSearch unavailable:** Mark as "❓ Research required" and ask user to provide

5. **Call-to-Action / Final Offer**
   - Custom build service? (Y/N + details)
   - Consultation offer? (Y/N + calendar link)
   - Download links? (where to find workflow)
   - Contact info (email, Discord, Twitter)
   - Example from script:
     ```
     "If you'd rather have someone build it for you or handle customization,
     I'm happy to help. You can find my email in the description below."
     ```

6. **Personal Preferences**
   - Video tone (formal/casual/friendly)
   - Level of technical detail (high/medium/low)
   - Video length target (5-10min, 10-20min, 20+min)
   - Branding elements (logo, colors, intro/outro)

7. **Scenario Test Data Specifics** (Optional but helpful)
   - Real-world example data (company names, amounts, dates)
   - User may have preferences: "Use CloudProvider-Inc as vendor"
   - Skill can generate generic data if not provided

### Key Insights from Script Analysis

From analyzing the professional script (`youtube-video-script-version-2.md`):

**What Makes a Good Script:**
1. **Clear "Who This Is For" section** (Section 3) - Requires user to define target audience and pain points
2. **Detailed Tools Table** (Section 4) - Requires pricing research (WebSearch) or user input
3. **Workflow Assumptions** (Section 5) - Can be inferred from code validation logic
4. **Multiple Concrete Scenarios** (Sections 8-10) - Can be designed from code paths
5. **Customization Ideas** (Section 11) - Can be identified from code structure
6. **Personal Call-to-Action** (Section 12-13) - Requires user input (contact, offers)

**Script Structure Pattern:**
- Welcome (generic)
- What You'll Learn (from code understanding)
- Who This Is For (USER INPUT REQUIRED)
- Tools Stack with pricing (WEBSEARCH or USER INPUT)
- Assumptions (from code analysis)
- Setup confirmation (from code requirements)
- Demo scenarios (from code paths + test data)
- Customization options (from code structure)
- Call-to-action (USER INPUT REQUIRED)
- Download/resources (USER INPUT REQUIRED)
- Closing (generic)

**Critical User Inputs Identified:**
1. Target audience definition (cannot be automated)
2. Pain point articulation (user's perspective)
3. Value proposition hook (user's marketing angle)
4. Tool pricing (if WebSearch unavailable)
5. Personal offers (custom build, consultation)
6. Contact information and links

### User Input Collection Strategy

The skill should ask these questions AFTER repo analysis:

```markdown
## User Input Required

I've analyzed your project and understand how it works technically. 
Now I need some context from you to create compelling video content:

### 1. Target Audience (Required)
Who is this video for? Select all that apply:
- [ ] Beginners learning automation
- [ ] Experienced developers exploring n8n/LlamaCloud
- [ ] Business owners wanting to automate processes
- [ ] Freelancers/agencies looking for client solutions

What's their main goal?
[Free text: e.g., "Automate invoice processing to save time"]

### 2. Pain Point (Required)
What frustrating manual process does this solve?
[Free text: e.g., "Manual data entry from invoice PDFs takes hours"]

### 3. Key Value Proposition (Required)
In one sentence, what's the main benefit?
[Free text: e.g., "Automatically extract invoice data with AI and organize files"]

### 4. Call-to-Action (Required)
What should viewers do after watching?

- [ ] Offer custom build service
  - Contact: [email/link]
  - Message: [e.g., "I can build this for your specific needs"]

- [ ] Offer consultation
  - Calendar link: [URL]
  - Duration: [e.g., "30-min setup call"]

- [ ] Provide download
  - Location: [GitHub, description, website]
  - Setup guide: [link or "included"]

- [ ] Community/Contact
  - Discord: [link]
  - Email: [address]
  - Twitter: [handle]

### 5. Tool Pricing (If WebSearch unavailable)
⚠️ I detected these external services: [n8n, LlamaCloud, etc.]

I need web search to look up their pricing automatically.
WebSearch is not available.

Options:
A) You provide pricing info manually (I'll format it)
B) I mark pricing as "Research required" (not recommended)

Your choice: [A/B]

If A, please provide for each tool:
- Free tier limits
- When payment is needed
- Approximate costs

### 6. Video Preferences (Optional)
- Tone: [Casual/Professional/Friendly] (default: Friendly)
- Technical depth: [High/Medium/Low] (default: Medium)
- Target length: [5-10min/10-20min/20+min] (default: 10-20min)
```

## Output Template Structure

The skill will use this as the template for `video-context.md`:

```markdown
# Video Context: [Title]

**Generated:** [Date]
**Project:** [Project Name]
**Type:** [Tutorial/Feature Demo/Workflow/Integration]

---

## 📌 USER-PROVIDED CONTEXT

> This section contains information provided by the user that cannot be automatically gathered from code.

### Problem Statement / Pain Point
**What frustrating problem does this solve?**
[User's answer - e.g., "Manual invoice data entry from PDFs takes hours and is error-prone"]

**Why it matters:**
[Impact - e.g., "Finance teams waste 10+ hours/week on data entry that could be automated"]

### Target Audience
**Who is this video for?**
[User's selection - e.g., "Business owners wanting to automate back-office processes, freelancers offering automation services"]

**Their main goal:**
[What they want to accomplish - e.g., "Automate invoice processing to eliminate manual data entry"]

**Skill level:** [Beginner/Intermediate/Advanced]
**Assumes viewer knows:** [Prerequisites from user]

### Key Value Proposition / Hook
**One-sentence benefit:**
[User's input - e.g., "Watch your Gmail inbox for invoice emails, use AI to extract data, and organize everything automatically"]

**"Wow" factor:**
[Most impressive aspect - e.g., "AI reads PDFs and extracts structured data—no manual typing"]

### Video Preferences
- **Tone:** [Casual/Professional/Friendly]
- **Technical depth:** [High/Medium/Low]
- **Target length:** [5-10min / 10-20min / 20+min]

### Call-to-Action
**Custom build service:**
- Offered: [Yes/No]
- Contact: [email/link]
- Message: ["I can customize this workflow for your specific needs"]

**Consultation:**
- Offered: [Yes/No]
- Link: [calendar link]
- Details: ["Book a 30-min setup call"]

**Download/Resources:**
- Workflow JSON: [GitHub/website/description]
- Setup guide: [link or included]
- Sample data: [link if provided]

**Community/Contact:**
- Discord: [link]
- Email: [email]
- Twitter: [@handle]
- Other: [links]

---

## 🤖 AUTO-GENERATED CONTEXT

> This section is automatically gathered from codebase analysis.

### Solution Overview

[What does the viewer learn/build? High-level approach and key benefits - generated from code understanding]

---

## Tools & Technologies

| Tool | Purpose | Pricing | Setup Complexity |
|------|---------|---------|------------------|
| Tool 1 | What it does | Free tier info | Easy/Medium/Hard |
| Tool 2 | What it does | Cost details | Easy/Medium/Hard |

---

## Prerequisites

**Required:**
- [ ] Software/account 1
- [ ] Software/account 2

**Background Knowledge:**
- Understanding of X
- Familiarity with Y

**Time Estimate:** ~X hours to follow along

---

## Workflow/Process

```
Step 1: [High-level description]
   ↓
Step 2: [High-level description]
   ↓
Step 3: [High-level description]
```

**Detailed Flow:**
1. User starts with [input]
2. System processes via [method/code path]
3. Result appears as [output]

---

## Demo Scenarios

### 1. Flagship Scenario: [Name]
**Purpose:** [Main value prop demonstration]

**Setup Requirements:**
- Config file: `config.json` with:
  ```json
  {
    "api_key": "demo_key_123",
    "endpoint": "https://api.example.com"
  }
  ```
- Environment: `API_SECRET=test_secret`

**Test Data:**
- `users.csv` (3 rows):
  - Row 1: admin user (email: admin@example.com, role: admin)
  - Row 2: regular user (email: user@example.com, role: user)
  - Row 3: guest (email: guest@example.com, role: guest)

**Execution Steps:**
1. Run: `python main.py --input users.csv --config config.json`
2. System reads CSV and validates users
3. Calls API endpoint for each user (src/api/client.py, line 45)
4. Processes responses and generates report
5. Outputs: `report.html` and `summary.json`

**Expected Outcome:**
- Success message: "Processed 3 users in 2.3s"
- HTML report with user cards and status badges
- JSON summary with statistics

**Demo Timing:** ~3-4 minutes

### 2. Secondary Scenario: [Name]
[Similar detailed structure...]

### 3. Edge Case Demo: [Name]
**Purpose:** Show error handling/validation
[Similar structure...]

---

## Technical Deep Dive Notes

**Key Code Paths:**
- Entry point: `src/main.py` → `main()` function (line 12)
- Core logic: `src/processor.py` → `process_data()` (line 89)
- API integration: `src/api/client.py` → `fetch_user_data()` (line 45)

**Architecture Decisions:**
- Uses async/await for parallel API calls (improves performance 3x)
- Caches responses in memory (reduces API calls)
- Validates input with Pydantic models (type safety)

**Integration Points:**
- External API: Uses REST API with JWT authentication
- Database: SQLite for local caching (optional)
- File I/O: Supports CSV, JSON, and Excel inputs

**Performance Notes:**
- Processes ~100 rows/second
- Memory usage: ~50MB for typical workload
- Handles up to 10k rows efficiently

---

## Key Value Propositions

1. **Time Savings:** Automates 2-hour manual process to 5 minutes
2. **Cost Reduction:** Eliminates need for [expensive tool] ($99/month)
3. **Quality Improvement:** 100% consistent validation vs error-prone manual work
4. **Scalability:** Handles 10k records easily vs manual limit of ~100
5. **Flexibility:** Supports multiple input formats and custom configurations

---

## Assumptions

- Viewer has Python 3.8+ installed
- Viewer comfortable with command line basics
- Viewer has used APIs before (familiar with JSON, HTTP)
- Project setup takes ~10 minutes
- Demo examples use test/mock data (no real credentials required)

---

## Limitations & Caveats

- Does not support real-time streaming (batch processing only)
- API rate limits may affect large datasets (mention workarounds)
- Requires internet connection for API calls
- Windows users need WSL for shell scripts (provide PowerShell alternatives)

---

## Customization Options

**For Viewers:**
- Swap CSV for Excel input (change `--format` flag)
- Use different API endpoints (modify config.json)
- Add custom validation rules (extend validator classes)
- Change output format (HTML, PDF, JSON, CSV)

**Extension Points:**
- Plugin system for custom processors (src/plugins/)
- Config file supports custom templates
- API client can be subclassed for different services

---

## Call-to-Action Ideas

- **Custom Build:** "Need this tailored to your workflow? [Contact link]"
- **Consultation:** "Book 30-min setup call: [Calendar link]"
- **Downloads:** 
  - GitHub repo: [link]
  - Sample data: [link]
  - Config templates: [link]
- **Community:**
  - Discord: [link]
  - Email: your@email.com
  - Twitter: @yourhandle

---

## Notes for Script Writer

[Any additional context that doesn't fit above categories but would help with script writing]

- Emphasize the "wow" moment when results appear in under 3 seconds
- Show side-by-side comparison (manual vs automated) in intro
- Use real terminal window (not slides) for CLI demos
- Mention common pitfalls during setup (API key format, file permissions)
- Consider adding a "troubleshooting" segment (3 most common errors)
```

---

## Iteration Strategy (22 Iterations Total)

### Iteration 1-4: Foundation
- [ ] **Iteration 1:** Create skill structure and SKILL.md outline
- [ ] **Iteration 2:** Implement Phase 0 (Tool Availability Check) with "No Hallucination" policy
- [ ] **Iteration 3:** Implement Phase 1 (Input Discovery) logic
- [ ] **Iteration 4:** Implement Phase 2 (Project Type Detection)

### Iteration 5-8: Analysis Engine
- [ ] **Iteration 5:** Implement Phase 3 (Deep Codebase Analysis) - Entry points
- [ ] **Iteration 6:** Phase 3 continued - Workflow mapping
- [ ] **Iteration 7:** Phase 3 continued - Value proposition identification
- [ ] **Iteration 8:** Phase 3 continued - Feature tracing and demo readiness

### Iteration 9-12: Demo Planning
- [ ] **Iteration 9:** Implement Phase 4 (Demo Scenario Planning) - Flagship scenario design
- [ ] **Iteration 10:** Phase 4 continued - Secondary scenarios and edge cases
- [ ] **Iteration 11:** Phase 4 continued - Test data specification
- [ ] **Iteration 12:** Phase 4 continued - Execution steps and outcomes

### Iteration 13-16: User Context & Assembly
- [ ] **Iteration 13:** Implement User Context Collection (ask questions after analysis)
- [ ] **Iteration 14:** Implement Phase 5 (Tool & Technology Inventory)
- [ ] **Iteration 15:** Implement Phase 6 (Context Document Generation) - User-provided section
- [ ] **Iteration 16:** Phase 6 continued - Auto-generated section

### Iteration 17-19: Reference Materials
- [ ] **Iteration 17:** Create reference file: project-type-detection-patterns.md
- [ ] **Iteration 18:** Create reference file: demo-scenario-templates.md
- [ ] **Iteration 19:** Create reference file: video-context-examples.md

### Iteration 20-22: Testing & Refinement
- [ ] **Iteration 20:** Test on Python CLI project (full flow including user questions)
- [ ] **Iteration 21:** Test on Web app project (full flow including user questions)
- [ ] **Iteration 22:** Test on n8n workflow project, final refinements

---

## Success Criteria

The skill is complete when:

1. **Works standalone:** Functions without video-ideas.md file
2. **Works integrated:** Properly consumes video-ideas.md when available
3. **Deep analysis:** Traces actual code paths, not just surface inspection
4. **Concrete demos:** Produces executable demo scenarios with specific data
5. **Tool-aware:** Identifies all external dependencies with pricing/setup info
6. **Script-ready:** Output enables script writer to work without scanning repo
7. **Comprehensive:** All sections of video-context.md template filled meaningfully
8. **Tested:** Works on 3+ different project types (CLI, web, workflow)
9. **No Hallucination Policy:** Never makes up information it doesn't have access to
10. **Tool Check:** Verifies required tools before starting, warns about missing optional tools
11. **Graceful Degradation:** Works with minimal tools, enhances with optional tools

---

## Measurement: Output Quality Check

A good `video-context.md` should have:

- [ ] **Problem Statement:** Clear, relatable pain point (not generic)
- [ ] **Demo Scenarios:** Minimum 1 flagship + 1 secondary scenario
- [ ] **Test Data:** Specific examples for each scenario (not "provide sample data")
- [ ] **Execution Steps:** Numbered, concrete steps with actual commands/actions
- [ ] **Expected Outcomes:** Specific outputs/results (not "data will be processed")
- [ ] **Tools Table:** Every external dependency listed with pricing
- [ ] **Code Paths:** At least 3 specific file/function references
- [ ] **Value Props:** Quantified benefits (time, cost, quality) not vague claims
- [ ] **Technical Notes:** Architecture decisions or interesting implementation details
- [ ] **Assumptions:** Explicit about what viewer needs to know/have

---

## Future Enhancements (Post-V1)

- Interactive mode: Ask follow-up questions to refine context
- Code execution: Actually run the project to verify demo scenarios
- Screenshot capture: Generate demo screenshots automatically
- Video length optimizer: Adjust detail based on target length
- Multi-video planning: Suggest series structure for complex projects
- Test data generator: Create actual sample files (not just specifications)

---

## Iteration Log

### Session 1 (Current)
- Created initial skill design document
- Defined 6-phase workflow architecture (Phases 1-6)
- Established input/output contracts
- Outlined iteration strategy (20 iterations)
- Defined success criteria and quality metrics
- Documented tool usage patterns

### Session 1 - Update 1
- **Added Phase 0: Tool Availability Check**
- **Implemented "No Hallucination" Policy:** Skill will never make up information
- **Specified exact MCP servers and tool names:**
  - `user-n8n-mcp` with tools: `n8n_get_workflow`, `n8n_validate_workflow`, `get_node`
  - `WebSearch` (built-in) for API pricing research
  - `user-github` (optional) for enhanced README context
- **Defined tool check strategy:**
  - Required tools → Abort if missing
  - Project-specific tools (n8n-mcp, WebSearch) → Warn user, provide install instructions
  - Optional tools → Silent graceful fallback
- **Updated iteration count:** 20 → 21 iterations (added Phase 0)
- **Added tool status report:** Display what's available at startup
- **Key principle:** If tool needed but unavailable → Stop, tell user, provide solution

### Session 1 - Update 2 (Reverse-Engineering from Real Script)
- **Analyzed professional YouTube script** (`youtube-video-script-version-2.md`)
- **Identified clear boundary:** What can be auto-gathered vs what requires user input
- **Auto-gathered from code (🤖):**
  - Technical implementation details
  - Tools/technologies and integration patterns
  - Demo scenario design (based on code paths)
  - Customization points and extension opportunities
  - Workflow assumptions (from validation logic)
- **Must ask user (👤):**
  - Target audience definition and pain points
  - Key value proposition / marketing hook
  - Tool pricing info (if WebSearch unavailable)
  - Call-to-action details (custom build offers, consultation, contact info)
  - Video preferences (tone, depth, length)
  - Download/resource links
- **Updated video-context.md template:**
  - Split into "USER-PROVIDED CONTEXT" and "AUTO-GENERATED CONTEXT" sections
  - Clearly marks what cannot be inferred from code
  - Aligns with professional script structure
- **Key insight:** The script's "Who This Is For" section (Section 3) and "Call to Action" sections (12-13) are PURELY user-driven and cannot be automated
- **Strategy:** Run repo analysis first, THEN ask user targeted questions with context

**Next Steps:**
- Begin Iteration 1: Create skill folder and SKILL.md structure
- Implement Phase 0: Tool availability check with proper error handling
- Implement Phase 1: Input discovery logic (including user questions AFTER analysis)
- Update Phase 6 to use new two-section template (user-provided + auto-generated)
