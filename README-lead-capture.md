# AI Lead Capture Agent (WhatsApp to Google Sheets CRM)

An n8n workflow that chats with a new lead on WhatsApp, collects their **name and interest** (their WhatsApp number is captured automatically), saves them as a row in a Google Sheet that works as a simple CRM, and alerts the business owner on WhatsApp.

## How it works

1. **WhatsApp Webhook** receives incoming messages from Evolution API.
2. **Extract Message** pulls out the sender, name and text, and ignores groups and your own messages.
3. **AI Agent** (OpenAI, with per-chat memory) replies like a receptionist and asks for one missing detail at a time.
4. **Parse AI Reply** reads the agent's structured JSON output.
5. **Send Reply** sends the answer back through Evolution API.
6. **Lead Complete?** checks that name and interest were collected.
7. **Save to Google Sheet** adds the lead as a new row.
8. **Alert Owner** sends the owner a WhatsApp message with the lead's details.

## Tools

n8n, OpenAI API, WhatsApp (Evolution API), Google Sheets

## Setup

1. Run an Evolution API server and connect a WhatsApp number to an instance (scan the QR code).
2. Import the JSON into n8n (Workflows, Import from file). n8n must be reachable from the internet (n8n Cloud or a hosted n8n).
3. Open the **Config** node and fill in your Evolution server URL, instance name and API key.
4. In Evolution API, open the instance webhook settings, paste this workflow's **production** webhook URL, and enable the `MESSAGES_UPSERT` event.
5. Add credentials for OpenAI and Google Sheets.
6. Create a Google Sheet with a tab named `Leads` and these headers in row 1: `Date`, `Name`, `WhatsApp Number`, `Interest`. Paste its ID in **Save to Google Sheet**.
7. Set your own WhatsApp number in **Config** (`owner_number`, country code, no +) and replace `[YOUR BUSINESS NAME]` in the **AI Agent** system message.
8. Activate the workflow and message the connected WhatsApp number.

## Screenshot

Add a screenshot of the workflow canvas here.

## Author

Ashad Rashid
