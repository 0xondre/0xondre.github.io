# Engineering blog

A minimal Jekyll blog published at [0xondre.github.io](https://0xondre.github.io/). GitHub Pages builds the site from Markdown files on the `main` branch.

## Publish a post

Add a file named `_posts/YYYY-MM-DD-post-title.md`:

```markdown
---
title: "Post title"
description: "A short summary for search results and the article page."
date: 2026-10-19 10:00:00 +0200
tags: [Python, Performance]
read_time: 5
---

Write the article in Markdown here.
```

Use the same date in the filename and front matter. Posts with a future date might not appear on GitHub Pages. After committing and pushing to `main`, the newest posts appear automatically on the home page. The HTTP caching article is an example and can be replaced with your own writing.

## Change the site

- Site title and description: `_config.yml`
- Home page and post list: `index.html`
- About page: `about.html`
- Header and footer: `_layouts/default.html`
- Article layout: `_layouts/post.html`
- Styles: `assets/style.css`

## Local preview

With Ruby and Bundler installed, run:

```sh
bundle install
bundle exec jekyll serve
```

Then open the local URL printed by Jekyll, usually `http://127.0.0.1:4000`.
