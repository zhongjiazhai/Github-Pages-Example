---
layout: default
---

<body>
  <div class="index-wrapper">
    <div class="aside">
      <div class="info-card">
        <h1>翟忠佳的博客</h1>
        <a href="http://weibo.com/1944978350/" target="_blank"><img src="http://www.weibo.com/favicon.ico" alt="" width="25"/></a>
         <a href="http://instagram.com/rainzhai/" target="_blank"><img src="http://d36xtkk24g8jdx.cloudfront.net/bluebar/00c6602/images/ico/favicon.ico" alt="" width="22"/></a>
        <a href="https://twitter.com/imust_mr/" target="_blank"><img src="http://www.twitter.com/favicon.ico" alt="" width="22"/></a>
         <a href="https://www.douban.com/people/139902675/" target="_blank"><img src="http://www.douban.com/favicon.ico" alt="" width="22"/></a>
       
       
      </div>
      <div id="particles-js"></div>
    </div>

    <div class="index-content">
      <ul class="artical-list">
        {% for post in site.categories.blog %}
        <li>
          <a href="{{ post.url }}" class="title">{{ post.title }}</a>
          <div class="title-desc">{{ post.description }}</div>
        </li>
        {% endfor %}
      </ul>
    </div>
  </div>
</body>
