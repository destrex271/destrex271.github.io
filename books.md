---
layout: page
title: Books
---

<ul>
  {% for book in site.books %}
    <li>
      <a href="{{ book.url | relative_url }}">{{ book.title }}</a>
    </li>
  {% endfor %}
</ul>
