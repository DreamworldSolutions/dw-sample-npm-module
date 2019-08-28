# How to setup automated CI/CD for package new or existing project

- Create initial project with your desired build tool.
- .gitignore:
  - make sure `package-lock.json` is ignored
- Update package.json for followings:
  - name:
    - Must be with `@dreamworld` scope.
      - eg. "name": "@dreamworld/dw-sample-npm-module"
  - version:
    - Must be `"version": "0.0.0-development"`
  - devDependencies: Add `semantic-release` with `beta` version
```
  "devDependencies": {
    "semantic-release": "beta"
  }
```
  - publishConfig:
```
  "publishConfig": {
    "access": "public"
  }
```
- Copy `.circleci` folder from this project to root directory of your project
- Copy `release.config.js` from this project to root directory of your project
- Create GitHub project
- Push this project to Github
- Setup CircleCI for automated deployment
  - Open [CircleCI dashboard](https://circleci.com/add-projects/gh/DreamworldSolutions)
  - Find this newly created project
  - Click on `Setup Project` button
  - Click on `Start Building` button

## Setup for existing projects
- You would need to follow all the steps as above, excluding initial project creating and Github repository.
- You would also need to create a Git tag of last release to appropriate commit.
  - it should be in vMajor.Minor.Patch format. (`v` is prefix)
  - eg. `v1.2.0`
- Based on this latest tag, it would automatically determine next release versions.


## Notes
- You would never need to update your package version in package.json file. It would always stay as above.
