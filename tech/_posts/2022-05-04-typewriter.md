---
layout: post
title:  "Notes: Word count typewriter"
date:   2022-05-04
revised: false
categories: tech
author: Mark & Sarah
location: Duluth, Minn.
---

The cute blinking cursor pretends to add up the words on the page and type out the total, to honor the effort of creating the page and as a reminder that nothing's ever finished or perfect.

But first, here's how the draft/revised date works...

# Draft/Revised & date   

If the post metadata includes a `post.revised` date and it is later than `post.date`, the draft will display "Revised" and the revised date. If the revised date is earlier than the post date, it will display "Draft" and the revised date. If there is no revised date, it will display "Draft" and the post date.

Post metadata:

```yml
---
date:   2022-05-04
revised: 2022-05-05
---
```

_layouts/posts.html:

```
{% raw %}
{% assign var pdate = page.date | date: "%-m/%-d/%y" %}
{% assign var rdate = page.revised | date: "%-m/%-d/%y" %}
{% if page.revised %}
  {% if pdate < rdate %}
    Revised {{ rdate }}
  {% else if one >= two %}
    Draft {{ rdate }}
  {%- endif -%}
{%- else -%}
    Draft {{ pdate }}
{%- endif -%}
{% endraw %}
```

OK, on to the word count thingy.

# Word count typewriter effect

The include is placed in _layouts/posts.html:

```
{% raw %}{% include date-word-count.html %}{% endraw %}
```

Here's the relevant html from the include:

```html
Word count:
<span id="word-count"></span><span id="cursor" style="margin-left: -3px">|</span>
```

And here's the javascript:

```js
<script>
  window.onload = function() {

    // Blink cursor twice and leave it displayed
    blinkingCursor(2500);

    // Get page word count as formatted string
    var words = document.body.innerText || document.body.textContent;
    var wordCount = words.split(" ").length;
    var wordCountString = wordCount.toLocaleString("en-US");

    // Typewrite the word count
    var i = 0;
    var txt = wordCountString;
    var typeSpeed = 50;

    setTimeout(function() { typeWriter(); },2400);

    function typeWriter() {
      if (i < txt.length) {
        document.getElementById("word-count").innerHTML += txt.charAt(i);
        i++;
        setTimeout(typeWriter, typeSpeed);
      }
    }

    // Blink cursor one more time, then hide it
    setTimeout(function() { blinkingCursor(2400); },2400);
    setTimeout(function() { hideCursor(); },5400);

  }

  function blinkingCursor(timeout) {
    var cursor = true;
    var speed = 600;

    var blink = setInterval(() => {
       if(cursor) {
         document.getElementById('cursor').style.opacity = 0;
         cursor = false;
       }else {
         document.getElementById('cursor').style.opacity = 1;
         cursor = true;
       }
    }, speed);

    // Stop the blinking
    setTimeout(function() { clearInterval(blink); },timeout);

  }

  function hideCursor() {
    document.getElementById('cursor').style.opacity = 0;
  }

</script>
```
