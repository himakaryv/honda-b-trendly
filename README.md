# **Honda Trend Intelligence Workflow (OpenCode Agent)**

This project contains an **OpenCode-powered AI workflow** that analyzes signals (papers, patents, industry reports, regulatory reports, social/news) and generates **Top Trends** for any technology domain.

A user only needs to provide:

* **Purpose** (ex: technology scouting, investment thesis, risk monitoring)
* **Time Horizon** (ex: 1–2 years, 3–5 years)
* **Industry Boundary** (ex: robotics for logistics, automotive interiors)

The agent then:

* Generates or processes signals
* Scores them using source-specific scoring logic
* Aggregates them into trends
* Produces Top 5 Trends
* Outputs lifecycle stage, drivers, hype vs. substance
* Generates a leadership summary

This README guides **new users** through installation and running the workflow.

---

# 📦 1. Requirements

You need the following installed:

* **Git**
* **Python 3.10+**
* **OpenCode CLI**
* **OpenAI API Key**

---

# 🛠️ 2. Install Git

Check if Git is installed:

```bash
git --version
```

If not, install from:
[https://git-scm.com/downloads](https://git-scm.com/downloads)

---

# 🐍 3. Install Python 3.10+

Check your version:

```bash
python3 --version
```

If you need Python:

### macOS (Homebrew):

```bash
brew install python
```

### Windows:

Install from [https://www.python.org/downloads/](https://www.python.org/downloads/)

---

# 📁 4. Clone This Repository

Replace `<your-repo>` with the actual URL:

```bash
git clone <your-repo>
cd <repo-name>
```

---

# 🧪 5. (Optional) Create Virtual Environment

```bash
python3 -m venv .venv
source .venv/bin/activate        # Windows PowerShell: .venv\Scripts\Activate.ps1
```

Install dependencies if provided:

```bash
pip install -r requirements.txt
```

---

# ⚙️ 6. Install OpenCode CLI

OpenCode runs the agent.

### Recommended install:

```bash
curl -fsSL https://opencode.ai/install | bash
```

If the above URL is temporarily unavailable:

### Alternative:

```bash
npm install -g opencode-ai@latest
```

Check installation:

```bash
opencode --version
```

---

# 🔑 7. Configure Your OpenAI API Key

You need an OpenAI API key to run the workflow.

### 7.1 Get your key

Go to:

[https://platform.openai.com](https://platform.openai.com)
→ Login → API Keys → Create new key.

### 7.2 Add the key to OpenCode

```bash
opencode auth login
```

Then:

1. Select **OpenAI**
2. Paste your secret API key
3. Confirm

OpenCode will store it securely.

---

# 🚀 8. Run the Workflow

From the repo root:

```bash
opencode
```

Inside the OpenCode terminal:

### Step 1 — Choose a model

```text
/models
```

Select:

```
openai / gpt-4.1
```

### Step 2 — Start the agent

```text
@trend-workflow
Start a new analysis run.
Ask me for:
1) Purpose
2) Time horizon
3) Industry boundary
Then run the full workflow.
```

### Step 3 — Provide the inputs when asked

Example:

```
Purpose: Technology scouting for Honda R&D robotics investments.
Time horizon: Next 3–5 years.
Industry boundary: Robotics for logistics and warehousing.
```

The agent will then output:

* Signals (LLM-generated)
* Signal scoring tables
* Trend aggregation (5–7 trends)
* Trend scoring table
* Top 5 trends
* Lifecycle, drivers, hype vs. substance
* Leadership summary

All inside the OpenCode session.

---

# 📂 9. Project Structure

```
.opencode/
  agent/
    trend-workflow.md     ← Main agent definition
scoring/
  Scoring-logic-Papers.txt
  scoring-logic-patents.txt
  scoring-logic-industry-reports.txt
  scoring-logic-regulatory-reports.txt
  scoring-logic-social.txt
data/
  (optional input files)
README.md
```

---

# 🧠 10. Troubleshooting

### ❗ Agent only outputs "plans"

You may be in a **read-only environment** (sandbox).
Use simulated mode:

```text
Run the full workflow in simulated execution mode.
```

### ❗ Colors hard to read (macOS Terminal)

Switch to **Pro** profile:

```
Terminal → Settings → Profiles → Pro → Default
```

Or use iTerm2 with a dark theme.

### ❗ `opencode` not found

Re-run install:

```bash
curl -fsSL https://opencode.ai/install | bash
```

or

```bash
npm install -g opencode-ai
```

---

# 🎉 You are ready to use the Honda Trend Workflow Agent!

If you need help or want to extend the project, feel free to open an issue or contact the team.

---

If you want, I can also generate:

* A **shorter version** for GitHub
* A **developer-focused README**
* A **slide-friendly setup page**
* A **video-script style walkthrough**

Just tell me!
