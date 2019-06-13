---
title: "Hugo Theme Two"
date: 2019-06-14T00:51:49+08:00
tags:
  - hugo
  - development
---

There doesn't seem to be a lot of info out there about creating a theme in Hugo so I've been reading the docs to figure out how the various [functions] and [variables] work. So here's a list of things I figured out while on a plane flying eight hours to attend my cousin's wedding.


## New theme scaffolding

```bash
hugo new theme fantasy
```

This command creates a new theme called `fantasy` within the themes folder. You should know that it's quite sparse. The basic directory structure is all setup and a few html files are created, but the html files are blank.

Generating with this theme essentially creates a *blank* page. Fear the white canvas!

## Partials

`partial` is how Hugo splits a page into partials. The structure is basically

```
{{ partial "path/name" $CONTEXT}}
```

So something like this.

```html
<!-- index.html -->
{{ partial "header" . }}
<p>something in between</p>
{{ partial "footer" . }}


<!-- header.html -->
<h1>I am a header</h1>


<!-- footer.html -->
<span>I am a footer</span>
```

Generates a html like this.

```html
<h1>I am a header</h1>
<p>something in between</p>
<span>I am a footer</span>
```

`partial` seems to automagically refer to anything within the `layouts/partials` directory. You can even refer to a partial from a partial, like so.

```html
<!-- header.html -->
<h1>{{ partial "nested" . }}</h1>


<!-- nested.html -->
<p> I am nested within header </p>


<!-- generates this -->
<h1><p> I am nested within header </p></h1>
```

## The Dot
The dot is basically like `this` in Javascript. It refers to the current context. Using the same example as in partials, it basically means 'pass in all data from index into header'. Using just `.` passes in the global context, basically **everything**. You can also pass in something more specific, like only page contents using the [.Page] variable. This is useful when your partial is only generating something limited, like say a list of posts or tags.

```html
{{ partial "nested" .Page }}
```

## Looping things

You can loop using the `range` keyword.

```html
<!-- $ARRAY := [1, 2, 3] -->
{{ range $ARRAY }}
  <span>{{ . }}</span>
{{ end }}

<!-- generates -->
<span>1</span>
<span>2</span>
<span>3</span>
```

## Things I couldn't figure out

- how to get SASS to work
- how to get postcss to work

My excuse was that I was on a plane flying over open water with ~~no~~ ridiculously expensive internet access. Downloading NPM packages didn't really seem worth the costs.

## Next action
I've messed around with it enough to get something sort of working. I should probably spend a couple days working on a design.

[variables]: https://gohugo.io/variables/
[functions]: https://gohugo.io/functions/
[.Page]: https://gohugo.io/variables/page/#pages
