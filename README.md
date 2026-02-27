# Mood Companion WhatsApp Bot – Setup Guide

## Overview
A unique WhatsApp bot that detects user mood, responds empathetically, and offers jokes, motivational quotes, or activity suggestions. Powered by n8n, Mistral AI, and Twilio WhatsApp Sandbox, with free-tier data storage.

---

## 1. Twilio WhatsApp Sandbox Setup

1. Sign up at https://www.twilio.com/try-twilio
2. Go to [WhatsApp Sandbox](https://www.twilio.com/console/sms/whatsapp/sandbox)
3. Note your sandbox number and join code
4. Set the webhook URL to:
   ```
   https://<your-n8n-domain>/webhook/moodbot
   ```
   (If local, use [ngrok](https://ngrok.com/) to expose your n8n instance)

---

## 2. Mistral API Key

1. Register at https://console.mistral.ai/
2. Create an API key
3. Store it in n8n as an environment variable: `MISTRAL_API_KEY`

---

## 3. Data Storage (n8n Data Store)

- No setup needed for local demo. For production, consider Airtable or Google Sheets.

---

## 4. Deploy n8n

- Use [n8n.cloud](https://n8n.cloud/) (free tier) or self-host (Docker, Railway, Render, or local)
- For local, run:
  ```
  npx n8n
  ngrok http 5678
  ```
- Set Twilio webhook to your ngrok URL + `/webhook/moodbot`

---

## 5. Environment Variables

- `MISTRAL_API_KEY` – your Mistral API key
- `TWILIO_WHATSAPP_NUMBER` – your Twilio WhatsApp sandbox number (e.g., whatsapp:+14155238886)
- Twilio credentials (set up in n8n credentials UI)

---

## 6. Import the Workflow

1. In n8n, go to Workflows → Import
2. Upload `mood-companion-n8n-workflow.json`
3. Activate the workflow

---

## 7. Sample Conversation Flows

**User:** Hi!
**Bot:** 👋 Hello! I’m your Mood Companion. How are you feeling today?

**User:** I’m a bit down.
**Bot:** I’m here for you. Remember, tough times don’t last. Would you like a joke or a motivational quote? 😊

**User:** Tell me a joke.
**Bot:** Why don’t scientists trust atoms? Because they make up everything! 😄

**User:** Can you suggest something fun?
**Bot:** How about watching a comedy movie or listening to your favorite upbeat song? 🎬🎶

**User:** (in Spanish) Hola, estoy aburrido.
**Bot:** ¡Hola! ¿Te gustaría que te sugiera un juego rápido o una actividad divertida? 😃

---

## 8. Daily Motivational Messages (Optional)

- Add a new workflow in n8n:
  - Trigger: Cron (e.g., every day at 9 AM)
  - Get all users from Data Store with daily opt-in
  - For each, call Mistral with: "Generate a short motivational quote or uplifting message for a good morning."
  - Send via Twilio WhatsApp

---

## 9. Notes & Tips

- All services used have free tiers suitable for demos.
- The workflow is well-commented for easy modification.
- Handles errors gracefully (fallback message if Mistral fails).
- For production, use Airtable or Google Sheets for persistent storage.

---

## 10. Troubleshooting

- If you get no reply, check Twilio logs and n8n execution logs.
- Ensure all environment variables and credentials are set.
- For local testing, ensure ngrok is running and webhook is updated in Twilio.

---

Enjoy your Mood Companion bot!