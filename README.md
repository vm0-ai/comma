# Comma - Your AI Assistant

A general-purpose AI assistant for productivity, communication, and knowledge work. Comma helps you manage emails, documents, team communications, and automate routine tasks.

## What Can Comma Do?

- 📧 **Email Management** - Read, send, organize, and summarize emails
- 💬 **Team Communication** - Slack messaging, channel monitoring, and summaries
- 📝 **Document Management** - Create and manage Notion pages and Google Sheets
- 🔍 **Web Research** - Scrape websites, extract content, gather information
- 🤖 **AI-Powered** - Generate content, summarize text, answer questions
- 📁 **File Handling** - Upload, organize, and share files via cloud storage
- ⏰ **Scheduled Tasks** - Automate daily/weekly routines

## Quick Start

### 1. Prerequisites

- [VM0 account](https://platform.vm0.ai) (sign up for free)
- VM0 CLI installed: `npm install -g @vm0/cli`

### 2. Setup Secrets

Configure your API credentials in the [VM0 platform](https://platform.vm0.ai):

### 3. Deploy

```bash
# Clone this repository
git clone https://github.com/vm0-ai/comma.git
cd comma

# Deploy the agent
vm0 compose vm0.yaml
```

### 4. Start Using

**Via CLI:**
```bash
vm0 agent run comma "Check my unread emails from today"
vm0 agent run comma "Create a meeting notes page in Notion"
```

## Example Use Cases

### Morning Routine
```
"Check my unread emails and prioritize them"
"Summarize overnight messages in #general"
"Create today's goals page in Notion"
```

### Email to Action
```
"Download attachments from the latest email from Sarah"
"Create a Notion page summarizing the project proposal email"
"Reply to John's email confirming the meeting at 2pm"
```

### Research & Documentation
```
"Research the latest AI assistant trends and create a summary doc"
"Scrape https://competitor.com/pricing and compare to ours"
"Generate a blog post about productivity tips"
```

### Team Communication
```
"Post the meeting notes to #team-updates"
"Summarize what the team discussed in #planning today"
"Find all messages mentioning 'deadline' in the last week"
```

### Data Work
```
"Add this expense to the tracker spreadsheet"
"Read the sales data from Q4 and calculate totals"
"Create a summary report from the customer feedback sheet"
```

### Adding More Skills

Browse [vm0-skills](https://github.com/vm0-ai/vm0-skills) repository for 70+ additional skills:

**Popular additions:**
- GitHub/GitLab - Code repository management
- Linear/Jira - Issue tracking
- Discord/Lark - Alternative messaging
- CRM tools - Streak, HubSpot, Zendesk
- PDF tools - Document conversion
- Social media - Instagram, YouTube

To add a skill:

1. Edit `vm0.yaml`:
   ```yaml
   skills:
     # ... existing skills ...
     - https://github.com/vm0-ai/vm0-skills/tree/main/github
   ```

2. Add required secrets in VM0 platform

3. Redeploy:
   ```bash
   vm0 compose vm0.yaml
   ```

## Scheduled Automation

Set up recurring tasks:

```bash
# Daily email summary
vm0 schedule create --cron "0 18 * * *" \
  --agent comma \
  --prompt "Summarize my unread emails and post to #daily-digest"

# Weekly planning
vm0 schedule create --cron "0 9 * * 1" \
  --agent comma \
  --prompt "Create weekly goals page in Notion"

# Nightly cleanup
vm0 schedule create --cron "0 23 * * *" \
  --agent comma \
  --prompt "Organize files uploaded today and update file index"
```

View schedules:
```bash
vm0 schedule list
```

## Use Case Configurations

### For Developers

Add these skills for code-related work:

```yaml
skills:
  - https://github.com/vm0-ai/vm0-skills/tree/main/github
  - https://github.com/vm0-ai/vm0-skills/tree/main/linear
  - https://github.com/vm0-ai/vm0-skills/tree/main/sentry
```

### For Sales Teams

Add CRM and outreach tools:

```yaml
skills:
  - https://github.com/vm0-ai/vm0-skills/tree/main/streak
  - https://github.com/vm0-ai/vm0-skills/tree/main/instantly
  - https://github.com/vm0-ai/vm0-skills/tree/main/resend
```

### For Content Creators

Add media generation tools:

```yaml
skills:
  - https://github.com/vm0-ai/vm0-skills/tree/main/elevenlabs
  - https://github.com/vm0-ai/vm0-skills/tree/main/runway
  - https://github.com/vm0-ai/vm0-skills/tree/main/instagram
```

### For Customer Support

Add ticketing and chat tools:

```yaml
skills:
  - https://github.com/vm0-ai/vm0-skills/tree/main/zendesk
  - https://github.com/vm0-ai/vm0-skills/tree/main/intercom
  - https://github.com/vm0-ai/vm0-skills/tree/main/chatwoot
```

## License

MIT License - see [LICENSE](LICENSE) file

## Credits

Built on [VM0](https://vm0.ai) - Agent-native infrastructure

---

**Ready to get started?** Deploy comma in 5 minutes: `vm0 compose vm0.yaml`
