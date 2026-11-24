<!-- Canonical source: server-source/packaging/carrier/server/README.md — do not edit here by hand. -->
# Zenvara

**Describe the automation. Zenvara builds it.**

[![Latest release](https://img.shields.io/github/v/release/zenvara-platform/server?label=release)](https://github.com/zenvara-platform/server/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/zenvara-platform/server/total)](https://github.com/zenvara-platform/server/releases)
[![Docker Hub](https://img.shields.io/docker/v/zenvara/server?label=docker&logo=docker)](https://hub.docker.com/r/zenvara/server)
[![Docs](https://img.shields.io/badge/docs-docs.zenvara.ai-blue)](https://docs.zenvara.ai)
[![Website](https://img.shields.io/badge/website-zenvara.ai-blue)](https://zenvara.ai)

Zenvara is an AI-native automation platform. Tell the chat what you want automated and it writes the pipeline, or write it yourself as YAML. Either way Zenvara compiles it to a typed graph and checks it before anything runs, runs it on a schedule or when something happens, logs every step, and rolls back its own writes if something breaks partway through.

If it has an API, a database, files, a queue or a mailbox, Zenvara can automate it. It serves three jobs organisations usually buy three platforms for:

- **Data integration** — ETL, joins, change detection.
- **Service integration** — HTTP, SOAP/WSDL, GraphQL, SFTP, S3, Kafka, SQL and NoSQL databases, plus discovery that turns any OpenAPI, WSDL or GraphQL spec into callable actions without writing code.
- **AI workflows** — Claude, ChatGPT, Gemini or a model you host yourself, as native, typed pipeline steps.

It ships as a single self-contained binary — the .NET runtime is embedded. No JVM, no Python runtime, no cluster required.

## What sets it apart

- **No code needed to start.** In Basic mode the chat does everything Pro mode does: it builds, changes and runs every kind of flow Zenvara supports, and shows you what it built before it goes live.
- **AI agents that work as a team.** Several agents share a chat room, work in parallel, message each other and wait for each other's answers. People can edit the same flow with them, live.
- **Your passwords stay yours.** When an agent needs a credential, it sends a one-time link. You type the secret in your own browser, and it never reaches the transcript, the model or a log.
- **AI that costs nothing at run time.** The AI drafts the flow; the published flow runs as a checked pipeline with no tokens per run. While you build, the assistant starts on the cheapest model and only escalates when it has to. Or keep everything local with Ollama, LM Studio, vLLM or llama.cpp.
- **Managed like software.** Tests for your flows, branches, promotion, revert, backups and a full audit trail.

## Use it from an AI agent (MCP)

Zenvara is an MCP server for the whole platform, not just a way to trigger workflows. Its 55 tools let an agent build, run, inspect and fix flows:

| What an agent can do | Tools (examples) |
|---|---|
| Build and change flows, connections and templates | `create-entity`, `update-entity`, `apply-entity-edit`, `validate-entity`, `publish-draft` |
| Run flows and their tests, and read the results | `run-flow`, `run-flow-tests`, `get-run-result`, `get-diagnostics`, `control-run` |
| Discover what exists | `list-entities`, `list-entity-types`, `read-entity`, `read-resource` |
| Version and recover | `promote-branch`, `revert-entity`, `restore-backup` |
| Handle secrets without seeing them | `request-secret-link`, `await-secret`, `rotate-secret` |
| Work with people and other agents | `collab-session`, `post-chat-message`, `await-chat-message`, `open-direct-message` |
| Operate the instance | `manage-triggers`, `manage-package`, `manage-user`, `perform-maintenance` |

The server answers MCP at `/mcp` on the same port as Studio. To connect Claude Code:

```bash
claude mcp add --transport http zenvara http://localhost:5000/mcp \
  --header "X-API-Key: $ZENVARA_API_KEY"
```

Create the key in Studio on the **People** page. Use an API key rather than a sign-in token: tokens expire after an hour, keys last a year by default. Claude Desktop, Cursor and other MCP clients take the same URL and header. On a local instance with authentication switched off, no key is needed. See [Authentication](https://docs.zenvara.ai/secrets-auth/authentication/).

## How it compares

We publish the full, scored comparisons ourselves, including the rows the other tool wins:

- **Where n8n wins:** far more ready-made connectors (about 1,100 against our 62), building by dragging nodes on a canvas (ours is a viewer), a more mature managed cloud and a larger community. [Zenvara vs n8n](https://zenvara.ai/compare/n8n)
- **Where Apache Airflow wins:** a larger connector and operator ecosystem, mature managed offerings, a larger community, and column-level lineage with a data-quality test framework. [Zenvara vs Airflow](https://zenvara.ai/compare/airflow)
- **Where Zenvara wins:** flows are compiled and checked before they run, completed writes roll back when a step fails, the AI drafts the flow and costs nothing per run, 55 MCP tools cover the whole platform, and it runs as one binary on your own servers.

---

## About this repository

> **This repository does not contain Zenvara's source code.** Zenvara is a proprietary product. This repo is the public home for:
>
> - 📦 **Releases** — download the latest binaries from the [**Releases**](../../releases) tab.
> - 🐞 **Issues** — report bugs and track fixes in [**Issues**](../../issues).
> - 💬 **Discussions** — ask questions and share patterns in [**Discussions**](../../discussions).

## Quick start

Binaries come from the [latest release](https://github.com/zenvara-platform/server/releases/latest). Verify a downloaded archive against our signed release manifest before installing — see [SECURITY.md § Verifying downloads](SECURITY.md#verifying-downloads) (the per-archive `.sha256` file alone is not sufficient — it proves the download is self-consistent, not that it came from us). Once running, open [localhost:5000](http://localhost:5000/) — the built-in Studio IDE.

### Docker

```bash
docker run -d --name zenvara -p 5000:5000 -v zenvara-data:/data zenvara/server:latest
```

### Linux

Download `zenvara-linux-x64.tar.gz` (or `-arm64`), then:

```bash
mkdir -p ~/zenvara
tar xzf zenvara-linux-x64.tar.gz -C ~/zenvara
~/zenvara/Zenvara.App
```

### Windows

Download `zenvara-win-x64.zip`, then:

```powershell
Expand-Archive zenvara-win-x64.zip -DestinationPath C:\Zenvara
C:\Zenvara\Zenvara.App.exe
```

### macOS

**Not supported yet.** No macOS build is published, so there is nothing to
download here. macOS builds return once the binaries are code-signed and
notarized — an unsigned build is terminated by the kernel at launch on current
macOS, which is why shipping one anyway would be worse than shipping none.

Run the server on Linux or Windows, or use Docker on a Mac.

For more information, refer to the [official documentation site](https://docs.zenvara.ai).

## Reporting an issue

The full guide — channel selection, required facts, format, redaction — is in [CONTRIBUTING.md](CONTRIBUTING.md). The short version:

1. Check the [docs](https://docs.zenvara.ai) and the [troubleshooting guide](https://docs.zenvara.ai/getting-started/troubleshooting/).
2. Search [existing issues](https://github.com/zenvara-platform/server/issues) to avoid duplicates.
3. File with the facts listed in [CONTRIBUTING.md](CONTRIBUTING.md) — version, deployment target, logs.

> ⚠️ **Security issues:** please do **not** open a public issue for suspected vulnerabilities. Email **security@zenvara.ai** instead. See [SECURITY.md](SECURITY.md).

## License

Zenvara is commercial, proprietary software. © Zenvara. All rights reserved. Use is governed by your license agreement; binaries published here are distributed under those terms. See [LICENSE.md](LICENSE.md).
