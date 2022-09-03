# How to setup setup a new project
- Create New GitHub repo with readme file.
- Clone repo to your workspace and perform following steps in your workspace.
- Initialize npm package with your desired build tool. e.g. `npm init`
  - Set your package group/scope to `@dreamworld`. e.g. `"name": "@dreamworld/dw-sample-npm-module"`
  - Set version to `0.0.0-development`
- Add `publishConfig` to `package.json`.
```
  "publishConfig": {
    "access": "public"
  }
```
- Copy/Add `.gitignore`. Make sure that `package-lock.json` is added to `.gitignore`. And `yarn.lock` **is not ignored**.
- Integrate `semantic-release` and `circleci`.
- Add semantic-release:
  - Add following `devDependencies` and `release` configuration to `package.json`.

```
  "devDependencies": {
    "semantic-release": "17.0.8"
  },
  "release": {
    "branches": [
      "+([0-9])?(.{+([0-9]),x}).x",
      "master",
      {
          "name": "feature/*",
          "prerelease": "${name.replace(/^feature\\//g, \"\")}",
          "channel": "${name.replace(/^feature\\//g, \"\")}"
      }
    ]
  }
```

- [Optional] If its an ES module, add `"type": "module"` in package.json.

- Copy `.circleci` folder from this project to root directory of your project
- Commit this changes and push to `master` branch. Make sure that semantic-prefix `fix:`, `feat:` etc. are NOT applied
to this commit message.
- Setup CircleCI for automated deployment. **Can be done by Admin only. So, Ask Chirag to perfomr this step**
  - Open [CircleCI dashboard](https://circleci.com/add-projects/gh/DreamworldSolutions)
  - User your Github account to login. (signup for CircleCI if you haven't)
  - Find this newly created project.
  - Click on `Setup Project` button.
  - Click on `Start Building` button.
- Follow the circle-ci project & Ask other team members to do the same to watch logs & get notified on new build.
- Create your first feature branch to start developing initial feature. e.g. `feature/init`. Follow this guideline for
snapshot version deployment during feature development.
- When this feature branch is merged to `master` with commit message is prefixed with `feat:` first version `1.0.0` is
released to the public NPM registry.

# Setup for existing projects
- Make sure that your package name is `@dreamworld/xxx`.
- Change version to `0.0.0-development`.
- Follow same steps from above guide from `Initialize npm package ...` steps.
- You would also need to create a Git tag of last release to appropriate commit.It should be in vMajor.Minor.Patch
format. (`v` is prefix) eg. `v1.2.0`. Based on this latest tag, it would automatically determine next release versions.
**This step can be safely skipped if no version is yet released.**

# Setup for Forked repository
- Same as above "Setup for existing projects", but make sure to update the repository URLs in `package.json` as well.

# Setup for typescript repository
For any Javascript NPM package, we just publish the source code to NPM registry. But for Typescript projects, they need to be complied accordingly.

- Same as above "Setup for existing projects"
- Configure pipeline to build the package in the `circleci/config.yml` file, before releasing the package.

See this [DreamworldSolutions/addon-redux](https://github.com/DreamworldSolutions/addon-redux/pull/1) repository that we forked and setup CircleCI Pipeline.
- [Commit1](https://github.com/DreamworldSolutions/addon-redux/commit/9667e0189c8f45ce60087d1080f073eeb60f1a00)
- [Commit2](https://github.com/DreamworldSolutions/addon-redux/commit/dffc492cf38d1c6518bff65f595e0056af561a8c)

## Notes
- You would never need to update your package version in `package.json` file. It would always stay as above.
