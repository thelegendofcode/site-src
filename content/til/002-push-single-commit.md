---
title: "Push Single Commit"
date: 2019-06-26T16:36:19+09:00
tags:
  - til
  - git
summary: Pushing a single commit out of a series of commits into a remote branch.
---

Pushing a single commit out of a series of commits into a remote branch.

```zsh
# git push <REMOTE_NAME> COMMIT_SHA1:REMOTE_BRANCH_NAME
$ git push origin 1q2w3e:branch-name
```
