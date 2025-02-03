# ReAct Job Scout

An autonomous job-search agent that demonstrates the **ReAct** reasoning paradigm — *Reasoning + Acting* interleaved in a single loop. Give it your resume and a job title; it searches listings, fetches job descriptions, scores each match, and drafts tailored cover letters.

## How it works

The agent follows the classic ReAct cycle:

```
Thought → Action → Observation → Thought → ...
```

Each iteration the LLM reasons about what to do next, calls one of the available tools, and uses the result to inform the next step. The loop terminates when the agent decides it has enough information or hits the iteration limit.

### Tools

| Tool | Description |
|---|---|
| `search_jobs` | Search job boards for listings matching a query |
| `fetch_jd` | Fetch and parse a full job description from a URL |
| `read_resume` | Load and parse the candidate's resume |
| `score_match` | Score the fit between a resume and a job description |
| `draft_cover_letter` | Draft a tailored cover letter for a job |

## Installation

```bash
git clone https://github.com/amzaandrei/react-job-scout
cd react-job-scout
python -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
cp .env.example .env  # add your Anthropic API key
```

## Usage

```bash
job-scout --resume examples/sample_resume.txt --query "senior AI engineer"
```

## Configuration

| Variable | Default | Description |
|---|---|---|
| `ANTHROPIC_API_KEY` | — | Your Anthropic API key |
| `RJS_MODEL` | `claude-opus-4-7` | Main agent model |
| `RJS_SCORING_MODEL` | `claude-haiku-4-5` | Cheap model for scoring |
| `RJS_DRAFTING_MODEL` | `claude-sonnet-4-6` | Mid-tier for letter drafts |
| `RJS_MAX_ITERATIONS` | `12` | Max ReAct loop iterations |
| `RJS_LOG_LEVEL` | `INFO` | Logging verbosity |

## Running tests

```bash
pytest
```

Traces of each agent run are saved as JSON under `traces/`.
