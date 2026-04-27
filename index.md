---
layout: default
title: 首页
summary: PM视角下的 multi-agent 学习路线、阶段总结与设计抽象。
---

<section class="hero">
  <div class="hero-grid">
    <div>
      <div class="eyebrow">PM Perspective · Multi-Agent Notes</div>
      <h1>把 multi-agent 从概念拆到边界</h1>
      <p class="lede">
        这个站点整理的是一套面向 PM 的 multi-agent 学习笔记。重点不是记框架配置，而是抓住 agent、context、workspace、tools、sandbox、runtime 和渐进式披露之间的结构关系。
      </p>
      <div class="pill-row">
        <span class="pill">Agent 基础</span>
        <span class="pill">Context / Workspace</span>
        <span class="pill">Tools / Sandbox</span>
        <span class="pill">Routing</span>
        <span class="pill">Delegate</span>
        <span class="pill">Runtime</span>
        <span class="pill">Progressive Disclosure</span>
      </div>
    </div>
    <div class="card">
      <h2>这不是代码模板</h2>
      <p>这是一个学习型项目，适合想从产品和系统设计视角理解 multi-agent 的读者。</p>
      <p>如果你的目标是先建立设计判断，再迁移到具体框架，这个仓库比一堆配置片段更合适。</p>
    </div>
  </div>
</section>

<section class="card" id="reading-path">
  <h2>推荐阅读顺序</h2>
  <ul class="path-list">
    <li>
      <strong><a href="{{ '/study-plan/' | relative_url }}">学习清单</a></strong>
      先建立总路线，知道每一阶段要回答什么问题。
    </li>
    <li>
      <strong><a href="{{ '/agent-basics/' | relative_url }}">第一阶段：Agent 基础</a></strong>
      先理解 agent 是最小运行单元，而不是一段 prompt。
    </li>
    <li>
      <strong><a href="{{ '/context-and-workspace/' | relative_url }}">第二阶段：上下文与工作空间</a></strong>
      搞清楚为什么成熟系统不默认共享全部信息。
    </li>
    <li>
      <strong><a href="{{ '/tools-and-sandbox/' | relative_url }}">第三阶段：Tools 与 Sandbox</a></strong>
      从“知道什么”推进到“能做什么”，建立能力边界视角。
    </li>
    <li>
      <strong><a href="{{ '/multi-agent-routing/' | relative_url }}">第四阶段：Multi-Agent Routing</a></strong>
      理解任务如何分发、结果如何回收，以及为什么协调层必须保持薄。
    </li>
    <li>
      <strong><a href="{{ '/delegate-architecture/' | relative_url }}">第五阶段：Delegate Architecture</a></strong>
      理解 agent 如何以独立身份代表人或组织行动，以及自治为什么必须逐级开放。
    </li>
    <li>
      <strong><a href="{{ '/runtime-and-progressive-disclosure/' | relative_url }}">番外：Runtime 与渐进式披露</a></strong>
      把运行机制和权限开放节奏串起来看。
    </li>
  </ul>
</section>

<section class="split" id="notes">
  <div class="card">
    <h2>核心判断</h2>
    <ul>
      <li>多 agent 的价值不在多角色，而在多边界。</li>
      <li>边界至少包括信息、工具、权限和身份这四层。</li>
      <li>运行时系统负责裁决能不能做，大模型负责提出想做什么。</li>
      <li>成熟的系统依赖渐进式披露，而不是默认全量开放。</li>
    </ul>
  </div>
  <div class="card">
    <h2>适合谁看</h2>
    <ul>
      <li>想从 PM 视角理解 multi-agent 的人。</li>
      <li>不想一开始就陷入框架配置细节的人。</li>
      <li>想先掌握抽象，再迁移到 OpenClaw 或其他框架的人。</li>
    </ul>
  </div>
</section>

<section class="card">
  <h2>笔记目录</h2>
  <ul class="note-list">
    <li>
      <a href="{{ '/study-plan/' | relative_url }}">
        <strong>基于 OpenClaw 学习 Multi-Agent 框架学习清单</strong>
        用整体路线图组织学习顺序和阶段目标。
        <span class="note-meta">Open note</span>
      </a>
    </li>
    <li>
      <a href="{{ '/agent-basics/' | relative_url }}">
        <strong>第一阶段学习总结：Agent 基础</strong>
        解释 agent、workspace、session、tools 和 identity 的最小模型。
        <span class="note-meta">Open note</span>
      </a>
    </li>
    <li>
      <a href="{{ '/context-and-workspace/' | relative_url }}">
        <strong>第二阶段学习总结：上下文与工作空间</strong>
        解释 context layering、最小必要暴露和信息边界。
        <span class="note-meta">Open note</span>
      </a>
    </li>
    <li>
      <a href="{{ '/tools-and-sandbox/' | relative_url }}">
        <strong>第三阶段学习总结：Tools 与 Sandbox 权限控制</strong>
        解释工具即权限，以及 runtime 如何执行边界。
        <span class="note-meta">Open note</span>
      </a>
    </li>
    <li>
      <a href="{{ '/multi-agent-routing/' | relative_url }}">
        <strong>第四阶段学习总结：Multi-Agent Routing</strong>
        解释任务分发、结果回收、下一跳判断与薄协调层。
        <span class="note-meta">Open note</span>
      </a>
    </li>
    <li>
      <a href="{{ '/delegate-architecture/' | relative_url }}">
        <strong>第五阶段学习总结：Delegate Architecture</strong>
        解释代理身份、on-behalf-of 授权、自治分层与安全硬化。
        <span class="note-meta">Open note</span>
      </a>
    </li>
    <li>
      <a href="{{ '/runtime-and-progressive-disclosure/' | relative_url }}">
        <strong>番外学习总结：Agent Runtime 与渐进式披露</strong>
        解释运行循环、审批门、权限升级节奏与自治层级。
        <span class="note-meta">Open note</span>
      </a>
    </li>
  </ul>
</section>
