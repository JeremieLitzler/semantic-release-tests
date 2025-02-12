This repo simply taught me when semantic release decides to create a new release or not.

It works with conventional commits. But semantic release doesn't create new releases on following types:

- `docs`
- `test`
- `refactor`

So I added them to the `releaseRules` on this repo:

```json
        "releaseRules": [
          {
            "type": "docs",
            "release": "patch"
          },
          {
            "type": "test",
            "release": "patch"
          },
          {
            "type": "refactor",
            "release": "patch"
          }
        ],
```

Following this, we also need to add the `release-notes-generator` configuration:

```json
[
  "@semantic-release/release-notes-generator",
  {
    "preset": "conventionalcommits",
    "presetConfig": {
      "types": [
        {
          "type": "feat",
          "section": "Features"
        },
        {
          "type": "fix",
          "section": "Bug Fixes"
        },
        {
          "type": "docs",
          "section": "Others"
        },
        {
          "type": "refactor",
          "section": "Others"
        },
        {
          "type": "test",
          "section": "Others"
        },
        {
          "type": "chore",
          "hidden": true
        },
        {
          "type": "style",
          "hidden": true
        }
      ]
    }
  }
]
```
