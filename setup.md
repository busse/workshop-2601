---
layout: default
title: Setup Instructions
---

# Pre-Workshop Setup

<p class="page-meta">Complete these steps before arriving. Total time: about 5 minutes.</p>

### 1. Install Claude Code

Follow the instructions at [code.claude.com](https://code.claude.com). Verify it's working by opening a terminal and running:

```
claude --version
```

### 2. Clone the workshop repo

```
git clone https://github.com/busse/mini-crm.git
cd mini-crm
```

### 3. Install Python dependencies

Python 3.10+ is required. Check your version first:

```bash
python3 --version   # must be 3.10 or newer
```

**macOS / Linux:**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -e ".[dev]"
```

**Windows (PowerShell):**
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -e ".[dev]"
```

### 4. Seed the database

**macOS / Linux:** `python3 scripts/seed.py`

**Windows:** `python scripts/seed.py`

### 5. Verify everything works

```
pytest
uvicorn app.main:app
```

Visit [http://localhost:8000](http://localhost:8000) — you should see the app running. Press Ctrl+C to stop the server.

---

### Troubleshooting

**Wrong Python version?** Run `python3 --version`. You need 3.10 or newer.

- **macOS (Homebrew):** `brew install python@3.12` then use `python3.12 -m venv .venv`
- **Ubuntu / Debian:** `sudo apt install python3.12 python3.12-venv`
- **pyenv:** `pyenv install 3.12 && pyenv local 3.12`
- **Windows:** Download from [python.org/downloads](https://www.python.org/downloads/)

**`pip install` fails with "requires-python"?** Your Python is too old — see above.

**`ModuleNotFoundError: No module named 'venv'`?** On Ubuntu/Debian: `sudo apt install python3.X-venv` (replace `3.X` with your version).

---

If you run into other issues, don't worry — we'll have a few minutes at the start of the workshop to troubleshoot.

Questions? Contact [cbusse@singlestoneconsulting.com](mailto:cbusse@singlestoneconsulting.com)
