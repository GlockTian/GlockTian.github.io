---
layout: post
title: "Subtle Animation"
subtitle: "Learning intersection observer"
date: 2022-11-05 21:45:13 -0400
background: '/img/posts/06.jpg'
tags: [JavaScript]
---

<head>
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
  </style>
</head>
<section class="hidden">
  <h1>CSS section</h1>
  <code>
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
  </code>
</section>
<section class="hidden">
  <h1>JavaScript section</h1>
  <code>
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
  