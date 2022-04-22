# Node CI

This is a continuous integration suite designed for a TypeScript powered Node.js application. It will run the `lint`, `build`, and `test` steps.

> [!ATTENTION]
> By default, the `npm init` generated `package.json` file will include a `test` script. This script will throw an exit code 1 which will fail this workflow. I recommend changing the script to something like `"echo 'No tests yet'"`.

```yaml
name: Node.js CI
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  ci:
    name: Lint / Build / Test
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [16.x]

    steps:
      - name: Checkout Source Files
        uses: actions/checkout@v3

      - name: Use Node.js v${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}

      - name: Install Dependencies
        run: npm ci

      - name: Lint Source Files
        run: npm run lint

      - name: Verify Build
        run: npm run build

      - name: Run Tests
        run: npm run test
```

If you are missing any of these scripts in your `package.json` the workflow will fail.
