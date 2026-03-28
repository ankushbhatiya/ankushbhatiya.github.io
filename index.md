---
layout: home
title: "Welcome"
---

# 🌐 Global Alpha Engine

![Multi-Agent Hedge Fund Banner](/assets/images/banner.svg)

An autonomous algorithmic trading system leveraging a collaborative multi-agent architecture to synthesize sentiment, mathematical rigor, and risk management across global equity markets.

## 📝 Latest Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span class="post-date">{{ post.date | date: "%B %d, %Y" }}</span>
    </li>
  {% endfor %}
</ul>

## 🏗 System Architecture

The project is divided into four specialized agents:

1. **🔍 The Analyst** — Alpha & Sentiment Engine
2. **🔢 The Quant** — Strategy Architect  
3. **🛡️ The Risk Manager** — Safety & Execution
4. **📚 The Librarian** — Data Ingestion

[View on GitHub](https://github.com/ankushbhatiya/hedge_fund){: .btn .btn-primary }
