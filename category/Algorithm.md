---
layout: page
---
<div class="posts">
  {% for post in site.categories.Algorithm %}
    <article class="post">

      <a href="{{ post.url }}"><h1>{{ post.title }}</h1>
        <div class="date">
          {{ post.date | date: "%B %e, %Y" }}
        </div>
  
        <div class="entry">
          {{ post.excerpt }}
        </div>
      </a>
    </article>
  {% endfor %}
</div>