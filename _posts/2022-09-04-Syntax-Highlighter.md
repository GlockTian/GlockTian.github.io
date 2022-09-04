---
layout: post
title: "Syntax Highlighter"
subtitle: "Highlightjs"
date: 2022-09-04 13:45:13 -0400
background: '/img/posts/06.jpg'
tags: [JavaScript, Highlightjs]
---

I finally got the syntax highlighter working. It's very easy to set up. I'm using [Highlightjs](https://highlightjs.org/).

## What did I do?

### In the head
```js
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.10/styles/monokai.min.css">
```

### In the body
```js
  <script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.10/highlight.min.js"></script>
  <script>hljs.initHighlightingOnLoad();</script>
```
