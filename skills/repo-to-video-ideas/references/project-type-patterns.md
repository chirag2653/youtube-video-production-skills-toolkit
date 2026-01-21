# Project Type Detection & Analysis Patterns

**Purpose:** How to detect project types and extract core functionality for video idea generation.

## n8n Workflows

**Detection:**
- JSON file with `nodes` array and `connections` object
- Workflow has `name`, `active`, `versionId` fields

**Analysis approach:**
```
1. Read workflow JSON
2. Extract workflow name
3. List all node types (Gmail, HTTP Request, Code, IF, etc.)
4. Identify external services (Google, Slack, AI services, databases)
5. Trace the flow: trigger → processing → outputs
6. Count total nodes for complexity estimate
```

**Key info to extract:**
- Workflow name and purpose
- Trigger type (manual, schedule, webhook, app trigger)
- External services integrated
- Decision points (IF nodes, Switch nodes)
- Data transformations (Code nodes, Set nodes)
- Final outputs (where data goes)

**If n8n-mcp available:**
- Use `get_node` to get detailed node documentation
- Use `validate_workflow` to check for issues

**Code assessment:**
- ✅ n8n workflows are typically 🟢 Fully Built (the workflow IS the implementation)
- Check for multiple workflow files (enables "comparison" video ideas)
- Check node count and complexity (determines tutorial length)
- Comparison ideas need 2+ workflows → Usually 🟢 if both exist

---

## Claude Code Skills

**Detection:**
- `SKILL.md` file in root or subdirectory
- YAML frontmatter with `name` and `description`

**Analysis approach:**
```
1. Read SKILL.md frontmatter for name/description
2. Read SKILL.md body for workflow steps
3. Check for references/ folder (additional docs)
4. Check for scripts/ folder (executable code)
5. Check for assets/ folder (templates, images)
```

**Key info to extract:**
- Skill name and trigger phrases
- What the skill helps accomplish
- Required tools or MCP servers
- Scripts included and their purpose
- Reference files and what they document

**Code assessment:**
- ✅ Skills are typically 🟢 Fully Built (the skill IS the implementation)
- Check for scripts/ folder → Enables "script showcase" ideas
- Check for reference/ folder → Indicates depth for "deep dive" ideas
- If scripts exist → Tutorial/demo ideas are 🟢
- Comparison ideas (vs other skills) → Usually 🟡 (need comparison write-up)

---

## Python Projects

**Detection:**
- `pyproject.toml` or `requirements.txt` or `setup.py`
- `.py` files in root or `src/`

**Analysis approach:**
```
1. Read pyproject.toml or requirements.txt for dependencies
2. Find entry point: main.py, app.py, cli.py, __main__.py
3. Read entry point to understand what it does
4. Check for README.md for project description
5. Look for config files (.env.example, config.py)
```

**Key info to extract:**
- Project name and description
- Key dependencies (what libraries power it)
- Entry point and main functionality
- CLI commands if applicable
- Configuration options

**Code assessment:**
Search for these patterns to assess video ideas:

**CLI/Scripts:**
- `cli_*.py`, `cmd_*.py`, `scripts/*.py` → Enables tutorial ideas (🟢 if comprehensive)
- Check for argparse/click decorators → Shows available commands

**Comparisons:**
- `compare_*.py`, `*_vs_*.py` → 🟢 if exists, 🟡 if needs to be built
- Multiple implementation files (method_a.py, method_b.py) → 🟡 for comparison

**Benchmarks:**
- `benchmark_*.py`, `performance_*.py` → 🟢 if exists, 🔴 if missing
- `timeit`, `time` imports in files → Indicates timing code exists

**Visualizations:**
- Check requirements for: `matplotlib`, `plotly`, `seaborn` → Enables chart-based videos
- Visualization scripts in scripts/ folder → 🟢 if exist, 🟡 if need to add

**API/Web:**
- `app.py`, `api.py`, `main.py` with Flask/FastAPI → Enables API demo videos (🟢)
- Frontend folders (`templates/`, `static/`) → Enables UI demo videos (🟢)

---

## JavaScript/Node Projects

**Detection:**
- `package.json` in root

**Analysis approach:**
```
1. Read package.json for name, description, scripts
2. Check main/module field for entry point
3. Identify framework: Next.js, Express, React, Vue, etc.
4. Read entry point or key files
5. Check for README.md
```

**Key info to extract:**
- Project name and description
- Framework/stack used
- Key dependencies
- Available npm scripts
- Build/run commands

**Code assessment:**
**Frontend/UI:**
- React/Vue/Next.js components → 🟢 for UI demo videos
- Pages/routes → Count to estimate tutorial complexity

**Backend/API:**
- Express/Fastify routes → 🟢 for API tutorials
- GraphQL schema → 🟢 for GraphQL demos

**Comparisons:**
- Multiple similar files (auth_jwt.js, auth_session.js) → 🟡 for comparison videos
- Multiple implementation approaches → Need comparison script

**Scripts:**
- scripts/ folder with utilities → 🟢 for specific feature demos
- Package.json scripts → Shows available commands for tutorials

---

## Claude Agent SDK Projects

**Detection:**
- Python project with `anthropic` or `claude-code-sdk` in dependencies
- Files importing from `anthropic` or agent-related modules

**Analysis approach:**
```
1. Standard Python analysis first
2. Identify agent architecture (tools, system prompts)
3. Find tool definitions
4. Understand agent workflow
```

**Key info to extract:**
- Agent purpose
- Tools the agent has access to
- System prompt approach
- Use cases the agent handles

---

## General Fallback

If no specific type detected:

**Analysis approach:**
```
1. Read README.md if exists
2. Read CLAUDE.md if exists
3. List top-level files and folders
4. Make best guess at purpose from file names
5. Ask user to describe the project
```

---

## Quick Detection Table

| Check For | Project Type |
|-----------|--------------|
| JSON with `nodes` + `connections` | n8n workflow |
| `SKILL.md` with YAML frontmatter | Claude Code skill |
| `pyproject.toml` or `requirements.txt` | Python |
| `package.json` | JavaScript/Node |
| `anthropic` in Python deps | Claude Agent SDK |
| `CLAUDE.md` only | General project with AI context |
