# Demo Scenario Templates

This guide provides templates and examples for designing concrete, executable demo scenarios.

## Core Principles

1. **Be Specific:** Include actual commands, file names, data examples
2. **Be Executable:** Viewer should be able to replicate exactly
3. **Show Value:** Each scenario demonstrates a key benefit
4. **Include Context:** Setup, data, steps, outcomes - all detailed

---

## Scenario Template (Full Format)

```markdown
### Scenario N: [Descriptive Name]

**Purpose:** [What this scenario demonstrates]

**Value Demonstrated:** [Key benefit shown - time saved, automation, accuracy, etc.]

**Estimated Demo Time:** [Minutes in video]

---

#### Setup Requirements

**Configuration Files:**
- `config.json`:
  ```json
  {
    "api_key": "demo_key_123",
    "endpoint": "https://api.example.com"
  }
  ```

**Environment Variables:**
- `API_SECRET=test_secret_value`
- `DATABASE_URL=sqlite:///test.db`

**Prerequisites:**
- Service X account created (free tier)
- API key generated (show where to get it)
- Dependencies installed: `pip install -r requirements.txt`

**Initial State:**
- Database empty / has seed data
- Folder structure: `/input`, `/output` exist
- No prior executions

---

#### Test Data

**Input Files:**

`users.csv` (3 rows):
```csv
email,name,role
admin@example.com,Admin User,admin
user@example.com,Regular User,user
guest@example.com,Guest User,guest
```

`config.json`:
```json
{
  "batch_size": 100,
  "timeout": 30
}
```

**Mock API Responses** (if needed):
- For user@example.com: {"status": "success", "id": "usr_123"}
- For admin@example.com: {"status": "success", "id": "usr_456"}

---

#### Execution Steps

1. **Prepare input data**
   - Place `users.csv` in `/input` folder
   - Verify file has 3 rows: `cat input/users.csv`

2. **Run the command**
   ```bash
   python main.py --input input/users.csv --config config.json
   ```

3. **What happens (code level):**
   - Entry point: `main.py` → `main()` function (line 12)
   - Reads CSV: `src/reader.py` → `read_csv()` (line 23)
   - Validates each row: `src/validator.py` → `validate_user()` (line 45)
   - Calls API: `src/api/client.py` → `process_user()` (line 89)
   - Saves results: `src/storage.py` → `save_report()` (line 67)

4. **Monitor progress**
   - Terminal shows: "Processing user 1/3..."
   - API calls logged: "Calling API for admin@example.com"
   - Progress bar updates (if implemented)

5. **Check outputs**
   - File created: `output/report_2026-01-21.html`
   - Summary JSON: `output/summary.json`
   - Database updated: 3 new rows in `users` table

---

#### Expected Outcomes

**Console Output:**
```
Starting process...
Loaded 3 users from input/users.csv
Validating users... OK
Processing user 1/3: admin@example.com... SUCCESS
Processing user 2/3: user@example.com... SUCCESS
Processing user 3/3: guest@example.com... SUCCESS
✅ Processed 3 users in 2.3 seconds
📊 Report saved to output/report_2026-01-21.html
```

**Generated Files:**
- `output/report_2026-01-21.html` (23 KB)
  - Contains 3 user cards with status badges
  - Shows processing time per user
  - Includes success/error indicators

- `output/summary.json`:
  ```json
  {
    "total": 3,
    "successful": 3,
    "failed": 0,
    "duration": 2.3,
    "timestamp": "2026-01-21T10:30:00Z"
  }
  ```

**Database State:**
```sql
SELECT * FROM users;
-- Returns 3 rows with processed user data
```

**Visual Indicators:**
- ✅ Green checkmarks for successful processing
- 📊 Report icon clickable link
- ⏱️ Processing time displayed

---

#### Common Variations

**Different input sizes:**
- 10 users: ~7 seconds
- 100 users: ~65 seconds
- Shows scalability

**Different user roles:**
- Admin gets extra permissions field
- Guest gets limited access flag
- Shows flexibility

**With API rate limiting:**
- Add `--delay 1` flag
- Shows 1-second delay between calls
- Demonstrates rate limit handling

---

#### Talking Points for Script

- "Notice the command is simple - just input and config"
- "Watch how it validates before processing - no bad data gets through"
- "See the progress in real-time - you always know what's happening"
- "The report is generated automatically - no manual formatting"
- "This took 2.3 seconds - manually this would take 10+ minutes"

---

#### Things to Mention

**Why this approach:**
- "We validate first to catch errors early"
- "API calls are batched for efficiency"
- "Reports are timestamped for tracking"

**Customization options:**
- "You can change batch_size in config.json"
- "Add more fields to the CSV if needed"
- "Output format can be JSON, HTML, or PDF"

**Error handling** (if showing):
- "If API fails, it retries up to 3 times"
- "Invalid emails are logged but don't stop processing"
- "You get a detailed error report at the end"
```

---

## Scenario Type: Flagship (Main Demo)

**Purpose:** Show the primary use case - the "wow" moment

**Characteristics:**
- Demonstrates core value proposition
- Typical user journey (happy path)
- Shows most impressive feature
- Takes 40-50% of demo time

**Example - Invoice Processing:**

```markdown
### Flagship Scenario: Basic Invoice Processing

**Purpose:** Show end-to-end automated invoice processing

**Value:** Eliminates manual data entry, saves hours per week

#### Test Data

Invoice PDF: `CloudProvider-Inc_Invoice.pdf`
- Vendor: CloudProvider Inc
- Invoice #: INV-2025-042
- Amount: $350.00
- Date: 2025-01-20

Email setup:
- From: billing@cloudprovider.com
- Subject: Invoice INV-2025-042
- Attachment: invoice.pdf (250 KB)

#### Steps

1. Send test email to monitored inbox
2. n8n workflow triggers (Gmail poll every 60s)
3. PDF extracted from attachment
4. LlamaCloud classifies as "invoice" (confidence: 0.92)
5. AI extracts: vendor, amount, invoice #, date
6. Filename created: `2025-01-20_CloudProvider-Inc_INV-2025-042.pdf`
7. Uploaded to Google Drive `/Invoices` folder
8. Row added to Google Sheets tracker
9. Email marked as read

#### Expected Outcome

- Processing time: ~30 seconds
- File in Drive: Organized with smart filename
- Sheets row: All data extracted accurately
- No manual data entry required

#### "Wow" Moment

"Watch as the AI reads this PDF and extracts every field automatically. 
No typing, no copy-paste, just pure automation."
```

---

## Scenario Type: Secondary (Variation)

**Purpose:** Show flexibility and additional features

**Characteristics:**
- Alternative workflow or use case
- Different input/configuration
- Shows adaptability
- Takes 20-30% of demo time

**Example - High-Value Invoice:**

```markdown
### Secondary Scenario: High-Value Invoice Alert

**Purpose:** Demonstrate conditional logic and notifications

**Difference from Flagship:** Invoice amount > $500 triggers Slack alert

#### Test Data

Invoice PDF: `Enterprise-Corp_Invoice.pdf`
- Amount: $1,250.00 (exceeds $500 threshold)

#### Key Differences

- Same processing flow as flagship
- Additional step: Slack notification sent
- Shows conditional branching in workflow

#### Expected Outcome

- All standard processing completes
- PLUS: Slack message to #finance channel:
  ```
  🚨 High-Value Invoice: $1,250.00
  Vendor: Enterprise Corp
  Due: 2025-02-15
  [View PDF in Drive]
  ```

#### Talking Points

"Notice the workflow detected this is over $500 and automatically 
notified the team. The threshold is configurable - set it to 
whatever makes sense for your business."
```

---

## Scenario Type: Edge Case (Error Handling)

**Purpose:** Show robust error handling and validation

**Characteristics:**
- Something goes wrong (intentionally)
- System handles it gracefully
- Shows reliability
- Takes 10-20% of demo time

**Example - Duplicate Detection:**

```markdown
### Edge Case: Duplicate Invoice Detection

**Purpose:** Show how system prevents duplicate processing

**Setup:** Same invoice already processed previously

#### Test Data

Send the SAME invoice email from Scenario 1 again:
- Same sender: billing@cloudprovider.com
- Same invoice #: INV-2025-042

#### Steps

1. Email received by workflow
2. Classification and extraction happen
3. **Duplicate check triggers:** 
   - Compares sender email + invoice # against Google Sheets
   - Finds existing match
4. **Processing stops:**
   - No upload to Drive (file already exists)
   - No new row in Sheets (duplicate detected)
   - Email still marked as read (prevents re-processing)

#### Expected Outcome

- Console log: "⚠️ Duplicate detected: INV-2025-042 from billing@cloudprovider.com"
- No new files created
- No duplicate data in Sheets
- Saves API costs (no unnecessary processing)

#### Talking Points

"This is important - if someone forwards an invoice or there's a 
delivery retry, the system catches it. No duplicate entries, 
no wasted API calls."
```

---

## Quick Scenario Checklist

Before finalizing a scenario, verify:

- [ ] **Specific test data** - Not "provide sample data", but actual examples
- [ ] **Exact commands** - Copy-pasteable
- [ ] **File names** - Specific paths and names
- [ ] **Expected outputs** - Concrete results, not vague descriptions
- [ ] **Timing** - Approximate duration for viewer expectations
- [ ] **Code references** - File paths where relevant
- [ ] **Visual cues** - What viewer sees (console output, UI changes)
- [ ] **Value statement** - Why this matters (time saved, errors prevented)

---

## Anti-Patterns to Avoid

❌ **Too vague:**
```
"Provide some sample invoice data"
"Run the workflow"
"Check the output"
```

✅ **Specific:**
```
"Create invoice.pdf with these details: Vendor=Acme Corp, Amount=$350"
"Run: node workflow.js --input invoice.pdf"
"Verify output.json contains: {vendor: 'Acme Corp', amount: 350}"
```

---

❌ **No expected outcome:**
```
"The workflow will process the data"
```

✅ **Concrete outcome:**
```
"Expected: Console shows 'Processed 3 invoices in 2.1s', 
output/ folder contains 3 PDFs with timestamped names"
```

---

❌ **Missing setup:**
```
"Just run the command"
```

✅ **Complete setup:**
```
"Before running:
1. Set environment: export API_KEY=test_123
2. Create folder: mkdir output/
3. Place test file: cp test.csv input/"
```

---

## Scenario Planning Workflow

1. **Identify the feature** to demonstrate
2. **Choose scenario type** (flagship / secondary / edge case)
3. **Design the test data** (specific files, values, configurations)
4. **Map the execution** (command → code path → output)
5. **Determine expected outcome** (files, console output, UI changes)
6. **Note talking points** (why this matters, customization options)
7. **Add timing estimate** (how long in the video)

---

## Common Scenario Patterns

### Pattern: API Integration Demo

```markdown
Setup: API key, endpoint configuration
Test Data: Sample request payload
Steps: Send request → process response → store result
Outcome: Success response, data saved, confirmation displayed
```

### Pattern: File Processing Demo

```markdown
Setup: Input folder, output folder
Test Data: Sample CSV/PDF/Excel file (show exact contents)
Steps: Read file → validate → transform → write output
Outcome: Output file created, summary displayed
```

### Pattern: Workflow Automation Demo

```markdown
Setup: Trigger configuration, credentials
Test Data: Trigger event (email, webhook, schedule)
Steps: Trigger → process → integrate → notify
Outcome: All steps complete, notifications sent, data synced
```

### Pattern: Error Handling Demo

```markdown
Setup: Intentionally broken input (invalid format, missing fields)
Test Data: Bad file that should fail validation
Steps: Attempt process → validation fails → error handled gracefully
Outcome: Error message clear, no crash, recovery possible
```

---

## Remember

**Good scenarios = Good scripts**

A script writer needs:
- Specific steps to describe
- Concrete data to reference
- Expected outcomes to explain
- Value propositions to highlight

If your scenario has these, the script will be clear and compelling.
