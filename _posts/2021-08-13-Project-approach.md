---
layout: post
title: "Design Project Implementation"
subtitle: "How I find different approaches in designing and implementing a scheduling application"
date: 2021-08-13 10:09:13 -0400
background: '/img/posts/02.jpg'
tags: [Design, Project Management]
---

Source: GithubLink

When I approaches my first project:

1. design the data structure → design the components → design the highest level algorithm
2. design the highest level algorithm  → design the components → design the data structure

However, both of them are too naive.

**the former approach** creates a lot of unnecessary building blocks (unused method, inconvenient use of data structure).  It is not good to design the low-level architecture (choice for data type, function and etc. ) before we figure out the high level requirement.

**the latter approach** is sightly better, but creates a lot of constraint in data structure, as they needs to fit the high level design decision.

The above cases occur because the high level design and low level design are too closely connected together. To solved it we can apply the dependency inversion principle. 

## Dependency Inversion

Definition from Wikipedia: 

a specific form of loosely coupling software modules.

Notion: High level module should be independent of the low-level modules. 

This also increases the reusability, and testability  of the code.

## Proposed Approach:

Design the building blocks → design the algorithm and data structure

Design the interface first allows the team to create an outline of  different tasks in the project

In this approach, tasks can be separate into smaller sizes and start simultaneously at the same time. This require a lot of planning ahead of the implementation, but can increase the quality of the products by implementing testing early in the project phase.


<script type="text/javascript">
    let saber_arr = [
      "saber",
      "artoria",
      "arthur",
      "servant",
      "caliburn",
      "excalibur",
      "avalon",
      "shirou",
      "master",
      "呆毛",
      "棉被",
      "雨衣",
      "alter",
      "lily",
      "eater",
      "lion",
      "waifu",
    ];
    document.body.addEventListener("click", function (e) {
      console.log("clicked");
      if (e.target.tagName === "A") {
        return;
      }
      console.log("start assigning");
      let x = e.pageX,
        y = e.pageY,
        span = document.createElement("span"),
        index = Math.floor(Math.random() * saber_arr.length);

      span.textContent = saber_arr[index] + " +1";
      span.style.cssText = [
        "z-index: 9999999; position: absolute; color: #fb6c9b; top: ",
        y - 20,
        "px; left: ",
        x,
        "px;",
      ].join("");
      document.body.appendChild(span);
      console.log("start animate");

      animate(span);
    });
    function animate(el) {
      let i = 0,
        top = parseInt(el.style.top),
        id = setInterval(frame, 16.7);

      function frame() {
        if (i > 180) {
          clearInterval(id);
          el.parentNode.removeChild(el);
        } else {
          i += 2;
          el.style.top = top - i + "px";
          el.style.opacity = (180 - i) / 180;
        }
      }
    }
  </script>