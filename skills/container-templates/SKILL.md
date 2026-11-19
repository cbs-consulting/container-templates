---
name: container-templates
description: >-
  Starts a new SAP BTP or CAP project from the cbs Dev Container Templates
  (ghcr.io/cbs-consulting/container-templates), and fixes a template container or
  generator that does not start. Use when the user wants to create a new BTP, CAP or
  UI5 project in a dev container, asks for a cbs template such as btp-generator, or
  reports a problem with one.
license: Apache-2.0
---

# cbs Dev Container Templates

A template turns an empty folder into a dev container. On first start, the container runs
a project generator. The generator writes the real project, including its own
`devcontainer.json`, and the user then rebuilds the container into that project
environment. The README of <https://github.com/cbs-consulting/container-templates> lists
the templates and the ways to apply them; read it instead of guessing.

## Pick a template

| Template | Use it for |
| --- | --- |
| `btp-generator` | A new SAP BTP project. Runs `yo @cbs-consulting/btp` interactively. |

If the README lists templates that are not in this table, the README is right.

## Check before you apply

1. **The folder is new or empty.** Run `ls -A`. If it has files, ask the user before you
   go on. Never overwrite an existing `.devcontainer/`; suggest a new folder instead.
2. **Docker runs.** `docker info` must succeed. If it fails, ask the user to start Docker
   Desktop, Rancher Desktop or Podman with Docker compatibility. Don't install Docker for
   them.
3. **A way to open the container.** Either VS Code with the Dev Containers extension, or
   the Dev Container CLI (`devcontainer --version`; install with
   `npm install -g @devcontainers/cli`).

## Apply the template

With the CLI, from inside the new folder:

```bash
devcontainer templates apply \
  --template-id ghcr.io/cbs-consulting/container-templates/btp-generator \
  --workspace-folder .
```

In VS Code the user runs **Dev Containers: Add Dev Container Configuration Files…**,
chooses **Show All Definitions** and enters the same template ID. If the CLI is missing
and the user does not want it, they can also copy `src/<template>/.devcontainer/` from the
repository.

## Hand over the first start

The generator asks the user questions about their project. It needs an interactive
terminal, and only the user knows the answers. So don't start the container from your own
shell, and don't answer the questions for the user. Tell them to:

1. Open the folder in VS Code and choose **Reopen in Container**, or run
   `devcontainer up --workspace-folder .` in their own terminal.
2. Answer the generator's questions.
3. Run **Dev Containers: Rebuild Container** when the setup prints
   "Setup complete". The folder then opens in the project's own environment.

After the rebuild the template is done. The project's `devcontainer.json` belongs to the
project now; change it there, not in the template.

## When something fails

| Symptom | What to do |
| --- | --- |
| `denied` or `unauthorized` when pulling from `ghcr.io` | The templates and features are public. A stale login causes this: run `docker logout ghcr.io` and try again. |
| Pull hangs or times out | Check the network or the corporate proxy with the user. Docker needs the proxy too, not only the shell. |
| `npm install -g yo @cbs-consulting/generator-btp` fails | Usually the npm registry or proxy. In the container terminal run `npm config get registry` and retry the install. |
| The generator stopped or the user cancelled it | In the container terminal run `yo @cbs-consulting/btp` again, then rebuild the container. |
| After the rebuild the generator starts again | The project's `devcontainer.json` was not written, so the template's file is still used. Check that the generator finished and wrote `.devcontainer/devcontainer.json`. |

For anything else, look at the container log (VS Code: **Dev Containers: Show Container
Log**) before you change files. Report bugs in a template at
<https://github.com/cbs-consulting/container-templates/issues>.
