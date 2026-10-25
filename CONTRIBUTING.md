# Contributing

Thank you for helping to improve the cbs Dev Container Templates. This guide
explains how to propose a change.

By taking part in this project you agree to follow our
[Code of Conduct](CODE_OF_CONDUCT.md). To report a security problem, follow the
[Security Policy](SECURITY.md) instead of opening an issue.

## Reporting bugs and requesting features

Search the [existing issues](https://github.com/cbs-consulting/container-templates/issues)
first. If nothing matches, open a new issue with the bug report or feature
request form. For a larger change, such as a new Template, open an issue before
you start so we can agree on the approach.

## Making a change

1. Fork the repository and create a branch from `main`.
2. Open the repository in its dev container. It comes with Node.js, Docker and
   the [Dev Container CLI](https://github.com/devcontainers/cli) preinstalled.
   Outside the container, install the CLI with
   `npm install -g @devcontainers/cli`.
3. Make your change. Each Template lives in `src/<template>/` and contains a
   `devcontainer-template.json` plus a `.devcontainer/` folder. See the
   [Templates specification](https://containers.dev/implementors/templates/)
   for the format.
4. Bump the `version` in the Template's `devcontainer-template.json`, following
   [Semantic Versioning](https://semver.org/).
5. Test the Template in a temporary folder. Copy its `.devcontainer/` folder
   there and start the container:

   ```sh
   mkdir -p /tmp/template-test
   cp -r src/<template>/.devcontainer /tmp/template-test/
   devcontainer up --workspace-folder /tmp/template-test
   ```

   If the Template has options, replace their `${templateOption:...}`
   placeholders with test values in the copy first.

6. Update [README.md](README.md) if you added a Template or changed how one
   behaves.
7. Open a pull request against `main` and fill in the template.

## Commit messages

Use [Conventional Commits](https://www.conventionalcommits.org/), for example
`feat(btp-generator): add Java feature` or `fix: correct registry namespace`.
Keep each pull request to one topic; it is squashed into a single commit when
merged.

## License

By contributing you agree that your contribution is licensed under the
[Apache License 2.0](LICENSE), the license of this project.
