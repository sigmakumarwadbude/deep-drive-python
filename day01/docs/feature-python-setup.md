# Feature: Python Setup

## Branch Information

### Branch Name

```bash
feature/python-setup
```

### Purpose

This feature branch contains the initial Python development environment setup including:

* Python virtual environment creation
* Virtual environment activation
* VS Code configuration
* Jupyter Notebook setup
* OpenAI SDK installation
* Git ignore configuration

---

# Tasks Completed

## 1. Create Virtual Environment

### Windows CMD

```cmd
python -m venv myvenv
```

Verify environment creation:

```cmd
dir myvenv
```

---

## 2. Activate Virtual Environment

### Windows CMD

```cmd
myvenv\Scripts\activate
```

Expected:

```text
(myenv) project-root>
```

### Verify Active Environment

```cmd
where python
```

Expected:

```text
<project-root>\myenv\Scripts\python.exe
```

---

## 3. Install Required Packages

```cmd
pip install openai
pip install python-dotenv
pip install jupyter
pip install ipykernel
```

Export dependencies:

```cmd
pip freeze > requirements.txt
```

---

## 4. Register Jupyter Kernel

```cmd
python -m ipykernel install --user --name=myenv --display-name "Python (myvenv)"
```

Verify:

```cmd
jupyter kernelspec list
```

---

## 5. Configure .gitignore

Create `.gitignore`

```gitignore
# Virtual Environment
myvenv/
venv/

# Environment Variables
.env

# Python
__pycache__/
*.pyc

# Jupyter
.ipynb_checkpoints/

# VS Code
.vscode/

# OS Files
.DS_Store
Thumbs.db
```

---

## 6. Configure Environment Variables

Create `.env`

```env
OPENAI_API_KEY=your-api-key
```

Never commit:

```text
.env
```

to Git.

---

## 7. Verify OpenAI Setup

```python
from dotenv import load_dotenv
import os
from openai import OpenAI

load_dotenv()

client = OpenAI(
    api_key=os.getenv("OPENAI_API_KEY")
)

response = client.responses.create(
    model="gpt-4.1-mini",
    input="Hello OpenAI"
)

print(response.output_text)
```

---

# Git Commands

## Create Branch

```bash
git checkout -b feature/python-setup
```

## Add Changes

```bash
git add .
```

## Commit

```bash
git commit -m "feat: add python environment setup and gitignore"
```

## Push Branch

```bash
git push -u origin feature/python-setup
```

---

# Pull Request Description

## Title

```text
[SETUP] Python Environment, Virtual Environment and Git Configuration
```

## Description

### Changes

* Added Python virtual environment setup
* Added virtual environment activation guide
* Added Jupyter kernel configuration
* Added OpenAI SDK installation
* Added environment variable configuration using .env
* Added .gitignore for Python projects
* Added Day-1 setup documentation

### Validation

* Virtual environment created successfully
* Jupyter kernel registered and selected
* OpenAI SDK installed successfully
* Environment variables loaded from .env
* Notebook executed successfully

### Future Work

* Python Fundamentals
* Control Flow
* Functions
* OOP
* Pandas
* NumPy
* Data Engineering Modules
* OpenAI Integrations

```
```
