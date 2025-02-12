This repo simply taught me when semantic release decides to create a new release or not.

It works with conventional commits. But semantic release doesn't create new releases on following types:

- `docs`
- `test`

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
          }
        ],
```

Following this, we also need to add the `release-notes-generator` configuration:

```json
    [
      "@semantic-release/release-notes-generator",
      {
        "preset": "conventionalcommits",
        //REQUIRED ⬇️ because of [the comment at the bottom of the package docs](https://github.com/semantic-release/release-notes-generator?tab=readme-ov-file#configuration)
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
              "type": "chore",
              "hidden": true
            },
            {
              "type": "docs",
              "section": "Others"
            },
            {
              "type": "style",
              "hidden": true
            },
            {
              "type": "refactor",
              "section": "Others"
            },
            {
              "type": "perf",
              "section": "Others"
            },
            {
              "type": "test",
              "section": "Others"
            }
          ]
        }
      }
    ],

```
