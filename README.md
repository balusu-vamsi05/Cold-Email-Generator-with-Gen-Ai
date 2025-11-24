# Cold Email Generator with Gen-AI

[![License: MIT](https://img.shields.io/badge/License-MIT-green)](#)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](#)
[![Build Status](https://img.shields.io/badge/CI-pending-lightgrey)](#)

---

## 🚀 Project Overview

**Cold Email Generator with Gen-AI** is a simple, configurable tool that generates tailored cold email drafts using generative AI. It's designed for salespeople, founders, and recruiters who want to quickly produce personalization-driven outreach without starting from scratch.

Key goals:

* Produce short, high-conversion cold email drafts based on a small set of inputs.
* Keep prompts and business logic transparent and easy to modify.
* Provide an offline-first CLI + optional web demo (if you add UI later).

---

## ✨ Features

* Template-driven prompt system for consistent email tone and structure.
* Input fields for prospect data: name, role, company, pain point, and call-to-action.
* Support for multiple AI backends (placeholder hooks for OpenAI / Azure / local LLMs).
* Example dataset and simple CLI to generate emails.
* Configurable temperature/creativity and output length options.

---

## 🔧 Quick Preview

```bash
# Example usage (after setup)
python generate_email.py --name "Asha" --role "CTO" --company "Acme" --pain "slow ML deployment" --tone "friendly"
```

This prints 2–3 candidate emails to stdout and saves them to `output/` with timestamped filenames.

---

## 📦 Prerequisites

* Python 3.8 or newer
* pip
* (Optional) Virtual environment recommended

---

## 🛠️ Installation

```bash
# clone
git clone https://github.com/balusu-vamsi05/Cold-Email-Generator-with-Gen-Ai.git
cd Cold-Email-Generator-with-Gen-Ai

# create venv (recommended)
python -m venv venv
source venv/bin/activate  # macOS/Linux
venv\Scripts\activate     # Windows

# install dependencies
pip install -r requirements.txt
```

If you want reproducible builds, consider using `pip-tools` or `poetry` and check in a `requirements.txt` or `poetry.lock` file.

---

## ⚙️ Configuration

Copy `.env.example` to `.env` and update the values (API keys, model selection, default temperature, etc.). Example entries:

```
OPENAI_API_KEY=sk-...
DEFAULT_MODEL=gpt-4o-mini
DEFAULT_TEMPERATURE=0.6
OUTPUT_DIR=output
```

**Important:** Never commit `.env` or secret keys to git. Add them to `.gitignore`.

---

## 🧭 How it works (architecture)

1. CLI or script collects prospect inputs (CSV or manual flags).
2. A templating layer converts inputs into a structured prompt.
3. The AI backend is called to generate one or more email drafts.
4. Output is formatted, deduplicated, and saved to `output/`.

Directory snapshot:

```
├─ data/                 # example CSVs & test inputs
├─ prompts/              # prompt templates and variants
├─ src/                  # core python code (generate_email.py, ai_client.py)
├─ output/               # generated emails
├─ tests/                # unit tests
├─ .env.example
├─ requirements.txt
└─ README.md
```

---

## 📈 Usage examples

### 1) Generate from CLI flags

```bash
python src/generate_email.py \
  --name "Ramesh" \
  --role "Head of Product" \
  --company "BlueFin" \
  --pain "slow user onboarding" \
  --tone professional
```

### 2) Batch generate from CSV

Place a CSV `data/prospects.csv` with columns `name,role,company,pain,tone` and run:

```bash
python src/batch_generate.py --csv data/prospects.csv
```

---

## ✅ Testing

Add unit tests under `tests/` and run:

```bash
pytest -q
```

Aim to test: prompt rendering, basic output shape, and safe handling of missing fields.

---

## 🧪 Examples & Demo

Include a short GIF or screenshot of the CLI output or web demo (if added). Place images under `docs/screenshots` and reference them in the README.

---

## ♻️ Safety & Privacy

* Sanitize and review generated content before sending — AI can hallucinate facts (company names, metrics, etc.).
* Do not store or share sensitive personal data without consent.

---

## 🛡️ License

This project is released under the **MIT License**. See `LICENSE` for details.

---

## 🤝 Contributing

Please open issues or PRs. Add a `CONTRIBUTING.md` to describe your preferred workflow (branch names, tests required, code linters, formatting with `black`).

---

## 📬 Contact

Created by **Vamsi** — open an issue or reach out via your GitHub profile for questions.

---

## 🔜 Roadmap & Ideas

* Web UI with React + Tailwind to preview many variations.
* Multi-language support for localized outreach.
* A/B testing harness to track open & reply rates.
* Integration with Gmail API / SMTP for controlled sending (careful with rate limits & anti-spam rules).
