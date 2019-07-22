---
title: "Remove Git Submodule"
date: 2019-07-23T07:55:29+09:00
tags:
  - dev
  - git
summary: Converting a submodule into a regular folder
---

Had problems deploying a [Hugo] site to [Netlify] because of problems with the theme submodule. Found it easier to simply remove it.

```zsh
THEME_PATH = "theme/theme_name"
git rm --cached $THEME_PATH
git rm .gitmodules
rm -rf $THEME_PATH
git add $THEME_PATH
git commit -m "removed theme submodule"
```

[Hugo]: https://gohugo.io
[Netlify]: https://www.netlify.com
