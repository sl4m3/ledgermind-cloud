# LedgerMind Cloud Connector

**LedgerMind Cloud** is the managed service: memory processing and storage run in
the managed backend. The **LedgerMind Cloud Connector** is the small local
component that connects an agent on your machine to that service with a
workspace API key.

This repository is the distribution home of the connector: release archives,
checksums, and installation documentation. It does not contain the managed
service, its deployment configuration, or any backend source.

## Install

```bash
curl -fsSL https://ledgermind.org/install-cloud.sh | sh
```

The installer downloads the release archive from this repository, verifies its
SHA-256 checksum, creates an isolated Python environment under
`${XDG_DATA_HOME:-$HOME/.local/share}/ledgermind/cloud`, and links the
`ledgermind-cloud` command into `~/.local/bin`.

Requirements: Python 3.10 or newer, `curl`, and `sha256sum`.

Then create a workspace API key in the [LedgerMind Cloud dashboard](https://ledgermind.org/dashboard)
and connect an agent:

```bash
ledgermind-cloud connect AGENT
ledgermind-cloud doctor
```

Supported agents: `codex`, `claude-code`, `hermes`, `opencode`, `openclaw`.

## Verify a release manually

```bash
version=0.2.0b1
base=https://github.com/sl4m3/ledgermind-cloud/releases/download/cloud-v${version}
curl -fsSLO "$base/ledgermind-cloud-${version}.tar.gz"
curl -fsSLO "$base/ledgermind-cloud-${version}.tar.gz.sha256"
sha256sum -c "ledgermind-cloud-${version}.tar.gz.sha256"
```

The archive contains the connector wheel, the public integration and protocol
wheels, their third-party dependencies, and `source-manifest.json` with the
source revisions used for the build.

## What is inside the archive

| Component | Purpose |
|---|---|
| `ledgermind_cloud` | Connector CLI (`ledgermind-cloud`) |
| `ledgermind_integrations` | Public agent adapters and runtime client |
| `ledgermind_protocol` | Public protocol contracts |
| `source-manifest.json` | Source revisions used for this build |

The archive never contains the managed service: no server package, worker,
database schema, migrations, deployment files, environment files, or provider
credentials.

## Versions

Connector releases use the `cloud-v*` tag line, independent of the
`ledgermind` Local release line. The current connector version is `0.2.0b1`.

## Source

The connector is developed in the private LedgerMind engine monorepo and built
from a clean revision with the published release script. Public inspectable
sources of the pieces the connector links against:

- [ledgermind-integrations](https://github.com/sl4m3/ledgermind-integrations) —
  agent adapters and protocol contracts (Apache-2.0)
- [ledgermind-local](https://github.com/sl4m3/ledgermind-local) — the Local
  runtime and installer source

## Links

- [LedgerMind Cloud](https://ledgermind.org)
- [Install guide](https://ledgermind.org/install)
- [LedgerMind Local](https://github.com/sl4m3/ledgermind)
- [Contact](mailto:s.zotov@ledgermind.org)
