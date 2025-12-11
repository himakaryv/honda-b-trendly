# honda-b-trendly

# **Honda Trend Intelligence Workflow (Multi-Agent, OpenCode)**

This project contains a **multi-agent, OpenCode-powered AI workflow** that analyzes signals (papers, patents, industry reports, regulatory reports, news, social) and turns them into **actionable trend intelligence**.

At the center is the **Honda Orchestrator Agent**, which coordinates three worker agents:

1. **Source Agent** – collects diverse signals from multiple sources
2. **Scoring Agent** – scores each signal along four key dimensions
3. **Synthesis Agent** – turns scored signals into trends, lifecycle stages, and leadership summaries

The orchestrator enforces a clear **Layer 1 scope** before any AI work happens:

* **Purpose** (e.g., technology scouting, investment thesis, risk monitoring)
* **Time Horizon** (e.g., 1–2 years, 3–5 years, 10+ years)
* **Industry / Domain Boundary** (e.g., automotive interiors, robotics for logistics)

From there, the agents:

* Collect signals from multiple sources
* Score them using source-aware scoring logic
* Aggregate them into trends
* Assign lifecycle stage, primary drivers, and hype vs. substance
* Generate a concise **leadership summary**

This README guides **new users** through:

* Installation and setup
* Running the **Honda Orchestrator Agent** end-to-end
* Understanding how the agents and layers fit together

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

Install from:
[https://www.python.org/downloads/](https://www.python.org/downloads/)

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

OpenCode runs the agents.

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

# 🚀 8. Run the Workflow (Orchestrator + Multiple Agents)

From the repo root:

```bash
opencode
```

This opens the OpenCode terminal.

### Step 1 — Choose a model

In the OpenCode prompt:

```text
/models
```

Select:

```text
openai / gpt-4.1
```

(or any other configured model you prefer.)

### Step 2 — Start the **Honda Orchestrator Agent**

List available agents (optional):

```text
/agents
```

Then start the orchestrator, for example by prompting:

```text
Run honda-orchestrator-agent to get trends in automotive industry with 3-5 years horizon and interiors as scope. Run the complete workflow and show me the results at each step and also mention clearly when the orchestrator agent is calling other agents - state it in the CLI output.
```

The orchestrator will:

1. **Enforce Layer 1 scope**

   * Clarify **Purpose**, **Time Horizon**, and **Industry Scope** if needed.
2. **Call the Source Agent**

   * Collect signals from primary, secondary, and social sources.
3. **Call the Scoring Agent**

   * Score signals for **Credibility, Frequency, Recency, Relevance**.
4. **Call the Synthesis Agent**

   * Aggregate scored signals into trends.
   * Assign lifecycle stage, primary driver, and hype vs. substance.
   * Generate leadership-ready summaries.

> The CLI output should clearly log when the orchestrator calls each agent, e.g.:
> `→ [Orchestrator] Calling Source Agent...`
> `→ [Orchestrator] Calling Scoring Agent...`
> `→ [Orchestrator] Calling Synthesis Agent...`

### Step 3 — Provide the inputs when asked

Example scope:

```text
Purpose: Technology scouting for Honda R&D automotive investments.
Time horizon: Next 3–5 years.
Industry boundary: Interiors in automotive.
```

You should see, in sequence:

* Structured **scope confirmation** (Layer 1)
* **Signals** collected by the Source Agent
* **Scoring tables** from the Scoring Agent
* **Trend aggregation** and profiles from the Synthesis Agent
* A final **Top Trends + leadership summary**

All within the same OpenCode session, with the orchestrator narrating which agent it is delegating to at each step.

---

# 🧱 9. Workflow Layers & Agents

The workflow is designed as a layered system, with each layer answering a different “why” and “how” question.

## 9.1 Layer 1 — Scope & Framing (Why this matters)

Layer 1 is the **anchor** for everything else. It defines:

* **Purpose** – What decision are we supporting?

  * Technology scouting? Investment thesis? Identifying long-term shifts? Prioritizing near-term opportunities?
* **Time Horizon** – 1 year vs 3–5 vs 10+ years implies very different maturity and risk profiles.
* **Industry Scope** – Insights are only useful when grounded in a concrete domain.

Without this shared lens, teams interpret “trends” differently and produce inconsistent or even contradictory outputs. The Orchestrator Agent enforces this layer upfront so downstream agents operate with the same frame.

## 9.2 Source Layer — Source Agent

**Problem we heard:** Users spend hours scraping papers, news, conference decks, and social feeds, but the information never comes together. Some teams over-index on academic sources, others on fast signals like news or social.

**Why it matters:**
Trends behave like ecosystems. A technology might appear first in patents, then papers, then industry news, then social chatter. Looking at only one source gives a distorted picture.

The **Source Agent** pulls from three buckets:

* **Primary sources → depth**
  Expert interviews, events, conferences, first-party insights.
* **Secondary sources → credibility**
  Papers, patents, industry and regulatory reports.
* **Social / fast signals → recency & weak signals**
  News, social media, Google Trends, etc.

Output: a **diverse list of candidate signals** for the defined purpose, horizon, and domain.

## 9.3 Scoring Layer — Scoring Agent

**Problem we heard:** Teams can collect signals, but they don’t have a consistent way to **prioritize** or **trust** them. Decisions end up driven by intuition or whoever speaks loudest.

The **Scoring Agent** scores each signal along four dimensions:

1. **Credibility** – Can I trust this signal?

   * Peer-reviewed papers and patents vs speculative blog posts.
2. **Frequency** – Does it show up repeatedly across independent sources?
3. **Recency** – Is it emerging now, peaking, or already fading?
4. **Relevance** – Does it actually map back to the specified **purpose**, **time horizon**, and **industry scope**?

Output: a **scoring table** with signals as rows and the four dimensions as columns.

This turns subjective impressions into **comparable, quantitative insight** with fewer blind spots.

## 9.4 Synthesis Layer — Synthesis Agent

**Problem we heard:** The hardest part is synthesis. People end up with notes, PDFs, and screenshots, but no clear story.

The **Synthesis Agent** converts scored signals into structured trend profiles, answering:

* **Lifecycle Stage** – Where is this trend on its maturity curve?

  * Emerging, growing, maturing, or saturated?
* **Primary Driver** – What’s pushing it?

  * Tech push, regulation push, consumer pull, market/competition, etc.
* **Hype vs Substance** – Is this mainly media noise, or is it backed by real, credible activity?

Output:

* 5–7 **named trends** for the scope
* A **trend scoring table**
* Concise **leadership summaries** that decision-makers can actually use

Instead of a pile of articles, you get **decision-ready insight**.

## 9.5 Orchestrator Layer — Honda Orchestrator Agent

The **Honda Orchestrator Agent** is the single entry point for users. It:

* Validates and locks in **Layer 1 scope**
* Calls the **Source Agent**, then the **Scoring Agent**, then the **Synthesis Agent** in sequence
* Ensures context is passed correctly between layers
* Produces an end-to-end **narrated CLI output**, clearly marking when each sub-agent is called

This is the agent you interact with directly in OpenCode.

---

# 📂 10. Project Structure

```text
.opencode/
  agent/
    honda-orchestrator-agent.md   ← Controls the full workflow (entry point)
    honda-source-agent.md         ← Collects signals from multiple source types
    honda-scoring-agent.md        ← Scores signals (Credibility, Frequency, Recency, Relevance)
    honda-synthesis-agent.md      ← Aggregates trends & generates summaries
scoring/
  scoring-logic-papers.txt
  scoring-logic-patents.txt
  scoring-logic-industry-reports.txt
  scoring-logic-regulatory-reports.txt
  scoring-logic-social.txt
data/
  (optional input files, historical runs, or domain-specific configs)
README.md
```

> File names may vary slightly depending on your local setup, but conceptually there is **one orchestrator** and **three worker agents**.

---

# 🔮 11. Evaluation & Future Directions

A key question is: **“How do we know the output is actually good?”**

The planned **Evaluation Workflow**:

1. Take **historical signals** from a past year (e.g., 2018).
2. Run them through the **same multi-agent workflow** with an appropriate scope.
3. Compare the system’s predicted trend ranking against **what actually happened** in the real world in the following years.
4. Use gaps to refine:

   * Scoring logic
   * Weights for the four dimensions
   * Thresholds for trend elevation

Over time, this can turn the system into a **self-improving model** of how technology evolves:

* Learns from past trend trajectories
* Becomes better at spotting weak signals earlier
* Calibrates hype vs substance more accurately

Future extensions:

* A dedicated **Verification / Fact-Checking Agent** to validate citations and flag inconsistencies in external sources.
* Evaluation dashboards that visualize model performance over time.
* Support for **multiple personas** and **different downstream tasks** (e.g., executive briefs vs research deep dives).

---

# ⚙️ 12. Current Limitations (Prototype)

As with any early prototype, there are a few important limitations to be aware of:

1. **CLI-only interface**

   * The system currently runs in a **command-line environment** (OpenCode).
   * From user interviews, we know people prefer dashboards, heat maps, and interactive visualizations. The CLI is deliberately lightweight and optimized for workflow validation, not presentation.

2. **Manually defined scoring logic**

   * Scoring rules and weights for Credibility, Frequency, Recency, and Relevance are currently **hand-crafted** based on research and expert input.
   * Long-term, we want the evaluation workflow to **learn and adjust** these automatically.

3. **No independent fact checking**

   * The system can read reports, patents, and news, but it **cannot independently verify** whether citations or claims are correct.
   * This is a general limitation of LLM-driven systems today. A **Verification Agent** is a natural next step.

Despite these constraints, the prototype already demonstrates a **repeatable, multi-agent design** that can be evolved into a full product with richer UI and evaluation.

---

# 🚀 13. Next Steps & How This Can Grow

Some concrete directions for extending this work:

1. **Deploy within Honda / HRI workflows**

   * Let real users run their day-to-day trend questions through the orchestrator.
   * Use their feedback to refine scoring, sources, and personas.

2. **Integrate internal Honda knowledge**

   * Right now the system uses mostly **public signals** (papers, patents, news, public reports).
   * Incorporating **internal reports, historical decks, third-party market research** will make the system more Honda-specific and impactful.

3. **Add a Verification Agent**

   * Work alongside the orchestrator to cross-check citations, detect conflicting data, and flag low-credibility sources.

4. **Expand to more personas & downstream tasks**

   * The current workflow is tuned to a specific user persona and decision type.
   * With configuration changes, the same architecture can support:

     * R&D teams
     * Strategy teams
     * External-facing content (blogs, LinkedIn posts, reports)

5. **Implement the full Evaluation Workflow**

   * Use past years’ data, run the pipeline, compare against real history, and iterate on scoring logic.
   * This is crucial for long-term reliability.

6. **Create a living database of trend signals**

   * Store signals, scores, and trend profiles over time to build a **trend knowledge base**.
   * This can support internal reporting, monitoring dashboards, and research.

7. **Automated content generation**

   * Use the Synthesis Agent outputs to generate material for **Medium / LinkedIn / internal newsletters**.

8. **Dashboards and visualization**

   * Even though the workflow runs via CLI, its outputs can be consumed by other tools to build **real-time monitoring dashboards**, heatmaps, and trend scorecards.

---

# 🧠 14. Troubleshooting

### ❗ Agent only outputs "plans"

You may be in a **read-only environment** (sandbox).
Use simulated mode:

```text
Run the full workflow in simulated execution mode.
```

### ❗ Colors hard to read (macOS Terminal)

Switch to **Pro** profile:

```text
Terminal → Settings → Profiles → Pro → Default
```

Or use iTerm2 with a dark theme.

### ❗ `opencode` not found

Re-run install:

```bash
curl -fsSL https://opencode.ai/install | bash
```

or:

```bash
npm install -g opencode-ai
```

---

# 🎉 15. You are ready to use the Honda Trend Intelligence Workflow!

Use the **Honda Orchestrator Agent** as your entry point, give it a clear purpose, time horizon, and industry scope, and let the multi-agent workflow take care of the rest.

If you need help or want to extend the project, feel free to open an issue or contact the team.
