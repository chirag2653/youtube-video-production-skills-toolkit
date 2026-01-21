# Project Type Detection Patterns

This reference guide helps identify different project types and determine the appropriate demo approach.

## Detection Strategy

```
1. Find package/config files (Glob)
2. Identify frameworks (Grep)
3. Check for UI components
4. Determine demo format needed
```

---

## Project Type: n8n Workflow

### Indicators

**Primary:**
- `workflow.json` exists

**Secondary:**
- Multiple `workflow-*.json` files
- n8n package in dependencies
- `.n8n` folder

### Tech Stack Patterns

```
File to check: workflow.json
Structure: {
  "nodes": [...],
  "connections": {...},
  "settings": {...}
}
```

### Demo Approach

- **Recording:** n8n web interface + execution results
- **Setup:** n8n instance (cloud or self-hosted)
- **Focus:** Node connections, data flow, trigger → output

### Key Analysis Points

1. **Entry node:** Usually Gmail Trigger, Webhook, Schedule
2. **Processing nodes:** Code, HTTP Request, Function
3. **Integration nodes:** Google Sheets, Slack, Drive, etc.
4. **Logic nodes:** IF, Switch, Merge

### Use n8n-mcp if available:

```
- n8n_get_workflow: Parse workflow structure
- get_node: Understand each node's purpose
- n8n_validate_workflow: Check if functional
```

---

## Project Type: Python CLI Tool

### Indicators

**Primary:**
- `requirements.txt` or `pyproject.toml`
- `main.py` or `cli.py`
- Click or argparse usage

**Framework Detection (Grep):**
```
"import click"
"from click import"
"import argparse"
"ArgumentParser()"
```

### Tech Stack Patterns

```python
# Click-based CLI
@click.command()
@click.option('--input', help='Input file')
def main(input):
    pass

# Argparse-based CLI
parser = argparse.ArgumentParser()
parser.add_argument('--input')
```

### Demo Approach

- **Recording:** Terminal/command prompt
- **Setup:** Python environment, dependencies installed
- **Focus:** Command execution, output display

### Key Analysis Points

1. **Commands:** Find all @click.command or subparsers
2. **Options:** Required vs optional flags
3. **Input:** File paths, API keys, config files
4. **Output:** stdout, files generated, exit codes

---

## Project Type: Python Web API (FastAPI/Flask)

### Indicators

**Primary:**
- `requirements.txt` with fastapi or flask
- `app.py`, `main.py`, or `server.py`

**Framework Detection (Grep):**
```
"from fastapi import"
"from flask import"
"@app.route"
"@app.get"
"@app.post"
```

### Tech Stack Patterns

```python
# FastAPI
from fastapi import FastAPI
app = FastAPI()

@app.get("/api/endpoint")
async def endpoint():
    pass

# Flask
from flask import Flask
app = Flask(__name__)

@app.route("/api/endpoint")
def endpoint():
    pass
```

### Demo Approach

- **Recording:** Postman/Insomnia + code walkthrough
- **Setup:** Local server running, database if needed
- **Focus:** API requests, responses, data flow

### Key Analysis Points

1. **Endpoints:** All routes (@app.route, @app.get, etc.)
2. **Authentication:** JWT, API keys, OAuth
3. **Database:** Models, schemas, migrations
4. **External APIs:** Third-party integrations

### Finding endpoints:

```
Grep pattern: "@app\\.(get|post|put|delete|route)"
Or: "router\\.(get|post|put|delete)"
```

---

## Project Type: Node.js Web App (Express/React)

### Indicators

**Primary:**
- `package.json` with express, react, next, etc.
- `index.js`, `server.js`, or `app.js`

**Framework Detection (Grep):**
```
"express()"
"require('express')"
"import express"
"import React"
"import { createApp }" (Vue)
```

### Tech Stack Patterns

```javascript
// Express API
const express = require('express');
const app = express();

app.get('/api/endpoint', (req, res) => {
  res.json({...});
});

// React Frontend
import React from 'react';
function Component() {
  return <div>...</div>;
}
```

### Demo Approach

**Backend:**
- Terminal for server logs
- Postman for API testing

**Frontend:**
- Browser screen recording
- DevTools for debugging

### Key Analysis Points

1. **Backend routes:** app.get, app.post, router definitions
2. **Frontend components:** Page structure, UI flows
3. **State management:** Redux, Context, Zustand
4. **API integration:** fetch(), axios, API calls

---

## Project Type: Full-Stack Web Application

### Indicators

**Primary:**
- Both backend and frontend in same repo
- Monorepo structure (e.g., `/frontend`, `/backend`)
- Or integrated (Next.js, Django with templates)

**Detection:**
```
Glob patterns:
- "*/frontend/*", "*/backend/*"
- "*/client/*", "*/server/*"
- "pages/**/*.tsx" (Next.js)
- "templates/**/*.html" (Django)
```

### Demo Approach

- **Recording:** Browser for UI + code walkthrough
- **Focus:** User journey from UI → API → database → response
- **Show:** Both frontend interaction and backend processing

### Key Analysis Points

1. **User flows:** Registration, login, main features
2. **API contracts:** Request/response formats
3. **Database interactions:** CRUD operations
4. **Authentication:** Sessions, tokens, cookies

---

## Project Type: Data Pipeline / ETL

### Indicators

**Primary:**
- Scripts for data extraction, transformation, loading
- Database connection configs
- CSV/Excel input/output handling
- Scheduled jobs (cron, Airflow)

**Framework Detection (Grep):**
```
"pandas"
"import csv"
"sqlalchemy"
"psycopg2"
"pymongo"
```

### Demo Approach

- **Recording:** Terminal + data visualization
- **Show:** Input data → processing → output data
- **Focus:** Data quality, transformation logic, results

### Key Analysis Points

1. **Data sources:** Files, APIs, databases
2. **Transformations:** Cleaning, aggregation, joins
3. **Output:** Databases, files, dashboards
4. **Error handling:** Invalid data, missing fields

---

## Project Type: Automation Script

### Indicators

**Primary:**
- Single or few Python/JavaScript files
- Task automation (file processing, web scraping, etc.)
- May use selenium, puppeteer, requests

**Framework Detection (Grep):**
```
"from selenium import"
"import requests"
"puppeteer"
"const axios"
```

### Demo Approach

- **Recording:** Terminal + results visualization
- **Show:** Before/after state
- **Focus:** Time saved, accuracy improvements

### Key Analysis Points

1. **Input:** What triggers the automation
2. **Actions:** Steps performed automatically
3. **Output:** Files generated, updates made
4. **Schedule:** Manual, cron, triggered

---

## Project Type: Library/Package

### Indicators

**Primary:**
- `setup.py` or `pyproject.toml` with package metadata
- `package.json` with library configuration
- `/src` or `/lib` directory structure
- No main entry point for execution

**Detection:**
```
Files: setup.py, pyproject.toml, package.json
Structure: src/package_name/__init__.py
           lib/index.js
```

### Demo Approach

- **Recording:** Code walkthrough + usage examples
- **Show:** Import → use → output
- **Focus:** API design, use cases, examples

### Key Analysis Points

1. **Public API:** Exported functions/classes
2. **Use cases:** Common scenarios
3. **Installation:** pip install, npm install
4. **Documentation:** README examples

---

## Mixed/Complex Projects

### Indicators

- Multiple of the above patterns
- Monorepo with services
- Microservices architecture

### Strategy

1. Identify the **main demo focus:**
   - What's the primary user-facing feature?
   - What provides the most value?

2. **Choose primary project type** for demo approach

3. **Note other components** in context:
   - "This also includes a CLI tool for admin tasks"
   - "Backend API powers the frontend"

4. **Plan demo priority:**
   - Start with main feature (flagship scenario)
   - Show complementary features (secondary scenarios)

---

## Demo Format Decision Tree

```
Has UI (web browser)?
├─ YES → Screen recording (browser + code walkthrough)
│
└─ NO → Is it a CLI tool?
    ├─ YES → Terminal recording
    │
    └─ NO → Is it an API?
        ├─ YES → Postman + code walkthrough
        │
        └─ NO → Is it a workflow?
            ├─ YES → n8n interface + execution
            │
            └─ NO → Code walkthrough + results visualization
```

---

## Common Configurations to Look For

### Environment Variables

```
Glob: ".env.example", ".env.sample", "config.sample.*"
Look for: API keys, database URLs, service credentials
```

### Configuration Files

```
Glob: "config.*", "settings.*", "*.config.js"
Common: config.json, settings.py, next.config.js
```

### Credentials Setup

```
Grep: "API_KEY", "api_key", "credentials", "token"
Note: What services need authentication
```

### Database Schema

```
Grep: "CREATE TABLE", "class.*Model", "Schema =", "model.py"
Look for: Data structure, relationships
```

---

## Quick Reference Table

| Project Type | Primary Indicator | Demo Format | Key Tools |
|--------------|-------------------|-------------|-----------|
| n8n Workflow | workflow.json | n8n interface | n8n-mcp |
| Python CLI | main.py + click/argparse | Terminal | - |
| Python API | fastapi/flask + @app | Postman + code | - |
| Node.js API | express + package.json | Postman + code | - |
| React/Vue App | React/Vue + components | Browser | - |
| Full-Stack | Frontend + Backend | Browser + API | - |
| Data Pipeline | pandas + data processing | Terminal + viz | - |
| Automation | selenium/requests | Terminal + results | - |
| Library | setup.py + /src | Code + examples | - |

---

## Tips

1. **Start with package files:** package.json, requirements.txt, go.mod
2. **Look for framework imports:** FastAPI, Express, React, etc.
3. **Check for main entry point:** main.py, index.js, app.py
4. **Identify external integrations:** Third-party APIs, services
5. **Note setup complexity:** Local dev easy? Requires external services?

Use this guide to quickly identify project type and plan the appropriate demo approach.
