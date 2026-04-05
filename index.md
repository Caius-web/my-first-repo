---
layout: default
title: 首页
---

<div style="display: flex; gap: 40px; flex-wrap: wrap;">
    <!-- 左侧：文章列表 -->
    <div style="flex: 2; min-width: 250px;">
        <h2>📝 最新文章</h2>
        {% for post in site.posts %}
        <div style="margin-bottom: 30px; border-bottom: 1px solid #eee; padding-bottom: 20px;">
            <h3 style="margin-bottom: 5px;">
                <a href="{{ post.url | relative_url }}" style="color: #333; text-decoration: none;">{{ post.title }}</a>
            </h3>
            <div style="color: #999; font-size: 0.9em; margin-bottom: 10px;">
                {{ post.date | date: "%Y-%m-%d" }}
            </div>
            <div>
                {% for category in post.categories %}
                <span style="background: #667eea; color: white; padding: 2px 8px; border-radius: 15px; font-size: 0.8em;">{{ category }}</span>
                {% endfor %}
            </div>
            <p style="margin-top: 10px; color: #666;">{{ post.excerpt | strip_html | truncate: 100 }}</p>
        </div>
        {% endfor %}
    </div>

    <!-- 右侧：侧边栏 -->
    <div style="flex: 1; min-width: 200px;">
        <!-- 搜索框 -->
        <div style="background: #f5f5f5; padding: 20px; border-radius: 10px; margin-bottom: 30px;">
            <h3>🔍 搜索文章</h3>
            <input type="text" id="search-input" placeholder="输入关键词..." style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
            <div id="search-results" style="margin-top: 10px;"></div>
        </div>

        <!-- 分类目录 -->
        <div style="background: #f5f5f5; padding: 20px; border-radius: 10px; margin-bottom: 30px;">
            <h3>📂 分类目录</h3>
            <ul style="list-style: none; padding: 0;">
                {% assign categories = site.categories | sort %}
                {% for category in categories %}
                <li style="margin-bottom: 8px;">
                    <a href="#" style="color: #667eea; text-decoration: none;">{{ category[0] }}</a>
                    <span style="color: #999;">({{ category[1].size }})</span>
                </li>
                {% endfor %}
            </ul>
        </div>

        <!-- 标签云 -->
        <div style="background: #f5f5f5; padding: 20px; border-radius: 10px;">
            <h3>🏷️ 标签</h3>
            <div>
                {% assign tags = site.tags | sort %}
                {% for tag in tags %}
                <a href="#" style="display: inline-block; background: #fff; padding: 3px 10px; margin: 3px; border-radius: 15px; text-decoration: none; color: #667eea; font-size: 0.9em;">{{ tag[0] }}</a>
                {% endfor %}
            </div>
        </div>
    </div>
</div>

<!-- 搜索功能的 JavaScript -->
<script>
    document.getElementById('search-input').addEventListener('input', function() {
        var searchTerm = this.value.toLowerCase();
        var posts = document.querySelectorAll('.post-item');
        var resultsDiv = document.getElementById('search-results');
        
        if (searchTerm === '') {
            resultsDiv.innerHTML = '';
            return;
        }
        
        var results = [];
        {% for post in site.posts %}
        if ("{{ post.title }}".toLowerCase().includes(searchTerm) || "{{ post.content | strip_html }}".toLowerCase().includes(searchTerm)) {
            results.push('<div style="margin-bottom: 10px;"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></div>');
        }
        {% endfor %}
        
        if (results.length > 0) {
            resultsDiv.innerHTML = '<div style="background: white; padding: 10px; border-radius: 5px;">' + results.join('') + '</div>';
        } else {
            resultsDiv.innerHTML = '<div style="background: white; padding: 10px; border-radius: 5px;">没有找到相关文章</div>';
        }
    });
</script>