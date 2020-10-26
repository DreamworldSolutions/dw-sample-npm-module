# Update package's type to module

Simply updateing package.json to be type=module will fail, as semantic-release intally `requires` release.config.js file via `require` method, which would fail with following error:

> [11:37:37 AM] [semantic-release] › ✖  An error occurred while running semantic-release: Error [ERR_REQUIRE_ESM]: Must use import to load ES Module: /home/circleci/project/release.config.js
> require() of ES modules is not supported.
> require() of /home/circleci/project/release.config.js from /home/circleci/project/node_modules/import-fresh/index.js is an ES module file as it is a .js file whose nearest parent package.json contains "type": "module" which defines all .js files in that package scope as ES modules.
> Instead rename release.config.js to end in .cjs, change the requiring code to use import(), or remove "type": "module" from /home/circleci/project/package.json.

To fix it, we just don't use `release.config.js` and instead, move it to `package.json`

- Update `package.json` to have: `"type": "module"`
- Make updates as per [this commit](https://github.com/DreamworldSolutions/dw-sample-npm-module/commit/1f8c8a1dd0dbec7a477644578b08597c777a0880)
    - Move `release` configuration from `release.config.js` to `package.json`
    - Delete `release.config.js` file
    - `.circleci/config.yml`: Use node 14
