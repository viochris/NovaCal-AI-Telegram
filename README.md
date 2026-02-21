# 📅 NovaCal AI: Intelligent Google Calendar Assistant (Telegram Bot Edition)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram-Bot-2CA5E0?logo=telegram&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-Agent-blueviolet?logo=langchain&logoColor=white)
![Google Gemini](https://img.shields.io/badge/Gemini%202.5%20Flash-8E75B2?logo=google&logoColor=white)
![Google Calendar](https://img.shields.io/badge/Google%20Calendar-API-4285F4?logo=googlecalendar&logoColor=white)
![Status](https://img.shields.io/badge/Status-Active-success)

## 📌 Overview
**NovaCal AI** is a streamlined, highly capable Virtual Assistant built for seamless Google Calendar management directly from Telegram.

Powered by a **LangChain Tool-Calling Agent** and **Google Gemini 2.5 Flash**, this bot operates on a **Zero-Memory (Stateless)** architecture. It is designed for maximum token efficiency, minimal hallucinations, and lightning-fast single-turn command execution. It features custom-built scheduling tools (The Sniper & The Fetcher) to securely Create, Read, Update, and Delete (CRUD) your calendar events.

> **🌐 EXPLORE OTHER VERSIONS OF NOVACAL AI:**
> * **[Streamlit Dashboard Edition](https://github.com/viochris/NovaCal-AI-Streamlit.git):** If you are looking for the Visual Web UI version of NovaCal AI.
> * **[Stateful Telegram Edition (With Memory)](https://github.com/viochris/telegram-calendar-ai-bot.git):** If you are looking for the conversational, SQL-backed memory version capable of multi-turn interactions.

## ⚠️ IMPORTANT: Why This Bot Is Locked To A Single User?
> This bot is authenticated using your personal Google Calendar credentials. If it were open to the public, anyone on Telegram could read your private schedules, add fake events, or delete your important meetings!
>
> To prevent this massive security risk, the bot is strictly locked to YOU (the developer). By matching the user's ID with the 'TELEGRAM_DEVELOPER_CHAT_ID' stored in your environment variables, the system ensures that only your specific Telegram account can give commands or read your Google Calendar. 
>
> If any stranger attempts to chat with the bot, it will instantly block them and send an intrusion alert directly to your DM.

## ✨ Key Features

### 🧠 Tool-Calling Agent Architecture
Using `create_tool_calling_agent`, the system navigates a strict Standard Operating Procedure (SOP):
1.  **Analyze Intent:** Understands complex time-based requests relative to the current system time.
2.  **Execute Tools:** Uses custom-built, highly optimized tools like `get_id_of_schedules` (The Sniper) and `get_all_schedules` to reliably fetch data.
3.  **Self-Correction (Swap Method):** If an event update fails, the Agent seamlessly falls back to creating a new event and deleting the old one.

### ⚡ Zero-Memory Engine (Stateless)
Designed for maximum token efficiency and zero hallucinations. NovaCal processes each command independently without persistent memory, ensuring lightning-fast execution for single-turn CRUD operations.

### 🛡️ Private Security Bouncer
The bot is hard-locked to a specific `TELEGRAM_DEVELOPER_CHAT_ID`. Any unauthorized attempts to interact with the bot are immediately blocked, logged, and silently reported to the developer's DM.

### ☁️ Cloud Deployment Ready (Railway)
Features a dynamic credential generator that automatically builds physical `credentials.json` and `token.json` files on the server directly from cloud environment variables upon startup, bypassing the need to upload sensitive files.

## 🛠️ Tech Stack
* **LLM:** Google Gemini 2.5 Flash (via `ChatGoogleGenerativeAI`).
* **Bot Framework:** `python-telegram-bot`
* **Orchestration:** LangChain (Tool-Calling Agent).
* **Calendar Integration:** Google Calendar API (`google-api-python-client` & `CalendarToolkit`).

## ⚠️ Limitations & Disclaimers
### 1. One-Shot Command Rule
Because the bot is stateless, all necessary parameters (Title, Date, Start Time, End Time) must be provided in a single message.
### 2. Timezone Hardcoding
The time boundary extraction in the custom fetcher tools currently uses a fixed `+07:00` (WIB/Jakarta) timezone offset for daily queries.
### 3. Native Tool Bypassing
Native LangChain search tools (`CalendarSearchEvents`) are intentionally disabled/banned in the system prompt due to instability, replaced entirely by custom-built extraction functions for maximum reliability.

## 📦 Installation & Deployment

1.  **Clone the Repository**
    ```bash
    git clone https://github.com/viochris/NovaCal-AI-Telegram.git
    cd NovaCal-AI-Telegram
    ```

2.  **Install Dependencies**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Local Environment Setup (`.env`)**
    Create a `.env` file for local testing:
    ```env
    TELEGRAM_TOKEN_Nova_cal=your_telegram_bot_token
    TELEGRAM_CHAT_ID=your_personal_telegram_id
    GOOGLE_API_KEY=your_gemini_api_key
    ```

4.  **Cloud Deployment (Railway)**
    Instead of uploading JSON files, add these to your Railway Variables:
    * `GOOGLE_CALENDAR_CREDENTIALS`: Paste the raw JSON content of your `credentials.json`.
    * `GOOGLE_CALENDAR_TOKEN`: Paste the raw JSON content of your `token.json`.

5.  **Run Locally**
    ```bash
    python NovaCal-AI-Telegram.py
    ```

### 🖥️ Expected Terminal Output
You will see the bot initialize the LangChain Agent and start polling in real-time:

```text
2026-02-20 09:19:26,123 - root - INFO - 🚀 NovaCal AI Telegram Bot is currently online and listening...
2026-02-20 09:25:10,001 - httpx - INFO - HTTP Request: POST https://api.telegram.org/bot1234...:98.../getUpdates "HTTP/1.1 200 OK"
2026-02-20 09:30:45,432 - root - WARNING - 🚨 INTRUSION ATTEMPT: Unauthorized access blocked from User ID: 9876...
```

### 🚀 Cloud Deployment
This script is designed to be **Always On** via continuous polling. It is best deployed on:
* **Railway (PaaS) — 🌟 WE USE THIS:** Highly recommended for seamless GitHub integration and continuous deployment.
* **Docker Container** (using the provided Dockerfile).
* **VPS** (Virtual Private Server) like DigitalOcean or AWS EC2.
* **Hugging Face Spaces** (as a Docker Space).

**Strict Instructions for Railway Deployment:**
Do **NOT** upload your physical `credentials.json` or `token.json` files to the cloud. The script features a Dynamic Credential Generator. Instead, add these directly into your Railway Variables:

* `GOOGLE_CALENDAR_CREDENTIALS`: Paste the raw JSON content of your `credentials.json`.
* `GOOGLE_CALENDAR_TOKEN`: Paste the raw JSON content of your `token.json`.
* `TELEGRAM_TOKEN_Nova_cal`: Your bot token.
* `TELEGRAM_CHAT_ID`: Your exact developer chat ID.
* `GOOGLE_API_KEY`: Your Gemini API Key.

## 🚀 Usage Guide
Once the bot is running, start a chat on Telegram:
* `/start` - Initializes the bot and shows the welcome guidelines.
* `/info` - Displays technical specifications and architecture details.
* `/howtouse` - Provides the full CRUD operation cheat sheet.
* **Natural Chat:** Talk directly to perform actions (e.g., *"Book a Team Sync tomorrow from 2 PM to 3:30 PM"* or *"Cancel my meeting today"*).

---
**Author:** Silvio Christian, Joe
*"Automate your schedule. Experience intelligent time management."*
