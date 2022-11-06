---
layout: post
title: "Subtle Animation"
subtitle: "Learning intersection observer"
date: 2022-11-05 21:45:13 -0400
background: '/img/posts/06.jpg'
tags: [JavaScript]
---

<head>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.10/styles/monokai.min.css">
<style>
  section {
    display: grid;
    place-items: center;
    align-items: center;
    min-height: 100vh;
  }
  .hidden {
    opacity: 0;
    filter: blur(10px);
    transform: translateX(-100%);
    transition: all 1s;
  }
  .show {
    opacity: 1 !important;
    filter: blur(0px);
    transform: translateX(0);
  }
  .parent {
    height: 400px;
    width: 400px;
    background-color: #f1f1f1;
  }
  .child {
    width: 50%;
    height: 50%;
    background-color: black;
    animation: move-around 1s ease-in-out infinite;
  }
  .parent:hover .child {
    animation-play-state: paused;
  }
  @keyframes move-around {
    0% {
      transform: translate(0, 0);
    }
    25% {
      transform: translate(100%, 0);
    }
    50% {
      transform: translate(100%, 100%);
    }
    75% {
      transform: translate(0, 100%);
    }
    100% {
      transform: translate(0, 0);
    }
  }
  </style>
</head>
<section class="hidden">
  <h1>CSS section</h1>
  ```js
      .hidden {
        opacity: 0;
        filter: blur(10px);
        transform: translateX(-100%);
        transition: all 1s;
      }
      .show {
        opacity: 1 !important;
        filter: blur(0px);
        transform: translateX(0);
      }
  ```
</section>
<section class="hidden">
  <h1>JavaScript section</h1>
```js
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add("show");
      } else {
        entry.target.classList.remove("show");
      }
    });
  });
  const hidden = document.querySelectorAll(".hidden");
  hidden.forEach((element) => {
    observer.observe(element);
  })
```
</section>
<section class="hidden">
<h1>Simple Animation Section</h1>
  <div class="parent">
    <div class="child">
    </div>
  </div>
```js
    .parent {
      height: 400px;
      width: 400px;
      background-color: #f1f1f1;
    }
    .child {
      width: 50%;
      height: 50%;
      background-color: black;
      animation: move-around 1s ease-in-out infinite;
    }
    .parent:hover .child {
      animation-play-state: paused;
    }
    @keyframes move-around {
      0% {
        transform: translate(0, 0);
      }
      25% {
        transform: translate(100%, 0);
      }
      50% {
        transform: translate(100%, 100%);
      }
      75% {
        transform: translate(0, 100%);
      }
      100% {
        transform: translate(0, 0);
      }
    }
```
</section>
<script>
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add("show");
      } else {
        entry.target.classList.remove("show");
      }
    });
  });
  const hidden = document.querySelectorAll(".hidden");
  hidden.forEach((element) => {
    observer.observe(element);
  })
</script>
  