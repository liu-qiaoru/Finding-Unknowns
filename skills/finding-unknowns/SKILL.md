---
name: finding-unknowns
description: Use when starting or steering complex AI-assisted work with ambiguous requirements, unfamiliar code or domains, unclear success criteria, subjective taste, hidden constraints, long-horizon coding, product/design work, or when a model may need to make assumptions.
---

# Finding Unknowns

## 概览

使用这个 skill，把模糊意图转成可执行上下文。核心原则是：prompt、计划和上下文只是地图；真实代码库、领域、用户需求和约束才是领土；两者之间的差距，就是需要发现的 unknowns。

## 未知分类

行动前先分类不确定性：

- **已知的已知：** 用户已经说清楚的事实、目标和约束。
- **已知的未知：** 用户知道自己还没有决定或还没有弄明白的问题。
- **未知的已知：** 用户心里有判断标准，但还没有语言化的品味、经验或直觉。
- **未知的未知：** 用户和 agent 都还没有显式意识到的风险、约束、惯例或选项。

## 工作流

1. **重述地图和领土。**
   说明用户已经给了什么信息、真正的工作会发生在哪里，以及哪些约束可能不在 prompt 里。

2. **在不熟悉的区域做 blind-spot pass。**
   先检查相关代码、领域资料或上下文，再列出可能的未知未知。解释每个盲点为什么可能改变方向。

3. **用 artifact 暴露未知的已知。**
   当成功标准主观或难以描述时，先做轻量选项：原型、草图、HTML mock、设计方向、样例输出或对照表。让用户先反应，再投入昂贵实现。

4. **只追问会改变方向的问题。**
   一次问一个简洁问题。优先问那些会改变架构、数据模型、用户体验、范围或集成策略的问题。如果答案只影响文案或小样式，做保守假设并记录。

5. **语言不够时使用参考。**
   请求或读取源码、现有组件、历史文档、截图、竞品案例或库实现。源码通常是最丰富的参考。

6. **重大工作前写实施计划。**
   先列用户最可能想调整的决策：数据模型、公开 API、UX flow、迁移路径、风险和测试策略。机械重构和显然步骤放后面。

7. **实现中记录发现。**
   长任务中维护临时笔记，例如 `implementation-notes.md`。记录偏离计划的地方、假设、边界情况和保守选择，让下一轮迭代可以学习。

8. **实现后闭环。**
   给 reviewer 一份短解释：改了什么、为什么改、还剩哪些假设、处理了哪些风险、如何验证。复杂变更可以用 quiz 检查自己或用户是否真的理解行为。

## Prompt 模板

```text
Do a blind-spot pass before implementation. I know [context], but I may be missing hidden constraints in [codebase/domain]. Find my relevant unknown unknowns and help me prompt you better.
```

```text
Before wiring anything up, create [N] lightweight alternatives for [feature/output] so I can react to the direction. Optimize for exposing tradeoffs and assumptions.
```

```text
Interview me one question at a time. Prioritize questions where my answer would change architecture, UX, data model, scope, or integration strategy.
```

```text
Read [reference path/link/module]. Recreate the same semantics/style/behavior for [target], and call out any assumptions where the reference does not map cleanly.
```

```text
Write an implementation plan. Lead with decisions I may want to tweak, then list risks, tests, and only then the mechanical steps.
```

```text
Keep implementation notes. If you deviate from the plan because of an edge case, choose the conservative path, log it under Deviations, and keep going.
```

## Artifact 选择规则

使用这个 skill 时，默认一次只产出一个当前阶段最有用的 artifact，不要一次性生成全套材料。

### 默认顺序

1. **Unknowns brief：** 任务开始、需求模糊、领域不熟或隐藏约束较多时，先产出它。
2. **Interview：** `Unknowns brief` 发现关键决策未定时，一次只问一个会改变方向的问题。
3. **Prototype set：** 成功标准主观、用户说不清但看得出来时，先给几个低成本方向。
4. **Implementation plan：** 关键未知收敛、准备执行前再写。可变更决策在前，机械步骤在后。
5. **Implementation notes：** 长任务或实现中发现新未知、偏离计划时维护。
6. **Reviewer explainer：** 完成后需要交接、评审或争取 buy-in 时产出。

### 默认落盘策略

- 探索期默认把 `Unknowns brief` 保存到 `docs/finding-unknowns/YYYY-MM-DD-<topic>-unknowns.md`。
- 如果继续进入计划阶段，把 `Implementation plan` 保存到 `docs/finding-unknowns/YYYY-MM-DD-<topic>-plan.md`。
- `Prototype set` 默认保存到 `docs/finding-unknowns/YYYY-MM-DD-<topic>-prototypes.md`；如果是可视化 HTML，则保存为 `.html`。
- `Implementation notes` 默认保存为当前任务目录下的 `implementation-notes.md`，因为它是实现中的临时工作笔记。
- `Reviewer explainer` 默认保存到 `docs/finding-unknowns/YYYY-MM-DD-<topic>-reviewer-explainer.md`。
- 如果用户明确说“不要落盘”或任务很短，只在对话中输出，并说明未保存文件。

### 命名规则

- `<topic>` 使用 3-6 个英文 kebab-case 词，来自任务目标，例如 `auth-provider-unknowns`。
- 文件开头写清楚：任务、日期、当前阶段、下一步建议。
- 每次保存后，在回复里给出文件路径和本轮只产出了哪一种 artifact。

## 常见错误

- 以为 prompt 更长就等于上下文足够；更长的地图仍然可能漏掉领土。
- 在检查可用代码或参考之前问太多问题。
- 对主观任务直接实现，而不是先给用户可以反应的东西。
- 在最终答案里才暴露假设，而不是做决策时就记录。
- 把模型限制得太死，导致它发现计划错误后也不敢转向。
