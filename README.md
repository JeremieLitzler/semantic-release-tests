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

Also, in version 2.0.3, I added two temporary rules, to use on new projects up to the first major release.

They allow to bump the patch until you remove or update them to release the first major:

```json
          {
            "breaking": true,
            "release": "patch"
          },
          {
            "type": "feat",
            "release": "patch"
          },
```

BTW: to find the syntax for the `releaseRules`, checkout `node_modules\@semantic-release\commit-analyzer\lib\default-release-rules.js` ;)

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

PS: for the `feat` and `BREAKING CHANGE`, I didn't make any updates to the changelog configuration. It can stay as it is, whether you're passed your first major release or not.
