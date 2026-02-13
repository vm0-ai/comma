# Migration from my-agent to Comma

This document explains how Comma differs from [e7h4n/my-agent](https://github.com/e7h4n/my-agent) and helps existing my-agent users understand the changes.

## Philosophy Change

**my-agent**: Specialized for developer teams working on vm0-ai/vm0 project
**Comma**: General-purpose assistant for any team or individual

## Key Differences

### 1. Team-Specific Content Removed

| my-agent | Comma |
|----------|-------|
| Hardcoded team members table | Dynamic user resolution via API queries |
| Default repo: vm0-ai/vm0 | No default repository |
| Default Linear project: vm0 | No default project |
| Developer-centric operations | General productivity operations |

### 2. Skills Configuration

**my-agent (10 skills):**
```yaml
- github          # Developer tool
- linear          # Developer tool
- slack
- plausible       # Analytics
- agentmail
- axiom           # Monitoring
- notion
- vm0-cli
- vm0-agent
- slack           # from e7h4n/elephant
```

**Comma (8 skills):**
```yaml
- slack           # Communication
- gmail           # Communication
- notion          # Productivity
- google-sheets   # Productivity
- firecrawl       # Intelligence
- openai          # Intelligence
- cloudinary      # Utility
- vm0-cli         # Utility
```

**Changes:**
- ❌ Removed: github, linear, plausible, axiom, agentmail, vm0-agent
- ✅ Added: gmail, google-sheets, firecrawl, openai, cloudinary
- ✅ Kept: slack, notion, vm0-cli

### 3. Operations Removed

These developer-specific operations were removed:

**Development Workflow:**
- `deep research` - Codebase analysis
- `deep innovate` - Solution architecture
- `deep plan` - Implementation planning
- `issue plan` - GitHub/Linear issue workflow
- `issue action` - Follow up on issues
- `issue create` - Create technical issues

**Team Management:**
- `my work` - Personal GitHub/Linear tasks
- `we work` - Team-wide task view
- `my backlog` - Personal backlog items
- `we backlog` - Team backlog view

**Why?** These are too specialized for developers. Business users need different workflows.

### 4. Instructions Reorganized

**my-agent structure:**
- Team Members (hardcoded)
- External References (#, ~ syntax)
- GitHub Default Context
- Operations (deep research, issue plan, etc.)

**Comma structure:**
- Core Principles (universal)
- Skills Available (what can be done)
- Memory & Context
- File & Document Management
- Communication
- Productivity & Knowledge Work
- Scheduled Tasks
- Common Workflows
- Self-Management

**Why?** Organized by use case rather than platform/operation.

### 5. New Capabilities

Comma adds several capabilities not in my-agent:

**Cross-Session Memory:**
```
"Remember that I prefer short summaries"
"Recall what we discussed about the project"
```

**Scheduled Automation:**
```
"Every day at 6pm, summarize my unread Slack messages"
"Weekly on Friday, generate a summary of completed tasks"
```

**Common Workflows:**
- Morning Routine
- Email to Action
- Research to Document
- Meeting Follow-up
- Weekly Review

### 6. Use Case Focus

**my-agent target users:**
- Software developers
- Working on specific GitHub repository
- Using Linear for issue tracking
- Team-based workflows

**Comma target users:**
- Office workers
- Knowledge workers
- Content creators
- Sales teams
- Customer support
- Anyone needing productivity assistance

## Migration Path

### For Developer Teams

If you're a developer team and want my-agent functionality in Comma:

1. **Add developer skills back:**

```yaml
skills:
  # ... existing Comma skills ...
  - https://github.com/vm0-ai/vm0-skills/tree/main/github
  - https://github.com/vm0-ai/vm0-skills/tree/main/linear
```

2. **Add environment variables:**

```yaml
environment:
  # ... existing variables ...
  GH_TOKEN: ${{ secrets.GH_TOKEN }}
  LINEAR_API_KEY: ${{ secrets.LINEAR_API_KEY }}
```

3. **Customize AGENTS.md** with your team's operations

### For Business Teams

Comma works out of the box! Just:

1. Set up required secrets (Slack, Notion, etc.)
2. Deploy: `vm0 compose vm0.yaml`
3. Start chatting

## Feature Comparison

| Feature | my-agent | Comma |
|---------|----------|-------|
| GitHub integration | ✅ | ➕ (add manually) |
| Linear integration | ✅ | ➕ (add manually) |
| Slack integration | ✅ | ✅ |
| Email (Gmail) | ❌ | ✅ |
| Notion | ✅ | ✅ |
| Google Sheets | ❌ | ✅ |
| Web research | ❌ | ✅ (Firecrawl) |
| AI generation | ❌ | ✅ (OpenAI) |
| File hosting | ❌ | ✅ (Cloudinary) |
| Code analysis | ✅ | ➕ (add GitHub) |
| Issue tracking | ✅ | ➕ (add Linear/Jira) |
| Team workflows | ✅ (dev-focused) | ✅ (general) |
| Memory | ✅ (elephant) | ✅ (Notion-based) |
| Scheduling | ✅ | ✅ |
| Self-update | ✅ | ✅ |

Legend:
- ✅ Built-in
- ➕ Can be added
- ❌ Not available

## What to Choose?

**Use my-agent if:**
- You're a developer team
- Working on vm0-ai/vm0 or similar project
- Need GitHub/Linear deep integration
- Want opinionated developer workflows

**Use Comma if:**
- You're a business user
- Need email, docs, and general productivity
- Want flexible, customizable agent
- Don't need code-specific features
- Want to add skills as needed

**Use a hybrid if:**
- You're a mixed team (devs + business)
- Fork Comma and add GitHub/Linear skills
- Customize AGENTS.md for your workflows

## Example Customizations

### Adding Developer Operations Back

Create `DEVELOPER_OPS.md` with your team's dev workflows:

```markdown
## Operation: Issue Plan

**Usage:** `issue plan [issue-id]`

Start working on a GitHub issue...
```

Then reference it in AGENTS.md:

```markdown
## Developer Operations

For developer-specific operations, see [DEVELOPER_OPS.md](./DEVELOPER_OPS.md)
```

### Hybrid Configuration

```yaml
version: "1.0"
agents:
  hybrid-assistant:
    framework: claude-code
    instructions: AGENTS.md
    skills:
      # Comma's core skills
      - https://github.com/vm0-ai/vm0-skills/tree/main/slack
      - https://github.com/vm0-ai/vm0-skills/tree/main/gmail
      - https://github.com/vm0-ai/vm0-skills/tree/main/notion
      - https://github.com/vm0-ai/vm0-skills/tree/main/google-sheets

      # my-agent's dev skills
      - https://github.com/vm0-ai/vm0-skills/tree/main/github
      - https://github.com/vm0-ai/vm0-skills/tree/main/linear

      # Intelligence
      - https://github.com/vm0-ai/vm0-skills/tree/main/firecrawl
      - https://github.com/vm0-ai/vm0-skills/tree/main/openai
```

## Questions?

- **Can I use both?** Yes! Deploy them separately with different names
- **Will my-agent be deprecated?** No, it's still maintained for developer teams
- **Can I contribute to Comma?** Yes! PRs welcome at github.com/vm0-ai/comma
- **How do I migrate my data?** Memory and configurations are separate, no migration needed

## Credits

Comma is inspired by and based on learnings from:
- [e7h4n/my-agent](https://github.com/e7h4n/my-agent) by @e7h4n
- [VM0 Skills](https://github.com/vm0-ai/vm0-skills) ecosystem
- Community feedback on agent use cases

Thank you to the my-agent community for pioneering agent-based workflows!
