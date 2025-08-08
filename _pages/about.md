---
permalink: /
title: "Academic Pages is a ready-to-fork GitHub Pages template for academic personal websites"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

## Welcome!

Hello! I'm Aylin, a graduate student at ETH Zurich, currently working on my Master's thesis with [Prof. Ludwig Schmidt's group](https://people.csail.mit.edu/ludwigs/index.html) at Stanford. My research focuses on generating open-source datasets for computer use models.

### Latest blog post

{% assign published_posts = site.posts | where_exp: "post", "post.date <= site.time" %}
{% assign latest_post = published_posts | sort: "date" | last %}

{% if latest_post %}
- **Latest**: [{{ latest_post.title }}]({{ latest_post.url | relative_url }})
  
  {{ latest_post.excerpt | default: latest_post.content | strip_html | truncatewords: 40 }}
  
  [Read more →]({{ latest_post.url | relative_url }})
{% else %}
No posts yet. Check back soon!
{% endif %}

### Projects

- **IDE Grounding Kit**: I developed a tool for [automatically generating agent training data](https://github.com/AylinAkkus/IDE-grounding-kit) for the Cursor IDE using its underlying Electron Browser.
![Bounding Boxes on Cursor Screen](images\Cursor_bbox.png)

### Personal

In my free time I love to explain my research ideas to my (probably tired from coding) [boyfriend](https://mertunsall.github.io/) who is also an AI researcher! When I'm not immersed in the world of large language models, I enjoy learning about other cultures in ridiculous detail and experimenting with their culinary techniques, particularly those involving koji and fermentation like in this [Noma fermentation guide](https://www.wired.com/story/noma-guide-to-fermentation-book-review/)

### Publications

- **EasyARC: Evaluating Vision Language Models on True Visual Reasoning**: Our paper was accepted to the ViSCALE workshop at CVPR 2025. You can read it [here](https://arxiv.org/abs/2506.11595).

Feel free to reach out if you share similar interests or have any questions!