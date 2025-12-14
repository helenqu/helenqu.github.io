---
layout: index
title: "Blog"
permalink: /blog/
---

{% for post in site.posts %}
<article>

  <h2>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
  </h2>

  <p>
    {{ post.date | date: "%a %b %-d, %Y" }}
    {% if post.author %} by {{ post.author }}{% endif %}
  </p>

  <p>
    {{ post.excerpt | strip_html | truncatewords: 60 }}
  </p>

  <p>
    <a href="{{ post.url | relative_url }}">Read more &rarr;</a>
  </p>

</article>

<hr />

{% endfor %}
