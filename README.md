<!-- Canonical source: server-source/packaging/carrier/server/README.md — do not edit here by hand. -->
# Zenvara

**Orchestration you can reason about.**

[![Latest release](https://img.shields.io/github/v/release/zenvara-platform/server?label=release)](https://github.com/zenvara-platform/server/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/zenvara-platform/server/total)](https://github.com/zenvara-platform/server/releases)
[![Docker Hub](https://img.shields.io/docker/v/zenvara/server?label=docker&logo=docker)](https://hub.docker.com/r/zenvara/server)
[![Docs](https://img.shields.io/badge/docs-docs.zenvara.ai-blue)](https://docs.zenvara.ai)
[![Website](https://img.shields.io/badge/website-zenvara.ai-blue)](https://zenvara.ai)

Zenvara is an AI-native automation platform. You describe pipelines in YAML; Zenvara compiles them to a typed graph, runs them on schedule, logs every step, and rolls them back if something breaks partway through. It serves three jobs organisations usually buy three platforms for:

- **Data integration** — ETL, joins, change detection.
- **Service integration** — HTTP, SOAP/WSDL, GraphQL, SFTP, S3, Kafka, SQL and NoSQL databases.
- **AI workflows** — Claude, ChatGPT, and Gemini as native, typed pipeline steps.

It ships as a single self-contained binary — the .NET runtime is embedded. No JVM, no Python runtime, no cluster required.

---

## About this repository

> **This repository does not contain Zenvara's source code.** Zenvara is a proprietary product. This repo is the public home for:
>
> - 📦 **Releases** — download the latest binaries from the [**Releases**](../../releases) tab.
> - 🐞 **Issues** — report bugs and track fixes in [**Issues**](../../issues).
> - 💬 **Discussions** — ask questions and share patterns in [**Discussions**](../../discussions).

## Quick start

Binaries come from the [latest release](https://github.com/zenvara-platform/server/releases/latest). Verify a downloaded archive against our signed release manifest before installing — see [SECURITY.md § Verifying downloads](SECURITY.md#verifying-downloads) (the per-archive `.sha256` file alone is not sufficient — it proves the download is self-consistent, not that it came from us). Once running, open [localhost:5000/studio](http://localhost:5000/studio/) — the built-in Studio IDE.

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

Download `zenvara-osx-arm64.tar.gz` (Apple Silicon) or `zenvara-osx-x64.tar.gz` (Intel), then:

```bash
mkdir -p ~/zenvara
tar xzf zenvara-osx-arm64.tar.gz -C ~/zenvara
xattr -dr com.apple.quarantine ~/zenvara   # clear Gatekeeper quarantine
~/zenvara/Zenvara.App
```

For more information, refer to the [official documentation site](https://docs.zenvara.ai).

## Reporting an issue

The full guide — channel selection, required facts, format, redaction — is in [CONTRIBUTING.md](CONTRIBUTING.md). The short version:

1. Check the [docs](https://docs.zenvara.ai) and the [troubleshooting guide](https://docs.zenvara.ai/getting-started/troubleshooting/).
2. Search [existing issues](https://github.com/zenvara-platform/server/issues) to avoid duplicates.
3. File with the facts listed in [CONTRIBUTING.md](CONTRIBUTING.md) — version, deployment target, logs.

> ⚠️ **Security issues:** please do **not** open a public issue for suspected vulnerabilities. Email **security@zenvara.ai** instead. See [SECURITY.md](SECURITY.md).

## License

Zenvara is commercial, proprietary software. © Zenvara. All rights reserved. Use is governed by your license agreement; binaries published here are distributed under those terms. See [LICENSE.md](LICENSE.md).
