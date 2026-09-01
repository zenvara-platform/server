<!-- Canonical source: server-source/packaging/carrier/server/CONTRIBUTING.md — do not edit here by hand. -->
# Filing Issues

This repository holds no source code — Zenvara is proprietary. Issues and Discussions are the contribution surface. This guide covers how to file an issue that gets fixed fast.

## Pick the right channel

| You have… | Go to |
|---|---|
| A question, "how do I…", flow-authoring help | [Discussions](https://github.com/zenvara-platform/server/discussions) or [docs.zenvara.ai](https://docs.zenvara.ai) |
| A reproducible defect | [Bug report](https://github.com/zenvara-platform/server/issues/new?template=bug_report.yml) |
| An idea or missing capability | [Feature request](https://github.com/zenvara-platform/server/issues/new?template=feature_request.yml) |
| A problem tied to your specific installation | Built-in support channel — see [SUPPORT.md](SUPPORT.md) |
| A security vulnerability | **security@zenvara.ai** — never a public issue. See [SECURITY.md](SECURITY.md) |

## Before you file

1. Check the [troubleshooting guide](https://docs.zenvara.ai/getting-started/troubleshooting/) and the [error catalog](https://docs.zenvara.ai/reference/errors/).
2. Search [existing issues](https://github.com/zenvara-platform/server/issues?q=is%3Aissue) — including closed ones. Add a 👍 or a comment with your details to an existing issue instead of duplicating it.
3. Upgrade if you can: check whether the [latest release](https://github.com/zenvara-platform/server/releases/latest) already fixes it.

## Gather the facts

The bug form asks for these — here's where to find them:

- **Version**: `GET /api/v1/platform/diagnostics` on your install, or the release tag you downloaded.
- **Logs**: configured via the `Serilog` section of `appsettings.yaml`. Include the startup pack-load lines if the problem is a missing operator, and the full error entry (it carries the error code and category from the [error catalog](https://docs.zenvara.ai/reference/errors/)).
- **Error codes**: failed runs report a typed code (`timeout`, `invalid-parameters`, `retry-exhausted`, …) in the log and in the REST/GraphQL response body. Quote it verbatim.
- **Flow YAML**: if the bug involves a flow, include the smallest flow that reproduces it — not your production pipeline.

## Format

- **Title**: symptom, not judgement. `SFTP connector: retry-exhausted after exactly 3 attempts despite retry: 5` beats `SFTP broken!!`.
- **One bug per issue.** Two problems = two issues; they get fixed on different timelines.
- **Fenced code blocks** for YAML, logs, and JSON — triple backticks with a language tag (`yaml`, `json`, `text`). Never screenshots of text.
- **Numbered repro steps**, starting from a state we can reach: "fresh install, deploy this flow, trigger via X".
- **Expected vs actual**, one line each.

## Redact before posting

Issues are public and permanent. Strip from logs, YAML, and screenshots:

- Credentials, API keys, tokens, connection strings.
- Internal hostnames, IPs, and bucket/queue names if they matter to you.
- Personal data flowing through your pipelines.

Replace with placeholders (`<S3_BUCKET>`, `<API_KEY>`) rather than deleting lines — context matters.

## After you file

- New issues get the `triage` label automatically. We confirm, reproduce, and re-label — or ask follow-up questions. Issues waiting on your reply that stay silent may be closed as stale; a comment reopens the conversation.
- Fixes ship in releases; the release notes reference the issues they close.
- No promises on timelines for feature requests — 👍 reactions on the issue are what we sort by.
