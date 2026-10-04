# 📚 Snap & Study — AI Study Buddy (with Gmail SMTP)

**Snap & Study** is an AI-powered study companion built with **Streamlit**, **Google Gemini (Vision + Chat)**, and **Gmail (SMTP)**.

A student enters their name and email address once during onboarding, then chats with their AI study buddy by asking academic questions or uploading photos of homework problems, diagrams, or handwritten notes. Gemini explains concepts step-by-step in clear, plain language. When finished, clicking **"📤 Send to Email"** automatically compiles a structured study recap and emails it directly to the student's inbox.

---

## 🌟 Key Features

- **Multimodal Concept Explanations**: Powered by Google Gemini (`gemini-2.5-flash`), accepting both text questions and photos of textbook pages, math/science problems, and diagrams.
- **100% Free Email Delivery via Gmail SMTP**: Uses Python's built-in `smtplib` and `email.mime.text`. No third-party accounts, paid tiers, or Twilio sandbox setup needed.
- **Continuous Study Session Memory**: Maintains full conversation context to handle follow-up doubts like *"Can you give me another example?"* or *"What formula did you use in step 2?"*.
- **One-Click Study Guide Email**: Rereads the entire session's exchanges and delivers an organized study recap with key formulas, explanations, and bullet-point takeaways.

---

## 📁 Project Structure

```text
ai project/
├── app.py                        # Streamlit app logic, onboarding, chat & Gmail SMTP delivery
├── prompts.py                    # AI study buddy persona, system prompt & email recap prompt
├── requirements.txt              # Dependencies (streamlit, google-genai, pillow)
├── .gitignore                    # Ensures .streamlit/secrets.toml & cache are not committed
├── .streamlit/
│   └── secrets.toml.example      # Template for your API keys and Gmail App Password
└── README.md                     # Documentation, setup & deployment instructions
```

---

## 🛠️ Prerequisites & Setup

### 1. Requirements
- Python 3.9 or higher
- A free [Google AI Studio](https://aistudio.google.com/) account for a Gemini API key.
- A Gmail account with 2-Step Verification enabled.

### 2. Generate a Gmail App Password
1. Go to your [Google Account Security Settings](https://myaccount.google.com/security) and ensure **2-Step Verification** is turned on.
2. Visit [Google App Passwords](https://myaccount.google.com/apppasswords).
3. Create a new App Password (e.g., name it `SnapAndStudy`).
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
python -m streamlit run app.py
```

The application will open in your browser at `http://localhost:8501`.

1. Complete the onboarding screen with your name and email address.
2. Ask any study question or upload an image of a problem/diagram.
3. Once you've discussed at least one topic, click **"📤 Send to Email"** to receive the study notes in your inbox.

---

## ☁️ Deployment (Streamlit Community Cloud)

1. Push your repository to GitHub (ensure `.streamlit/secrets.toml` is not committed).
2. Visit [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
3. Click **"New app"**, select your repository, branch, and specify `app.py` as the entrypoint.
4. Under **Advanced Settings → Secrets**, paste the contents of your local `secrets.toml`:
   ```toml
   GEMINI_API_KEY = "your-gemini-api-key"
   GMAIL_ADDRESS = "your-email@gmail.com"
   GMAIL_APP_PASSWORD = "your-16-char-app-password"
   GEMINI_MODEL = "gemini-2.5-flash"
   ```
5. Click **Deploy**! Your app is now live with a public URL.
