---
title: "Shebang Node"
date: 2019-07-22T12:36:19+09:00
tags:
  - til
  - node
summary: Launch a nodejs executable from the terminal
---

```zsh
#!/usr/bin/env node
```

`#!` (pronounced *shebang*) tells the system what interpreter to pass that file to for execution. When a file has the above line is included, the system (*nix) will use Node.js to execute the file. This only works because Node makes a special exception for shebang characters. This will not work in a browser.

example file without .js extension
```js
// hello
#!/usr/bin/env node

console.log('hello node env');
```

```zsh
$ chmod +x ./hello
$ ./hello
$ hello node env
```
