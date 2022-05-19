---
layout: post
title:  "Sandbox: Enumerated headings"
date:   2022-05-04
categories: tech
author: false
---

This post lists a bunch of headings, to show how styles are working.

# Enumerated heading 1

## Enumerated heading 2
.
## Enumerated heading 2
.
## Enumerated heading 2
.

# Enumerated heading 1

## Enumerated heading 2
.
## Enumerated heading 2
.
## Enumerated heading 2
.
# Enumerated heading 1

### Heading three 3
.
#### Heading four 4
.
# Enumerated heading 1
.
# Enumerated heading 1
.
# Enumerated heading 1
.

##### Heading five 5
.

# Enumerated heading 1
.

## Enumerated heading 2
.
## Enumerated heading 2
.
## Enumerated heading 2
.

# Enumerated heading 1
.
## Enumerated heading 2
.
## Enumerated heading 2
.
## Enumerated heading 2
.

# Enumerated heading 1
.

###### Heading six 6
.

# Enumerated heading 1
.

## Enumerated heading 2
.
## Enumerated heading 2
.
## Enumerated heading 2
.

# Enumerated heading 1
.

## Enumerated heading 2
.
## Enumerated heading 2
.
## Enumerated heading 2
.

# Enumerated heading 1

Here's the markdown for this page:

```md
# Enumerated heading 1

## Enumerated heading 2
## Enumerated heading 2
## Enumerated heading 2

# Enumerated heading 1

## Enumerated heading 2
## Enumerated heading 2
## Enumerated heading 2

# Enumerated heading 1

### Heading three 3
#### Heading four 4

# Enumerated heading 1
# Enumerated heading 1
# Enumerated heading 1

##### Heading five 5

# Enumerated heading 1

## Enumerated heading 2
## Enumerated heading 2
## Enumerated heading 2

# Enumerated heading 1

## Enumerated heading 2
## Enumerated heading 2
## Enumerated heading 2

# Enumerated heading 1

###### Heading six 6

# Enumerated heading 1

## Enumerated heading 2
## Enumerated heading 2
## Enumerated heading 2

# Enumerated heading 1

## Enumerated heading 2
## Enumerated heading 2
## Enumerated heading 2

# Enumerated heading 1
```

Css:
```css
body {counter-reset: h1counter; counter-reset: h2counter;}

h1, h5, h6 {counter-reset: h2counter;}
.post-content, h5, h6 {counter-reset: h1counter;}

.post-content h1::before {
	content: counter(h1counter, upper-roman) ".\0000a0\0000a0";
	counter-increment: h1counter;
	width: 4em;
	float: left;
}

.post-content h2::before {
	content: "\0000a0\0000a0\0000a0\0000a0\0000a0\0000a0\0000a0\0000a0" counter(h2counter) ".\0000a0\0000a0";
	counter-increment: h2counter;
	width: 6em;
	float: left;
}
```
