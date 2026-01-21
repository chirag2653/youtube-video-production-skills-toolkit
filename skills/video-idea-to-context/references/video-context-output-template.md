# Video Context Output Template

This is the definitive template for `video-context.md`. Follow this structure exactly.

---

## File Header

```markdown
# Video Context: [Video Title]

**Generated:** [Date - ISO format: 2026-01-21]
**Project:** [Project Name from repo or package.json]
**Type:** [Tutorial / Feature Demo / Workflow Walkthrough / Integration Guide]
**Project Type:** [n8n Workflow / Python CLI / Web App / API / etc.]
```

---

## Section 1: USER-PROVIDED CONTEXT

This section contains information gathered from user questions. It cannot be automatically inferred from code.

```markdown
---

## 📌 USER-PROVIDED CONTEXT

> This section contains information provided by the user that cannot be automatically gathered from code analysis.

### Problem Statement / Pain Point

**What frustrating problem does this solve?**

[User's exact wording from Question 2]

Example:
"Manual invoice data entry from PDFs takes 10+ hours per week for finance 
teams. It's tedious, error-prone, and doesn't scale as the business grows."

**Why it matters:**

[Impact statement - from Question 2 follow-up or inferred]

Example:
"Finance teams waste valuable time on repetitive work instead of strategic 
tasks. Errors in data entry can lead to missed payments or accounting issues."

---

### Target Audience

**Who is this video for?**

[User's answer from Question 1 - list format]

Example:
- Business owners wanting to automate back-office processes
- Finance managers looking to streamline invoice workflows
- Freelance automation consultants seeking client solutions

**Their main goal:**

[From Question 1 follow-up]

Example:
"Learn how to automate invoice processing to eliminate manual data entry 
and save hours per week."

**Skill level:** [Beginner / Intermediate / Advanced]

[Inferred from target audience selection]

**Assumes viewer knows:**

[Prerequisites based on tech stack and target audience]

Example:
- Basic understanding of email and cloud storage
- Familiarity with spreadsheets (Google Sheets/Excel)
- No coding experience required

---

### Key Value Proposition / Hook

**One-sentence benefit:**

[User's answer from Question 3 - the "hook"]

Example:
"Watch your Gmail inbox for invoice emails, use AI to extract data, and 
organize everything automatically with zero manual work."

**"Wow" factor:**

[From Question 3 follow-up]

Example:
"AI reads PDF invoices and extracts structured data—no manual typing, no 
copy-paste, just pure automation."

---

### Video Preferences

**Tone:** [Casual / Professional / Friendly]
**Technical depth:** [High / Medium / Low]
**Target length:** [5-10 minutes / 10-20 minutes / 20+ minutes]

[From Question 6, or defaults if not specified]

---

### Call-to-Action

**Custom build service:**
- **Offered:** [Yes / No]
- **Contact:** [email / website / form link]
- **Message:** [User's exact wording]

Example:
"If you'd like this workflow customized for your specific business needs, 
I'm happy to help. Email me at example@email.com"

**Consultation:**
- **Offered:** [Yes / No]
- **Link:** [Calendar URL]
- **Details:** [Duration, format, cost]

Example:
"Book a 30-minute setup call: [calendar link] - Free for first-time users"

**Download/Resources:**
- **Workflow location:** [GitHub repo / Download link / Website]
- **Setup guide:** [Included in README / Separate link / Will be in description]

Example:
- GitHub: https://github.com/username/invoice-automation
- Setup guide: See README.md in repository

**Community/Contact:**
- **Email:** [address]
- **Discord:** [invite link]
- **Twitter:** [@handle]
- **Website:** [URL]
- **Other:** [LinkedIn, YouTube, etc.]

[From Question 5 - all parts]
```

---

## Section 2: AUTO-GENERATED CONTEXT

This section is filled from codebase analysis. Script generator relies primarily on this.

```markdown
---

## 🤖 AUTO-GENERATED CONTEXT

> This section is automatically gathered from deep codebase analysis.

### Solution Overview

[High-level description of how the project works - from Phase 3 analysis]

Example:
"This n8n workflow monitors a Gmail inbox for emails with invoice attachments. 
When an invoice arrives, it uses LlamaCloud AI to classify the document and 
extract structured data (vendor, amount, invoice number, date). The extracted 
data is used to create an organized filename, then the invoice is uploaded to 
Google Drive and logged in Google Sheets. If the invoice amount exceeds a 
configurable threshold, a Slack notification alerts the team."

**Key capabilities:**
- [Bullet list of main features from code analysis]

Example:
- Automatic email monitoring and PDF extraction
- AI-powered document classification and data extraction
- Smart filename generation with normalized vendor names
- Duplicate detection to prevent reprocessing
- Conditional Slack notifications for high-value invoices
- Complete audit trail in Google Sheets

---

### Tools & Technologies

[Table format - one row per external tool/service detected]

| Tool | Purpose/Role in Workflow | Pricing | Setup Complexity |
|------|-------------------------|---------|------------------|
| [Tool 1] | [What it does] | [Free tier info + when to pay] | [Easy/Medium/Hard] |
| [Tool 2] | [What it does] | [Free tier info + when to pay] | [Easy/Medium/Hard] |

**Example filled table:**

| Tool | Purpose/Role in Workflow | Pricing | Setup Complexity |
|------|-------------------------|---------|------------------|
| **n8n** | Orchestrates the entire workflow, connects all tools, executes automation logic | Always Free (with limits) - Free tier: 5,000 executions/month. Pay when exceeding limits or needing team features. Starter: $20/month. | Medium - Self-host (free) or use cloud. Need to configure credentials. |
| **LlamaCloud** | AI classifies documents (invoice/receipt/other) and extracts structured data automatically | Always Free (with limits) - Free tier: 1,000 API calls/month. Pay when exceeding free tier. Pro: $49/month. | Easy - Sign up, get API key, add to n8n credentials. |
| **Gmail** | Monitors inbox for invoice emails and downloads PDF attachments | Free | Easy - Use existing Google account, enable API access. |
| **Google Drive** | Stores invoice PDFs with organized, searchable filenames | Always Free (15GB included) - Pay when needing more than 15GB. Google One: $1.99/month for 100GB. | Easy - Use existing Google account, connect to n8n. |
| **Google Sheets** | Logs extracted invoice data and enables duplicate detection | Free | Easy - Create spreadsheet, connect to n8n. |
| **Slack** | Sends team notifications for high-value invoices (optional) | Always Free (with limits) - Free tier: 90-day message history. Pay for extended history and advanced features. Pro: $7.25/user/month. | Easy - Create workspace, get webhook URL, add to n8n. |

**Pricing Notes:**

[If WebSearch was used:]
"Pricing information researched on [date]. May change - verify current pricing 
before publishing video."

[If user provided pricing:]
"Pricing information provided by user. Verify current pricing before publishing video."

[If marked for research:]
"❓ Pricing marked for research. Must be completed before script generation."

---

### Prerequisites

**Required:**

[List what viewer must have before starting]

Example:
- [ ] Google account (Gmail, Drive, Sheets)
- [ ] n8n account (cloud or self-hosted instance)
- [ ] LlamaCloud account and API key
- [ ] Slack workspace (if using notifications)

**Background Knowledge:**

[What viewer should understand - based on target audience skill level]

Example:
- Basic understanding of email and cloud storage
- Familiarity with automation concepts (helpful but not required)
- No coding experience needed

**Time Estimate:**

[How long to follow along and set up]

Example:
"~45 minutes to set up all credentials and configure the workflow"

---

### Workflow/Process

**High-Level Flow:**

[Text-based flow diagram showing main steps]

Example:
```
1. Gmail Trigger (every 60s)
   ↓
2. Email with PDF attachment received
   ↓
3. Filter PDF Attachments (exclude signatures, logos)
   ↓
4. Upload PDF to LlamaCloud
   ↓
5. Classify Document (invoice? receipt? other?)
   ↓
6. Extract Structured Data (vendor, amount, invoice #, date)
   ↓
7. Check for Duplicates (against Google Sheets)
   ↓
8. Build Smart Filename (date_vendor_invoice.pdf)
   ↓
9. Upload to Google Drive
   ↓
10. Log to Google Sheets
   ↓
11. IF amount > $500 → Send Slack notification
   ↓
12. Mark email as processed
```

**Detailed Process Description:**

[Step-by-step explanation with code references]

Example:
"The workflow begins with a Gmail Trigger node that polls the inbox every 
60 seconds for unread emails with attachments. When an email arrives, the 
Filter PDF Attachments code node (workflow.json, node ID 'filter_pdfs') 
examines each attachment, excluding obvious non-invoices like signatures or 
logos based on filename patterns and file size. Candidates are then uploaded 
to LlamaCloud for classification..."

[Continue with each major step, referencing actual code/nodes]

---

### Demo Scenarios

[One section per scenario designed in Phase 4]

#### Scenario 1: [Name] (Flagship)

**Purpose:** [What this demonstrates]

**Value Demonstrated:** [Key benefit shown]

**Estimated Demo Time:** [X minutes]

---

**Setup Requirements:**

*Configuration Files:*
```
[Show exact file contents]

Example:
config.json:
{
  "gmail_label": "Invoices",
  "drive_folder_id": "1AbC123...",
  "sheets_id": "1XyZ789...",
  "alert_threshold": 500
}
```

*Environment Variables:*
```
[List all required env vars with example values]

Example:
- LLAMA_API_KEY=test_key_abc123
- SLACK_WEBHOOK=https://hooks.slack.com/services/T00/B00/xxx
```

*Prerequisites:*
- [Specific setup steps]

Example:
- Google Drive folder "/Invoices" created
- Google Sheet "Invoice Tracker" with columns: Date, Vendor, Invoice #, Amount, File Link, Sender Email
- Slack channel "#finance" configured
- All n8n credentials configured

*Initial State:*
- [What must be true before starting]

Example:
- Gmail inbox has no unread invoice emails
- Google Sheet has header row but no data
- Workflow is activated in n8n

---

**Test Data:**

[Be EXTREMELY specific]

Example:

*Invoice PDF:* `CloudProvider-Inc_Invoice.pdf`
```
Vendor: CloudProvider Inc
Invoice Number: INV-2025-042
Invoice Date: 2025-01-20
Due Date: 2025-02-20
Amount: $350.00
Line Items:
  - Cloud hosting: $200.00
  - Data transfer: $100.00
  - Support: $50.00
```

*Email:*
```
From: billing@cloudprovider.com
To: your-email@gmail.com
Subject: Invoice INV-2025-042 for January Services
Body: "Please find attached invoice for January 2025 services."
Attachment: CloudProvider-Inc_Invoice.pdf (250 KB)
```

---

**Execution Steps:**

[Numbered, specific steps with code references]

Example:

1. **Send test email**
   - From billing@cloudprovider.com to monitored inbox
   - Attachment: CloudProvider-Inc_Invoice.pdf

2. **Gmail Trigger fires** (within 60 seconds)
   - Node: "Gmail Trigger" (workflow.json, node_id: "gmail_trigger_1")
   - Picks up unread email with attachment
   - Downloads PDF as binary data

3. **Filter PDF Attachments executes**
   - Node: "Filter PDF Attachments" (Code node)
   - Checks filename against exclusion patterns: /(signature|logo|terms)/i
   - Checks file size: 5KB < size < 10MB
   - Result: 1 candidate PDF, hasCandidates = true

4. **Upload to LlamaCloud**
   - Node: "Upload PDF" (HTTP Request)
   - POST to https://api.llamaindex.cloud/api/v1/files
   - Returns: file_id = "file_abc123"

5. **Create Classification Job**
   - Node: "Classify Document" (HTTP Request)
   - Rules: invoice (0.6), receipt (0.6), other (0.5)
   - Processing time: ~10 seconds

6. **Get Classification Results**
   - Returns: { type: "invoice", confidence: 0.92 }
   - Confidence exceeds 0.6 threshold → Proceed to extraction

7. **Create Extraction Job**
   - Node: "Extract Data" (HTTP Request)
   - Schema: vendor_name, invoice_number, invoice_date, total_amount, currency, line_items
   - Processing time: ~15 seconds

8. **Get Extraction Results**
   - Returns:
     ```json
     {
       "vendor_name": "CloudProvider Inc",
       "invoice_number": "INV-2025-042",
       "invoice_date": "2025-01-20",
       "total_amount": 350.00,
       "currency": "USD",
       "line_items": [...]
     }
     ```

9. **Build Smart Filename**
   - Node: "Build File Path" (Set node)
   - Normalizes: "CloudProvider Inc" → "CloudProvider-Inc"
   - Normalizes: "INV-2025-042" → "INV-2025-042"
   - Result: "2025-01-20_CloudProvider-Inc_INV-2025-042.pdf"

10. **Check for Duplicates**
    - Node: "Check Duplicate" (Google Sheets)
    - Reads all rows from Sheet
    - Compares: sender_email + invoice_number
    - Result: No match found (isDuplicate = false)

11. **Upload to Google Drive**
    - Node: "Upload to Drive" (Google Drive)
    - Folder: "/Invoices"
    - Filename: "2025-01-20_CloudProvider-Inc_INV-2025-042.pdf"
    - Returns: webViewLink

12. **Log to Google Sheets**
    - Node: "Log to Sheets" (Google Sheets - Append Row)
    - Row data:
      ```
      Received Date: 2026-01-21 10:30:00
      Vendor: CloudProvider Inc
      Invoice #: INV-2025-042
      Invoice Date: 2025-01-20
      Amount: $350.00
      Currency: USD
      Invoice File: [webViewLink]
      Sender Email: billing@cloudprovider.com
      ```

13. **Check High-Value Threshold**
    - Node: "High Value Invoice?" (IF node)
    - Condition: amount > 500
    - Result: false (350.00 < 500) → Skip Slack notification

14. **Mark Email as Processed**
    - Node: "Mark as Read" (Gmail)
    - Marks email as read
    - Prevents re-triggering on next poll

---

**Expected Outcomes:**

*Console/Execution Log:*
```
✅ Email processed: Invoice INV-2025-042
📎 PDF extracted: CloudProvider-Inc_Invoice.pdf (250 KB)
🤖 Classification: invoice (confidence: 0.92)
📊 Data extracted: $350.00 from CloudProvider Inc
💾 Saved to Drive: 2025-01-20_CloudProvider-Inc_INV-2025-042.pdf
📝 Logged to Sheets: Row 2
⏱️ Total processing time: ~35 seconds
```

*Google Drive:*
- New file in "/Invoices" folder
- Filename: "2025-01-20_CloudProvider-Inc_INV-2025-042.pdf"
- Size: 250 KB
- Searchable by: date, vendor name, invoice number

*Google Sheets:*
- New row appended (row 2)
- All fields populated accurately
- Invoice File column contains clickable link to Drive
- Timestamp shows when processed

*Gmail:*
- Original email marked as read
- Won't be picked up by trigger again

*Slack:*
- No notification sent (amount < $500 threshold)

---

**Talking Points for Script:**

[Suggestions for what to emphasize during this demo]

- "Notice how the workflow polls every minute - you can adjust this timing"
- "The filter step saves API costs by excluding obvious non-invoices"
- "See the confidence score of 0.92? We set the threshold at 0.6 for our use case"
- "The smart filename makes invoices searchable - no more hunting through folders"
- "This took 35 seconds - manually this would take 5-10 minutes per invoice"
- "The duplicate check prevents processing the same invoice twice if forwarded"

---

**Code References:**

[Important files/nodes to mention or show]

Example:
- workflow.json - Complete n8n workflow definition
- Node: "Filter PDF Attachments" (Code node) - Exclusion patterns can be customized
- Node: "Build File Path" (Set node) - Filename format is configurable
- Classification threshold: 0.6 (workflow settings, line 234)
- High-value threshold: $500 (IF node condition, line 567)

---

#### Scenario 2: [Name] (Secondary)

[Repeat same structure as Scenario 1]

**Purpose:** [Different use case or variation]

[Continue with Setup, Test Data, Steps, Outcomes, Talking Points, Code References]

---

#### Scenario 3: [Name] (Edge Case)

[Repeat same structure]

**Purpose:** [Error handling or validation demo]

[Continue with Setup, Test Data, Steps, Outcomes, Talking Points, Code References]

---

### Technical Deep Dive Notes

[Interesting implementation details for the script writer]

**Key Code Paths:**

[File paths and important functions/nodes]

Example:
- Entry point: workflow.json → Gmail Trigger node (node_id: "gmail_trigger_1")
- Classification logic: LlamaCloud API → 3 rules with 0.6 threshold
- Extraction schema: 6 core fields + line_items array
- Duplicate detection: Compare sender_email + invoice_number against Sheets

**Architecture Decisions:**

[Why things are built this way]

Example:
- "Uses LlamaCloud instead of local OCR for higher accuracy and no infrastructure"
- "Filters PDFs before classification to save API credits"
- "Duplicate check uses sender + invoice # (not just invoice #) because different 
   vendors might use same numbering"
- "Smart filename includes date prefix for chronological sorting"
- "Threshold of $500 is configurable - common for small business expense approval workflows"

**Integration Points:**

[How external services connect]

Example:
- Gmail: IMAP connection with OAuth2 authentication
- LlamaCloud: REST API with API key authentication
- Google Drive: API v3 with service account credentials
- Google Sheets: API v4 with same service account
- Slack: Incoming webhook (no authentication beyond webhook URL)

**Performance Notes:**

[Speed, scalability, limitations]

Example:
- Processing time: ~30-40 seconds per invoice
- Bottleneck: AI classification + extraction (~25 seconds)
- Can handle ~120 invoices per hour with current setup
- Free tiers sufficient for <1000 invoices/month
- No concurrent processing (sequential by design for simplicity)

**Error Handling:**

[How errors are managed]

Example:
- Failed classification → Workflow continues, logs "unknown" in Sheets
- API timeout → Retries up to 3 times with exponential backoff
- Invalid PDF → Skipped, email marked as read, logged as "error" in Sheets
- Duplicate invoice → Silently skipped, email still marked as read

---

### Key Value Propositions

[Quantified benefits - from code analysis + user context]

Example:

1. **Time Savings:** 
   - Automates 5-10 minutes of manual work per invoice
   - For 100 invoices/month: Saves ~10 hours/month
   - ROI: First month pays for all tool costs

2. **Cost Reduction:**
   - Eliminates need for manual data entry staff ($15-25/hour labor cost)
   - Free tier sufficient for <50 invoices/month (zero cost)
   - At 100 invoices/month: ~$30/month total tool costs vs $250+/month labor

3. **Quality Improvement:**
   - 100% consistent data extraction (no typos)
   - Zero missed invoices (automated monitoring)
   - Complete audit trail (every invoice logged with timestamp)

4. **Scalability:**
   - Handles 1 invoice or 1000 invoices with same setup
   - Manual process breaks down at ~50 invoices/month
   - No additional overhead as volume grows

5. **Reliability:**
   - Duplicate detection prevents double-processing
   - Automatic error recovery with retries
   - High-value alerts ensure nothing falls through cracks

---

### Workflow Assumptions

[What we assume about the input/environment - inferred from code validation]

Example:

- Invoices are shared as email attachments (not links or embedded content)
- PDFs are the primary invoice format (JPG/PNG not supported)
- Invoice emails arrive in a single monitored Gmail inbox
- Each email contains at most one invoice PDF attachment
- Invoice data follows standard formats (vendor, invoice #, dates, amounts)
- Sender email is consistent per vendor (used for duplicate detection)
- Internet connection available (cloud services required)
- Gmail, Drive, Sheets all use same Google account

**Limitations:**

[What doesn't work]

Example:
- Does not handle scanned images (needs OCR preprocessing)
- Does not process invoice links (must be PDF attachments)
- Does not support multi-page invoices with different vendors
- Cannot process password-protected PDFs
- No offline mode (requires cloud API access)

---

### Customization Options

[How viewers can adapt this - from code structure analysis]

**Tool Swaps:**

Example:
- **Slack → Teams/Discord:** Replace Slack notification node with Microsoft Teams or Discord webhook
- **Google Sheets → Airtable:** Swap Sheets nodes with Airtable API calls
- **LlamaCloud → OpenAI:** Replace classification/extraction with GPT-4 Vision API
- **Gmail → Outlook:** Use Microsoft Graph API instead of Gmail trigger

**Configuration Changes:**

Example:
- **Alert threshold:** Change $500 to any amount (IF node condition)
- **Poll frequency:** Change Gmail trigger from 60s to any interval
- **Filename format:** Modify Set node to use different naming convention
- **Classification rules:** Adjust confidence thresholds or add new document types
- **Filter patterns:** Update exclusion patterns to skip different file types

**Extensions:**

Example:
- **Multi-currency support:** Add currency conversion node
- **Vendor database:** Link to vendor management system
- **Payment automation:** Integrate with QuickBooks/Xero for automatic bill creation
- **Approval workflow:** Add approval step before Drive upload for high-value invoices
- **Email notifications:** Send confirmation emails to finance team
- **Analytics dashboard:** Connect to Power BI or Tableau for invoice insights

**Alternative Use Cases:**

Example:
- **Receipt processing:** Change classification rules and extraction schema
- **Contract management:** Adjust for contract documents
- **Purchase orders:** Modify for PO processing
- **Expense reports:** Adapt for employee expense reimbursement

---

### Notes for Script Writer

[Additional context that helps with script creation but doesn't fit elsewhere]

Example:

- **Opening hook:** Lead with the pain point - "Finance teams waste 10+ hours per week 
  on manual invoice data entry. Let me show you how to automate the entire process."

- **Flagship scenario timing:** Spend 40-50% of video time on Scenario 1 (basic processing), 
  showing node-by-node breakdown

- **Secondary scenarios:** Quick walkthroughs (10% each), highlight differences only

- **Customization section:** Show 2-3 examples of swaps (Slack → Teams, Sheets → Airtable)

- **Emphasize "wow" moments:**
  - AI reading PDF and extracting structured data (no typing!)
  - Smart filename generation (chronological, searchable)
  - Duplicate detection (prevents errors automatically)

- **Common pitfalls to mention:**
  - API keys must have correct permissions
  - Gmail trigger needs "Mark as read" to prevent loops
  - Duplicate check requires sender email (not just invoice #)
  - File size limits: LlamaCloud maxes at 10MB per file

- **Visual cues for video:**
  - Show n8n canvas with all nodes visible
  - Zoom in on specific nodes when explaining logic
  - Display actual terminal/console output
  - Show Drive folder before/after
  - Show Sheets before/after with new row highlighted

- **Call-to-action placement:**
  - After customization section (natural transition)
  - Mention download link when showing workflow canvas
  - Custom build offer after explaining complexity of setup

---

## End of Context File

---

## Metadata for Script Generator

**Generated by:** video-idea-to-context skill
**Analysis date:** [ISO timestamp]
**Tools used:** [List tools: SemanticSearch, Grep, Read, WebSearch (if used), etc.]
**MCP servers:** [List if any: n8n-mcp, user-github, etc.]

**Completeness check:**
- [x] User context gathered
- [x] Technical analysis complete
- [x] Demo scenarios designed
- [x] Tool pricing documented
- [x] All sections filled

**Notes:**
[Any caveats, warnings, or follow-up needed]

Example:
"Tool pricing marked for manual research - must be completed before script generation."
"Project uses deprecated API version - mention upgrade path in video."
```

---

## Template Usage Notes

### Required Sections

Every video-context.md MUST have:
- File header
- USER-PROVIDED CONTEXT (all subsections)
- AUTO-GENERATED CONTEXT (all subsections)
- At least 1 demo scenario (flagship)

### Optional Sections

Can be omitted if not applicable:
- Secondary/edge case scenarios (if only flagship exists)
- Slack/notifications (if project doesn't have them)
- Database details (if project doesn't use DB)

### Formatting Rules

1. **Use markdown consistently:**
   - `# ` for main sections
   - `## ` for major subsections
   - `### ` for scenario names
   - `#### ` for scenario components

2. **Use code blocks for:**
   - Configuration files (```json, ```yaml, ```env)
   - Terminal commands (```bash)
   - Code snippets (```python, ```javascript)

3. **Use tables for:**
   - Tools & Technologies
   - Comparison matrices

4. **Use lists for:**
   - Prerequisites
   - Steps
   - Bullet points

5. **Use emphasis:**
   - **Bold** for labels and important terms
   - *Italic* for explanatory notes
   - `Code formatting` for file names, commands, variables

### Quality Check

Before saving video-context.md, verify:

- [ ] All USER-PROVIDED sections filled (no "[TODO]" placeholders)
- [ ] All AUTO-GENERATED sections filled
- [ ] At least 1 complete demo scenario with specific test data
- [ ] Tool pricing researched or marked for research
- [ ] Code references include actual file paths
- [ ] Expected outcomes are concrete, not vague
- [ ] No hallucinated information
- [ ] Markdown formatting correct
- [ ] File saved in `demo-video/video-context.md`

---

## Example: Minimal Valid Output

```markdown
# Video Context: Invoice Processing Automation

**Generated:** 2026-01-21
**Project:** n8n-invoice-automation
**Type:** Tutorial
**Project Type:** n8n Workflow

---

## 📌 USER-PROVIDED CONTEXT

### Problem Statement / Pain Point
Manual invoice data entry takes 10+ hours per week and is error-prone.

**Why it matters:** Finance teams waste time on repetitive work.

### Target Audience
- Business owners wanting to automate back-office processes

**Their main goal:** Eliminate manual invoice data entry

**Skill level:** Beginner
**Assumes viewer knows:** Basic email and spreadsheets

### Key Value Proposition / Hook
**One-sentence benefit:** Automatically extract invoice data from emails using AI

**"Wow" factor:** AI reads PDFs—no manual typing

### Video Preferences
**Tone:** Friendly
**Technical depth:** Medium
**Target length:** 10-20 minutes

### Call-to-Action
**Custom build service:** Yes - Contact via email@example.com
**Consultation:** No
**Download:** GitHub repo - github.com/user/project
**Contact:** email@example.com

---

## 🤖 AUTO-GENERATED CONTEXT

### Solution Overview
n8n workflow monitors Gmail for invoice PDFs, uses LlamaCloud AI to extract data, 
saves to Google Drive with smart filenames, logs to Google Sheets.

**Key capabilities:**
- Automatic email monitoring
- AI data extraction
- Smart file organization
- Duplicate detection

[Continue with all other sections...]
```

This minimal example shows the required structure. A complete video-context.md should be much more detailed, especially in demo scenarios and technical notes.
