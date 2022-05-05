---
layout: post
title:  "Notes: Setting up this site"
date:   2022-05-03
categories: tech
author: false
---

Notes on (re)building the site, which runs on Jekyll.

# Contents:
* [Basic setup](#basic)
* [_includes/, assets/, and _layouts](#ial)
* [_sass/ and related files](#sass)

<a name="basic"></a>
### Basic setup
##### Install Jekyll

See: [Jekyll quickstart][quickstart].

[quickstart]: https://jekyllrb.com/docs/

##### CNAME, README, & _config.yml

To enable custom domain, create file called "CNAME" containing: `mark.grindy.net`.

For GitHub, create file called "README.md" containing: `<!-- # mark.grindy.net -->`.

To customize site info, revise _config.yml as described in file, and add the following lines:

```yml
twitter_username: markgrindy
github_username:  markgrindy
instagram_username: markgrindy
strava_username: markgrindy
rss: RSS feed

header_pages:
  - about.md
```

##### Revise Gemfile, fix errors

To prep for GitHub Pages, revise Gemfile as follows:

{% highlight ruby %}
# gem "jekyll", "~> 4.2.2"
# This is the default theme for new Jekyll sites. You may change this to anything you like.
gem "minima", "~> 2.5"
# If you want to use GitHub Pages, remove the "gem "jekyll"" above and
# uncomment the line below. To upgrade, run `bundle update github-pages`.
gem "github-pages", group: :jekyll_plugins
{% endhighlight %}

Modifying the Gemfile creates several errors.

In terminal, running `bundle exec jekyll serve` runs into: `cannot load such file -- webrick (LoadError)`.
  * Problem: Webrick is no longer a bundled gem.
  * Solution: Add `gem "webrick"` to Gemfile.
  * Source: [GitHub forum][github-forum].

In terminal, running `TK` runs into: `Bundler could not find compatible versions for gem "jekyll-feed"`.
  * Problem: The existing Gemfile.lock freezes all the versions at what was originally in the Gemfile.
  * Solution: Delete Gemfile.lock. In terminal, run `bundle update` to rebuild Gemfile.lock.
  * Source: [Jekyll forum][jekyll-forum].

[github-forum]: https://github.com/jekyll/jekyll/issues/8523
[jekyll-forum]: https://talk.jekyllrb.com/t/bundler-could-not-find-compatible-versions-for-gem-jekyll/6275/3

<a name="ial"></a>
### _includes/, assets/, and _layouts/
##### Customize _includes/

## Line break

In includes, add a file called "br.html" containing `<p style="text-align: center;" align="center">&#65121; &#65121; &#65121;</p>`. Type `{% raw %}{% include br.html %}{% endraw %}` to deploy. Result:
{% include br.html %}

## Strava

In _includes/social.html, add code for Strava:

{% highlight html %}
{% raw %}
{%- if site.strava_username -%}<li><a href="https://www.strava.com/athletes/{{ site.strava_username| escape }}"><svg class="svg-icon"><use xlink:href="{{ '/assets/minima-social-icons.svg#strava' | relative_url }}"></use></svg> <span class="username">{{ site.strava_username| escape }}</span></a></li>{%- endif -%}
{% endraw %}
{% endhighlight %}

##### Customize assets/

## More Strava

In assets/minima-social-icons.svg, add code for Strava icon:

```html
  <symbol id="strava" fill-rule="evenodd" clip-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="1.414">
    <path transform="scale(0.26)" d="M41.03 47.852l-5.572-10.976h-8.172L41.03 64l13.736-27.124h-8.18"/>
    <path transform="scale(0.26)" d="M27.898 21.944l7.564 14.928h11.124L27.898 0 9.234 36.876H20.35"/>
  </symbol>
```

##### Customize _layouts/

Add code for end symbols to post.html, just before the closing tag `</article>`:

```html
<p style="text-align: center;" align="center">&#35; &#35; &#35;</p>
```

Result (automatically appears at end of all posts):
<p style="text-align: center;" align="center">&#35; &#35; &#35;</p>

<a name="sass"></a>
### Customize _sass/ and related files

##### Fonts

In _sass/minima.scss, switch to the serif font family and font size used by Medium:

```scss
$base-font-family: charter, Georgia, Cambria, "Times New Roman", Times, serif;

$base-font-size:   18px !default;
```
##### Headings

In _sass/minima/_base.scss, style the headings:

```scss
/**
 * Headings
 */
h1, h2, h3, h4, h5, h6 {
  font-size: $base-font-size;
  // font-weight: $base-font-weight;
}

h1 {
  font-weight: bold;
  text-decoration: underline;
}

h2 {
  font-style: italic;
  font-weight: normal;
  text-decoration: underline;
  // text-transform: uppercase;
}

h3 {
  font-style: italic;
  font-weight: normal;
  text-decoration: underline;
  text-transform: uppercase;
}

h4 {
  text-align: center;
  background-color: #000;
  color: #fff;
  // text-transform: uppercase;
}

h5 {
  text-align: center;
  background-color: #ccc;
  // text-transform: uppercase;
}
```

Result:

# Heading 1

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

Note that a new h1, h3, or h4 triggers the h5 enumeration to reset.

###### Heading 6

Any new heading (except h6) triggers the h6 enumeration to reset.

##### Header and nav formatting

In _sass/minima/_layout.scss, make a bunch of changes:

```scss

.site-header {
  // border-top: 5px solid $grey-color-dark;
  // [...]
}

.site-title {
  // @include relative-font-size(1.625);
  // font-weight: 300;
  line-height: $base-line-height * $base-font-size * 2.25;
  // letter-spacing: -1px;
  margin-bottom: 0;
  /* float: left; */

  // add custom styles here:
  font-weight: bold;

  &,
  &:visited {
    // color: $grey-color-dark;
    color: $text-color;
  }
}

.site-nav {
  // float: right;
  // line-height: $base-line-height * $base-font-size * 2.25;
  // [...]
}

.page-link {
  color: $text-color;
  line-height: $base-line-height;

  // custom scss
  // text-transform: uppercase;
  // font-style: italic;

  // Gaps between nav items, but not on the last one
  &:not(:last-child) {
    // margin-right: 20px;
    margin-right: $base-font-size * 0.5;
  }
}

// [...]

.custom-header {
  text-align: center;
}

// [...]
.post-header {
  // margin-bottom: $spacing-unit;
}
```

In turn, revise includes/header.html:

```html
<br/>
<!-- <div class="wrapper"> -->
<div class="wrapper custom-header">

<!-- [...] -->
<!-- <div class="trigger">
  {%- for path in page_paths -%}
    {%- assign my_page = site.pages | where: "path", path | first -%}
    {%- if my_page.title -%}
      <a class="page-link" href="{{ my_page.url | relative_url }}">{{ my_page.title | escape }}</a>
    {%- endif -%}
  {%- endfor -%}
</div> -->
<div class="trigger">
  {%- for path in page_paths limit: 2 -%}
    {%- assign my_page = site.pages | where: "path", path | first -%}
    {%- if my_page.title -%}
      <a class="page-link" href="{{ my_page.url | relative_url }}">{{ my_page.title | escape }}</a>
    {%- endif -%}
  {%- endfor -%}
  {%- for path in page_paths offset: continue -%}
    {%- assign my_page = site.pages | where: "path", path | first -%}
    {%- if my_page.title -%}
    &#8226;
      <a class="page-link" href="{{ my_page.url | relative_url }}">{{ my_page.title | escape }}</a>
    {%- endif -%}
  {%- endfor -%}
</div>
<br/>
```

Back in _sass/minima/_layout.scss, adjust .post-meta and .post-title:

```scss

.post-meta {
  // font-size: $small-font-size;
  // color: $grey-color;

  // custom scss
  font-weight: bold;
  margin-top: -$base-font-size * 0.8;
  text-align: center;
}

// [...]

.post-title {

  text-align: center;
  text-decoration: none;
  text-transform: capitalize;

  // @include relative-font-size(2.625);
  // letter-spacing: -1px;
  // line-height: 1;
  //
  // @include media-query($on-laptop) {
  //   @include relative-font-size(2.25);
  // }
}
```

In turn, revise _layouts/post.html:

{% highlight html %}
{% raw %}
<header class="post-header">
  <h1 class="post-title p-name" itemprop="name headline">{{ page.title | escape }}</h1>
  <p class="post-meta">
    {%- if page.author -%}
      By <span itemprop="author" itemscope itemtype="http://schema.org/Person"><span class="p-author h-card" itemprop="name">{{ page.author }}</span></span><br/>
    {%- endif -%}
    <time class="dt-published" datetime="{{ page.date | date_to_xmlschema }}" itemprop="datePublished">
      {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
      {{ page.date | date: date_format }}
    </time>
    </p>
</header>
{% endraw %}
{% endhighlight %}

##### Code block formatting

In _sass/minima.scss, create a new default code background color:

```scss
$code-bg-color:    #eee;
```

In _sass/minima/_base.scss, set the default:

```scss
code {
  @include relative-font-size(0.9375);
  border: 1px solid $grey-color-light;
  border-radius: 3px;
  // background-color: #eef;
  background-color: $code-bg-color;
}
```

In _sass/minima/_syntax-highlighting.scss, set the default here, too:
```scss
.highlight {
  background: #fff;
  @extend %vertical-rhythm;

  .highlighter-rouge & {
    // background: #eef;
    background: $code-bg-color;
  }
```
##### Post feed formatting

Style :

```scss
.post-list-heading {
  // @include relative-font-size(1.75);

  // custom scss
  font-style: normal;  
  font-weight: bold;
  text-align: center;
  text-decoration: none;
}

// [...]

.post-link {
  display: block;
  // @include relative-font-size(1.5);
}
```

##### Footer

Style :

```scss
.footer-heading {
  // @include relative-font-size(1.125);
  margin-bottom: $spacing-unit / 2;
}

// [...]

.footer-col-wrapper {
  // @include relative-font-size(0.9375);
  color: $grey-color;
  margin-left: -$spacing-unit / 2;
  @extend %clearfix;
}
```
