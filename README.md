# Finding Unknowns Skill

一个用于 Codex 的技能：在复杂 AI 协作任务开始前、执行中和完成后，帮助发现盲点、隐藏假设、模糊成功标准和还没有说清楚的约束。

它来自「地图不是领土」这个思路：提示词、计划和上下文只是地图；真正的代码库、业务、用户需求和现实约束才是领土。地图和领土之间的差距，就是需要被发现和管理的 unknowns。

## 安装

### Codex

在 Codex 里使用内置的 skill installer，不需要直接运行 Python 脚本：

```text
$skill-installer
Install https://github.com/liu-qiaoru/Finding-Unknowns/tree/main/skills/finding-unknowns
```

安装后重启 Codex，让新 skill 生效。

### Claude Code

Claude Code 使用 plugin marketplace 安装。这个仓库已经包含 `.claude-plugin/marketplace.json` 和 plugin 目录：

```text
/plugin marketplace add liu-qiaoru/Finding-Unknowns
/plugin install finding-unknowns@finding-unknowns
/reload-plugins
```

安装后使用：

```text
/finding-unknowns:finding-unknowns
```

## 使用

当任务存在需求模糊、代码库不熟、领域不熟、成功标准主观、隐藏约束较多，或者模型可能需要自行猜测时，可以这样使用：

```text
Use $finding-unknowns to do a blind-spot pass before we implement this feature.
```

也可以直接用中文说：

```text
使用 $finding-unknowns，先帮我找出这个任务里的未知、盲点和需要确认的问题。
```

## 它会产出什么

- **未知清单：** 已知事实、已知未知、可能的盲点、建议追问的问题。
- **原型方向：** 对主观或难描述的目标，先做几个轻量选项让你反应。
- **高价值访谈：** 一次问一个会改变架构、交互、数据模型或范围的问题。
- **实施计划：** 先列最可能需要你调整的决策，再列风险、测试和机械步骤。
- **实施笔记：** 记录假设、偏离计划的地方、边界情况和保守选择。
- **评审解释：** 完成后用简短说明帮助 reviewer 理解变更、验证方式和残余风险。
