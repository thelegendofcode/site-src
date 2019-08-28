---
title: "Create Hugo Theme Pt 3: Page Variables"
date: 2019-08-27T00:42:14+09:00
tags:
  - dev
  - hugo
summary: In today's episode, we learn how to generate a single page template using Page Variables.
---

This post will be rather short. The main focus is just a quick run down of the various `Page Variables` we'll be using.

### List of stuff to generate
- [Title](#title)
- [Dates and Formatting](#dates-and-formatting)
- [Tags](#tags)
- [Main Content](#main-content)
- [Next/Previous Posts](#next-previous-posts)


## Title

This one is simple, it places whatever is written in `title` in the front matter at the top of the page. For this page, it'll

```html
<h1 class="ArticleTitle">
  {{ .Title }}
</h1>

<!-- when rendered becomes -->

<h1 class="ArticleTitle">
  Create Hugo Theme Pt 3: Page Variables
</h1>
```

## Dates and Formatting

Over here I've used `PublishDate` instead of `Date`. `PublishDate` is for when you'd like articles to have a particular date to be published. If it's set in the future, it will not be generated yet. If it's set in the past, it'll render on that exact day. Nice thing about `PublishDate` is that if it doesn't exist, it automatically falls back to `Date`.

`Format` is basically the way you'd like the date to be formatted. I like dates in hierarchical order, so I've set mine in `YYYY - MM - DD` format. One thing to be aware of is that when setting the format, you have to use what's called Go's *magical reference date*.

```go
Mon Jan 2 15:04:05 MST 2006
```

When written another way, looks like this.

```go
01/02 03:04:05PM '06 -0700
```

What it means is that each segment of the date corresponds to a specific value that will not clash with another segment. 

```html
<p class="ArticleDate">{{ .PublishDate.Format "2006 - 01 - 02" }}</p>

<!-- when rendered becomes -->
<p class="ArticleDate">2019 - 08 - 27</p>
```

## Tags

This bit seemed reusable so I've moved it out into it's own partial at `layouts/partials/article-tags.html`. 

```html
<div class="ArticleTags">
  {{ with .Params.tags }}
    {{ $tags := . }}
    {{ $len := len $tags }}

    {{ range $index, $element := $tags }}
      <a href="{{ absURL "tags/" }}{{ . | urlize }}">
        <span class="ArticleTag">{{ . }}</span>
      </a> 
      {{ if ne (add $index 1) $len }}
        |
      {{ end }}
    {{ end }}
  {{ end }}
</div>

```

There's quite a lot going on here but basically, we're telling Hugo to skip this block if the page doesn't have any tags using the `with` variable. We then loop through and render the contents and use `|` as a separator between tags.

The tags are converted into an link using `absURL`, here we're telling Hugo to use an absolute link like `https://legendofcode.com/tags/tagname`, instead of a relative link like `tags/tagname`. `urlize` converts spaces into hyphens, so `some text like this` becomes `some-text-like-this`.

Lastly, a `|` separator is inserted if this is the last tag.
`ne` means `not equal`.

Breaking it down in plain English, `if current index + 1, not equals lenth of array, add |`.

## Main Content

It's simple `Content`. This surprised me.

```html
{{ .Content }}
```

## Next/Previous Posts

`PrevInSection` and `NextInSection` are basically the same thing so I've included ony the `PrevInSection` snippet.

```html
<section class="PreviousArticle">
  {{ if .PrevInSection }}
    <span class="PagerLabel">Previous</span>
    <a href="{{ .PrevInSection.Permalink }}" class="ArticleTitle">{{ .PrevInSection.Title }}</a>
  {{ end }}
</section>
```

That's it for today. Next part will deal with setting up article lists.
