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

Python 3.11+ is required.

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

If you run into issues, don't worry — we'll have a few minutes at the start of the workshop to troubleshoot.

Questions? Contact [cbusse@singlestoneconsulting.com](mailto:cbusse@singlestoneconsulting.com)
