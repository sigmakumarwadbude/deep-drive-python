# Feature: Python Setup with uv

## Branch Name

```bash
feature/python-setup-uv
```

## Objective

Migrate from the traditional Python environment management approach (`venv + pip`) to the modern **uv** workflow.

This setup provides:

* Faster package installation
* Dependency locking
* Reproducible environments
* Jupyter Notebook integration
* VS Code kernel support
* Modern Python project structure

---

# Migration Overview

## Day 1 (Traditional)

```bash
python -m venv myenv
myenv\Scripts\activate
pip install -r requirements.txt
```

## Day 2 (Modern)

```bash
uv init --bare
uv venv
uv add -r requirements.txt
uv sync
```

---

# Step 1: Remove Existing Virtual Environment

Deactivate environment if active:

```bash
deactivate
```

Remove old virtual environment:

### Windows

```cmd
rmdir /s /q myenv
```

Verify:

```cmd
dir
```

Ensure:

```text
myenv
```

is no longer present.

---

# Step 2: Install uv

Open PowerShell and run:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Verify installation:

```bash
uv --version
```

Expected:

```text
uv x.y.z
```

---

# Step 3: Initialize uv Project

Navigate to project root:

```bash
cd <project-root>
```

Initialize project:

```bash
uv init --bare
```

Generated:

```text
pyproject.toml
```

---

# Step 4: Create Virtual Environment

```bash
uv venv
```

Generated:

```text
.venv/
```

Verify:

```bash
dir .venv
```

---

# Step 5: Import Existing Dependencies

Existing dependencies are stored in:

```text
requirements.txt
```

Add all dependencies:

```bash
uv add -r requirements.txt
```

This command:

* Reads dependencies from `requirements.txt`
* Updates `pyproject.toml`
* Creates `uv.lock`
* Resolves dependency versions

Generated files:

```text
pyproject.toml
uv.lock
```

---

# Step 6: Synchronize Environment

```bash
uv sync
```

Verify installed packages:

```bash
uv pip list
```

---

# Step 7: Install Jupyter Support

Install notebook dependencies:

```bash
uv add jupyter ipykernel
```

Verify:

```bash
uv pip list
```

Expected packages:

```text
jupyter
ipykernel
```

---

# Step 8: Register Jupyter Kernel

Register uv environment as a notebook kernel:

```bash
uv run python -m ipykernel install --user --name deep-drive-python --display-name "Python (deep-drive-python)"
```

Expected:

```text
Installed kernelspec deep-drive-python
```

Verify:

```bash
jupyter kernelspec list
```

Expected:

```text
Available kernels:
  deep-drive-python
  python3
```

---

# Step 9: Select Kernel in VS Code

Open:

```text
notebooks/01_openai_demo.ipynb
```

Click:

```text
Select Kernel
```

Choose:

```text
Python (deep-drive-python)
```

or

```text
<project-root>\.venv\Scripts\python.exe
```

---

# Alternative: Select Interpreter

If the kernel is not visible:

Open Command Palette:

```text
Ctrl + Shift + P
```

Run:

```text
Python: Select Interpreter
```

Choose:

```text
<project-root>\.venv\Scripts\python.exe
```

Reload notebook.

---

# Verify Active Kernel

Create a notebook cell:

```python
import sys

print(sys.executable)
```

Expected:

```text
<project-root>\.venv\Scripts\python.exe
```

---

# OpenAI SDK Setup

Install dependencies:

```bash
uv add openai python-dotenv
```

---

# Environment Variables

Create:

```text
.env
```

Content:

```env
OPENAI_API_KEY=your-api-key
```

---

# Notebook Example

### Cell 1

```python
from dotenv import load_dotenv

load_dotenv()
```

### Cell 2

```python
import os

api_key = os.getenv("OPENAI_API_KEY")

if not api_key:
    raise ValueError("OPENAI_API_KEY not found")
```

### Cell 3

```python
from openai import OpenAI

client = OpenAI(
    api_key=api_key
)
```

### Cell 4

```python
response = client.responses.create(
    model="gpt-4.1-mini",
    input="Hello OpenAI"
)

print(response.output_text)
```

---

# Project Structure

```text
<project-root>
│
├── day01/
│   └── docs/
│
├── day02/
│   └── docs/
│       └── feature-python-setup.md
│
├── notebooks/
│   └── 01_openai_demo.ipynb
│
├── .venv/
├── .env
├── .gitignore
├── pyproject.toml
├── uv.lock
├── requirements.txt
└── README.md
```

---

# .gitignore

```gitignore
# uv
.venv/

# Secrets
.env

# Python
__pycache__/
*.pyc

# Jupyter
.ipynb_checkpoints/

# VS Code
.vscode/

# OS
.DS_Store
Thumbs.db
```

---

# Git Workflow

Create branch:

```bash
git checkout -b feature/python-setup-uv
```

Add changes:

```bash
git add .
```

Commit:

```bash
git commit -m "feat: migrate python environment management to uv"
```

Push:

```bash
git push -u origin feature/python-setup-uv
```

---

# Key Learnings

* Traditional venv vs uv
* Dependency management using pyproject.toml
* Dependency locking using uv.lock
* Migrating from requirements.txt
* Jupyter kernel registration
* VS Code kernel selection
* Secure API key management using .env
* OpenAI SDK integration

---

# Day 2 Completion Checklist

* [x] Removed old virtual environment
* [x] Installed uv
* [x] Initialized uv project
* [x] Created .venv
* [x] Imported dependencies from requirements.txt
* [x] Generated pyproject.toml
* [x] Generated uv.lock
* [x] Installed Jupyter
* [x] Registered kernel
* [x] Selected kernel in VS Code
* [x] Configured .env
* [x] Verified OpenAI SDK
* [x] Created Git feature branch
* [x] Pushed changes to GitHub

---

## References

Repository:

https://github.com/sigmakumarwadbude/deep-drive-python

Instructor:

Sharad Rajore

GitHub:

https://github.com/srajore
