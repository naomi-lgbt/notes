# Angular Deploy

This script will deploy an Angular app to GitHub Pages using the `angular-cli-ghpages` tool. Deployments are triggered on push to `main`, so this will run if you commit directly to `main` or merge a PR into `main`.

```yaml
name: Deploy to GitHub Pages via angular-cli-ghpages

on:
  push:
    branches: ["main"]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Use Node.js 16.x
        uses: actions/setup-node@v3
        with:
          node-version: 16.x

      - name: Prepare and deploy
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          npm ci
          npm run deploy
```

## Angular Setup

To use this with your Angular project, you'll need to install the CLI package with `npm i angular-cli-ghpages`. Then, in your `package.json`, add a script `deploy: "ng deploy"`.

Finally, configure your `angular.json` settings to use the CLI tool (this goes nested in the same level as your other script settings, such as `e2e`):

```json
"deploy": {
  "builder": "angular-cli-ghpages:deploy",
  "options": {
    "baseHref": "https://www.nhcarrigan.com",
    "cname": "www.nhcarrigan.com",
    "name": "Naomi Carrigan",
    "email": "nhcarrigan@gmail.com"
}
```

The `options` values are configurable. The `baseHref` is used to tell Angular what your root URL will be for the project, which affects the build step. The `cname` value adds a CNAME file to set the custom domain for the GitHub Pages settings (this is optional). The `name` and `email` are tied to the commit to the `gh-pages` branch.

> [!WARNING]
> The `name` and `email` should match your GitHub name and email EXACTLY.
