# ⟳ MicroReset AI — Smart Learning Break Generator

> Turn your study break into a memory boost — powered by AI.

MicroReset AI is an intelligent study break tool that generates personalized micro-activities based on what you just studied. Instead of scrolling social media, students get short, fun, concept-related activities — followed by a memory recall question and instant AI feedback.


## Features

- Personalized break activities based on subject, concept, energy level, and time
- Each activity shows a title, instruction, and purpose note
- AI-generated memory recall question after all activities
- Instant answer analysis — classified as Strong, Partial, or Incorrect
- Warm, encouraging feedback with a correct answer summary
- Clean dark-mode UI with smooth screen transitions
- No backend required — runs entirely in the browser

---

## Architecture

This project calls the Groq API directly from the browser. No servers, no n8n, no backend needed.

```
Student fills form
      ↓
Groq API (Key 1) — generates activities + recall question
      ↓
Student completes activities one by one
      ↓
Student answers recall question
      ↓
Groq API (Key 2) — analyses the student's answer
      ↓
Feedback displayed: classification + feedback + correct summary
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML, CSS, JavaScript (single file) |
| AI Model | Groq — `llama-3.3-70b-versatile` |
| AI API | Groq API (called directly from browser) |
| Fonts | Playfair Display + Nunito (Google Fonts) |
| Hosting | GitHub Pages |

---

## Project Structure

```
microreset-ai/
├── smart-break.html     # Complete app — frontend + AI logic (single file)
└── ReadMe.md            # This file
```

---

## Setup

### 1. Get your Groq API keys

1. Go to [console.groq.com](https://console.groq.com)
2. Sign up for a free account
3. Go to **API Keys → Create API Key**
4. Create two keys — one for activities, one for analysis

### 2. Add your keys to the HTML file

Open `smart-break.html` and find these two lines near the top of the `<script>` section:

```javascript
const GROQ_KEY_ACTIVITIES = 'YOUR_GROQ_API_KEY_1';  // Key for generating activities & question
const GROQ_KEY_ANALYZE    = 'YOUR_GROQ_API_KEY_2';  // Key for analysing answers
```

Replace `YOUR_GROQ_API_KEY_1` and `YOUR_GROQ_API_KEY_2` with your actual keys.

---

## Running Locally

**Option A — VS Code Live Server**

1. Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension
2. Right-click `smart-break.html`
3. Click **Open with Live Server**
4. App opens at `http://127.0.0.1:5500/smart-break.html`

**Option B — Python**

```bash
python -m http.server 8080
```

Then open `http://localhost:8080/smart-break.html`

> **Important:** The app must be served from a local server — not opened directly as a file (`file://...`). Opening as a file causes CORS errors when calling the Groq API.

---


## How the AI Prompts Work

### Prompt 1 — Generate Activities (Groq Key 1)

Sends the student's subject, concept, energy level, time, difficulty, and activity count to Groq. Returns a JSON object with an array of activities (each with title, instruction, and purpose) plus one recall question.

### Prompt 2 — Analyse Answer (Groq Key 2)

Sends the concept, recall question, and the student's answer to Groq. Returns a JSON object with a classification (Strong / Partial / Incorrect), warm encouraging feedback, and a one-sentence correct answer summary.

---

## Customisation

**Add more subjects**

Find `<select id="subject">` in the HTML and add more `<option>` tags.

**Change the AI model**

Find this line in the script section:

```javascript
const GROQ_MODEL = 'llama-3.3-70b-versatile';
```

Replace with any model available on your Groq account, such as `llama3-8b-8192` for faster responses.

**Change number of activities**

The pill buttons already support 1, 2, or 3 activities — selected by the student before generating.

---

## Created For

**Rysera STEM — AI Essentials: From Data to Agents**
Final Project — Smart Learning Break Generator

---

## Author

**Isuru Kodiarachchi**
[GitHub](https://github.com/isurukodiarachchi)
