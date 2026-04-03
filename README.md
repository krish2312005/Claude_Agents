# ⚡ Claude Code – Agent Workflow Guide

> Personal workflow for using Claude Code with custom agents via simple terminal commands.

---

## 📌 Overview

This setup allows you to use **high-level commands** instead of manually managing agents.

The system automatically:
- Understands your request
- Selects the required agents
- Executes them in the correct order

---

## 🚀 Commands

Use these directly in your terminal:

```
/build
/deploy
/feature
/fix
```

---

## ⚙️ How It Works

- Commands act as entry points
- The system determines which agents are needed
- All agents are loaded automatically from:

```
.claude/agents/
```

- Execution is handled without manual intervention

---

## 🧠 Example

```
/build create a task management SaaS with user authentication and a team dashboard
```

### What this does:
- Breaks down the request
- Loads required agents
- Runs the full build workflow

---

## 🏗️ Notes

- Designed for fast, hands-off development
- Best suited for larger tasks or full features
- Requires properly configured agents

---

## 📄 Usage Scope

This setup is for **personal use only**.

---