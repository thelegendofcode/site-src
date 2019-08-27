---
title: "How to delete a git tag"
date: 2019-08-28T00:09:00+09:00
tags:
  - dev
  - git
---

Delete remote tags

```zsh
$ git push origin :tag_name

# or to be more precise

git push --delete origin tag_name

# or if there's a branch with the same name

git push --delete origin :refs/tag/tag_name
```

Delete local tags
```zsh
git tag --delete tag_name
```

Source: https://stackoverflow.com/a/5480292
