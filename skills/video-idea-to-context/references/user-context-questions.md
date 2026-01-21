# User Context Questions

This reference provides the complete set of questions to ask users AFTER technical analysis is complete.

## Timing: When to Ask

**IMPORTANT:** Ask these questions AFTER you've analyzed the codebase.

Why?
- You understand what the project does technically
- You can pre-fill suggestions based on your findings
- Questions are context-aware and relevant
- User sees you've done your homework

---

## Question 1: Target Audience (Required)

### Context to Provide First

```
I've analyzed your project and found it [brief technical summary].

Example:
"I've analyzed your project and found it's an n8n workflow that 
automates invoice processing using AI extraction, Google Drive storage, 
and Slack notifications."
```

### The Question

```
Who is this video for? (Select all that apply)

[ ] Beginners learning [specific technology - e.g., n8n, automation, Python]
[ ] Intermediate developers exploring [specific tools - e.g., AI APIs, workflow automation]
[ ] Experienced developers optimizing [specific area - e.g., business processes]
[ ] Business owners wanting to automate [specific processes - e.g., back-office tasks]
[ ] Freelancers/agencies looking for client solutions
[ ] Other: [specify]
```

### Follow-up

```
What's their main goal from watching this video?

Example answers:
- "Learn how to automate invoice processing to save time"
- "See what's possible with n8n and AI automation"
- "Build a similar workflow for their business"
- "Understand how to integrate multiple tools"

Your answer:
[Free text input]
```

### How to Use the Answer

Store this for the video-context.md "Target Audience" section:
- "Skill Level" - Infer from their selection (beginner/intermediate/advanced)
- "Persona" - Use their exact wording
- "Their main goal" - Quote directly

---

## Question 2: Pain Point / Problem Statement (Required)

### Context to Provide First

```
Based on the code, I see this project [what it automates/solves].

Example:
"Based on the code, I see this project automates extracting data from 
invoice PDFs and organizing them in Drive and Sheets."
```

### The Question

```
What frustrating manual process or problem does this solve?

Think about:
- What did people do BEFORE this automation?
- How much time did it take?
- What could go wrong?
- Why is it painful?

Example answers:
- "Manual invoice data entry from PDFs takes 10+ hours per week and is error-prone"
- "Finding old invoices in messy email threads wastes time and causes stress"
- "Missing high-value invoices because of inbox overload costs money"

Your answer:
[Free text input]
```

### Follow-up (Optional but Helpful)

```
Why does this matter to your target audience?

Example:
- "Finance teams waste valuable time on repetitive data entry"
- "Businesses lose money when invoices are missed or mis-filed"
- "Manual processes don't scale as the business grows"

Your answer (optional):
[Free text input]
```

### How to Use the Answer

Store for "Problem Statement / Pain Point" section:
- First part: User's exact wording of the problem
- "Why it matters": Impact statement

---

## Question 3: Value Proposition / Hook (Required)

### Context to Provide First

```
I noticed your project [key technical feature].

Example:
"I noticed your project uses AI to automatically extract structured 
data from PDFs and organizes everything with smart filenames."
```

### The Question

```
In one sentence, what's the main benefit viewers get from watching?

This is your "hook" - why someone should watch this video.

Example formats:
- "Watch your Gmail inbox for invoice emails, use AI to extract data, 
  and organize everything automatically"
- "Build a workflow that eliminates manual invoice data entry using 
  n8n and AI"
- "Automate invoice processing from email to Google Drive in 30 seconds 
  per invoice"

Your answer:
[Free text input - aim for one compelling sentence]
```

### Follow-up

```
What's the most impressive or "wow" aspect?

Example:
- "AI reads PDFs and extracts structured data—no manual typing"
- "Complete automation from email arrival to organized storage"
- "Handles 100+ invoices per month with zero manual work"

Your answer:
[Free text input]
```

### How to Use the Answer

Store for "Key Value Proposition / Hook" section:
- "One-sentence benefit": User's hook statement
- "Wow factor": The most impressive aspect

---

## Question 4: Tool Pricing (Conditional - Only if WebSearch Unavailable)

### When to Ask

Only if:
1. External APIs/services detected in code, AND
2. WebSearch tool is NOT available

### Context to Provide First

```
I detected these external services in your code:
- [List all services found - e.g., n8n, LlamaCloud, Gmail, Google Drive, Slack]

For the video context, I need pricing information for each tool so 
viewers know what to expect.

WebSearch is not available, so I can't look this up automatically.
```

### The Question

```
Please provide pricing information for each service:

For each tool, I need:
1. Free tier limits (if any)
   Example: "n8n: Free tier includes 5,000 workflow executions/month"
   
2. When viewers need to pay
   Example: "Pay when you exceed 5,000 executions or need team features"
   
3. Approximate cost (if applicable)
   Example: "Starter plan: $20/month for 20,000 executions"

---

ALTERNATIVELY:

If you don't have this info readily available, I can:
A) Mark pricing as "❓ Research required" (you'll add it before script generation)
B) Wait while you research each service now

Your choice: [Provide now / Mark as research required / Wait while I research]
```

### If User Chooses to Provide:

```
Great! Please provide for each service:

[Service 1 - e.g., n8n]:
- Free tier: 
- When to pay:
- Cost:

[Service 2 - e.g., LlamaCloud]:
- Free tier:
- When to pay:
- Cost:

[etc.]
```

### How to Use the Answer

Store for "Tools & Technologies" table:
- Fill "Pricing" column with exact user-provided info
- If marked "research required": Add "❓ User will research before script generation"

### If WebSearch IS Available

Skip this question entirely. You'll research pricing automatically in Phase 5.

---

## Question 5: Call-to-Action (Required)

### Context to Provide First

```
After viewers watch this video and learn about your project, what 
should they do next?

Many creators offer custom builds, consultations, or provide downloads.
Let's set up your call-to-action.
```

### The Questions (Multiple Parts)

#### Part A: Custom Build Service

```
Do you offer custom build services?

Meaning: Can viewers hire you to build a customized version of this 
workflow/project for their specific needs?

[ ] Yes, I offer custom builds
    → Contact method: [email / website form / calendar link]
    → Message to display: [e.g., "I can customize this workflow for your specific business needs"]

[ ] No, I don't offer this service
```

#### Part B: Consultation

```
Do you offer consultation calls?

Meaning: Can viewers book time with you for setup help, guidance, or questions?

[ ] Yes, I offer consultations
    → Calendar link: [URL]
    → Duration & format: [e.g., "30-minute setup call" or "1-hour strategy session"]
    → Cost: [Free / Paid - specify]

[ ] No, I don't offer this service
```

#### Part C: Download / Resources

```
Where can viewers get this workflow/code?

[ ] GitHub repository: [URL]
[ ] Direct download in video description
[ ] Website: [URL]
[ ] Other: [specify]

Is there a setup guide?
[ ] Yes, included in README
[ ] Yes, separate guide: [URL]
[ ] No, but I'll mention setup in video description
```

#### Part D: Community & Contact

```
How can viewers reach you or join your community?

Email: [address or "not provided"]
Discord: [invite link or "not provided"]
Twitter/X: [@handle or "not provided"]
Website: [URL or "not provided"]
Other: [LinkedIn, YouTube, etc.]
```

### How to Use the Answers

Store for "Call-to-Action" section with this structure:

```markdown
**Custom build service:**
- Offered: [Yes/No]
- Contact: [method]
- Message: [user's exact wording]

**Consultation:**
- Offered: [Yes/No]
- Details: [calendar link, duration, cost]

**Download/Resources:**
- Location: [GitHub, website, etc.]
- Setup guide: [link or details]

**Community/Contact:**
- Email: [address]
- Discord: [link]
- Twitter: [@handle]
- Other: [links]
```

---

## Question 6: Video Preferences (Optional)

### Context to Provide First

```
A few quick preferences about the video style.

These are optional - defaults work fine, but if you have preferences, 
let me know.
```

### The Questions

#### Tone

```
What tone should the video have?

[ ] Casual - Friendly, conversational, approachable
[ ] Professional - Formal, business-focused, polished
[ ] Friendly (default) - Warm but informative, balanced

Default if not specified: Friendly
```

#### Technical Depth

```
How technical should the explanation be?

[ ] High - Deep dives into code, architecture decisions, implementation details
[ ] Medium (default) - Explain what matters, skip low-level details
[ ] Low - High-level overview, focus on results not implementation

Default if not specified: Medium
```

#### Target Length

```
How long should the video be?

[ ] 5-10 minutes - Quick overview, essential points only
[ ] 10-20 minutes (default) - Thorough walkthrough with examples
[ ] 20+ minutes - Comprehensive tutorial, multiple scenarios

Default if not specified: 10-20 minutes
```

### How to Use the Answers

Store for "Video Preferences" section:
```markdown
- **Tone:** [Casual/Professional/Friendly]
- **Technical depth:** [High/Medium/Low]
- **Target length:** [5-10min / 10-20min / 20+min]
```

---

## Question Flow Summary

```
[After deep codebase analysis completes]

👋 "I've analyzed your project. Now I need some context from you 
    to create compelling video content."

1️⃣ Target Audience
   "I found it does [X]. Who is this for?"
   → Get persona, skill level, their goal

2️⃣ Pain Point
   "What frustrating manual process does this replace?"
   → Get problem statement, why it matters

3️⃣ Value Proposition
   "I noticed it [technical feature]. What's the main benefit?"
   → Get hook sentence, "wow" factor

4️⃣ Tool Pricing (only if WebSearch unavailable)
   "I found these services: [list]. Need pricing info."
   → Get pricing or mark for research

5️⃣ Call-to-Action
   "What should viewers do after watching?"
   → Get custom build, consultation, download, contact info

6️⃣ Video Preferences (optional)
   "Any preferences on tone, depth, length?"
   → Get style preferences or use defaults

✅ "Perfect! I have everything I need. Generating video-context.md..."
```

---

## Tips for Asking Questions

1. **Show your work first:**
   - "I analyzed your code and found..."
   - "I see this uses..."
   - Demonstrates you understand the project

2. **Provide examples:**
   - Users often don't know what to say
   - Examples guide them to good answers

3. **Make it conversational:**
   - Not a form to fill out
   - Natural dialogue

4. **Offer defaults:**
   - "If you're not sure, we'll use [default]"
   - Reduces decision fatigue

5. **Explain why you're asking:**
   - "This helps the script writer understand your audience"
   - "This becomes the video's opening hook"

6. **Pre-fill when possible:**
   - "Based on the code, I think the target audience might be [X]. Does that sound right?"
   - Easier to confirm/adjust than start from scratch

---

## Handling Non-Responses

### If user says "I don't know"

**For Target Audience:**
```
Based on the technical complexity, I'll assume [intermediate/advanced] 
developers. We can adjust this later if needed.
```

**For Pain Point:**
```
I'll infer from the code that this solves [observed problem]. 
Sound reasonable?
```

**For Value Prop:**
```
I'll use: "Automate [process] using [technology]" as the hook.
```

### If user says "You decide"

Use your technical findings to create reasonable defaults:
- Target audience: Match to tech stack complexity
- Pain point: What the automation replaces
- Value prop: Main technical capability

**BUT:** Always present your assumptions back to the user:
```
"Based on the code, here's what I'm going with:
- Target audience: [your assumption]
- Pain point: [your assumption]
- Value prop: [your assumption]

Do these work for you?"
```

---

## What NOT to Ask

Don't ask questions you can answer from code:
- ❌ "What technologies does this use?" → You can detect this
- ❌ "How does the workflow work?" → You can trace this
- ❌ "What are the main features?" → You can find these
- ❌ "What files are input and output?" → You can read the code

Only ask what CANNOT be inferred from technical analysis:
- ✅ Marketing/positioning (audience, pain point, value prop)
- ✅ Business offerings (custom builds, consulting)
- ✅ Contact information
- ✅ Pricing (if you can't research it)
- ✅ Style preferences

---

## Example Question Session

```
Agent: "I've analyzed your n8n workflow. It automates invoice processing 
        from Gmail using AI extraction, then organizes files in Google 
        Drive and logs to Google Sheets. Very impressive!
        
        Now I need some context about your audience and goals.
        
        Who is this video for?"

User: "Business owners who want to automate their back-office processes 
       but don't have technical skills."

Agent: "Perfect! And what frustrating manual process does this solve?"

User: "Finance teams spend 10+ hours per week manually typing invoice 
       data from PDFs into spreadsheets. It's tedious and error-prone."

Agent: "Got it. In one sentence, what's the main benefit viewers get?"

User: "Watch your Gmail inbox for invoice emails, use AI to extract 
       data, and organize everything automatically with zero manual work."

Agent: "Excellent hook! After watching, what should viewers do? Do you 
        offer custom builds or consultations?"

User: "Yes, I offer custom builds. They can email me at example@email.com"

Agent: "Great! Any video style preferences, or should I use defaults 
        (friendly tone, medium technical depth, 10-20 minutes)?"

User: "Defaults are fine."

Agent: "Perfect! I have everything I need. Generating video-context.md now..."
```

---

## Success Criteria

Before moving to output generation, verify you have:

- [ ] Clear target audience definition
- [ ] Specific pain point statement
- [ ] Compelling value proposition / hook
- [ ] Pricing info (researched or user-provided or marked for research)
- [ ] Complete call-to-action details
- [ ] Video preferences (or using defaults)
- [ ] User feels heard (you showed understanding of their project)

If missing any required items, ask follow-up questions before proceeding.
