---
layout: post
title:  "Notes: Category links"
date:   2022-05-05
category: tech
author: false
---

Jotting down changes made to modify the header. 

In `header.html`:

```html
{% raw %}
<div class="trigger">
  {% assign var i = 0 %}
  {%- for path in page_paths -%}
    {%- assign my_page = site.pages | where: "path", path | first -%}
    {%- if my_page.title -%}
      {% if i > 0 %}
        <span class="page-link-bullet">
          <!-- &#8226; -->
          &#xb7;
        </span>
      {% endif %}
      {% assign var i = 1 %}
    <a class="page-link" href="{{ my_page.url | relative_url }}">{{ my_page.title | escape }}</a>
    {%- endif -%}
  {%- endfor -%}
</div>
{% endraw %}
```

In `category-links.html`:

```html
{% raw %}
<div class="trigger" id="category-links">
    {% for category in site.data.category_metadata.mycategories %}
      {% if category.emoji %}
        <a class="page-link" href="{{ category.url }}">
          <span class="category-label">{{ category.label }}</span>
          <span class="category-emoji">{{ category.emoji }}</span>
        </a>
      {% endif %}
    {% endfor %}
</div>
{% endraw %}
```

Under `.site nav {`:

```css
.page-link {
  color: $text-color;
  line-height: $base-line-height;
  text-transform: uppercase;
  font-size: $base-font-size * 0.8;

  // custom scss
  // text-transform: uppercase;
  // font-style: italic;

  // Gaps between nav items, but not on the last one
  &:not(:last-child) {
    // commented this out because we are using raised dots in some cases
    // margin-right: 20px;
  }
}

.category-label {
  display: none;
}

.category-emoji {
  margin-left: $base-font-size / 2;
}

div#category-links a:first-child .category-emoji {
  margin-left: 0;
}

.page-link:hover > .category-emoji {
  margin-left: 0;
}

.page-link:hover > .category-label {
  display: inline;
}
```

And under `@include media-query($on-palm) {`:
```css
.page-link-bullet {
    display: none;
    font-size: $base-font-size * 0.8;
}

.category-label {
  display: inline;
}

.category-emoji {
  margin-left: 0;
}
```
