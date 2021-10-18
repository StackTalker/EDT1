
# check-git-status-action

[![Test](https://github.com/CatChen/check-git-status-action/actions/workflows/test.yml/badge.svg)](https://github.com/CatChen/check-git-status-action/actions/workflows/test.yml)
[![Ship](https://github.com/CatChen/check-git-status-action/actions/workflows/ship.yml/badge.svg)](https://github.com/CatChen/check-git-status-action/actions/workflows/ship.yml)

Do you check in dependency packages or build artefacts? If yes this GitHub Action helps you ensure they are not out-of-sync. Examples:

1. Say we set up to [run Yarn offline](https://classic.yarnpkg.com/blog/2016/11/24/offline-mirror/) and we check in Yarn offline mirror. We want to make sure the offline mirror is in sync with the dependencies declared in the `package.json`. We can set up a GitHub Workflow to run `yarn install` and then use this Action to check if the offline mirror is changed.
2. Say we generate TypeScript type definitions from [JSON Schemas](https://json-schema.org/). The generated TypeScript files are part of the codebase. We want to make sure people remember to regenerate these files when they modify any JSON Schema. We can use a GitHub Workflow to run the code generation and then use this GitHub Action to check if the files are changed. If they are changed this Action can commit the changes and add them to the Pull Request.

## Usage

Set up a GitHub Action like this:

```yaml
name: Verify Build

on:
  pull_request:
    branches: [main] # or [master] if that's name of the main branch

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3