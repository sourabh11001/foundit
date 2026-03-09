# foundit[README.md](https://github.com/user-attachments/files/25835181/README.md)
# 🚀 AI Career Copilot — Autonomous Job Hunter

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![React](https://img.shields.io/badge/Frontend-React%20%2B%20Vite-61DAFB?logo=react&logoColor=black)
![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688?logo=fastapi&logoColor=white)
![AI Models](https://img.shields.io/badge/Powered%20By-Google%20Gemini-4285F4?logo=google&logoColor=white)

AI Career Copilot is a production-grade, intelligent job-hunting platform designed to automate the painful parts of applying for roles. By leveraging advanced generative AI, it parses unstructured resumes, deeply analyzes complex job descriptions, scores your eligibility, and generates highly targeted application material in seconds.

## ✨ Features

- **pdfplumber Extraction:** Accurately extracts text from uploaded PDF resumes.
- **Intelligent Parsing:** Uses *Gemini 2.5 Flash* to instantly clean and structure chaotic resume and job description text into strict, deterministic JSON schemas.
- **AI Matching Engine:** Uses *Gemini 3.0 Flash Preview* to reasoning over your capabilities against the job requirements, assigning a realistic 0-100 eligibility score and highlighting critical missing skills.
- **Auto Application Generator:** Instantly write tailored cover letters and professional HR emails based on *your specific matched skills*.
- **Premium Dashboard:** A modern, minimal, dark-mode SaaS interface built with React and custom glassmorphism utilities. 
- **Graceful Degradation:** The UI falls back to interactive mock data if the backend is down, allowing you to showcase the frontend design anywhere, anytime.

---

## 🏗️ Architecture Stack

- **Frontend:** React 18, Vite, React Router DOM, Lucide Icons, Pure CSS (Glassmorphism design).
- **Backend:** Python 3, FastAPI, Uvicorn.
- **Data Validation:** Pydantic (Enforcing strict JSON structures from the LLM).
- **AI Integration:** Official `google-genai` Python SDK.

---

## 🚀 Getting Started

To run the application locally, you will need two separate terminal windows for the frontend and backend.

### Prerequisites
- Python 3.9+
- Node.js 18+
- A Google Gemini API Key

### 1. Start the Backend API

```bash
cd backend

# Create and activate a virtual environment (Linux/macOS)
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install fastapi uvicorn pydantic pdfplumber google-genai python-multipart python-dotenv

# Set up your environment variables
cp .env.example .env
# Edit the .env file and add your GEMINI_API_KEY
```

Run the server:
```bash
uvicorn main:app --reload
# The API will be available at http://localhost:8000
```

### 2. Start the Frontend Application

```bash
cd frontend

# Install dependencies
npm install

# Start the development server
npm run dev
# The UI will be available at http://localhost:5173
```

---

## 🛠️ Upgrades & Customization (Making it Yours)

This project is built with a highly decoupled and modular architecture. You can easily swap components to fit your specific needs or turn it into a heavily monetized SaaS product.

### 1. Supercharging the AI Models
By default, the backend uses `gemini-2.5-flash` for fast parsing and `gemini-3.0-flash` for reasoning to keep costs low and speed high.

**To upgrade to heavier models, modify `backend/services/ai_engine.py`:**
- **For ultimate reasoning:** Swap `gemini-3.0-flash` with `gemini-1.5-pro` (or the latest Pro variant) if you are matching against senior/executive roles where nuanced reading is critical.
- **Using other providers:** Because the logic relies on standard Pydantic schemas, you can easily rip out `google-genai` and insert `openai` (GPT-4o) or `anthropic` (Claude 3.5 Sonnet) using the `Instructor` library to maintain the exact same strict JSON output formatting.

### 2. Adding Persistent Storage & Auth
Right now, the application is stateless (perfect for resumes and quick demos). To build a permanent user base:
- **Database:** Connect a PostgreSQL database using `SQLAlchemy`. Store user histories so the Dashboard shows historical matching trends over time.
- **Authentication:** Add `Clerk` or `Supabase Auth` to the frontend and validate JWT tokens on the FastAPI backend routes.

### 3. Automated Chrome Extensions
Integrate a Chrome Extension that scrapes the currently viewed LinkedIn or Indeed job posting and sends the text directly to `http://localhost:8000/api/match-job`, bypassing the need to copy and paste entirely.
