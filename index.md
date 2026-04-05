---
layout: default
title: 首页
---

## 📝 最新文章

<ul>
  {% for post in site.posts %}
    <li style="margin-bottom: 20px;">
      <a href="{{ post.url | relative_url }}" style="font-size: 1.2em; color: #667eea;">{{ post.title }}</a>
      <br>
      <small style="color: #999;">{{ post.date | date: "%Y年%m月%d日" }}</small>
      <p style="margin: 5px 0 0 0; color: #666;">{{ post.excerpt | strip_html | truncate: 100 }}</p>
    </li>
  {% endfor %}
</ul>

---

## 👋 关于我

你好！我是 Cassi，一名编程学习者。

这个博客用来记录我的学习笔记和生活感悟。

[GitHub 主页](https://github.com/Caius-web)