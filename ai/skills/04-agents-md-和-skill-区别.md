# AGENTS.md 和 Skill 的区别

`AGENTS.md` 和 skill 都能影响 Codex 的行为，但它们适合的范围不同。

## AGENTS.md

`AGENTS.md` 适合放项目长期默认规则。

例如：

- 这个项目统一用 pnpm
- 提交前必须跑测试
- 后端代码遵守某种分层结构
- 回答用户时统一使用中文
- 不要修改某些自动生成文件
- 代码审查时优先关注安全和回归风险

它像项目的“长期工作约定”。

适合放在：

```text
项目根目录/AGENTS.md
```

或某个子目录下：

```text
backend/AGENTS.md
```

越靠近当前工作目录的规则，通常越具体。

## Skill

skill 适合放某一类任务才需要的专用规则。

例如：

- 只有写客服回复时才使用客服话术
- 只有做法律风险检查时才使用法务清单
- 只有写小红书文案时才使用小红书风格规则
- 只有生成周报时才使用周报模板

它像“某个场景的专用工具包”。

适合放在：

```text
.agents/skills/skill-name/SKILL.md
```

## 怎么选择

如果规则应该一直生效，放 `AGENTS.md`。

如果规则只在某类任务中生效，做成 skill。

如果规则只是这一次对话需要，直接写在当前提示词里。

## 对比表

| 项目 | AGENTS.md | Skill |
| --- | --- | --- |
| 作用范围 | 项目或子目录默认规则 | 某类任务场景 |
| 触发方式 | 自动随项目上下文生效 | 显式 `$skill` 或隐式匹配 |
| 适合内容 | 编码规范、测试命令、项目约定 | 工作流程、话术、模板、引用资料 |
| 文件位置 | `AGENTS.md` | `.agents/skills/name/SKILL.md` |
| 是否适合多场景 A/B/C/D | 不太适合 | 很适合 |

## 推荐组合

可以这样搭配：

```text
AGENTS.md
.agents/
  skills/
    customer-reply/
      SKILL.md
    legal-risk-check/
      SKILL.md
```

`AGENTS.md` 写全项目通用规则。

不同 skill 写不同场景下的专用规则。
