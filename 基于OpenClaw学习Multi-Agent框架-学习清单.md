---
layout: note
title: 基于 OpenClaw 学习 Multi-Agent 框架学习清单
summary: 一份按阶段拆解的 multi-agent 学习路线图。
permalink: /study-plan/
---

# 基于 OpenClaw 学习 Multi-Agent 框架学习清单

## 1. 学习目标

这份清单的目标不是让你先记住 OpenClaw 的配置细节，而是借 OpenClaw 理解 multi-agent 框架的共性：

- 一个 agent 由哪些部分构成
- 为什么需要多个 agent，而不是一个超级总控
- 多 agent 协作时，路由、权限、上下文、身份如何隔离
- 什么叫渐进式披露，以及它在 agent 框架里如何落地
- 如何把 OpenClaw 的设计抽象迁移到其他框架

---

## 2. 学习总路线

按下面顺序学习，不要一开始就直接钻进 multi-agent 页面：

1. 单 agent 基础
2. workspace 与上下文组织
3. tools / sandbox / 权限边界
4. multi-agent routing
5. delegate architecture
6. 抽象对比其他框架
7. 自己设计一个最小多 agent 系统

核心原则：

- 先理解最小运行单元，再理解协作
- 先理解边界，再理解自治
- 先学抽象，再学配置

---

## 3. 第一阶段：理解单 Agent 是什么

### 目标

先搞清楚 OpenClaw 里的 agent 到底是什么，不要把 agent 理解成一段 prompt。

### 要看什么

- Getting Started
- Agent / Agent Workspace 相关概念页

### 要回答的问题

- 一个 agent 的最小组成是什么
- `workspace` 在 agent 运行里起什么作用
- `AGENTS.md`、`SOUL.md`、`USER.md` 分别承担什么职责
- session 和 workspace 的边界是什么
- agent 的“角色”和“身份”是不是一回事

### 学习产出

读完后，自己用一句话写出你对 agent 的定义：

`Agent = 指令上下文 + 工作目录 + 会话状态 + 工具能力 + 身份边界`

### 检查点

如果你还在把 agent 理解为“一个人设 prompt”，说明这一阶段还没过。

---

## 4. 第二阶段：理解上下文和工作空间

### 目标

理解为什么成熟框架不把所有知识默认共享给所有 agent。

### 要看什么

- Agent Workspace
- 与 context、session、auth 相关的概念

### 要回答的问题

- 为什么每个 agent 要有自己的 workspace
- 什么应该进入全局上下文，什么应该局部加载
- 多个 agent 之间默认共享哪些东西，不共享哪些东西
- 业务知识、用户偏好、执行记录、凭据，这四类信息是否应该放在同一层

### 学习产出

画一张简单图，区分：

- 全局知识
- agent 私有知识
- 当前任务上下文
- 历史会话
- 凭据 / auth

### 检查点

如果你的理解还是“所有 agent 都应该拿到完整背景，这样最聪明”，说明还没真正理解多 agent 的边界设计。

---

## 5. 第三阶段：理解 Tools、Sandbox、权限控制

### 目标

理解 multi-agent 的核心不是“多角色”，而是“不同 agent 拥有不同能力边界”。

### 要看什么

- Tools
- Multi-Agent Sandbox & Tools

### 要回答的问题

- 为什么工具要做 allow / deny
- 为什么不同 agent 不应该默认共享同一套工具
- sandbox 解决的是安全问题、稳定性问题，还是职责问题
- 凭据隔离和工具隔离有什么区别

### 学习产出

整理一张表：

| Agent | 可读 | 可写 | 可执行 | 可外呼/代发 | 备注 |
|------|------|------|--------|-------------|------|
| general | 是 | 否 | 否 | 否 | 总入口 |
| researcher | 是 | 可写草稿 | 有限 | 否 | 只做检索和整理 |
| operator | 是 | 是 | 是 | 视审批而定 | 风险较高 |

### 检查点

如果你发现自己默认想“所有 agent 都能做所有事”，那就是典型的单 agent 思维。

---

## 6. 第四阶段：理解 Multi-Agent Routing

### 目标

理解多 agent 框架中最重要的协调问题：请求怎么分发，结果怎么汇总。

### 要看什么

- Multi-Agent Routing

### 要回答的问题

- 入口 agent 和 specialist agent 的职责分别是什么
- 什么情况下应该新增 agent，什么情况下不该新增
- 一个任务是应该交给一个 agent 完成，还是拆给多个 agent
- routing 是静态规则，还是动态决策
- agent 之间如何通信，为什么不应该无限制互相调用

### 学习产出

用你自己的话写出一个“薄协调层”定义：

`协调层只负责识别任务类型、分发、回收结果，不承担全部专家能力。`

然后自己列出三个 specialist：

- research
- writer
- reviewer

并分别写明它们的输入、输出、边界。

### 检查点

如果你的设计开始出现一个“什么都懂、什么都做、什么都能调”的总控 agent，说明你已经偏向反模式了。

---

## 7. 第五阶段：理解 Delegate Architecture

### 目标

理解 OpenClaw 里的 `Delegate Architecture` 主要不是任务 handoff，而是“一个 agent 如何以独立身份代表某个人或组织行动”，以及它的自治能力为什么要逐级开放。

### 要看什么

- Delegate Architecture

### 要回答的问题

- OpenClaw 里的 `delegate` 为什么不等于普通意义上的 agent-to-agent 委托
- `delegate` 和 `routing` 的关系是什么
- 一个 delegate 为什么需要自己的 identity、principal、on-behalf-of 关系和 standing orders
- 为什么要从最低 tier 开始
- `Read-Only + Draft`、`Send on Behalf`、`Proactive` 三层分别适合什么场景
- 哪些动作必须人审
- 为什么 hardening 应该先于真实权限授予

### 学习产出

先写一句你自己的定义：

`Delegate = 一个有自己身份、在明确授权和边界下代表人或组织行动的 agent。`

再写一张能力升级表：

| Tier | 能力 | 适用场景 | 风险 | 是否建议默认开启 |
|------|------|----------|------|------------------|
| Tier 1 | 读取 + 起草 | 研究、总结、草拟 | 低 | 是 |
| Tier 2 | 代用户执行 | 代发消息、代填内容 | 中 | 否 |
| Tier 3 | 主动执行 | 定时任务、主动触达 | 高 | 否 |

### 检查点

如果你还把这一章理解成“多 agent 之间怎么继续传任务”，或者设计系统时第一反应就是“让 agent 自己全自动跑”，说明还没有真正理解 delegate 的身份含义和渐进式披露。

---

## 8. 第六阶段：做框架抽象，而不是停留在 OpenClaw

### 目标

把 OpenClaw 的设计语言抽象成你以后看其他框架也能复用的分析框架。

### 你要提炼出的五个核心维度

1. Agent 如何定义
2. Context 如何组织
3. Tools / Permission 如何隔离
4. Routing / Handoff 如何发生
5. Autonomy 如何逐步升级

### 学习产出

做一张对比表，后续看其他框架时都用同一张表来填：

| 维度 | OpenClaw | LangGraph | CrewAI | AutoGen |
|------|----------|-----------|--------|---------|
| Agent 定义 |  |  |  |  |
| 状态管理 |  |  |  |  |
| 路由方式 |  |  |  |  |
| 权限隔离 |  |  |  |  |
| 人审机制 |  |  |  |  |
| 渐进自治 |  |  |  |  |

---

## 9. 第七阶段：自己设计一个最小多 Agent 系统

### 目标

用最小例子把概念落地，不要停留在“看懂文档”。

### 建议题目

设计一个面向产品经理的最小 multi-agent 系统。

### 推荐角色

- `generalist-pm`
  - 负责 intake、任务分类、结果汇总
- `researcher`
  - 负责检索、竞品整理、资料收敛
- `spec-writer`
  - 负责输出 PRD 初稿
- `reviewer`
  - 负责 challenge、找缺口、提风险

### 你要明确写出来的东西

- 每个 agent 的职责
- 每个 agent 的必读上下文
- 每个 agent 的工具权限
- 哪些输出进入草稿，哪些输出必须人工确认
- 哪些动作不能自动发生

### 检查点

如果你设计完后发现：

- 每个 agent 都需要读完整业务手册
- 每个 agent 都有相同工具
- 总控 agent 还要亲自完成专家工作

那说明设计还没过关。

---

## 10. 推荐学习节奏

### Day 1

- 看单 agent 与 workspace
- 输出：agent 最小组成定义

### Day 2

- 看 tools、sandbox、权限
- 输出：权限分层表

### Day 3

- 看 multi-agent routing
- 输出：薄协调层设计说明

### Day 4

- 看 delegate architecture
- 输出：tier 升级表

### Day 5

- 做 OpenClaw 抽象总结
- 输出：五维对比表框架

### Day 6

- 设计自己的最小 multi-agent 系统
- 输出：角色、上下文、权限、交接图

### Day 7

- 再去看 LangGraph / CrewAI / AutoGen
- 输出：一页框架对比总结

---

## 11. 学习时最容易踩的坑

- 一上来就研究配置语法，而不是先理解设计抽象
- 只看 agent 人设，不看权限和上下文边界
- 把 multi-agent 理解成“多个 prompt 一起说话”
- 把总控 agent 设计成超级大脑
- 默认给所有 agent 高权限
- 只关注生成效果，不关注审计、回放、复盘

---

## 12. 建议你优先形成的判断标准

以后看任何 multi-agent 框架时，优先用下面这几个问题判断它是否成熟：

1. 它有没有明确的 agent 边界，而不是只有角色描述
2. 它有没有上下文隔离机制
3. 它有没有工具和权限分层
4. 它有没有清晰的 handoff / routing 逻辑
5. 它有没有人审或审批机制
6. 它有没有从低自治到高自治的升级路径
7. 它有没有状态、日志、审计、回放能力

---

## 13. OpenClaw 官方文档建议阅读入口

- Getting Started
- Agent
- Agent Workspace
- Tools
- Multi-Agent Sandbox & Tools
- Multi-Agent Routing
- Delegate Architecture

---

## 14. 一句话总结

用 OpenClaw 学 multi-agent，最好的路径不是：

`多 agent 页面 -> 抄配置`

而是：

`单 agent runtime -> workspace/context -> tools/sandbox -> routing -> delegate tiers -> 抽象迁移到通用框架`

只有这样，你最后学到的才不是 OpenClaw 的用法，而是 multi-agent 框架的底层设计方法。
