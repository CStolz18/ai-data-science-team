# AI Data Science Team: Plain English Guide

This guide explains what this repository is, how it is organized, and how to use it step by step.

## 1) What This Project Is

AI Data Science Team is a Python project that gives you:

- A set of specialized AI agents for common data science tasks
- A main Streamlit app called **AI Pipeline Studio**
- Additional demo apps for specific workflows (Pandas, SQL, EDA)

Think of it like a "team of assistants" for data science:

- One agent can load data
- Another can clean it
- Another can visualize it
- Another can do feature engineering
- Others can run modeling and MLflow/H2O workflows

Instead of writing every step manually, you can ask in plain language and let agents execute repeatable steps.

## 2) Main Idea in One Sentence

Use natural language to drive data science workflows, while the app keeps track of steps, artifacts, and pipeline lineage.

## 3) Quick Folder Map

Here are the most important folders and files:

- `apps/`
  - Streamlit applications you can run directly
  - Most important: `apps/ai-pipeline-studio-app/app.py`
- `ai_data_science_team/`
  - Core Python package (agents, tools, utilities, orchestration)
- `examples/`
  - Notebooks showing how to use agents programmatically
- `data/`
  - Sample datasets and example database
- `requirements.txt`
  - Python dependencies
- `setup.py`
  - Package install configuration
- `README.md`
  - High-level project overview
- `CONTRIBUTING.MD`
  - Setup and contribution workflow

## 4) Agent and Tool Concepts (Plain English)

## Agents

Agents are "role-based workers" that solve a type of task:

- Data loader agent
- Data cleaning agent
- Data wrangling agent
- EDA tools agent
- Data visualization agent
- SQL database agent
- Feature engineering agent
- ML agents (H2O / MLflow)

## Tools

Tools are callable functions used by agents to do actual work (load files, run SQL, create plots, etc.).

## Multi-agent workflows

Some modules combine multiple agents so they can collaborate (for example, SQL analyst and Pandas analyst flows).

## 5) Which App Should You Use?

Start with this:

- **AI Pipeline Studio**: `apps/ai-pipeline-studio-app/app.py`

Use other apps when you want a narrower use case:

- `apps/pandas-data-analyst-app/app.py`
- `apps/sql-database-agent-app/app.py`
- `apps/exploratory-copilot-app/app.py`

## 6) Step-by-Step: Recommended Daily Workflow

1. Activate your environment
- PowerShell: `.\.venv\Scripts\activate.ps1`

2. Start the main app
- `streamlit run apps/ai-pipeline-studio-app/app.py`

3. Choose LLM provider in the sidebar
- OpenAI or Ollama
- If OpenAI is selected, provide a valid API key (now auto-loaded from `.env` if set)

4. Load a dataset
- Upload a CSV/Excel file or use sample data

5. Ask practical task prompts
- "Show data summary and missing values"
- "Clean this dataset and explain changes"
- "Create 3 useful charts"
- "Engineer features for churn prediction"

6. Inspect outputs in tabs/panels
- Data table
- Charts
- EDA
- Generated code
- Model and MLflow outputs (if used)

7. Save project state
- Save when you want to continue later
- Use metadata-only or full-data modes depending on storage needs

## 7) Sidebar Settings Explained

Here is what the key sidebar items mean:

- `Proactive workflow mode`
  - If enabled, the supervisor can propose/run a broader multi-step workflow for high-level requests.
  - If disabled, behavior is usually more direct and request-by-request.

- `Upload CSV`
  - Yes, you can upload CSV files from this repo's `data/` folder.
  - Use the file picker and navigate to `data/`.

- `Active dataset (override)`
  - Forces which dataset is treated as active for downstream operations (cleaning, EDA, visualization, etc.).
  - `Auto` means it uses the supervisor's current active dataset.

- `Pipeline behaviors`
  - Controls save/restore behavior for pipeline files and dataset nodes.
  - Includes options like auto-save, overwrite, preserving nodes, and cache/persistence settings.

- `Chat ↔ Pipeline context`
  - Controls how much Pipeline Studio context is injected into chat.
  - When enabled, chat is better aligned with selected nodes and current pipeline state.

- `MLflow options`
  - Controls whether model-training runs are logged to MLflow and where artifacts/experiments are stored.

- `Debug options`
  - Troubleshooting controls.
  - `Verbose console logs` prints more details in terminal.
  - `Show progress in chat` and `Show live logs while running` improve visibility while agents execute.

Recommended beginner defaults:

1. Keep `Proactive workflow mode` off at first.
2. Keep `LLM intent parsing` on.
3. Keep `Chat ↔ Pipeline context` options on.
4. Turn on MLflow only if you want experiment tracking now.
5. Enable verbose logs only when debugging.

## 8) Good First Prompts

- "List all columns and tell me which have missing values."
- "Clean obvious data quality issues and summarize exactly what you changed."
- "Create a target-aware EDA summary for column `Churn`."
- "Build baseline features and train a first model, then report performance."
- "Create a business-facing chart explaining top churn drivers."

## 9) What Happens When You Ask a Question?

At a high level:

1. The app receives your prompt.
2. A planner/supervisor decides which agent(s) should act.
3. Selected agent(s) call tools and produce results.
4. App updates state, charts, tables, and artifacts.
5. You can continue iteratively with follow-up prompts.

## 10) Programmatic Use (Without Streamlit)

If you prefer notebooks/scripts, use `examples/` and import from `ai_data_science_team`.

Typical flow:

1. Create an LLM object
2. Initialize one or more agents
3. Invoke the agent with your task/input data
4. Inspect returned outputs (dataframe/code/messages/artifacts)

## 11) Common Issues and Fixes

## API key seems ignored

- Ensure `.env` contains `OPENAI_API_KEY=...`
- Restart Streamlit after changing `.env`
- Confirm provider is set to OpenAI in the sidebar

## No chat input / cannot ask

- Usually caused by missing or invalid API key validation
- Check sidebar for key status message

## Virtual env activation fails

- Verify `.\.venv\Scripts\activate.ps1` exists
- If script policy blocks activation, run:
  - `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass`

## 12) Mental Model: How to Succeed Fast

- Start small: ask for summary + cleaning first
- Keep prompts task-oriented and specific
- Validate outputs before moving to modeling
- Save working states often
- Treat agents as accelerators, not replacements for review

## 13) What to Learn Next

After you are comfortable with Pipeline Studio:

1. Explore `examples/` notebooks to understand agent APIs
2. Try the focused apps in `apps/` for SQL/Pandas/EDA patterns
3. Read source in `ai_data_science_team/agents/` to customize behavior
4. Extend with your own tools/agents for domain-specific workflows

---

If you want, the next step can be a second guide focused only on prompting patterns ("what to ask for best results"), with copy-paste prompt templates for each phase (EDA, cleaning, feature engineering, modeling, reporting).
