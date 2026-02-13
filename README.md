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

**Required:**
- `SLACK_BOT_TOKEN` - [Create a Slack app](https://api.slack.com/apps)
- `NOTION_TOKEN` - [Create a Notion integration](https://www.notion.so/my-integrations)
- `VM0_TOKEN` - Your VM0 API token (from platform.vm0.ai)

**Optional (add as needed):**
- `GMAIL_CREDENTIALS` - Google OAuth credentials JSON
- `GOOGLE_SHEETS_CREDENTIALS` - Google service account JSON
- `FIRECRAWL_API_KEY` - [Get from Firecrawl](https://firecrawl.dev)
- `OPENAI_API_KEY` - [Get from OpenAI](https://platform.openai.com)
- `CLOUDINARY_URL` - [Cloudinary connection URL](https://cloudinary.com)

### 3. Deploy

```bash
# Clone this repository
git clone https://github.com/vm0-ai/comma.git
cd comma

# Deploy the agent
vm0 compose vm0.yaml
```

### 4. Start Using

**Via Slack:**
- Invite the bot to your channels
- Mention `@comma` or DM it directly
- Example: "@comma summarize the last 50 messages in #engineering"

**Via CLI:**
```bash
vm0 agent run comma "Check my unread emails from today"
vm0 agent run comma "Create a meeting notes page in Notion"
```

**Via Platform:**
- Visit [platform.vm0.ai](https://platform.vm0.ai)
- Open your comma agent
- Chat in the web interface

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

## Configuration

### Default Skills (8 included)

**Communication:**
- Slack - Team messaging
- Gmail - Email management

**Productivity:**
- Notion - Documents & databases
- Google Sheets - Spreadsheet data

**Intelligence:**
- Firecrawl - Web scraping
- OpenAI - AI generation

**Utilities:**
- Cloudinary - File hosting
- VM0 CLI - Self-management

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

## Architecture

```
┌─────────────────────────────────────────┐
│         Comma Agent (Claude)            │
│  - Natural language understanding       │
│  - Task orchestration                   │
│  - Context management                   │
└─────────────────────────────────────────┘
                    │
        ┌───────────┼───────────┐
        │           │           │
        ▼           ▼           ▼
   ┌─────────┐ ┌─────────┐ ┌─────────┐
   │  Comm   │ │  Prod   │ │  Intel  │
   │ Skills  │ │ Skills  │ │ Skills  │
   ├─────────┤ ├─────────┤ ├─────────┤
   │ Slack   │ │ Notion  │ │Firecrawl│
   │ Gmail   │ │ Sheets  │ │ OpenAI  │
   └─────────┘ └─────────┘ └─────────┘
        │           │           │
        └───────────┼───────────┘
                    ▼
          ┌──────────────────┐
          │  VM0 Sandbox     │
          │  - Secure exec   │
          │  - State mgmt    │
          │  - Scheduling    │
          └──────────────────┘
```

## Tips for Best Results

### Be Specific
❌ "Check my messages"
✅ "Check my Slack messages in #engineering from today"

### Provide Context
❌ "Send this to the team"
✅ "Post this summary to #team-updates on Slack"

### Use Memory
✅ "Remember that I prefer bullet-point summaries"
✅ "Recall my team's Slack channels"

### Automate Repetitive Tasks
✅ Set up daily email digests
✅ Schedule weekly planning sessions
✅ Automate file organization

## Troubleshooting

### Agent not responding in Slack
- Check that bot is invited to the channel
- Verify `SLACK_BOT_TOKEN` is set correctly
- Check bot permissions in Slack app settings

### Can't access Gmail
- Ensure OAuth consent screen is configured
- Add your email to test users
- Verify credentials JSON is valid

### Skills not working
- Check that required secrets are set
- View agent logs: `vm0 agent logs comma`
- Verify skill URLs are correct in vm0.yaml

### Rate limits
- Most APIs have rate limits
- Space out requests or use scheduling
- Consider caching frequently accessed data

## Advanced

### Custom Memory Store

By default, memory is stored in Notion. To use a different store:

```yaml
environment:
  MEMORY_BACKEND: notion  # or: sqlite, postgres
  MEMORY_DATABASE: ${{ secrets.MEMORY_DB_URL }}
```

### Multi-Agent Workflows

Comma can coordinate with other agents:

```bash
# Create a specialized research agent
vm0 compose research-agent.yaml

# Have comma delegate research tasks
vm0 agent run comma "Use research-agent to analyze market trends"
```

### Custom Instructions

Add organization-specific instructions to `AGENTS.md`:

```markdown
## Company-Specific Guidelines

- Always use our brand voice: professional but friendly
- Default meeting time zone: EST
- File naming convention: YYYY-MM-DD-description
```

## Security & Privacy

- All credentials stored as encrypted VM0 secrets
- Agent runs in isolated sandbox
- No data persisted between runs (use Notion/cloud storage)
- API calls auditable via VM0 logs
- Compatible with enterprise SSO

## Limits & Quotas

**VM0 Free Tier:**
- 100 agent runs/month
- 10 scheduled tasks
- 1GB storage

**VM0 Pro:**
- Unlimited runs
- Unlimited schedules
- 100GB storage
- Priority support

**API Rate Limits:**
- Slack: 1 req/sec average
- Gmail: 250 quota units/user/second
- Notion: 3 req/sec average
- OpenAI: Depends on your tier

## Contributing

We welcome contributions!

- Report bugs via [GitHub Issues](https://github.com/vm0-ai/comma/issues)
- Suggest features via [Discussions](https://github.com/vm0-ai/comma/discussions)
- Submit PRs for improvements
- Share your use cases and configurations

## Resources

- **Documentation**: [docs.vm0.ai](https://docs.vm0.ai)
- **Skills Catalog**: [vm0-skills](https://github.com/vm0-ai/vm0-skills)
- **Examples**: [comma/examples](./examples)
- **Community**: [Discord](https://discord.gg/vm0)
- **Support**: support@vm0.ai

## License

MIT License - see [LICENSE](LICENSE) file

## Credits

Built on [VM0](https://vm0.ai) - Agent-native infrastructure
Inspired by [my-agent](https://github.com/e7h4n/my-agent) by @e7h4n

---

**Ready to get started?** Deploy comma in 5 minutes: `vm0 compose vm0.yaml`
