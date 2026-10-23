# AI-DLC POC

An AI-driven development lifecycle: from a Jira ticket to a plan, code, tests,
a pull request and a deployment, using LangGraph agents with human approval gates.

> Status: proof of concept, setup phase.
> Jira board: SCRUM (AI-DLC POC)

## Architecture (short)

```
Jira ticket -> Router -> Planner -> [Gate 1: approve plan]
            -> Coder -> Tester -> Reviewer
            -> Pull request [Gate 2: review PR]
            -> CI/CD -> Deploy [Gate 3: approve deploy]
            -> Jira update
```

A shared state object travels through the graph, and a checkpointer lets a
paused run resume exactly where it stopped.

## Setup

```bash
git clone https://github.com/VishRoy/ai-dlc-poc.git
cd ai-dlc-poc
python3 -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env           # then fill in your keys
```

Requires Python 3.11 or newer.

## Project structure

| Folder    | Purpose                                  |
| --------- | ---------------------------------------- |
| `agents/` | Router, Planner, Coder, Tester, Reviewer |
| `tools/`  | Jira and GitHub wrappers                 |
| `graph/`  | LangGraph flow: state, edges, gates      |
| `config/` | Settings and secrets loading             |
| `tests/`  | pytest tests                             |

## Conventions

- Never commit `.env`. Use `.env.example` to document required keys.
- Include the Jira ticket key in every commit message, for example `SCRUM-24`.
