---
title: "Theme Design Dos And Do-Nots"
date: 2019-06-16T02:24:52+09:00
tags:
  - hugo
  - development
summary: When gathering requirements, it's often just as helpful to define what are the things you *shouldn't* do as much as the things you should do.
---

When gathering requirements, it's often just as helpful to define what are the things you *shouldn't* do as much as the things you should do.

Having a goal in place defines the end point.

Having a list of things *not to do* prevents scope creep.

## Dos

- Home page (list)
  - list of all `Posts` and `TILs`, sorted by latest
  - no pagination, just list everything every written
  - title, publish date, tags, author
  - invisible block for title image (svg)
  - some kind of icon to identify post type (post/TIL/?)
  - post summary
- individual posts page (single)
  - hero image area, title, publish date, author, tags
  - return to home
  - next / prev article links (show titles)
- list articles by tags (list)
  - reusable also for posts, TILs, future categories
  - basically structure as home list
- About page
  - description about me, the page
- Contact
- get design 90% complete, then worry about hugo template syntax
  - create a design straight in plain html and css
  - focus on general structure
  - ignore pixel level minutiae
  - use placeholders for images and icons
  - monocolour only

## Do-Nots
- build a general use theme
  - this is for me only
  - don't bother setting a separate git repo for theme
- spend time on little details
  - type optimisation
  - optimising spacing between elements
  - code blocks and syntax highlighting
- designs for future planned content, only what we need right now
- separate `list` designs
- separate `single` designs
- unique pages
