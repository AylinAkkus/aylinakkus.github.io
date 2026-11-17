# Publishing an article

Create a Markdown file in `_posts` named `YYYY-MM-DD-your-title.md`. Start it with:

```yaml
---
layout: article
title: "Your article title"
description: "A one-sentence summary for the homepage, article list, and search results."
date: YYYY-MM-DD
tags:
  - Language Models
---
```

Write the article below the front matter using Markdown. Put images in `images/` and reference them as `![Description]({{ '/images/your-image.png' | relative_url }})`.

For equations, diagrams, or interactive plots, add `math: true`, `mermaid: true`, or `plotly: true` to the article's front matter. These scripts load only on pages that request them.

Commit and push the file to `master`. GitHub Pages will build the site; the article will appear on the homepage, the [Articles page](https://aylinakkus.github.io/articles/), and the RSS feed automatically.
