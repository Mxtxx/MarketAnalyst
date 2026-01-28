# MarketAnalyst n8n Workflow Setup Guide

Complete setup instructions for the automated market research workflow.

## Prerequisites

- Self-hosted n8n instance (v1.0+)
- Google Gemini Pro subscription (for API access)
- GitHub account with personal access token
- SMTP email access (Gmail, Outlook, or custom)

---

## Step 1: Import the Workflow

1. Open your n8n instance
2. Go to **Workflows** > **Import from File**
3. Select `workflows/market_research_workflow.json`
4. The workflow will appear in your workflow list

---

## Step 2: Configure Credentials

### A. Google Gemini API Key

1. Go to [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Click **Create API Key**
3. Copy the generated key

In n8n:
1. Go to **Credentials** > **Add Credential**
2. Search for **HTTP Query Auth**
3. Configure:
   - **Name**: `Gemini API Key`
   - **Name** (parameter): `key`
   - **Value**: Your API key
4. Save

### B. GitHub API Token

1. Go to GitHub > **Settings** > **Developer settings** > **Personal access tokens** > **Tokens (classic)**
2. Generate new token with scopes:
   - `repo` (full control of private repositories)
3. Copy the token

In n8n:
1. Go to **Credentials** > **Add Credential**
2. Search for **GitHub API**
3. Configure:
   - **Access Token**: Your GitHub token
4. Save

### C. SMTP Email (Gmail Example)

For Gmail:
1. Enable 2-Factor Authentication on your Google account
2. Go to Google Account > **Security** > **App passwords**
3. Generate an app password for "Mail"

In n8n:
1. Go to **Credentials** > **Add Credential**
2. Search for **SMTP**
3. Configure:
   - **User**: your.email@gmail.com
   - **Password**: Your app password (16 characters, no spaces)
   - **Host**: smtp.gmail.com
   - **Port**: 465
   - **SSL/TLS**: true
4. Save

---

## Step 3: Set Environment Variables

In n8n, go to **Settings** > **Variables** or set these as environment variables:

```bash
# Email Configuration
SENDER_EMAIL=your.email@gmail.com
RECIPIENT_EMAIL=your.email@gmail.com

# GitHub Configuration
GITHUB_OWNER=YourGitHubUsername
GITHUB_REPO=MarketAnalyst
```

Or in the workflow itself, replace the `$env.VARIABLE_NAME` references with hardcoded values.

---

## Step 4: Update Credential IDs

Open the workflow and update these placeholder credential IDs:

1. Find all nodes using `GEMINI_API_CREDENTIAL_ID` and link to your Gemini credential
2. Find all nodes using `SMTP_CREDENTIAL_ID` and link to your SMTP credential
3. Find all nodes using `GITHUB_CREDENTIAL_ID` and link to your GitHub credential

---

## Step 5: Test the Workflow

1. **Manual Test**: Click the "Execute Workflow" button to run once
2. **Check Email**: Verify you receive the test email
3. **Check GitHub**: Verify reports are committed to your repository

---

## Workflow Schedule

| Trigger | Frequency | Purpose |
|---------|-----------|---------|
| News Analysis | Every 6 hours | Scans news, checks for urgent alerts |
| Weekly Report | Sunday 8:00 AM | Comprehensive weekly analysis |

To modify schedules:
- Click on the Schedule Trigger nodes
- Adjust the cron expression or interval

---

## Customization Options

### Adjust Urgency Threshold
In `Process Analysis Result` node, change:
```javascript
const needsImmediateAlert = urgencyScore >= 8;
```
Lower the number (e.g., 7) for more alerts, higher (e.g., 9) for fewer.

### Add More News Sources
Add HTTP Request nodes for additional RSS feeds:
- Bloomberg: `https://feeds.bloomberg.com/markets/news.rss`
- CNBC: `https://www.cnbc.com/id/100003114/device/rss/rss.html`
- FT: `https://www.ft.com/rss/home`

### Change Risk Profile
Edit the prompts in the Gemini API calls to reflect different:
- Risk tolerance (conservative, moderate, aggressive)
- Asset allocation preferences
- Geographic focus

---

## Troubleshooting

### "401 Unauthorized" from Gemini
- Verify your API key is correct
- Check Google AI Studio for quota limits
- Ensure the key parameter name is exactly `key`

### Emails not sending
- Verify SMTP credentials
- For Gmail: ensure app password is used, not regular password
- Check spam folder

### GitHub commits failing
- Verify token has `repo` scope
- Check repository name matches exactly
- Ensure the reports directory structure exists (workflow creates it)

### Rate Limits
Google Gemini free tier limits:
- 15 requests per minute
- 1 million tokens per day

If hitting limits, increase the schedule interval or upgrade to paid tier.

---

## Data Storage Structure

Reports are saved to GitHub in this structure:
```
MarketAnalyst/
├── reports/
│   └── 2024/
│       ├── week_01.md
│       ├── week_02.md
│       └── ...
├── alerts/
│   ├── 2024-01-15_alert.json
│   └── ...
└── memory
```

---

## Cost Estimate

With a Gemini Pro subscription providing API access:
- **Gemini API**: Included in subscription
- **n8n**: Self-hosted (free) or Cloud ($20/month)
- **GitHub**: Free tier sufficient
- **Email**: Free with Gmail/Outlook

**Total monthly cost**: $0 (with existing Gemini Pro subscription)
