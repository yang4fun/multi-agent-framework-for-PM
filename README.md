# Multi-Agent Framework for PM

这是一个面向 PM 视角的 multi-agent 学习仓库。

仓库内容不是框架源码，而是围绕 OpenClaw 这类 agent 系统整理出的学习清单、阶段总结和抽象方法，重点放在以下几个问题上：

- Agent 到底是什么，而不是什么
- 多 agent 为什么不能退化成“多个名字的单 agent”
- 上下文、工作空间、工具、权限、运行时之间如何分层
- 渐进式披露为什么是 multi-agent 设计里的关键原则

## 仓库适合谁

这个仓库适合以下读者：

- 想从产品或系统设计视角理解 multi-agent 的 PM
- 不想一上来就陷入框架配置细节的人
- 想先抓住抽象，再迁移到具体实现的人

如果你的目标是直接找可运行代码，这个仓库不是代码模板，而是一套学习与设计笔记。

## 阅读建议

建议按下面顺序阅读：

1. [基于OpenClaw学习Multi-Agent框架-学习清单.md](./基于OpenClaw学习Multi-Agent框架-学习清单.md)
2. [第一阶段学习总结-Agent基础.md](./第一阶段学习总结-Agent基础.md)
3. [第二阶段学习总结-上下文与工作空间.md](./第二阶段学习总结-上下文与工作空间.md)
4. [第三阶段学习总结-Tools与Sandbox权限控制.md](./第三阶段学习总结-Tools与Sandbox权限控制.md)
5. [第四阶段学习总结-Multi-Agent Routing.md](./第四阶段学习总结-Multi-Agent Routing.md)
6. [番外学习总结-AgentRuntime与渐进式披露.md](./番外学习总结-AgentRuntime与渐进式披露.md)

阅读顺序对应的核心主线是：

`Agent 基础 -> Context / Workspace -> Tools / Sandbox -> Routing -> Runtime -> Progressive Disclosure`

## 文件说明

### 1. 学习清单

[基于OpenClaw学习Multi-Agent框架-学习清单.md](./基于OpenClaw学习Multi-Agent框架-学习清单.md)

这份文档定义了整体学习路线，重点不是记配置，而是建立 multi-agent 的共性认知。你可以把它当成整个仓库的导航页。

### 2. 第一阶段：Agent 基础

[第一阶段学习总结-Agent基础.md](./第一阶段学习总结-Agent基础.md)

这一阶段主要回答：

- Agent 为什么不只是 prompt
- workspace、session、tools、identity 分别是什么
- 设计一个 agent 时，最小需要定义哪些边界

### 3. 第二阶段：上下文与工作空间

[第二阶段学习总结-上下文与工作空间.md](./第二阶段学习总结-上下文与工作空间.md)

这一阶段主要回答：

- 为什么上下文不是越多越好
- workspace 和 context 有什么区别
- 全局知识、私有知识、任务上下文、会话历史、凭据为什么要分层

### 4. 第三阶段：Tools 与 Sandbox

[第三阶段学习总结-Tools与Sandbox权限控制.md](./第三阶段学习总结-Tools与Sandbox权限控制.md)

这一阶段把重点从“知道什么”推进到“能做什么”，核心是：

- 工具本身就是权限
- allow / ask / deny 比简单放权更成熟
- sandbox 不只是安全壳，更是职责边界的执行机制

### 5. 第四阶段：Multi-Agent Routing

[第四阶段学习总结-Multi-Agent Routing.md](./第四阶段学习总结-Multi-Agent Routing.md)

这一阶段主要回答：

- 入口 agent 和 specialist agent 的职责分别是什么
- 任务应该怎么分发，结果怎么回收
- routing 为什么不能退化成固定流水线
- 为什么协调层必须保持薄

### 6. 番外：Runtime 与渐进式披露

[番外学习总结-AgentRuntime与渐进式披露.md](./番外学习总结-AgentRuntime与渐进式披露.md)

这篇把运行机制和权限开放节奏连起来看，重点说明：

- agent runtime 的最小循环是什么
- 为什么 agent 不应该一次性被喂满上下文和权限
- 为什么自治、工具、凭据都应该按阶段开放

## 这套笔记的核心判断

如果只保留几条最关键的判断，这个仓库想表达的是：

- 多 agent 的价值不在“多角色”，而在“多边界”
- 边界至少包括信息边界、工具边界、权限边界和身份边界
- 运行时系统负责裁决能不能做，大模型负责提出想做什么
- 成熟的 multi-agent 系统依赖渐进式披露，而不是默认全量开放

## 后续可扩展方向

这个仓库后面可以继续补充：

- `Delegate Architecture` 分层总结
- 一个最小 PM multi-agent 系统设计稿
- 从抽象到具体框架的映射表

## 仓库状态

当前仓库以学习笔记为主，已经推送到 GitHub：

`https://github.com/yang4fun/multi-agent-framework-for-PM`
