---
layout: note
title: 第五阶段学习总结：Delegate Architecture
summary: 理解 delegate 不是任务 handoff，而是“有身份、可代表人行动”的代理架构。
permalink: /delegate-architecture/
---

# 第五阶段学习总结：Delegate Architecture

## 1. 这一阶段学到了什么

这一阶段最重要的收获，是把 `Delegate Architecture` 从一个容易误解的词，重新放回 OpenClaw 的真实语境里去理解。

一开始很容易把 `delegate` 理解成：

- 多个 agent 之间如何传任务
- specialist 之间如何 handoff
- 一个 agent 如何把子任务委托给另一个 agent

但在 OpenClaw 的这篇文档里，`Delegate Architecture` 主要不是在讲这个。

它讲的是：

`如何把一个 agent 设计成“有自己身份、代表某个人或组织行动的代理人”。`

核心结论：

`Delegate Architecture 不是任务传递拓扑，而是代理身份、代表关系、自治分层和安全硬化的组合设计。`

这也解释了为什么这一阶段会大量讨论 `Tier 1 / 2 / 3`。

因为在 OpenClaw 的语境里，`tier` 不是跑题，而是：

`delegate 被允许代表人行动到什么程度。`

## 2. 关键概念总结

### 2.1 OpenClaw 里的 Delegate，不是普通意义上的“任务委托”

在泛化的 multi-agent 语境里，`delegate` 很容易让人想到：

- handoff
- task routing
- agent-to-agent delegation

但 OpenClaw 这里的 `delegate` 更接近：

- 一个有自己身份的代理
- 代表一个或多个人行动
- 按明确授权范围工作
- 不伪装成人类本人

这类代理的典型比喻不是“调度器”，而是“组织里的执行助理”。

一句话压缩：

`Routing 更像“任务分给谁”，Delegate 更像“谁以什么身份、代表谁去做事”。`

### 2.2 Delegate 的核心不是“多一个 agent”，而是“多一个被授权的身份”

一个真正的 delegate，通常至少要满足下面几件事：

- 有自己的 identity
  例如邮箱、显示名、日历身份、频道身份

- 明确代表谁
  也就是 on-behalf-of relationship

- 有外部身份系统授予的权限
  例如组织级 identity provider 授权

- 有 standing orders
  也就是明确写清楚什么能自治、什么必须审批

所以 delegate 不是“功能更多的 agent”，而是：

`一个在组织规则下被授予代表权的 agent。`

### 2.3 Delegate 和 Routing 是相连的，但不是同一层问题

第四阶段的 `Multi-Agent Routing` 主要解决：

- 用户消息先进入谁
- 任务交给哪个 specialist
- 结果由谁回收
- 下一跳如何判断

第五阶段的 `Delegate Architecture` 主要解决：

- 哪个 agent 有自己的独立身份
- 它代表谁行动
- 它的自治边界到哪里
- 它和组织授权系统如何打通

所以二者关系可以理解成：

- `Routing`
  解决流转路径

- `Delegate`
  解决代表关系与执行责任

一句话总结：

`Routing 决定任务怎么流，Delegate 决定谁能以什么身份把动作做成。`

### 2.4 为什么这一阶段会重点讲 Tier

因为 OpenClaw 的 delegate 不是“有授权就全自动”，而是强调：

`能力和自治都应该逐级开放。`

delegate 的能力层级，文档里主要分成三档：

- `Tier 1: Read-Only + Draft`
  能读、能分析、能起草，但不直接正式发送或提交

- `Tier 2: Send on Behalf`
  能代表 principal 正式发送消息、创建事件、执行明确动作

- `Tier 3: Proactive`
  能按 standing orders 主动运行、持续执行、异步让人复查

所以 `tier` 在这一阶段里的意义不是“能力强弱”，而是：

`系统把多大的自治权交给 delegate。`

### 2.5 Tier 讲的不是“会不会”，而是“允不允许它直接生效”

这一阶段最容易混淆的，是把：

- `有没有能力`
- `能不能自主执行`

混成一回事。

更准确的分法应该是：

- `tool / permission`
  决定它有没有某类动作能力

- `tier / delegate`
  决定它能不能在当前任务里自主把这类动作正式做掉

所以：

`allow tool` 不等于 `allow delegate`。

例如一个 agent 可能：

- 技术上有发送邮件的能力
- 但制度上只能先起草邮件
- 必须经人确认后，才能真正发送

这说明：

- 它有发送能力
- 但默认没有自主发送的自治权

### 2.6 为什么默认应该从 Tier 1 开始

成熟系统不应该一开始就给到 `Tier 2` 或 `Tier 3`，原因至少有三类：

- `任务推进顺序`
  很多正式动作本来就应该建立在草稿、校对、确认之后

- `风险控制`
  草稿写错可以改，正式动作做错会直接影响外部世界

- `责任归属`
  正式执行意味着系统在替人行动，这需要明确授权，而不是模型自己判断“应该可以”

所以默认从 `Tier 1` 开始，不是因为 agent 不够强，而是因为：

`正式执行应该建立在更成熟的中间结果和更明确的授权之上。`

### 2.7 Tier 升级应该怎么发生

一个更成熟的 delegate 升级路径，通常不是永久拉高自治，而是：

`任务推进 -> agent 识别已到执行节点 -> 发起升级申请 -> 人批准 -> 获得单次执行权 -> 完成动作 -> 权限收回`

这里要分清：

- `agent`
  可以判断任务是否已经推进到需要正式执行

- `human`
  才是最终批准者

所以 delegate 可以：

- 判断风险
- 整理待发送内容
- 发起审批请求

但它不应该：

- 自己批准自己执行敏感动作

一句话总结：

`升级可以由 agent 发起，但批准不应该由 agent 自己完成。`

### 2.8 授权默认应该是单次、临时，而不是整类、永久

这点很重要。

如果一个 delegate 在一次邮件发送之后，就永久获得“今后都可自动发送”的权利，那么系统很快会失控。

因为：

- 第一封邮件成熟，不等于后面每一封都成熟
- 第一封适合发送，不等于后面每次都应该直接发
- 长期授权会绕开“先草稿，再确认”的护栏

所以默认更成熟的方式通常是：

- 对当前动作授权
- 对当前节点临时生效
- 动作完成后回收权限

这也是渐进式披露在 delegate 架构里的延续。

## 3. Delegate Architecture 的更完整学习框架

如果只按 `Tier 1 / 2 / 3` 来理解这一章，会把它讲窄。

更完整的框架应该是：

### 3.1 Delegate 是什么

不是 handoff agent，而是：

`一个有自己身份、可代表某个人或组织行动的代理。`

### 3.2 Delegate 和 Routing 的关系

`Routing`
解决任务流转。

`Delegate`
解决身份、授权、代表关系和执行责任。

### 3.3 Delegate 的核心组成

- identity
- principal / on-behalf-of relationship
- standing orders
- identity provider delegation
- channel binding
- auth isolation

### 3.4 Capability Tiers

- `Tier 1`
  读取 + 起草

- `Tier 2`
  代用户正式执行

- `Tier 3`
  主动持续执行

### 3.5 Hardening

在给 delegate 连真实身份和真实权限之前，必须先做边界加固，例如：

- hard blocks
- tool restrictions
- sandbox isolation
- audit trail

所以这一章真正讲的是：

`代理身份 + on-behalf-of 授权 + 自治分层 + 安全硬化`

而不只是“能力 tier 设计”。

## 4. 一个 PM 视角下的最小 Delegate 例子

假设系统里有一个 `org-assistant`，它不是普通写稿 agent，而是一个真正的组织代理。

它具备：

- 自己的邮箱身份
- 自己的显示名
- 可绑定到组织频道
- 可以代表某位负责人对外沟通

那么它的分层可以是：

### Tier 1

- 读取邮件线程
- 总结待办
- 草拟回复
- 给负责人确认

### Tier 2

- 在负责人确认后，代表其发送邮件
- 创建会议邀请
- 向指定团队频道发布确定通知

### Tier 3

- 每周定时整理竞品动态
- 按 standing orders 生成内部周报
- 发送到指定团队频道供异步复查

这个例子里最关键的不是“它会发邮件”，而是：

- 它是不是有自己的身份
- 它是不是代表某个 principal 行动
- 它是不是被明确限制了能做哪些事
- 它是不是只在特定 tier 下才能执行正式动作

## 5. 这一阶段是否通过的判断标准

如果你现在已经能稳定区分下面这些点，就算这一阶段过关：

- `Delegate Architecture` 在 OpenClaw 里主要不是 task handoff，而是组织代理架构
- `delegate` 的重点是身份、代表关系和授权边界，不只是“多一个 agent”
- `Routing` 和 `Delegate` 相连，但解决的是不同层问题
- `Tier 1 / 2 / 3` 讲的是自治程度，而不是单纯能力强弱
- `tool / permission` 和 `tier / delegate` 不是一回事
- agent 可以发起升级，但不应自己完成最终审批
- 默认授权更适合单次、临时，而不是整类、永久
- 在接真实权限前，必须先做 hardening，而不是先给权再补护栏

## 6. 下一阶段入口

第六阶段将进入：

`做框架抽象，而不是停留在 OpenClaw`

重点会从“OpenClaw 是怎么设计的”进一步推进到：

`如何把 agent、context、permission、routing、delegate 这些维度迁移到其他框架中对比分析。`

## 7. 参考来源

- [OpenClaw Delegate Architecture](https://docs.openclaw.ai/concepts/delegate-architecture)
