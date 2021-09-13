# Sample NPM package

A Sample NPM package with automated deployment based on branches to NPM for both release snapshot releases.

## Docs
- [How to setup automated CI/CD for package new or existing project](docs/howto-setup-automated-release.md)
- [How to add new feature or fix](docs/howto-add-new-feature-or-fix.md)
- [How to release final version](docs/howto-release-final-version.md)
- [How to update type to `module`](docs/howto-type-module.md)

> To skip automated release (CI/CD pipeline), add `[ci skip]` into your git commit message.

## Troubleshooting

### Pipeline fails with `Error [ERR_REQUIRE_ESM]: Must use import to load ES Module:`

Refer to [this document.](docs/howto-type-module.md)

### Pipeline completes, but doesn't release new version saying "This run was triggered by a pull request and therefore a new version won't be published."

When there is a Pull Request open for the branch, CircleCI would consider it as if its run from the PR, so semantic-release would not be able to release the version.

To fix it, just temporary close the PR and trigger the Pipeline again. Once its complete, you can re-open the same PR.
