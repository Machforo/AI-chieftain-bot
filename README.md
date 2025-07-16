# 🛎️ AI Chieftain – Hotel Concierge Bot

**AI Chieftain** is an AI-powered multi-modal concierge bot designed for hotels, offering seamless guest interaction across **Web**, **Voice**, **QR**, and **WhatsApp** channels. It integrates **LLMs**, **LangChain**, **Twilio**, and **Streamlit**, and logs every interaction in a centralized system with an **Admin Dashboard** for insights.

---

## Demo Video
**Drive Link**

## 🚀 Features

-  Web chat interface (Streamlit)
-  LLM via Groq (LLaMA3) with LangChain
-  Voice recognition and response
-  WhatsApp chatbot using Twilio
-  QR code for mobile access to web bot
-  Logging for all channels (web, voice, WhatsApp)
-  Admin dashboard with analytics
-  Optional intent classification using Rasa

---

## 📁 Project Structure

```
AI_CHIEFTAIN_BOT_ATHARVKUMAR/
├── app/
│   ├── __pycache__/                    # Cached bytecode files
│   ├── agents/
│   │   ├── __pycache__/
│   │   └── qa_agent.py                 # Core LLM logic for answering queries
│   ├── assets/
│   │   └── logo.jpg                    # Logo used in the UI
│   ├── interfaces/
│   │   ├── __pycache__/
│   │   ├── cli_interface.py           # CLI version of the bot
│   │   └── web_ui.py                  # Streamlit web interface
│   ├── logs/
│   │   └── chat_logs.csv              # Centralized chat logs
│   ├── services/
│   │   ├── __pycache__/
│   │   ├── intent_classifier.py       # Basic intent classification (Rasa optional)
│   │   ├── logger.py                  # Logging utilities
│   │   ├── nlu.yml                    # NLU training data (used by Rasa or stub)
│   │   ├── vector_store.py            # Vector DB (e.g., FAISS) and embeddings
│   │   └── config.py                  # Configurations and constants
├── data/
│   └── hotel_faq.csv                  # FAQ dataset used for context retrieval
├── logs/
│   └── bot.log                        # System and error logs
├── .env                               # API keys and environment variables
├── dashboard.py                       # Admin dashboard with analytics
├── main.py                            # CLI entry point
├── mic_test.py                        # Mic/audio debugging script
├── README.md                          # Documentation
├── requirements.txt                   # Python dependencies
├── test_audio.wav                     # Audio test file
└── twilio_webhook.py                  # WhatsApp + Twilio integration
```



---

## 🧩 Tech Stack

| Area               | Tool/Library                                |
|--------------------|---------------------------------------------|
| LLM Engine         | Groq (LLaMA 3) via LangChain                 |
| Vector DB          | FAISS                                       |
| Embeddings         | HuggingFace Transformers                    |
| Web UI             | Streamlit                                   |
| Voice              | speech_recognition + PyAudio + gTTS         |
| QR Code            | qrcode + Pillow                             |
| Messaging          | Twilio + WhatsApp Sandbox                   |
| Analytics          | Streamlit Charts                            |
| Intent Classifier  | Rasa NLU (optional)                         |

---

## ⚙️ Setup Instructions

### 🔐 1. Environment Setup

```bash
git clone https://github.com/Machforo/AI_Chieftain_Bot.git
cd AI_Chieftain_Bot
python -m venv venv
venv\Scripts\activate  # or source venv/bin/activate on Mac/Linux
pip install -r requirements.txt
```

### .env file
```ini
GROQ_API_KEY=your_groq_key
TWILIO_ACCOUNT_SID=your_sid
TWILIO_AUTH_TOKEN=your_token
TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886
```

### Web Interface (QR + Voice Suuported)
```bash
streamlit run app/interfaces/web_ui.py
```

-Scan the generated qr_code.png to open on mobile.
-Mic icon allows speaking instead of typing.
-Logs stored under app/logs/.

### CLI Interface
```bash
python main.py
```
-Use for simple debugging or text-only interaction.
-Automatically logs session to app/logs/.

### Whatsapp Bot via Twilio

#### Step 1: Start Flask server
```bash
python twilio_webhook.py
```

#### Step 2: Expose to Internet
```bash
npx localtunnel --port 5002
```

or

```bash
ngrok http 5002
```
#### Step 3: Set Webhook in Twilio Sandbox

Paste the public URL (e.g., https://xyz.ngrok.io) into the sandbox settings under **"WHEN A MESSAGE COMES IN"** or in the **POST** link box.

## 📁 Logging
Each session creates a log file in app/logs/ as:

```pgsql
session_<timestamp>.json
```

Example log structure:

```json
{
  "channel": "web" | "voice" | "whatsapp",
  "session_id": "abc123",
  "interactions": [
    {
      "timestamp": "2025-07-14T14:32:21Z",
      "user": "Where is the pool?",
      "bot": "The pool is on the 3rd floor, open from 7 AM to 10 PM."
    }
  ]
}
```


## 📊 Admin Dashboard
```bash
streamlit run app/interfaces/admin_dashboard.py
```

### Analytics includes:
- Session counts per channel
- Common intents (if classifier used)
- Timeline of usage
- Export logs (CSV/Excel)


## Rasa Intent Classifier
```bash
rasa train nlu
python app/rasa/intent_classifier.py
```
- Used for intent classification like the following:

```yaml
version: "2.0"
nlu:
- intent: greet
  examples: |
    - hello
    - hi
    - good morning
- intent: goodbye
  examples: |
    - bye
    - see you later
```

## 🎯 Future Work
- Multilingual support (via Hugging Face models)
- Hotel booking integration (via API)
- Concierge scheduling/reservation support
- Docker packaging for cross-platform deployment
- Enhanced analytics: session duration, device info
- Multi-agent support (concierge, booking, manager, etc.)

## 🙋‍♂️ Author

**Atharv Kumar**
📧 atharvkumar43@gmail.com
🔗 https://www.linkedin.com/in/atharv-kumar-270337222/
💻 https://github.com/Machforo

## Acknoewledgements

- LangChain
- Groq Cloud
- Twilio WhatsApp API
- Hugging Face
- Streamlit

