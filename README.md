# oracle-agent

> **🔮 Live A2A endpoint:** https://oracle-agent-768432456747.us-central1.run.app
>
> - Agent card (machine-discoverable):
>   `https://oracle-agent-768432456747.us-central1.run.app/a2a/app/.well-known/agent-card.json`
> - JSON-RPC endpoint: `POST https://oracle-agent-768432456747.us-central1.run.app/a2a/app`
> - API docs: `https://oracle-agent-768432456747.us-central1.run.app/docs`

A production-deployed Google ADK agent exposing the **[Agent2Agent (A2A) protocol](https://a2a-protocol.org/)** — other agents (in any framework, any language) can call it programmatically using JSON-RPC over HTTP. The agent itself responds in dramatic, technically-correct prophecies (Oracle of Delphi meets stage magician), but the value is the protocol surface, not the persona.

**Stack**
- Google ADK with the `adk_a2a` template — A2A protocol v0.3.0, JSON-RPC transport, streaming enabled
- Gemini 2.5 Flash via **Vertex AI** (service-account auth, no API keys in prod)
- Built-in `google_search` tool for grounded prophecies on current events
- FastAPI + Uvicorn, Cloud Run (scale-to-zero, 4 GiB)

**Discover the agent's capabilities** programmatically:
```bash
curl https://oracle-agent-768432456747.us-central1.run.app/a2a/app/.well-known/agent-card.json | jq
```

Validate the A2A implementation with the [A2A Protocol Inspector](https://github.com/a2aproject/a2a-inspector).

Sister repos in this portfolio:
- [caveman-agent](https://github.com/naveen-kalakata/caveman-agent) — text compression agent (browser chat UI)
- [docs-agent](https://github.com/naveen-kalakata/docs-agent) — RAG agent (Vertex AI Search)

---

Agent generated with `agents-cli` version `0.1.1`

## Project Structure

```
oracle-agent/
├── app/         # Core agent code
│   ├── agent.py               # Main agent logic
│   ├── fast_api_app.py        # FastAPI Backend server
│   └── app_utils/             # App utilities and helpers
├── tests/                     # Unit, integration, and load tests
├── GEMINI.md                  # AI-assisted development guide
└── pyproject.toml             # Project dependencies
```

> 💡 **Tip:** Use [Gemini CLI](https://github.com/google-gemini/gemini-cli) for AI-assisted development - project context is pre-configured in `GEMINI.md`.

## Requirements

Before you begin, ensure you have:
- **uv**: Python package manager (used for all dependency management in this project) - [Install](https://docs.astral.sh/uv/getting-started/installation/) ([add packages](https://docs.astral.sh/uv/concepts/dependencies/) with `uv add <package>`)
- **agents-cli**: Agents CLI - Install with `uv tool install google-agents-cli`
- **Google Cloud SDK**: For GCP services - [Install](https://cloud.google.com/sdk/docs/install)


## Quick Start

Install required packages:

```bash
agents-cli install
```

Test the agent with a local web server:

```bash
agents-cli playground
```

You can also use features from the [ADK](https://adk.dev/) CLI with `uv run adk`.

## Commands

| Command              | Description                                                                                 |
| -------------------- | ------------------------------------------------------------------------------------------- |
| `agents-cli install` | Install dependencies using uv                                                         |
| `agents-cli playground` | Launch local development environment                                                  |
| `agents-cli lint`    | Run code quality checks                                                               |
| `uv run pytest tests/unit tests/integration` | Run unit and integration tests                                                        |
| `agents-cli deploy`  | Deploy agent to Cloud Run                                                                   |
| [A2A Inspector](https://github.com/a2aproject/a2a-inspector) | Launch A2A Protocol Inspector                                                        |

## 🛠️ Project Management

| Command | What It Does |
|---------|--------------|
| `agents-cli scaffold enhance` | Add CI/CD pipelines and Terraform infrastructure |
| `agents-cli infra cicd` | One-command setup of entire CI/CD pipeline + infrastructure |
| `agents-cli scaffold upgrade` | Auto-upgrade to latest version while preserving customizations |

---

## Development

Edit your agent logic in `app/agent.py` and test with `agents-cli playground` - it auto-reloads on save.

## Deployment

```bash
gcloud config set project <your-project-id>
agents-cli deploy
```

To add CI/CD and Terraform, run `agents-cli scaffold enhance`.
To set up your production infrastructure, run `agents-cli infra cicd`.

## Observability

Built-in telemetry exports to Cloud Trace, BigQuery, and Cloud Logging.

## A2A Inspector

This agent supports the [A2A Protocol](https://a2a-protocol.org/). Use the [A2A Inspector](https://github.com/a2aproject/a2a-inspector) to test interoperability.
See the [A2A Inspector docs](https://github.com/a2aproject/a2a-inspector) for details.
