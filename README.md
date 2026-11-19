<div align="center">

<img src=".github/assets/logo.svg" alt="" width="120" />

# cbs Dev Container Templates

**Start a new SAP BTP project in a pre-configured container, in minutes.**

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![GHCR](https://img.shields.io/badge/ghcr.io-cbs--consulting%2Fcontainer--templates-0F4C5C?logo=github)](https://github.com/orgs/cbs-consulting/packages?repo_name=container-templates)
[![Dev Containers spec](https://img.shields.io/badge/spec-containers.dev-2496ED?logo=docker&logoColor=white)](https://containers.dev/implementors/templates/)

</div>

---

Dev Container Templates give you a complete `.devcontainer/` setup for an empty folder. They are built on [cbs container-features](https://github.com/cbs-consulting/container-features) and published to `ghcr.io/cbs-consulting/container-templates`.

## 📦 Templates

| Template | Description |
| --- | --- |
| [`btp-generator`](src/btp-generator) | Scaffolding environment with `yo` and `@cbs-consulting/generator-btp`. Runs the generator interactively on first start. |

## 🚀 Usage

### Option 1: VS Code

1. Open an empty folder in VS Code.
2. Run **Dev Containers: Add Dev Container Configuration Files…**
3. Choose **Show All Definitions**, then enter `ghcr.io/cbs-consulting/container-templates/btp-generator`.
4. Reopen the folder in the container. The generator starts automatically.

### Option 2: Dev Container CLI

```bash
mkdir my-btp-app && cd my-btp-app
devcontainer templates apply \
  --template-id ghcr.io/cbs-consulting/container-templates/btp-generator \
  --workspace-folder .
devcontainer up --workspace-folder .
```

### Option 3: Copy manually

Copy [`src/btp-generator/.devcontainer/`](src/btp-generator) into your project.

### Option 4: Ask your coding agent

This repository is also an agent plugin. Its skill teaches a coding agent to check Docker, apply a Template to an empty folder and help when the container or the generator does not start. Install it from the [cbs Agentic Marketplace](https://github.com/cbs-consulting/agentic-marketplace):

```text
/plugin marketplace add cbs-consulting/agentic-marketplace
/plugin install container-templates@cbs-consulting
```

That is Claude Code; the marketplace README has the steps for Codex, GitHub Copilot CLI and other agents. Then ask, for example, "Start a new BTP project in a dev container". You still answer the generator's questions yourself.

## 🔁 Typical workflow

```text
empty folder ──► apply btp-generator ──► open in container ──► generator scaffolds your app
```

When the generator finishes, your project already contains its own `devcontainer.json` based on the cbs Features.

## 🧩 Related

- [**container-features**](https://github.com/cbs-consulting/container-features): the building blocks these Templates use

## 🛠️ Contributing

Templates live in `src/<template>/` and contain a `devcontainer-template.json` plus a `.devcontainer/` folder. The agent skill lives in `skills/container-templates/`, with the plugin manifests `plugin.json` and `.claude-plugin/plugin.json`. Test a Template locally with `devcontainer templates apply` against a temporary folder.

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to propose a change, and follow the [Code of Conduct](CODE_OF_CONDUCT.md). Report security problems privately as described in [SECURITY.md](SECURITY.md).

## 📄 License

Copyright © 2026 cbs Corporate Business Solutions Unternehmensberatung GmbH.
Licensed under the [Apache License 2.0](LICENSE).

<sub>SAP and SAP BTP are trademarks of SAP SE. This project is not affiliated with or endorsed by SAP.</sub>
