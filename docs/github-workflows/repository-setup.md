# Repository Setup

These are the settings I tweak on each repository I create. Repositories are always created from the [`new-repo-template`](https://github.com/nhcarrigan/new-repo-template).

## Main Settings

Change these settings on the repository home view:

- Disable `releases`
- Disable `packages`
- Disable `environments` (UNLESS going to deploy on GH Pages)
- Add `description`, `topics`, and `url`.

Change these settings on the `options` page:

- Disable `Wikis`
- Disable `Projects`
- Disable `Allow Merge Commits`
- Disable `Allow Rebase Merging`
- Enable `Automatically delete head branches`

This will require that "squash and merge" be used on PRs, and that branches on the repo are auto-deleted on merge.

## Branches Settings

Change these settings on the `branches` page:

- Set `Branch name pattern` to `main`
- Enable `Require pull request reviews before merging`
  - Enable `Dismiss stale pull request approvals when new commits are pushed`
- Enable `Require status checks to pass before merging`
  - Enable `Require branches to be up to date before merging`
  - Add any GitHub Actions to the status checks selection area
- Click `Create` to save!

These settings will ensure that PRs are running on the latest state on `main`, that the actions all pass, and that at least one maintainer has approved the PR.

## Webhooks Settings

- Add the `discord-integrations` webhook to get notifications for the repository.
