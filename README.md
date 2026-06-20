# Multi-Agent LLM Debate Simulator

A simulation where two LLM-driven agents argue opposing sides of a contested topic across multiple rounds, with a third LLM acting as a neutral judge to evaluate the debate and declare a winner.

## What it does

1. **Agent 1** is prompted to argue one side of a debate topic.
2. **Agent 2** responds with a counter-argument, having access to the full conversation memory so far.
3. The two agents continue exchanging rounds, each building on the shared debate memory.
4. A **Judge** model reviews the complete transcript and produces a structured evaluation: summarizing each side's position, identifying strengths/weaknesses in their arguments, and declaring a final verdict with reasoning.

This explores how LLMs construct, defend, and critique arguments when placed in adversarial roles — and whether a separate LLM can act as a consistent, well-reasoned judge over multi-turn exchanges.

## Tech stack

- `google-generativeai` — Gemini API (`gemini-2.5-flash`) powers all three roles (Agent 1, Agent 2, Judge)
- `python-dotenv` — environment variable management for API key handling

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/SID-sai/multi-agent-debate-simulator.git
cd multi-agent-debate-simulator
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Get your Gemini API key

Get a free key at https://aistudio.google.com/apikey

### 4. Configure environment variables

Create a `.env` file in the project root (gitignored, never committed):

```
GEMINI_API_KEY=your_gemini_key_here
```

### 5. Run it

Open `agent_one.ipynb` in Jupyter and run the cells in order:

```bash
jupyter notebook agent_one.ipynb
```

The notebook will:
- Initialize the Gemini model
- Run a debate round between Agent 1 and Agent 2
- Print each agent's response as it's generated
- Run the judge evaluation at the end and print the verdict

## Project structure

```
multi-agent-debate-simulator/
├── agent_one.ipynb     # Core debate logic: agents + judge
├── requirements.txt
├── .gitignore
└── README.md
```

## Status

Functional prototype, single debate topic hardcoded per run. Potential next steps: parameterize the debate topic via CLI/config, support N rounds dynamically rather than manual cell execution, add multiple judge models for consensus scoring, log full transcripts to file for later analysis.

## Security note

The Gemini API key is loaded exclusively from environment variables (`.env`, gitignored) — never hardcoded in the notebook. If you fork this repo, generate your own key; do not reuse any key that may have previously been exposed in earlier versions of this project.
