# 📄 ATS Resume Checker

A Streamlit app that analyzes a resume and returns an **estimated ATS score**, a score breakdown, missing keywords, prioritized improvements, and rewritten bullet points. Powered by **Google Gemini Flash**.

> ⚠️ The score is an AI-based estimate, not the output of a real ATS. Use it as guidance.

## Features
- Upload **PDF, DOCX or TXT** resumes
- Optional **job description** for keyword matching
- Overall ATS score (0-100) calculated from weighted categories:
  Keywords & Skills (30%), Experience & Impact (25%), Formatting (20%), Readability (10%), Contact Info (10%), Education (5%)
- Strengths, weaknesses, missing keywords
- Prioritized (High / Medium / Low) improvement suggestions
- Before / after bullet-point rewrites

## Project structure
```
ats-resume-checker/
├── app.py
├── requirements.txt
└── README.md
```

## Run locally
1. Install Python 3.10+.
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Get a free API key from [Google AI Studio](https://aistudio.google.com/apikey).
4. Provide the key in **one** of these ways:
   - Paste it into the app's sidebar, **or**
   - Set an environment variable:
     - Mac/Linux: `export GEMINI_API_KEY="your_key"`
     - Windows (PowerShell): `$env:GEMINI_API_KEY="your_key"`
   - Or create `.streamlit/secrets.toml`:
     ```toml
     GEMINI_API_KEY = "your_key"
     ```
5. Start the app:
   ```bash
   streamlit run app.py
   ```

## Deploy on Streamlit Community Cloud
1. Push this project to a **GitHub repository** (see steps below).
2. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
3. Click **Create app** → **Deploy a public app from GitHub**.
4. Choose your repository, branch `main`, and main file path `app.py`.
5. Open **Advanced settings → Secrets** and add:
   ```toml
   GEMINI_API_KEY = "your_key"
   ```
6. Click **Deploy**. Your app gets a public `*.streamlit.app` URL.

## Push to GitHub using the web UI
1. Log in at [github.com](https://github.com) → click **+** (top right) → **New repository**.
2. Name it (e.g. `ats-resume-checker`), choose **Public**, and click **Create repository**.
3. On the empty repo page, click **uploading an existing file**.
4. Drag and drop `app.py`, `requirements.txt` and `README.md`.
5. Write a commit message (e.g. "Initial commit") and click **Commit changes**.

**Never upload your API key or `secrets.toml` to GitHub.** If you use a local `.streamlit/secrets.toml`, keep it out of the repo.

## Configuration notes
- Models are listed in `MODEL_OPTIONS` at the top of `app.py`. Google retires and renames models over time; if you see a "model not found" error, update that list using the current names in the [Gemini docs](https://ai.google.dev/gemini-api/docs/models).
- Scanned/image-only PDFs can't be read (ATS systems can't read them either). Use a text-based PDF or DOCX.
- Resume text is sent to the Gemini API for analysis. Don't use this with documents you aren't comfortable sharing, and review Google's data policy for your API tier.

## Troubleshooting
| Problem | Fix |
|---|---|
| "API key looks invalid" | Re-copy the key from AI Studio; no spaces or quotes |
| "Rate limit or quota reached" | Wait a minute, or switch to `gemini-2.5-flash-lite` |
| "Very little text extracted" | Your PDF is likely an image; export a text-based PDF |
| Deploy fails on Streamlit Cloud | Check `requirements.txt` is in the repo root |# AI-resume-analyzer
