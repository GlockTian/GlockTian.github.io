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
  .section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  .show {
    opacity: 1;
  }
  .hidden {
    opacity: 0;
    transition: all 1s;
  }
  </style>
</head>
<section class="hidden">
  <h1>Section 1</h1>
  <p>Some text</p>
</section>
<section class="hidden">
  <h1>Section 2</h1>
  <p>Some text</p>
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
  