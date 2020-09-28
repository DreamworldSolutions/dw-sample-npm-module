# How to add new feature or fix to NPM package

- Create a new feature branch from `master`. It must have prefix `feature/`
  - its name **MUST** be into `feature/myFeature` format, where, `myFeature` is your new feature.
  - other example of branch name could be `feature/standardise-buttons`, `feature/restyling`.
- Make changes as needed (as much commits as you want)
  - If you don't want to perform any of release, just don't add above prefixes into commit message.
- Automated release is triggered when commit message has following prefix:
  - `feat`: this would release a minor(feature) version.
  - `fix`: this would release a patch version.
  - `BREAKING CHANGE:` this would release a major version. It **MUST** be in a footer.
  - See [commit message format](https://semantic-release.gitbook.io/semantic-release/#commit-message-format) for more information.
- Snapshot/feature releases are published to NPM repository. Released version is accessible via `myFeature` tag.
  - eg. `"my-package-name": "myFeature"`
  - Performing `npm update @dreamworld/my-package-name` would use latest available version of `myFeature`
  - Notice `myFeature` is the branch name that you created.
