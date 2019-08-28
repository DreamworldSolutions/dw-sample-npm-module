# How to release final version of NPM package

- Submit merge request from your feature branch into `master` branch
- Make sure that your merge request commit message has desired prefix to determine version.
  - see prefix guide [here](./howto-add-new-feature-or-fix.md)
- Once accepted, it would trigger CI/CD Pipeline and release on NPM with final version.
- Pipeline would also tag version number to Github project

## How tags work
- Version is incremented automatically from last git tag.
- Git tag format is `v1.0.0`
