<!-- Canonical source: server-source/packaging/carrier/server/SECURITY.md — do not edit here by hand. -->
# Security Policy

## Reporting a vulnerability

Please do **not** open a public issue for suspected security vulnerabilities.

Email **security@zenvara.ai** with:

- A description of the issue and its impact.
- Steps to reproduce, or a proof of concept.
- The Zenvara version affected (from `GET /api/v1/platform/diagnostics`).
- Your environment (OS, deployment target).

We will acknowledge your report within **3 business days** and keep you informed of progress. Please give us a reasonable window to release a fix before any public disclosure.

## Supported versions

Security fixes land in the latest stable release. Check the [Releases](https://github.com/zenvara-platform/server/releases) page and upgrade using the [upgrade guide](https://docs.zenvara.ai/deployment/upgrades/).

## Verifying downloads

**The `zen` CLI verifies authenticity automatically.** `zen app fetch` and `zen app update` fetch the
release's signed `SHA256SUMS.jws` manifest, check its signature against our pinned release-signing key, and
refuse to install on a bad or missing signature — no manual step needed. **A plain `zen app fetch` /
`zen app update` with no flags is the recommended way to install and update** — it always resolves and
checks the signed manifest before touching disk.

Two flags change that behavior and should be used deliberately, not by default: `--sha256 <hex>` **replaces**
signed-manifest verification with a manual pin you supply yourself — the manifest is never fetched — so
reserve it for a private mirror whose digest you already trust from another channel. `--insecure-skip-verify`
disables verification entirely.

A bare `.sha256` file also ships next to every archive, for a quick corruption check on a download that
already came from a trusted channel:

```bash
sha256sum -c zenvara-linux-x64.tar.gz.sha256
```

```powershell
# Windows: compare against the value in the .sha256 file
Get-FileHash zenvara-win-x64.zip -Algorithm SHA256
```

**That `.sha256` file alone does not prove authenticity** — it sits next to the archive it hashes, so
whoever could replace one could replace the other. Authenticity comes only from the **signed**
`SHA256SUMS.jws` manifest published alongside every release, which `zen` checks against a public key
pinned inside the CLI binary itself (never fetched from the same place as the download). See
[`docs.zenvara.ai`](https://docs.zenvara.ai) for the manifest format if you need to verify it without the
`zen` client.
