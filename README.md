# OpenClaw-Telegram-Gmail-Automation
A self hosted AI automation agent that connects OpenClaw, Telegram, and Gmail to create a command-driven personal assistant. Interact with your system directly from Telegram to run commands, automate workflows, read emails, and send responses using Gmail integration.
This setup enables:

Remote command execution via Telegram
Gmail inbox reading and email sending
Automation pipelines and AI agents
Secure self-hosted control over your data
Designed for developers building automation agents, AI assistants, and productivity tools.

Features

Telegram bot control interface
Secure pairing system for Telegram users
Gmail API integration
Send/read emails via Telegram
Self hosted and customizable
Works on local machine or cloud (AWS/VM)

Architecture
Telegram Bot
   ↓
OpenClaw Server
   ↓
Gmail API (OAuth)
   ↓
Your Gmail Inbox
Requirements
Node.js 18+

Docker (recommended)
Telegram account
Gmail account
Google Cloud project
EC2

1. Install OpenClaw

Clone repository:git clone https://github.com/YOUR_USERNAME/openclaw-telegram-gmail.git
cd openclaw-telegram-gmail
Run with Docker:docker compose up -d
Create Telegram Bot

Open Telegram → search:/newbot
TELEGRAM_BOT_TOKEN=xxxxxxxx
TELEGRAM_BOT_TOKEN=your_token_here
3. Pair Telegram with OpenClaw
Message your bot:OpenClaw: access not configured
Pairing code: XXXXX
4. Setup Gmail API
https://console.cloud.google.com
Enable API

Create project

Enable Gmail API

Create OAuth credentials

Type:

Desktop app
Download:

client_id
client_secret

5. Generate Gmail refresh token

Install:

npm install googleapis


Create auth.js:

import { google } from "googleapis";

const oAuth2Client = new google.auth.OAuth2(
  "CLIENT_ID",
  "CLIENT_SECRET",
  "http://localhost"
);

const url = oAuth2Client.generateAuthUrl({
  access_type: "offline",
  scope: [
    "https://www.googleapis.com/auth/gmail.readonly",
    "https://www.googleapis.com/auth/gmail.send"
  ],
});

console.log(url);


Run:

node auth.js


Login → copy code → paste → get:

refresh_token

6. Add Gmail to OpenClaw

Add to .env:

GMAIL_CLIENT_ID=xxxxx
GMAIL_CLIENT_SECRET=xxxxx
GMAIL_REFRESH_TOKEN=xxxxx


Restart:

docker compose restart

7. Telegram Commands

Example commands:

/inbox      → show latest emails
/send       → send email
/summary    → summarize inbox
/run        → execute system command

Security

Never commit:

.env
refresh_token
client_secret
telegram token


Add .env to .gitignore.

Deployment
AWS EC2
sudo apt update
sudo apt install docker docker-compose
git clone repo
cd repo
docker compose up -d


Open port if needed:

22 (SSH)


Telegram works without public port.

Troubleshooting
Pairing error

Run:

openclaw pairing approve telegram CODE

openclaw command not found

If Docker:

docker exec -it openclaw openclaw pairing approve telegram CODE

Gmail not working

Check:

OAuth enabled

refresh token valid

correct scopes

Use Cases

Personal AI assistant

Email automation

Internship/job auto-apply bots

DevOps control panel

Remote server management

SaaS automation backend

Future Improvements

Multi-user access

AI email summarization

Workflow builder

RAG memory

Notion/Drive integration

Web dashboard

License

MIT
