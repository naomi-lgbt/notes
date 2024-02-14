# Label Templates

These are the templates I use for loading labels into a new repository.

## Default Labels

These are my default labels, present on ALL repositories. These are based on the [Creative Commons Labelling Standards](https://opensource.creativecommons.org/contributing-code/repo-labels/).

```json
[
  {
    "name": "🟥 priority: critical",
    "description": "Must be fixed ASAP",
    "color": "b60205"
  },
  {
    "name": "🟧 priority: high",
    "description": "Stalls work on the project or its dependents",
    "color": "ff9f1c"
  },
  {
    "name": "🟨 priority: medium",
    "description": "Not blocking but should be fixed soon",
    "color": "ffcc00"
  },
  {
    "name": "🟩 priority: low",
    "description": "Low priority and doesn't need to be rushed",
    "color": "cfda2c"
  },
  {
    "name": "🟪 priority: none",
    "description": "No priority, should only be performed when a developer is available",
    "color": "008672"
  },
  {
    "name": "🏁 status: ready for dev",
    "description": "Ready for work",
    "color": "cccccc"
  },
  {
    "name": "🚧 status: blocked",
    "description": "Blocked and therefore not ready for work",
    "color": "999999"
  },
  {
    "name": "🧹 status: ticket work required",
    "description": "Needs more details before it can be worked on",
    "color": "666666"
  },
  {
    "name": "🏷 status: label work required",
    "description": "Needs proper labelling before it can be worked on",
    "color": "666666"
  },
  {
    "name": "🙅 status: discontinued",
    "description": "Not suitable for work as repo is in maintenance",
    "color": "eeeeee"
  },
  {
    "name": "⛔️ status: discarded",
    "description": "Will not be worked on",
    "color": "eeeeee"
  },
  {
    "name": "🚦 status: awaiting triage",
    "description": "Has not been triaged & therefore, not ready for work",
    "color": "333333"
  },
  {
    "name": "⭐ goal: addition",
    "description": "Addition of new feature",
    "color": "ffffff"
  },
  {
    "name": "✨ goal: improvement",
    "description": "Improvement to an existing feature",
    "color": "ffffff"
  },
  {
    "name": "🛠 goal: fix",
    "description": "Bug fix",
    "color": "ffffff"
  },
  {
    "name": "📄 aspect: text",
    "description": "Concerns the documentation material in the repository",
    "color": "04338c"
  },
  {
    "name": "💻 aspect: code",
    "description": "Concerns the software code in the repository",
    "color": "04338c"
  },
  {
    "name": "🕹 aspect: interface",
    "description": "Concerns end-users' experience with the software",
    "color": "04338c"
  },
  {
    "name": "🤖 aspect: dx",
    "description": "Concerns developers' experience with the codebase",
    "color": "04338c"
  },
  {
    "name": "❓ talk: question",
    "description": "Can be resolved with an answer",
    "color": "f9bbe5"
  },
  {
    "name": "💬 talk: discussion",
    "description": "Open for discussions and feedback",
    "color": "f9bbe5"
  },
  {
    "name": "good first issue",
    "description": "New-contributor friendly",
    "color": "7f0799"
  },
  {
    "name": "help wanted",
    "description": "Open to participation from the community",
    "color": "7f0799"
  },
  {
    "name": "🔒 staff only",
    "description": "Restricted to project staff members",
    "color": "7f0799"
  },
  {
    "name": "🧠 Mentorship",
    "description": "Reserved for someone I am mentoring.",
    "color": "7f0799"
  }
]
```

## Pull Request Labels

I usually include these labels with the default labels, but these ones are applied to pull requests by an [action](/github-workflows/pr-labeller.md).

```json
[
  {
    "name": "🔍 pull: ready for review",
    "description": "PR is ready for maintainer review.",
    "color": "00FF00"
  },
  {
    "name": "⚠️ pull: merge conflict",
    "description": "PR has conflicts and requires a rebase.",
    "color": "FFFF00"
  },
  {
    "name": "⏫ pull: requires update",
    "description": "PR has requested changes that still need to be applied.",
    "color": "FF0000"
  },
  {
    "name": "⚒️ pull: work in progress",
    "description": "PR is still being worked on and is not ready for review.",
    "color": "cc00cc"
  },
    {
    "name": "✅ pull: accepted",
    "description": "PR has been merged. Thank you for your contribution!",
    "color": "ffffff"
  },
  {
    "name": "❌ pull: rejected",
    "description": "PR has been closed. We would welcome future contributions!",
    "color": "ffffff"
  },
];
```

## Hacktoberfest Labels

These labels are applied when I opt in a project for the [Hacktoberfest event](https://hacktoberfest.digitalocean.com/).

```json
[
  {
    "name": "invalid",
    "description": "Inappropriate or invalid for Hacktoberfest contributions",
    "color": "eeeeee"
  },
  {
    "name": "Hacktoberfest",
    "description": "Good issues for Hacktoberfest participants",
    "color": "883255"
  }
]
```

## Skill Labels

This template is used to create `skill` labels, which help contributors identify the skills needed to resolve an issue so they can find issues that match their skillset.

To use this, replace `skillname` with the skill (i.e. `TypeScript` or `Angular`), then add this object to your `labels` array.

```json
{
  "name": "💪 skill: <skillname>",
  "description": "Requires proficiency in <skillname>",
  "color": "5ff1f5"
}
```

## Miscellaneous Labels

This template is used for miscellaneous uncategorised labels. Miscellaneous labels should still follow the same standard naming conventions.

```json
{
  "name": "<emoji> <category> <name>",
  "description": "text here",
  "color": "000000"
}
```
