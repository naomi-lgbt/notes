# PR Labeller

This is a simple workflow to automatically manage the labels on pull requests. This is intended to pair with the [PR labels](/transfer-labels/templates.md#pull-request-labels).

```yml
name: "Pull Request Labeller"
on:
  pull_request_target:
    types:
      - closed
      - opened
      - reopened
      - synchronize
      - converted_to_draft
      - ready_for_review
      - review_requested
      - review_request_removed

jobs:
  label:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/github-script@v6
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          script: |
            const prNumber = context.issue.number;
            const pull = await github.rest.pulls.get({
              owner: context.payload.repository.owner.login,
              repo: context.payload.repository.name,
              pull_number:  context.issue.number
            });
            if (pull.data.state === "closed") {
              if (pull.data.merged) {
                await github.rest.issues.setLabels({
                  owner: context.payload.repository.owner.login,
                  repo: context.payload.repository.name,
                  issue_number: context.issue.number,
                  labels: ["✅ pull: accepted"]
                })
              }
              else {
                await github.rest.issues.setLabels({
                  owner: context.payload.repository.owner.login,
                  repo: context.payload.repository.name,
                  issue_number: context.issue.number,
                  labels: ["❌ pull: rejected"]
                })
              }
            } else if (pull.data.draft) {
              await github.rest.issues.setLabels({
                owner: context.payload.repository.owner.login,
                repo: context.payload.repository.name,
                issue_number: context.issue.number,
                labels: ["⚒️ pull: work in progress"]
              })
            } else {
              await github.rest.issues.setLabels({
                owner: context.payload.repository.owner.login,
                repo: context.payload.repository.name,
                issue_number: context.issue.number,
                labels: ["🔍 pull: ready for review"]
              })
            }
```
