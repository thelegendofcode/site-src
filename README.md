# site-src
Source for LoC website

## How to publish

```zsh
$ hugo
$ scripts/deploh.sh
```

## Theme

[KISS](https://github.com/ribice/kiss)

## Categories

These are the current categories available

- Posts
  - standard blog post
- TILs
  - also a blog post, but built specifically as a TIL
  - could've simply been just a Post with a TIL tag but wanted to make it separate because of below planned categories

Planned but not yet implemented categories
- Quotes
  - just a quote
  - could be a simple block of text, could be a twitter link, not really sure yet
- Image/meme/mood thingy
  - an image speaks a thousand words
  - sometimes posting a single image is easier than writing a whole article

## File naming conventions

All articles are written using the below structure

```zsh
# structure
${INDEX}-${TITLE}.md

# example
001-hello-world.md
```

- the index begins from `001`
- each category has its own index (post/TIL/?)
- `000` is reserved for drafts

Using this system, I'll be able to write up to 999 articles per category. This system can last me 19 years assuming an article a week. Should I somehow become a more prolific writer, I can simply prepend a 0 to all files.
