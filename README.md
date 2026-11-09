# n8n Lead Capture to CRM (AI scoring)

An n8n workflow that turns a web form into a qualified CRM record.

## What it does
1. Receives a lead through a webhook.
2. Cleans and validates the data (invalid emails are logged, not lost).
3. Scores the lead 1-10 with Anthropic(claude) and explains why.
4. Creates or updates the contact in HubSpot (no duplicates, matched by email).
5. Logs the lead in Google Sheets.
6. Sends a Telegram alert for hot leads (score 8 or higher).

## Flow
Webhook -> Clean -> Valid email? -> AI score -> Parse -> HubSpot -> Google Sheet -> Hot? -> Telegram

## Setup
1. Import `workflow.json` in n8n.
2. Connect credentials: HubSpot (private app token), Google Sheets, Gemini, Telegram.
3. Create the sheet and HubSpot properties from `SETUP.md`.
4. Activate the workflow and POST a test lead to the webhook.

## Test body
{"name":"Maria Lopez","email":"maria@example.com","message":"Need a quote, budget 2000 USD"}

## Design choices
- A human follows up on every hot lead. The AI only scores.
- Invalid or unreadable AI output goes to a "review" status instead of failing.
- No credentials are stored in this repo.

## Limits
Tested with sample data. Adjust the scoring prompt to the business.

MIT License
