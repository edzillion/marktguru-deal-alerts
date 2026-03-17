Project: Marktguru Deal Alert Automation

Stack:
- n8n automation
- Python scripts for API exploration
- Node.js snippets for n8n Function nodes

Goals:
- scrape Marktguru API for local deals
- filter deals by keywords and price thresholds
- send alerts via Telegram

Coding rules:
- All scripts must be idempotent
- No hardcoded secrets
- All configs in /config
- Output structured JSON

n8n rules:
- Use Function node only for lightweight transforms
- Complex logic lives in /scripts
- Workflows exported after each change

Logging:
- Always log:
  - API status
  - number of deals parsed
  - number of deals filtered

Testing:
- All filter logic must have unit tests