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
