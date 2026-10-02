---
layout: default
title: AIHOT Radar
---
{% assign zh_posts = site.posts | where: "lang", "zh" %}
{% assign en_posts = site.posts | where: "lang", "en" %}
{% assign latest_zh = zh_posts | first %}
{% assign latest_en = en_posts | first %}


<div id="aihot-home" class="radar-home">
  <header class="radar-nav">
    <a class="radar-brand" href="{{ '/' | relative_url }}" aria-label="AIHOT Radar 首页">
      <svg viewBox="0 0 32 32" aria-hidden="true"><path d="M4 21a12 12 0 0 1 24 0"/><path d="M8 21a8 8 0 0 1 16 0"/><path d="M12 21a4 4 0 0 1 8 0"/><circle cx="16" cy="21" r="2"/></svg>
      <span>AIHOT <b>RADAR</b></span>
    </a>
    <nav class="radar-actions" aria-label="快捷操作">
      <a href="{{ '/feed-zh.xml' | relative_url }}">订阅 RSS</a>
      <a href="https://github.com/hlpatw/Horizon_AIHot">管理站点</a>
    </nav>
  </header>


  <section class="radar-intro">
    <div>
      <p class="radar-status"><span></span> 自动更新中</p>
      <h1>把今天的 AI 变化，<br>压缩成一次有效阅读。</h1>
      <p class="radar-lead">聚合 Hacker News、Reddit、RSS 与 GitHub，由 AI 评分、去重并补充背景。打开即读，不再绕路。</p>
    </div>
    {% if latest_zh %}
    <div class="radar-signal" aria-label="最新一期信息">
      <span>最新一期</span>
      <strong>{{ latest_zh.date | date: "%m.%d" }}</strong>
      <small>{{ latest_zh.content | strip_html | size }} 字符情报</small>
    </div>
    {% endif %}
  </section>


  <div id="lang-zh" class="lang-section">
    {% if latest_zh %}
    <section class="digest-toolbar" aria-label="今日速递工具栏">
      <div>
        <span class="section-kicker">今日速递</span>
        <h2>{{ latest_zh.date | date: "%Y 年 %m 月 %d 日" }}</h2>
      </div>
      <label class="digest-search">
        <svg viewBox="0 0 24 24" aria-hidden="true"><circle cx="11" cy="11" r="6"/><path d="m16 16 4 4"/></svg>
        <input id="digest-search" type="search" placeholder="搜索今日资讯、标签或来源" autocomplete="off">
      </label>
    </section>


    <div class="digest-layout">
      <article id="latest-digest" class="embedded-digest">
        {{ latest_zh.content }}
      </article>
      <aside class="digest-aside">
        <div class="aside-sticky">
          <p>快速浏览</p>
          <nav id="digest-nav" aria-label="今日条目目录"></nav>
          <a class="full-report-link" href="{{ latest_zh.url | relative_url }}">独立阅读模式</a>
        </div>
      </aside>
    </div>
    {% else %}
    <div class="empty-radar">日报生成后会直接出现在这里。</div>
    {% endif %}


    <section class="archive-strip">
      <div><span class="section-kicker">往期归档</span><h2>继续回看</h2></div>
      <div class="archive-list">
        {% for post in zh_posts limit:8 %}
          <a href="{{ post.url | relative_url }}"><time>{{ post.date | date: "%m.%d" }}</time><span>{{ post.title | replace: 'Horizon Summary: ', '' | replace: ' (ZH)', '' }}</span></a>
        {% endfor %}
      </div>
    </section>
  </div>


  <div id="lang-en" class="lang-section hidden">
    {% if latest_en %}
      <section class="digest-toolbar"><div><span class="section-kicker">Latest briefing</span><h2>{{ latest_en.date | date: "%B %d, %Y" }}</h2></div></section>
      <article class="embedded-digest">{{ latest_en.content }}</article>
    {% endif %}
  </div>
</div>
