# Code Assessment Patterns

**Purpose:** How to assess code readiness for video ideas - what to search for and how to classify 🟢🟡🔴.

This guide helps you assess **code readiness** for video ideas: How much functionality already exists vs. what needs to be built?

## Core Principle

**We're NOT assessing demo data** (every demo needs data). We're assessing: **Does the CODE exist to execute this video idea?**

---

## Assessment Process

### Phase 1: Identify Potential Video Angles

After detecting project type and understanding functionality, brainstorm potential video angles:
- Tutorials (how to use the full system)
- Comparisons (tool A vs tool B)
- Deep dives (explain specific features)
- Benchmarks (performance tests)
- Walkthroughs (step-by-step processes)

### Phase 2: Check What Code Exists

For each potential angle, search for supporting code:

```
For "Comparison" ideas → Search: compare_*.py, *_vs_*.py, comparison scripts
For "Benchmark" ideas → Search: benchmark_*.py, performance_*.py, timing scripts
For "Visualization" ideas → Search: chart libs, plotting scripts, dashboard files
For "Tutorial" ideas → Search: CLI commands, main entry points, documented workflows
For "Deep dive" ideas → Search: specific feature files, implementation details
```

### Phase 3: Classify Code Readiness

**🟢 Fully Built**: All core features exist, just needs demo data
- Main functionality implemented
- Supporting scripts exist
- UI/CLI commands ready
- Only missing: sample data to demo with

**🟡 Partial**: Core exists, but needs 1-3 additional helper scripts
- Main feature works
- Missing: comparison scripts, visualization helpers, analysis tools
- Estimated effort: 2-6 hours of coding

**🔴 Needs Development**: Major features missing, significant work required
- Core functionality incomplete or missing
- Would need 4+ new files or complex logic changes
- Estimated effort: 1+ days of development

---

## Project-Type Specific Patterns

### Python Projects

**Check locations:**
- `*.py` files in root, `src/`, `scripts/`, `cli/`, `commands/`
- `pyproject.toml` or `requirements.txt` for installed libraries
- Entry points: `if __name__ == "__main__"` blocks, CLI decorators

**Common patterns:**

| Video Angle | Search For | Exists? |
|------------|------------|---------|
| CLI Tutorial | Click/argparse commands, `cli_*.py` | ✅/❌ |
| Comparison | `compare_*.py`, `*_vs_*.py` | ✅/❌ |
| Benchmarks | `benchmark_*.py`, `timeit`, `time` imports | ✅/❌ |
| Visualizations | `matplotlib`, `plotly`, `seaborn` in requirements | ✅/❌ |
| Data Analysis | Pandas scripts, analysis notebooks | ✅/❌ |

**Example checks:**
```
Idea: "Compare Method A vs Method B"
✓ Check: Does compare_methods.py exist?
✓ Check: Are both methods implemented?
✓ Check: Is there output/visualization code?
```

### JavaScript/Node Projects

**Check locations:**
- `src/`, `lib/`, `scripts/`, `bin/`
- `package.json` for dependencies and scripts
- Frontend: `pages/`, `components/`, `app/`

**Common patterns:**

| Video Angle | Search For | Exists? |
|------------|------------|---------|
| API Tutorial | Route handlers, Express/Fastify routes | ✅/❌ |
| UI Demo | Component files, pages, views | ✅/❌ |
| Comparison | Utility scripts, comparison functions | ✅/❌ |
| Integration | Service files, API clients | ✅/❌ |

### n8n Workflows

**Check locations:**
- `*.json` workflow files with nodes and connections
- Workflow nodes count and types

**Common patterns:**

| Video Angle | Search For | Exists? |
|------------|------------|---------|
| Full Tutorial | Complete workflow with 5+ nodes | ✅/❌ |
| Integration Focus | Specific service nodes (Gmail, Slack, etc.) | ✅/❌ |
| Error Handling | Error workflow branches | ✅/❌ |
| Multiple Workflows | 2+ related workflow files | ✅/❌ |

**Note:** n8n workflows are usually 🟢 Fully Built (the workflow IS the code).

### Claude Code Skills

**Check locations:**
- `SKILL.md` (main instructions)
- `scripts/` folder for utility scripts
- `references/` for supporting docs

**Common patterns:**

| Video Angle | Search For | Exists? |
|------------|------------|---------|
| Skill Tutorial | Complete SKILL.md with examples | ✅/❌ |
| Script Showcase | Python/bash scripts in scripts/ | ✅/❌ |
| Integration Demo | MCP tools, external APIs in skill | ✅/❌ |

**Note:** Skills are usually 🟢 Fully Built (the skill IS the code).

---

## Video Idea Specific Checks

### For "Comparison" Ideas

**Must exist:**
- ✅ Both/all items being compared implemented
- ✅ Common interface or test harness to run both

**Should exist (or mark 🟡):**
- ❓ Comparison script that runs both side-by-side
- ❓ Results aggregation/analysis code
- ❓ Visualization/charting code

**Example:**
```
Idea: "Firecrawl vs Scrapy: Which Finds More URLs?"

What exists:
✅ cli_discover_scrapy.py
✅ cli_discover_firecrawl.py
✅ cli_merge_results.py

What's missing:
❌ scripts/compare_discovery_methods.py
❌ Visualization for side-by-side results

Status: 🟡 Partial - Need comparison script (2-3 hours)
```

### For "Benchmark/Performance" Ideas

**Must exist:**
- ✅ The functionality to benchmark
- ✅ Ability to run it multiple times

**Should exist (or mark 🟡/🔴):**
- ❓ Timing/performance measurement code
- ❓ Different data sizes or configurations to test
- ❓ Results aggregation and stats

**Example:**
```
Idea: "Performance Showdown: Vector Search Speed Test"

What exists:
✅ Query engine implemented
✅ Vector database populated

What's missing:
❌ scripts/benchmark_query_performance.py
❌ Test queries at different scales
❌ Results charting

Status: 🔴 Needs Development - No benchmark infrastructure (1 day)
```

### For "Deep Dive / Explanation" Ideas

**Must exist:**
- ✅ The feature being explained is fully implemented
- ✅ Can demonstrate it working

**Usually 🟢 if:**
- Feature exists and is functional
- No comparison/benchmark needed
- Just needs demo data to show it working

**Example:**
```
Idea: "Hybrid Search Explained: Vector + Text Search"

What exists:
✅ Hybrid search implemented in query_engine.py
✅ CLI command to run queries

What might be missing:
❓ Can you toggle between vector-only/text-only/hybrid modes?

Check needed: Read query_engine.py to see if modes are switchable
If switchable: 🟢 Fully Built
If always hybrid: 🟡 Partial - Need mode switching (1-2 hours)
```

### For "Tutorial / Walkthrough" Ideas

**Must exist:**
- ✅ All steps in the tutorial are implemented
- ✅ CLI commands or scripts for each step
- ✅ Clear entry points

**Usually 🟢 if:**
- Full pipeline/workflow exists
- Documentation shows the steps
- Just needs to be executed with sample data

**Example:**
```
Idea: "Website to Vector DB: Complete Pipeline Tutorial"

What exists:
✅ cli_discover.py
✅ cli_scrape.py
✅ cli_chunk.py
✅ cli_embed.py
✅ cli_query.py

What's missing:
❓ None - full pipeline implemented

Status: 🟢 Fully Built - Just needs demo website
```

---

## Assessment Result

After assessing code readiness, classify each idea as:
- **🟢 Fully Built**: All code exists, just needs demo data
- **🟡 Partial**: Core exists, needs 1-3 helper scripts (2-6 hours)
- **🔴 Needs Development**: Major features missing (1+ days)

Document what exists vs what's missing, and estimate dev effort.

For exact output format, see `video-ideas-output-template.md`.

---

## Important Distinctions

### Demo Data vs Code Status

**Demo data** = Sample input to show the system working
- Example: A test website to scrape
- Example: Sample documents to process
- Example: Test API credentials

**Code status** = Does the functionality exist in the codebase?
- Example: Does compare_methods.py exist?
- Example: Are benchmark scripts written?

**DO NOT penalize ideas for needing demo data.** That's expected.

**ONLY assess:** Is the CODE ready?

### Minor Helpers vs Major Features

**Minor helpers** (mark 🟡):
- Comparison scripts that just run two existing things
- Visualization scripts using existing data
- Analysis scripts that aggregate existing outputs
- Usually 1-3 small files, 2-6 hours work

**Major features** (mark 🔴):
- Core functionality that doesn't exist
- Would require architectural changes
- Multiple interconnected files
- Usually 4+ files or 1+ days work

---

## Example: Complete Assessment

Project: Website to Vector Database Pipeline

**Idea 1: Full Pipeline Tutorial**
```
Check:
✅ All CLI commands exist (discover, scrape, chunk, embed, query)
✅ Documentation exists
✅ No additional code needed

Assessment: 🟢 Fully Built
Reason: Complete pipeline, just needs demo website
```

**Idea 2: Firecrawl vs Scrapy Comparison**
```
Check:
✅ Both methods implemented
✅ Merge logic exists
❌ No comparison/analysis script
❌ No visualization script

Assessment: 🟡 Partial
Missing: compare_discovery_methods.py, chart generation
Estimate: 2-3 hours
```

**Idea 3: Performance Benchmark Suite**
```
Check:
✅ Query engine exists
❌ No benchmark scripts
❌ No performance measurement code
❌ No different scale tests

Assessment: 🔴 Needs Development
Missing: Entire benchmark infrastructure
Estimate: 1+ day
```

---

## Quick Reference Checklist

For each video idea:
- [ ] Identify what code would be needed to execute this idea
- [ ] Search codebase for that code
- [ ] Check if supporting scripts exist (comparison, visualization, etc.)
- [ ] Classify as 🟢/🟡/🔴
- [ ] Document what exists vs what's missing
- [ ] Estimate dev effort if not fully built
- [ ] Group ideas by readiness
- [ ] Prioritize 🟢 ideas at the top of your list
