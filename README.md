# PhishDetector 🛡️ (Chrome Extension)

PhishDetector is a lightweight **Chrome extension (Manifest V3)** that analyzes email text and returns a **phishing probability score** with a short explanation.  
Built as an **Information Security course team project** to explore how LLMs can help users spot suspicious emails faster.

---

## ✨ Features
- **Phishing probability score** (e.g., Low / Medium / High)
- **Explanation of signals** (urgent tone, credential requests, suspicious links, impersonation cues, etc.)
- Simple UI (popup) for quick copy/paste analysis
- Uses OpenAI API via a small helper module (`gpt.js`)

---

## 📁 Project Structure
```txt
PhishDetector/
├─ images/            # Extension icons / UI assets
├─ index.html         # Popup UI
├─ style.css          # Popup styling
├─ content.js         # Content script (if used for page/email extraction)
├─ gpt.js             # OpenAI request + scoring logic
├─ config.js          # Configuration (API key / model / prompt settings)
└─ manifest.json      # Chrome extension manifest (MV3)
```

---

## 🚀 Getting Started (Local)

### 1) Download / Clone
```bash
git clone <YOUR_REPO_URL>
cd PhishDetector
```

### 2) Add Your OpenAI API Key (IMPORTANT)
This project uses `config.js` for configuration.

Open `config.js` and set your API key (example):
```js
export const OPENAI_API_KEY = "YOUR_KEY_HERE";
```

✅ **Recommended (safer) approach**  
Instead of hardcoding, you can:
- keep `config.js` as a local-only file, and
- add it to `.gitignore` so it never gets committed.

Create a `.gitignore` file (if you don’t have one):
```gitignore
config.js
```

> If you already committed your API key once, rotate it immediately in your OpenAI dashboard.

### 3) Load the Extension in Chrome
1. Go to: `chrome://extensions`
2. Enable **Developer mode** (top right)
3. Click **Load unpacked**
4. Select the `PhishDetector` project folder

---

## ✅ How To Use
1. Open an email in your email client
2. Copy the email body text (and suspicious links if possible)
3. Click the PhishDetector extension icon
4. Paste the text into the popup
5. Click **Analyze**
6. Review the **phishing score** + explanation

---

## 🧠 How It Works
1. User provides email text through the popup UI (`index.html`).
2. The extension sends the text to OpenAI (via `gpt.js`).
3. The model returns a structured response (score + reasoning).
4. The UI displays the result.

---

## ⚠️ Limitations / Notes
- **API key exposure risk**: calling OpenAI directly from a Chrome extension means the key can be extracted by a determined attacker.
- Cannot reliably analyze text inside **embedded images** (e.g., screenshots of invoices) without OCR.
- Results are probabilistic: the score is an assistive signal, not a guarantee.

---

## 🔒 Security Recommendations (If You Continue This Project)
- Move OpenAI calls to a **backend proxy** (server/API route) so the extension never stores a secret key.
- Add **URL extraction** and basic checks (punycode, mismatched domains, shortened URLs).
- Optionally add OCR for images (with user permission).

---

## 🛣️ Roadmap
- [ ] Backend proxy for API calls (remove API key from client)
- [ ] URL detection + warning highlights
- [ ] Better structured output (strict JSON parsing + UI formatting)
- [ ] Optional OCR support for screenshot-based phishing

---

## 👥 Team
- Kisang Hwang  
- Jordan Fung
- Quang Le

---
