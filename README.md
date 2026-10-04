# 🥗 MacroSnap — AI Nutrition Buddy (with Gmail SMTP)

MacroSnap is a Streamlit AI chat application powered by **Google Gemini (Vision + Chat)** and **Gmail (SMTP)**.

A user enters their name and email address once during onboarding, then chats with their AI nutrition buddy by typing descriptions or attaching photos of their meals to receive instant calorie and macro breakdowns. When ready, clicking the **"📤 Send to Email"** button sends a full nutrition summary of the session directly to their inbox.

---

## 🌟 Key Features

- **Multimodal AI Vision & Chat**: Powered by Google Gemini (`gemini-2.5-flash`), allowing both text meal queries and uploaded meal photos (JPG/PNG).
- **Free Email Delivery via Gmail SMTP**: Uses Python's built-in `smtplib` and `email.mime.text`. No third-party accounts, paid tiers, or Twilio sandbox setup needed.
- **Session Memory**: Maintains a conversational chat history to handle follow-up nutrition queries.
- **One-Click Email Recap**: Summarizes all meals logged during the session with total calories and macros, sent directly to the recipient's email address.

---

## 📁 Project Structure

```text
macrosnap/
├── app.py                        # Streamlit application logic & UI
├── prompts.py                    # AI persona, system prompt & templates
├── requirements.txt              # Project dependencies
├── .gitignore                    # Prevents secrets & cache from entering git
├── .streamlit/
│   └── secrets.toml.example      # Template for secrets configuration
└── README.md                     # Documentation and setup guide
```

---

## 🛠️ Prerequisites & Setup

### 1. Requirements
- Python 3.9 or higher
- A free [Google AI Studio](https://aistudio.google.com/) account for a Gemini API key.
- A Gmail account with 2-Step Verification enabled.

### 2. Generate a Gmail App Password
1. Go to your [Google Account Security settings](https://myaccount.google.com/security) and ensure **2-Step Verification** is turned on.
2. Visit [Google App Passwords](https://myaccount.google.com/apppasswords).
3. Create a new App Password (e.g. name it `MacroSnap`).
4. Copy the generated 16-character App Password. *(Never use your primary account password).*

### 3. Installation
Clone this repository and navigate to the project directory:

```bash
# Clone the repository
git clone <your-repo-url>
cd <repo-folder>

# (Optional) Create and activate a virtual environment
python -m venv venv
# On Windows PowerShell:
.\venv\Scripts\Activate.ps1
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

---

## 🔑 Configuration (Secrets)

1. Create a `secrets.toml` file inside the `.streamlit/` folder:
   - On Windows PowerShell:
     ```powershell
     Copy-Item .streamlit/secrets.toml.example .streamlit/secrets.toml
     ```
   - On macOS/Linux:
     ```bash
     cp .streamlit/secrets.toml.example .streamlit/secrets.toml
     ```

2. Open `.streamlit/secrets.toml` and fill in your actual credentials:
   ```toml
   GEMINI_API_KEY = "AIzaSy..."
   GMAIL_ADDRESS = "your-email@gmail.com"
   GMAIL_APP_PASSWORD = "xxxx xxxx xxxx xxxx"
   GEMINI_MODEL = "gemini-2.5-flash"
   ```

> ⚠️ **Important**: `.streamlit/secrets.toml` is ignored by `.gitignore`. Never commit your real secrets to GitHub!

---

## 🚀 Running Locally

Launch the app with Streamlit:

```bash
streamlit run app.py
```

The application will open in your browser at `http://localhost:8501`.

1. Complete the onboarding screen with your name and email address.
2. Ask questions about your food or upload a picture of a meal.
3. Once you have logged at least one meal, click **"📤 Send to Email"** to receive the daily recap directly in your inbox.

---

## ☁️ Deployment (Streamlit Community Cloud)

1. Push your repository to GitHub (ensure `.streamlit/secrets.toml` is not pushed).
2. Visit [share.streamlit.io](https://share.streamlit.io) and connect your GitHub account.
3. Click **"New app"**, select your repository, branch, and specify `app.py` as the entrypoint.
4. Under **Advanced Settings → Secrets**, paste the contents of your local `secrets.toml`:
   ```toml
   GEMINI_API_KEY = "your-gemini-api-key"
   GMAIL_ADDRESS = "your-email@gmail.com"
   GMAIL_APP_PASSWORD = "your-16-char-app-password"
   GEMINI_MODEL = "gemini-2.5-flash"
   ```
5. Click **Deploy**! Your app is now live with a public URL.
