# pr-agent

A PR agent that integrates Slack notifications, GitHub Actions analysis, and Claude Code for AI-powered workflows.

## 🚀 Quick Start

### 1. Clone the Repository

```sh
git clone https://github.com/virendrapatil24/pr-agent.git
cd pr-agent
```

### 2. Set Up Python Environment

Install [uv](https://github.com/astral-sh/uv) for fast dependency management:

```sh
pip install uv
```

Create and activate a virtual environment:

```sh
uv venv .venv
source .venv/bin/activate
```

Install dependencies:

```sh
uv pip install -r pyproject.toml
```

### 3. Claude Code Integration

This project uses Claude Code for AI workflow integration.  
Follow the [official Claude setup guide](https://docs.anthropic.com/en/docs/claude-code/setup).

Register your MCP server in Claude:

```sh
claude mcp add pr-agent  -- uv --directory /absolute/path/to/pr-agent/app run server.py
claude mcp list
```

### 4. GitHub Webhook Setup

Start the webhook server to receive GitHub Actions events:

Note: make sure you are using content type as application json.

```sh
python app/webhook_server.py
```

Events will be saved to `app/github_events.json`.

Expose your local server using Cloudflare Tunnel:

```sh
cloudflared tunnel --url http://localhost:8080
```

Configure your GitHub webhook to point to your tunnel URL.

### 5. Slack Integration

Set up a Slack Incoming Webhook:

1. Go to Slack API Apps and create a new app ("From scratch").
2. Enable "Incoming Webhooks" and add a new webhook to your chosen channel.
3. Copy the webhook URL.

Export your webhook URL:

```sh
export SLACK_WEBHOOK_URL="https://hooks.slack.com/services/YOUR/WEBHOOK/URL"
```

### 6. Running All Services

- **Terminal 1:** Start webhook server  
  `python app/webhook_server.py`
- **Terminal 2:** Start MCP server  
  `uv run app/server.py`
- **Terminal 3:** Start Cloudflare Tunnel  
  `cloudflared tunnel --url http://localhost:8080`

### 7. Using the PR Agent

- Ask Claude:  
  “Can you analyze my changes and suggest a PR template?”
- Analyze GitHub events:  
  “What GitHub Actions events have we received?”
- Summarize CI results:  
  “Analyze CI Results” or “Create Deployment Summary”
- Notify your team on Slack about CI/CD status and deployments:
  "Analyze CI Results and notify the team"

---

Here's the working [demo](https://youtu.be/lyhtDrNdHAQ?si=P_ZK0fPNmP-btS0q) (no voice).

For more details, see [app/server.py](app/server.py) and [app/webhook_server.py](app/webhook_server.py)
