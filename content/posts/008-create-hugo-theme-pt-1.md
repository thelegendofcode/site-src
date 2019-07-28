---
title: "Creating a Hugo theme from scratch, part 1"
date: 2019-07-26T00:50:14+09:00
tags:
  - dev
  - hugo
---

repo: https://github.com/SenHeng/ThemeOfTheAncients.git

Let's start with the scaffolding. The usual command is `hugo new site $SITE_NAME`, but I've often found myself needing to create one within an already existing directory, so this here is my preferred method.

```zsh
# 1. Create a directory
mkdir hugo_theme
# 2. Move into the directory
cd $_
# 3. Create a new Hugo site within the directory
hugo new site . --force
```

The below files and directory generated. Check the Hugo docs for an explaination of the [directory structure].

```zsh
.
├── archetypes
├── config.toml
├── content
├── data
├── layouts
├── static
└── themes
```

Since we're building a theme and not a standard site, we can remove `/data` and `/themes` as they serve no purpose here.

```zsh
rm -rf data themes
```

## Initial html file

Now that the initial set up is done, let's make sure everything works.

First we'll set the page title  in `config.toml`.

```toml
title = "Theme of the Ancients"
```

Followed by creating a simple HTML file named `index.html` in the `/layouts` directory that displays a single `hello hugo` on the page.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>{{ .Title }}</title>
</head>
<body>
  hello hugo
</body>
</html>
```

Now let's build the site by running `hugo server` in the terminal.

```zsh
                   | EN
+------------------+----+
  Pages            |  4
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  0
  Processed images |  0
  Aliases          |  0
  Sitemaps         |  1
  Cleaned          |  0

Total in 5 ms
Watching for changes in /Users/sen/projects/ThemeOfTheAncients/{content,layouts,static}
Watching for config changes in /Users/sen/projects/ThemeOfTheAncients/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Success! Let's load `http://localhost:1313` in the browser. 

![hello hugo](/static/images/hello-hugo.png)

Congratulations, you have the beginnings of a Hugo Theme.

[directory structure]: https://gohugo.io/getting-started/directory-structure/
