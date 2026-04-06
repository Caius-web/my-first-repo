---
layout: default
title: 首页
---

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Noto Sans", Helvetica, Arial, sans-serif;
        background: #fff;
        color: #1a1a1a;
        line-height: 1.5;
    }

    /* 整体容器：两栏布局 */
    .container {
        max-width: 1000px;
        margin: 0 auto;
        padding: 40px 20px;
        display: flex;
        gap: 60px;
    }

    /* 左侧边栏 */
    .sidebar {
        flex: 1;
        position: sticky;
        top: 40px;
        height: fit-content;
    }

    /* 右侧内容区 */
    .content {
        flex: 2;
    }

    /* 头像 */
    .avatar {
        width: 60px;
        height: 60px;
        border-radius: 50%;
        background: #1a1a1a;
        margin-bottom: 20px;
    }

    .site-title {
        font-size: 1.5rem;
        font-weight: 600;
        margin-bottom: 8px;
    }

    .site-title a {
        color: #1a1a1a;
        text-decoration: none;
    }

    .site-desc {
        font-size: 0.8rem;
        color: #666;
        margin-bottom: 30px;
        line-height: 1.5;
    }

    /* 侧边栏导航 */
    .nav-links {
        list-style: none;
        margin-bottom: 30px;
    }

    .nav-links li {
        margin-bottom: 8px;
    }

    .nav-links a {
        color: #1a1a1a;
        text-decoration: none;
        font-size: 0.85rem;
    }

    .nav-links a:hover {
        color: #666;
    }

    /* 侧边栏模块 */
    .sidebar-section {
        margin-bottom: 30px;
    }

    .sidebar-section h3 {
        font-size: 0.7rem;
        font-weight: 600;
        text-transform: uppercase;
        letter-spacing: 1px;
        color: #999;
        margin-bottom: 12px;
    }

    .category-list {
        list-style: none;
    }

    .category-list li {
        margin-bottom: 6px;
    }

    .category-list a {
        color: #1a1a1a;
        text-decoration: none;
        font-size: 0.8rem;
    }

    .category-list a:hover {
        color: #666;
    }

    .tag-list {
        display: flex;
        flex-wrap: wrap;
        gap: 6px;
    }

    .tag-list a {
        color: #1a1a1a;
        text-decoration: none;
        font-size: 0.7rem;
        background: #f0f0f0;
        padding: 2px 10px;
        border-radius: 20px;
    }

    /* 年份分组 */
    .year-group {
        margin-bottom: 30px;
    }

    .year-title {
        font-size: 1.2rem;
        font-weight: 600;
        margin-bottom: 16px;
        color: #1a1a1a;
    }

    /* 文章条目 */
    .post-item {
        margin-bottom: 24px;
    }

    .post-title {
        font-size: 1rem;
        font-weight: 500;
        margin-bottom: 4px;
    }

    .post-title a {
        color: #1a1a1a;
        text-decoration: none;
    }

    .post-title a:hover {
        text-decoration: underline;
    }

    .post-meta {
        font-size: 0.7rem;
        color: #999;
        margin-bottom: 6px;
    }

    .post-tags {
        display: flex;
        flex-wrap: wrap;
        gap: 8px;
    }

    .post-tags a {
        font-size: 0.7rem;
        color: #1a1a1a;
        text-decoration: none;
        background: #f0f0f0;
        padding: 2px 10px;
        border-radius: 20px;
    }

    /* 页脚 */
    .footer {
        max-width: 1000px;
        margin: 0 auto;
        padding: 30px 20px 60px;
        text-align: center;
        border-top: 1px solid #eaeaea;
        font-size: 0.7rem;
        color: #999;
    }

    @media (max-width: 768px) {
        .container {
            flex-direction: column;
            gap: 40px;
        }
        .sidebar {
            position: static;
        }
    }
</style>

<div class="container">
    <!-- 左侧边栏 -->
    <div class="sidebar">
        <div class="avatar"></div>
        <div class="site-title">
            <a href="/">Cassi's Blog</a>
        </div>
        <div class="site-desc">
            探索科技和艺术的十字路口~
        </div>

        <ul class="nav-links">
            <li><a href="/">首页</a></li>
            <li><a href="/about">About Me</a></li>
        </ul>

        <div class="sidebar-section">
            <h3>分类目录</h3>
            <ul class="category-list">
                {% assign categories = site.categories | sort %}
                {% for category in categories %}
                <li>
                    <a href="#">{{ category[0] }}</a>
                    <span style="color:#ccc; font-size:0.7rem;">({{ category[1].size }})</span>
                </li>
                {% endfor %}
            </ul>
        </div>

        <div class="sidebar-section">
            <h3>标签</h3>
            <div class="tag-list">
                {% assign tags = site.tags | sort %}
                {% for tag in tags limit: 20 %}
                <a href="#">#{{ tag[0] }}</a>
                {% endfor %}
            </div>
        </div>
    </div>

    <!-- 右侧内容区：文章列表（按年份分组） -->
    <div class="content">
        {% assign posts_by_year = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
        {% for year in posts_by_year %}
        <div class="year-group">
            <div class="year-title">{{ year.name }}</div>
            {% for post in year.items %}
            <div class="post-item">
                <div class="post-title">
                    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
                </div>
                <div class="post-meta">{{ post.date | date: "%Y-%m-%d" }}</div>
                <div class="post-tags">
                    {% for tag in post.tags %}
                    <a href="#">#{{ tag }}</a>
                    {% endfor %}
                </div>
            </div>
            {% endfor %}
        </div>
        {% endfor %}
    </div>
</div>

<div class="footer">
    <p>© 2026 Cassi's Blog. All Rights Reserved. Powered by GitHub Pages.</p>
</div>