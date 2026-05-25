# 🎵 AI Music Telegram Agent

An AI-powered music generation workflow built with:

* n8n
* Telegram Bot API
* DeepSeek AI
* Suno API

This workflow automatically:

1. Receives a music prompt from Telegram
2. Generates song lyrics with Suno
3. Uses AI to generate structured music metadata
4. Creates AI-generated music
5. Waits for generation completion
6. Downloads the MP3
7. Sends the final audio back to Telegram

---

# 🚀 Features

* Fully automated AI music generation
* Telegram integration
* DeepSeek-powered music analysis
* Async polling system
* Automatic MP3 delivery
* Structured JSON AI outputs
* Suno AI integration
* No backend required

---

# 🧠 Workflow Architecture

```text
Telegram Trigger
↓
Generate Lyrics
↓
Wait
↓
Check Lyrics Status
↓
AI Agent (DeepSeek)
↓
Generate Music
↓
Wait
↓
Check Music Status
↓
Download MP3
↓
Send Audio to Telegram
```

---

# 🛠 Technologies Used

| Tool             | Purpose                |
| ---------------- | ---------------------- |
| n8n              | Workflow automation    |
| Telegram Bot API | User interface         |
| DeepSeek         | AI metadata generation |
| Suno API         | Music generation       |
| HTTP Requests    | API communication      |

---

# 📦 Installation

## 1. Clone Repository

```bash
git clone https://github.com/YOUR_USERNAME/ai-music-telegram-agent.git
```

---

## 2. Import Workflow into n8n

* Open n8n
* Import the provided JSON workflow
* Configure credentials

---

## 3. Configure Telegram Bot

Create a Telegram bot using:

@BotFather

Then add the Telegram credentials inside n8n.

---

## 4. Configure Suno API

Add your Suno API key in the HTTP Request nodes.

---

## 5. Configure DeepSeek API

Add your DeepSeek credentials inside n8n AI nodes.

---

# 🔄 Async Polling System

The workflow uses:

* Wait nodes
* IF nodes
* Status polling

to handle asynchronous AI generation tasks.

---

# 📁 Project Structure

```text
/workflow
    ai-music-agent.json

/docs
    documentation.md

/assets
    screenshots/
```

---

# ⚠️ Important Notes

* This project uses an unofficial Suno API wrapper
* API limits may apply
* Some prompts may be blocked by Suno moderation

---

# 🔐 Security

Never expose:

* API keys
* Bearer tokens
* Telegram secrets

Use n8n Credentials whenever possible.

---

# 🎯 Future Improvements

* AI-generated cover art
* Memory system
* Multi-user queue
* Premium subscription system
* Database integration
* AI remix generation

---

# 📜 License

MIT License

---

# ❤️ Credits

Built with:

* n8n
* DeepSeek
* Suno API
* Telegram Bot API
