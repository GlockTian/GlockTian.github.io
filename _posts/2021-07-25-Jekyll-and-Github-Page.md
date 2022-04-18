---
layout: post
title: "Jekyll and Github Page"
subtitle: "What I did to set up"
date: 2021-07-25 23:45:13 -0400
background: '/img/posts/01.jpg'
tags: [Jekyll, Personal Project]
---

### Fun Fact
Initially I though Static means no css animation, but as you can see from my home page. There is a rotating ring. Silly old me.

### static site
According to wikipedia [don't do this for your thesis though], A static web page (sometimes called a flat page or a stationary page) is a web page that is delivered to the user's web browser exactly as stored, in contrast to dynamic web pages which are generated by a web application.

### Also
Apparently if you put script tag inside the post you can create all sorts of interesting effect, so I decided to put a script in this post. If you click randomly, you will see the effect.

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
      if (e.target.tagName === "A") {
        return;
      }
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