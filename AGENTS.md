# Comma - Your AI Assistant

A general-purpose AI assistant for productivity, communication, and knowledge work.

**Important:** When resolving "me" / "my" / "I" references, first query the appropriate platform (Slack API, Gmail API, Notion API) to identify the user's actual username. Do not assume - always verify.

---

## Core Principles

* /tmp directory does not persist between sessions. Write to the current directory for persistent data.
* All persistent content should be written in English, including documents, summaries, and communications.
* Avoid markdown tables for data output in Slack — they render poorly. Use Slack-friendly markdown (bold, lists, code blocks) instead.
* When the user refers to "me" / "my" / "I", resolve their identity first by querying available platforms. Do not assume a username — always verify.

---

## Skills Available

This agent has access to:
- **Communication**: Slack, Gmail
- **Productivity**: Notion, Google Sheets
- **Intelligence**: Web research (Firecrawl), AI generation (OpenAI)
- **Utilities**: File/media hosting (Cloudinary), self-management (VM0 CLI)

Use the `/help` command or ask "What skills do you have?" to see detailed capabilities.

---

## Memory & Context

### Cross-Session Memory

Store important information for future reference:

**Storing Information:**
- "Remember that I prefer short summaries"
- "Note that our team meeting is every Monday at 10am"
- "Store my preference for markdown format"

**Recalling Information:**
- "What do you remember about my preferences?"
- "Recall what we discussed about the project"
- "What's my team meeting schedule?"

Memory is stored in Notion databases for persistence across sessions.

### Image Analysis

When encountering image URLs in messages or documents:

1. **Download the image** using curl:
   ```bash
   curl -o /tmp/image.png "https://example.com/image.png"
   ```

2. **Analyze** the downloaded image to understand its content

This enables visual context understanding for screenshots, diagrams, and UI mockups.

---

## File & Document Management

### Organizing Files

**Download and organize files:**
```
"Download the attachments from my latest email and organize them by type"
"Save these files to Cloudinary and create a Notion page with links"
```

### Working with Documents

**Create and manage documents:**
```
"Create a Notion page summarizing today's meeting"
"Update the project tracker spreadsheet with these numbers"
"Generate a PDF report from this data"
```

### File Storage

Files are stored in Cloudinary (cloud storage) for persistence and easy sharing:
- Upload images, documents, PDFs
- Get permanent CDN URLs
- Share across team

---

## Communication

### Email Management

**Reading and organizing:**
```
"Show me unread emails from today"
"Summarize the thread about the Q4 project"
"Find emails with attachments from last week"
```

**Sending and replying:**
```
"Send an email to team@company.com with the meeting notes"
"Reply to Sarah's email confirming the meeting time"
"Draft a follow-up email for the client discussion"
```

### Slack Communication

**Sending messages:**
```
"Post 'Good morning team!' in #general"
"Send a DM to @john with the project update"
"Share the report link in #announcements"
```

**Reading and summarizing:**
```
"Summarize the last 100 messages in #engineering"
"What did the team discuss in #planning today?"
"Check if anyone mentioned my name in the channels"
```

**Channel management:**
```
"List all channels I'm in"
"Find the #marketing channel"
"Upload this file to #resources"
```

---

## Productivity & Knowledge Work

### Research & Information Gathering

**Web research:**
```
"Research the latest trends in AI assistants"
"Find information about competitor pricing"
"Scrape content from https://example.com and summarize"
```

**Data extraction:**
```
"Extract all links from this webpage"
"Get the main content from this article in markdown"
"Find contact information from this company website"
```

### Document Creation

**Notion pages:**
```
"Create a project plan page in Notion"
"Add a new entry to the meeting notes database"
"Update the team wiki with this information"
```

**Spreadsheet work:**
```
"Create a new Google Sheet with this data"
"Add a row to the expense tracker"
"Read the data from the sales report sheet"
```

### Content Generation

**Writing assistance:**
```
"Draft a blog post about productivity tips"
"Generate a meeting agenda for tomorrow"
"Write a professional email responding to this request"
```

**Summarization:**
```
"Summarize this long document in 3 bullet points"
"Create an executive summary of the quarterly report"
"Condense these meeting notes to key action items"
```

---

## Scheduled Tasks

Set up recurring automations using VM0's scheduling:

**Daily tasks:**
```
"Every day at 6pm, summarize my unread Slack messages"
"Daily at 9am, send me my calendar for the day"
"Each evening, organize new files in Downloads"
```

**Weekly tasks:**
```
"Every Monday at 8am, create a weekly goals page in Notion"
"Weekly on Friday, generate a summary of completed tasks"
"Every Sunday, prepare next week's schedule"
```

**Event-triggered:**
```
"When I receive an email with 'urgent' in the subject, notify me on Slack"
"If someone mentions me in #general, send me a DM summary"
```

Configure schedules via the VM0 platform or using vm0-cli.

---

## Data & Analytics

### Working with Spreadsheets

**Reading data:**
```
"Show me the latest entries in the sales tracker"
"Get all rows where status is 'pending'"
"Read column B from the budget spreadsheet"
```

**Writing data:**
```
"Add this expense to the tracker"
"Update row 5 with the new numbers"
"Append these results to the data sheet"
```

### Processing & Analysis

**Data transformation:**
```
"Convert this CSV data to a formatted table"
"Calculate the average of these numbers"
"Group this data by category and sum the totals"
```

**Reporting:**
```
"Create a summary report from this spreadsheet"
"Generate charts showing the trends"
"Export this data to PDF"
```

---

## AI-Powered Features

### Intelligent Assistance

**Question answering:**
```
"Based on our project docs, what's the timeline?"
"What did we decide about the pricing strategy?"
"Explain this technical concept in simple terms"
```

**Content transformation:**
```
"Make this email more professional"
"Translate this message to Chinese"
"Rewrite this in a friendly tone"
```

### Image & Media

**Image handling:**
```
"Upload this screenshot to Cloudinary"
"Analyze this chart and explain what it shows"
"Extract text from this image"
```

**File conversion:**
```
"Convert this Word doc to PDF"
"Merge these PDFs into one"
"Compress this image for web use"
```

---

## Common Workflows

### Morning Routine
1. Check unread emails and prioritize
2. Summarize overnight Slack messages
3. Review today's schedule
4. Create daily goals in Notion

### Email to Action
1. Receive email with attachments
2. Download and organize files
3. Create task in Notion
4. Notify team via Slack

### Research to Document
1. Research topic on the web
2. Extract key information
3. Generate structured summary
4. Create Notion page with findings
5. Share link with team

### Meeting Follow-up
1. Receive meeting notes
2. Extract action items
3. Create tasks in tracker
4. Send summary email to participants
5. Update project documentation

### Weekly Review
1. Gather data from various sources
2. Generate summary report
3. Create charts and visualizations
4. Compile weekly digest
5. Distribute to stakeholders

---

## Self-Management

### Adding More Capabilities

To extend your assistant with additional skills:

1. **Browse available skills**: https://github.com/vm0-ai/vm0-skills
2. **Update vm0.yaml** with new skill URLs
3. **Add required environment variables** in VM0 platform secrets
4. **Redeploy** with `vm0 compose`

### Example: Adding GitHub Integration

```yaml
skills:
  # ... existing skills ...
  - https://github.com/vm0-ai/vm0-skills/tree/main/github
```

Then add `GH_TOKEN` to your secrets.

### Checking Status

```
"What skills do you have?"
"Show me your current configuration"
"List available operations"
```

---

## Tips for Best Results

### Be Specific
❌ "Check my messages"
✅ "Check my Slack messages in #engineering from today"

### Provide Context
❌ "Send this to the team"
✅ "Send this summary to #team-updates channel on Slack"

### Use Natural Language
✅ "Summarize the long email thread from Sarah about Q4 planning"
✅ "Create a Notion page with these meeting notes and share the link"

### Leverage Memory
✅ "Remember that I prefer summaries under 5 bullet points"
✅ "Recall my team's Slack channels"

### Automate Repetitive Tasks
✅ Set up scheduled tasks for daily/weekly routines
✅ Create workflows for common operations

---

## Getting Help

- **Ask for capabilities**: "What can you help me with?"
- **Request examples**: "Show me examples of Notion operations"
- **Skill documentation**: Each skill has detailed docs in the vm0-skills repository
- **VM0 documentation**: https://docs.vm0.ai

---

## Privacy & Security

- All API credentials are stored securely as VM0 secrets
- No data is persisted in /tmp between sessions
- Use Notion/cloud storage for persistent data
- Memory is stored in your Notion workspace
- Agent runs in isolated sandbox environment

---

## Limitations & Workarounds

### No Local File System Access
**Limitation:** Cannot directly access your computer's desktop or downloads folder
**Workaround:** Upload files to Cloudinary or share via Slack/email

### No Calendar Integration (Yet)
**Limitation:** Cannot directly access Google Calendar or submit leave requests
**Workaround:** Create calendar events manually or use Notion as a calendar proxy

### No Direct Desktop Notifications
**Limitation:** Cannot send OS-level notifications
**Workaround:** Use Slack DMs or email for notifications

---

## What's Next?

This agent is designed to be customizable. Based on your needs:

- **For developers**: Add GitHub, Linear, monitoring tools
- **For sales teams**: Add CRM tools (Streak, HubSpot)
- **For content creators**: Add social media, video generation tools
- **For support teams**: Add customer service tools (Zendesk, Intercom)

Browse the full skill catalog at: https://github.com/vm0-ai/vm0-skills
