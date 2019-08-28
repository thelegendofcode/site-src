---
title: "Create Hugo Theme Pt 2: Modularisation"
date: 2019-08-25T06:46:16+09:00
tags:
  - dev
  - hugo
summary: This part will deal with splitting templates up into smaller, re-usable modules.
---

Continuing on from [part 1](https://legendofcode.com/posts/008-create-hugo-theme-pt-1/), the last time we completed some basic scaffolding.  I've updated the index.html with some content, as well as creating a new `post` in the contents folder.  The link on the index page will not work, because it's pointing towards a non-existent html file.

Start the dev server with the command `hugo server`

The index page can be accessed at http://localhost:1313
The single page can be accessed at http://localhost:1313/post/single/

Quick explanation, the way single pages are handled, the contents of each post are generated into a `index.html` and placed into the `/posts/` directory. I then updated the `config.toml` with a permalink option to load posts using only the title. The single page can now be accessed at http://localhost:1313/single/
 
```toml
[permalinks]
  post = ":title"
```

## Splitting the template  into parts using `Blocks`
Create a `layouts/_default/baseof.html` file. This is the file that Hugo *bases* all generated html off of.  Copy the contents from `index.html` into `baseof.html`, erase everything between the `<body>` tags , then add a single line `{{ block "main" . }}{{ end }}` . 

```html
<!-- baseof.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>{{ .Title }}</title>
</head>
<body>
  {{ block "main" . }}{{ end }}
</body>
</html>
```

What this does is tell Hugo to load all content that is defined as `main` into this block.

In `index.html`, delete everything outside of the body tags and replaced it like this. Do the same for `single.html`. This defines the content as a `main` block that gets loaded into `baseof.html`. This saves us from repeating the same block of code in every html file.

```html
<!-- index.html -->
{{ define "main" }}
<header class="Header">
...
</footer>
{{ end }}

<!-- single.html -->
{{ define "main" }}
<h1 class="ArticleTitle">
...
</footer>
{{ end }}
```

## Splitting pages up with `Partials`
Since we're splitting stuff up into various parts,  let's do the rest as well. Here, we've created a new `layouts/partials/` folder and add the below 3 html files, `head.html`, `main-header.html`, `main-footer.html`. 

```html
<!-- head.html -->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>{{ .Title }}</title>
</head>

<!-- main-header.html -->
<header class="Header">
  <p class="SiteHeader">
    <h1 class="SiteTitle">
      Legend of Code
    </h1>
    <span class="SiteSubtitle">is the website of</span>
  </p>

  <p class="SiteSecondaryHeader">Sen Heng</p>

  <p class="">
    Front end engineer,<br>
    UX designer,<br>
    based in Tokyo.<br>
  </p>
</header>

<!-- main-footer.html -->
<footer class="Footer">
  <a href="https://github.com/thelegendofcode" class="">github.com/thelegendofcode</a>

  <a href="mailto:sen@legendofcode.com" class="">sen@legendofcode.com</a>

  <a href="https://twitter.com/legendofcode" class="">@legendofcode</a>
</footer>
```

We shall now call the head partial from within `baseof.html`, and the main-header and main-footer from `index.html`.

```html
<!-- baseof.html -->
<!DOCTYPE html>
<html lang="en">
{{ partial "head" . }}
<body>
  {{ block "main" . }}{{ end }}
</body>
</html>

<!-- index.html -->
{{ define "main" }}
{{ partial "main-header" . }}
...
{{ partial "main-footer" }}
{{ end }}
```

## Difference between Blocks and Partials
`Blocks` are a higher level concept, based on default templates. You define blocks within the various templates like `single.html`, `list.html`  with the define command, like so `{{ define "main" }}`. Later, you use those blocks by calling them out from the `baseof.html` template using the block command `{{ block "main" }}`.

If you were to define a footer `Block`, presumably in a `footer.html` like this.
```html
{{ define "footer" }}
this is a footer!
{{ end }}
```

It wouldn't do anything, because footer is not a template.

`Partials` are basically the splitting up of a template into multiple parts, especially parts that can be reused. Like say, a `footer.html` or a `nav.html`. You can then re-use these `Partials` in the other templates.

[Part 3](https://legendofcode.com/create-hugo-theme-pt-3-page-variables/) will deal will generating single pages from data.
