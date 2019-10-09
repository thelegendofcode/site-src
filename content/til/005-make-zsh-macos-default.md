---
title: "005 Make Zsh Macos Default"
date: 2019-10-09T13:26:29+09:00
tags:
  - til
  - zsh
  - macos
---

Probably not necessary anymore now that ZSH is default in Catalina. But it's still something I learned today.

```zsh
brew install zsh
sudo sh -c "echo $(which zsh) >> /etc/shells"
chsh -s $(which zsh)
```
