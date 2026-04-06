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
        background-color: #fafafa;
        color: #1a1a1a;
        line-height: 1.5;
    }

    /* 头部 */
    .site-header {
        max-width: 900px;
        margin: 0 auto;
        padding: 40px 20px 20px 20px;
    }

    .site-title {
        font-size: 1.8rem;
        font-weight: 600;
        letter-spacing: -0.02em;
    }

    .site-title a {
        color: #1a1a1a;
        text-decoration: none;
    }

    .site-nav {
        margin-top: 20px;
        display: flex;
        gap: 24px;
        border-bottom: 1px solid #eaeaea;
        padding-bottom: 12px;
    }

    .site-nav a {
        color: #666;
        text-decoration: none;
        font-size: 0.9rem;
    }

    .site-nav a:hover {
        color: #1a1a1a;
    }

    /* 主容器 */
    .main-container {
        max-width: 900px;
        margin: 0 auto;
        padding: 0 20px;
        display: flex;
        gap: 48px;
    }

    /* 左侧：文章列表 */
    .posts-list {
        flex: 2;
    }

    /* 右侧：侧边栏 */
    .sidebar {
        flex: 1;
    }

    /* 文章卡片 */
    .post-item {
        margin-bottom: 48px;
    }

    .post-date {
        font-size: 0.8rem;
        color: #999;
        margin-bottom: 8px;
    }

    .post-title {
        font-size: 1.4rem;
        font-weight: 600;
        margin-bottom: 8px;
    }

    .post-title a {
        color: #1a1a1a;
        text-decoration: none;
    }

    .post-title a:hover {
        color: #666;
    }

    .post-category {
        font-size: 0.75rem;
        color: #1a1a1a;
        background: #f0f0f0;
        display: inline-block;
        padding: 2px 10px;
        border-radius: 20px;
        margin-bottom: 12px;
    }

    .post-excerpt {
        font-size: 0.85rem;
        color: #666;
        line-height: 1.6;
        margin-bottom: 12px;
    }

    .post-tag {
        font-size: 0.75rem;
        color: #1a1a1a;
        text-decoration: none;
        background: #f0f0f0;
        padding: 2px 10px;
        border-radius: 20px;
        display: inline-block;
        margin-right: 6px;
    }

    /* 侧边栏模块 */
    .sidebar-section {
        margin-bottom: 40px;
    }

    .sidebar-section h3 {
        font-size: 0.85rem;
        font-weight: 600;
        text-transform: uppercase;
        letter-spacing: 1px;
        color: #999;
        margin-bottom: 16px;
    }

    /* 搜索框 */
    .search-input {
        width: 100%;
        padding: 10px 12px;
        border: 1px solid #eaeaea;
        border-radius: 8px;
        font-size: 0.85rem;
        background: #fff;
    }

    .search-input:focus {
        outline: none;
        border-color: #ccc;
    }

    /* 分类列表 */
    .category-list {
        list-style: none;
    }

    .category-list li {
        margin-bottom: 10px;
    }

    .category-list a {
        color: #1a1a1a;
        text-decoration: none;
        font-size: 0.85rem;
    }

    .category-list a:hover {
        color: #666;
    }

    .category-count {
        color: #999;
        font-size: 0.75rem;
        margin-left: 6px;
    }

    /* 标签云 */
    .tag-list {
        display: flex;
        flex-wrap: wrap;
        gap: 8px;
    }

    .tag-list a {
        color: #1a1a1a;
        text-decoration: none;
        font-size: 0.75rem;
        background: #f0f0f0;
        padding: 4px 12px;
        border-radius: 20px;
    }

    .tag-list a:hover {
        background: #e0e0e0;
    }

    /* 关于我 */
    .about-text {
        font-size: 0.85rem;
        color: #666;
        line-height: 1.6;
        margin-bottom: 12px;
    }

    .about-link {
        font-size: 0.8rem;
        color: #1a1a1a;
        text-decoration: none;
    }

    /* 页脚 */
    .site-footer {
        max-width: 900px;
        margin: 60px auto 0;
        padding: 30px 20px;
        text-align: center;
        border-top: 1px solid #eaeaea;
        font-size: 0.75rem;
        color: #999;
    }

    /* 响应式 */
    @media (max-width: 768px) {
        .main-container {
            flex-direction: column;
            gap: 40px;
        }
        .site-title {
            font-size: 1.5rem;
        }
        .post-title {
            font-size: 1.2rem;
        }
    }
</style>

<div class="site-header">
    <div class="site-title">
        <a href="/">Cassi's Blog</a>
    </div>
    <div class="site-nav">
        <a href="/">首页</a>
        <a href="/about">About Me</a>
    </div>
</div>

<div class="main-container">
    <!-- 左侧：文章列表 -->
    <div class="posts-list">
        {% for post in site.posts %}
        <div class="post-item">
            <div class="post-date">{{ post.date | date: "%Y-%m-%d" }}</div>
            <div class="post-title">
                <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
            </div>
            {% if post.categories %}
            <div class="post-category">{{ post.categories | first }}</div>
            {% endif %}
            <div class="post-excerpt">
                {{ post.excerpt | strip_html | truncate: 100 }}
            </div>
            <div>
                {% for tag in post.tags limit: 3 %}
                <a href="#" class="post-tag">#{{ tag }}</a>
                {% endfor %}
            </div>
        </div>
        {% endfor %}
    </div>

    <!-- 右侧：侧边栏 -->
    <div class="sidebar">
        <!-- 搜索 -->
        <div class="sidebar-section">
            <h3>Q 搜索文章</h3>
            <input type="text" id="searchInput" class="search-input" placeholder="输入关键词...">
            <div id="searchResults" style="margin-top: 12px;"></div>
        </div>

        <!-- 分类目录 -->
        <div class="sidebar-section">
            <h3>分类目录</h3>
            <ul class="category-list">
                {% assign categories = site.categories | sort %}
                {% for category in categories %}
                <li>
                    <a href="#">{{ category[0] }}</a>
                    <span class="category-count">({{ category[1].size }})</span>
                </li>
                {% endfor %}
            </ul>
        </div>

        <!-- 标签 -->
        <div class="sidebar-section">
            <h3>标签</h3>
            <div class="tag-list">
                {% assign tags = site.tags | sort %}
                {% for tag in tags limit: 15 %}
                <a href="#">#{{ tag[0] }}</a>
                {% endfor %}
            </div>
        </div>

        <!-- 关于 -->
        <div class="sidebar-section">
            <h3>关于</h3>
            <div class="about-text">
                你好！我是 Cassi，一名编程学习者。
            </div>
            <a href="/about" class="about-link">了解更多 →</a>
        </div>
    </div>
</div>

<div class="site-footer">
    <p>© 2026 Cassi's Blog. Powered by GitHub Pages.</p>
</div>

<script>
    document.getElementById('searchInput').addEventListener('input', function() {
        var searchTerm = this.value.toLowerCase();
        var posts = document.querySelectorAll('.post-item');
        var resultsDiv = document.getElementById('searchResults');
        
        if (searchTerm === '') {
            resultsDiv.innerHTML = '';
            posts.forEach(post => post.style.display = 'block');
            return;
        }
        
        var results = [];
        posts.forEach(post => {
            var title = post.querySelector('.post-title a').innerText.toLowerCase();
            var excerpt = post.querySelector('.post-excerpt').innerText.toLowerCase();
            if (title.includes(searchTerm) || excerpt.includes(searchTerm)) {
                results.push(post.cloneNode(true));
            }
        });
        
        if (results.length > 0) {
            posts.forEach(post => post.style.display = 'none');
            resultsDiv.innerHTML = '';
            results.forEach(result => resultsDiv.appendChild(result));
        } else {
            posts.forEach(post => post.style.display = 'none');
            resultsDiv.innerHTML = '<div style="text-align:center; color:#999; padding:20px;">没有找到相关文章</div>';
        }
    });
</script>