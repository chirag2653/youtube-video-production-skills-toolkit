# Video Ideas Output Template

**This is the DEFINITIVE output format for `demo-video/video-ideas.md`.**

This file shows the exact structure, formatting, and example content that the skill generates. This is the single source of truth for output format - all other reference files support the generation process but defer to this file for output structure.

## Output Format

```markdown
# Video Ideas for [Project Name]

**Generated:** 2026-01-21
**Project Type:** Python Pipeline / n8n Workflow / Claude Skill / JavaScript App
**Total Ideas:** 8

---

## 🟢 Ready to Demo (Just needs demo data)

### Idea 1: [Catchy Title]
- **Audience:** [Specific persona]
- **Value prop:** [What they'll learn/gain]
- **Key demo moments:** [2-3 things to show]
- **Length:** Short (5min) / Medium (10-15min) / Deep dive (20+min)
- **Code Status:** 🟢 Fully Built

**What exists:**
- ✅ [Feature/script that exists]
- ✅ [Another existing component]
- ✅ [Third component]

**What needs to be built:**
- None

**Dev estimate:** None - Just needs demo data

---

### Idea 4: [Another Ready Title]
- **Audience:** [Specific persona]
- **Value prop:** [What they'll learn/gain]
- **Key demo moments:** [2-3 things to show]
- **Length:** Medium (12min)
- **Code Status:** 🟢 Fully Built

**What exists:**
- ✅ [Feature A]
- ✅ [Feature B]

**What needs to be built:**
- None

**Dev estimate:** None

---

## 🟡 Needs Minor Code Additions (1-3 files, 2-6 hours)

### Idea 2: [Comparison Title]
- **Audience:** [Specific persona]
- **Value prop:** [What they'll learn/gain]
- **Key demo moments:** [2-3 things to show]
- **Length:** Short (7min)
- **Code Status:** 🟡 Partial - Comparison script needed

**What exists:**
- ✅ [Method A implemented]
- ✅ [Method B implemented]
- ✅ [Common interface]

**What needs to be built:**
- ❌ scripts/compare_methods.py - Side-by-side analysis
- ❌ Optional: Visualization charts

**Dev estimate:** 2-3 hours

---

### Idea 5: [Another Partial Title]
- **Audience:** [Specific persona]
- **Value prop:** [What they'll learn/gain]
- **Key demo moments:** [2-3 things to show]
- **Length:** Medium (10min)
- **Code Status:** 🟡 Partial - Analysis script needed

**What exists:**
- ✅ [Core functionality]

**What needs to be built:**
- ❌ scripts/analyze_results.py

**Dev estimate:** 3-4 hours

---

## 🔴 Requires Feature Development (Significant work)

### Idea 7: [Advanced Feature Title]
- **Audience:** [Specific persona]
- **Value prop:** [What they'll learn/gain]
- **Key demo moments:** [2-3 things to show]
- **Length:** Deep dive (18min)
- **Code Status:** 🔴 Needs Development - Major features missing

**What exists:**
- ✅ [Basic functionality]

**What needs to be built:**
- ❌ [Feature module A]
- ❌ [Feature module B]
- ❌ [Integration layer]
- ❌ [Supporting infrastructure]

**Dev estimate:** 1-2 days

**Note:** Consider this for future videos after building the necessary features.

---

### Idea 8: [Complex Integration Title]
- **Audience:** [Specific persona]
- **Value prop:** [What they'll learn/gain]
- **Key demo moments:** [2-3 things to show]
- **Length:** Deep dive (20min)
- **Code Status:** 🔴 Needs Development - Integration layer missing

**What exists:**
- ✅ [Current system]

**What needs to be built:**
- ❌ [New integration module]
- ❌ [Adapter pattern]
- ❌ [Comparison framework]

**Dev estimate:** 2-3 days

**Note:** Strategic idea - consider for future content roadmap.
```

---

## Usage

This `video-ideas.md` file can be:
- Reviewed by content creators to select video ideas
- Used by video planning tools (e.g., video-idea-to-context skill)
- Shared with teams for content strategy discussions
- Referenced to prioritize feature development
- Archived as a snapshot of demo-able content at this point in time

Downstream tools can parse this file to extract specific ideas by number or code status.

---

## Complete Example: Website to Vector DB Project

```markdown
# Video Ideas for Website to Vector Database Pipeline

**Generated:** 2026-01-21
**Project Type:** Python CLI Pipeline
**Total Ideas:** 7

---

## 🟢 Ready to Demo (Just needs demo data)

### Idea 1: Website to Vector DB: Complete Pipeline in 10 Minutes
- **Audience:** Developers building RAG applications, AI enthusiasts
- **Value prop:** See the entire pipeline from URL to searchable vectors
- **Key demo moments:** Discovery → Scraping → Chunking → Embedding → Querying
- **Length:** Medium (10-12min)
- **Code Status:** 🟢 Fully Built

**What exists:**
- ✅ cli_discover.py - URL discovery
- ✅ cli_scrape.py - Content extraction
- ✅ cli_chunk.py - Text chunking
- ✅ cli_embed.py - Vector embedding
- ✅ cli_query.py - Search queries
- ✅ Full pipeline documented in CLAUDE.md

**What needs to be built:**
- None

**Dev estimate:** None - Just needs sample website URL

---

### Idea 4: Hybrid Search Explained with Live Demo
- **Audience:** Developers learning about vector databases
- **Value prop:** Understand how vector + text search work together
- **Key demo moments:** Vector-only, text-only, hybrid results comparison
- **Length:** Medium (12min)
- **Code Status:** 🟢 Fully Built

**What exists:**
- ✅ Hybrid search in query_engine.py
- ✅ CLI with search mode options
- ✅ Results ranking logic

**What needs to be built:**
- None

**Dev estimate:** None

---

## 🟡 Needs Minor Code Additions (1-3 files, 2-6 hours)

### Idea 2: Firecrawl vs Scrapy: Which Web Crawler Finds More URLs?
- **Audience:** Web scraping practitioners, data engineers
- **Value prop:** Head-to-head comparison of AI-powered vs traditional discovery
- **Key demo moments:** Run both methods, show overlap, compare unique URLs
- **Length:** Short (7min)
- **Code Status:** 🟡 Partial - Comparison script needed

**What exists:**
- ✅ cli_discover_scrapy.py - Traditional crawling
- ✅ cli_discover_firecrawl.py - AI-powered discovery
- ✅ cli_merge_discovered_urls.py - Merge logic

**What needs to be built:**
- ❌ scripts/compare_discovery_methods.py - Analysis script
- ❌ Optional: Visualization for side-by-side bar charts

**Dev estimate:** 2-3 hours

---

## 🔴 Requires Feature Development (Significant work)

### Idea 7: Performance Benchmark: 1K vs 10K vs 100K Documents
- **Audience:** Developers choosing vector DB solutions
- **Value prop:** See real performance at different scales
- **Key demo moments:** Query speed tests, resource usage, accuracy at scale
- **Length:** Deep dive (15min)
- **Code Status:** 🔴 Needs Development - No benchmark infrastructure

**What exists:**
- ✅ Query engine functional
- ✅ Database can scale

**What needs to be built:**
- ❌ scripts/benchmark_query_performance.py - Timing framework
- ❌ Test dataset generator for different scales
- ❌ Results aggregation and visualization
- ❌ Resource monitoring (memory, CPU)

**Dev estimate:** 1-2 days

**Note:** Great video concept but requires significant development. Consider for future after building benchmark suite.
```
