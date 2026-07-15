# Skill 目录结构

项目级 skill 的标准位置是：

```text
项目根目录/
  .agents/
    skills/
      skill-name/
        SKILL.md
```

注意是 `.agents`，不是 `.agent`。

每个 skill 都应该是一个独立文件夹。不要写成：

```text
.agents/skills/name1.md
.agents/skills/name2.md
```

也不要把多个 skill 混在一个目录名里：

```text
.agents/skills/name1,name2/SKILL.md
```

推荐：

```text
.agents/
  skills/
    customer-reply/
      SKILL.md
    legal-risk-check/
      SKILL.md
    xiaohongshu-copy/
      SKILL.md
```

## SKILL.md

`SKILL.md` 是必需文件，也是 skill 的入口。

它负责说明：

- skill 叫什么
- 什么时候使用
- 使用时按什么步骤做
- 必要时应该读取哪些资料或使用哪些模板

示例：

```markdown
---
name: refund-support
description: 用于退款、售后、客户投诉、客服回复场景。
---

# Refund Support

处理退款投诉时：

1. 先判断用户诉求类型
2. 再查看 `references/policy.md`
3. 按 `references/tone.md` 的语气回复
4. 如果用户要求超出政策，给出可执行替代方案
```

`SKILL.md` 不建议塞入太长资料。它更像导航页和操作流程。

## references/

`references/` 用来放需要阅读的资料。

常见内容：

- 业务规则
- 话术规范
- 产品说明
- 品牌风格
- 长案例
- 法务条款
- API 摘要
- 数据字段说明

示例：

```text
refund-support/
  SKILL.md
  references/
    policy.md
    tone.md
    examples.md
```

适合把大段文字放在这里，而不是全部塞进 `SKILL.md`。

## scripts/

`scripts/` 用来放可执行脚本。

适合处理：

- 批量转换文件
- 校验格式
- 生成固定模板
- 解析 CSV、Excel、PDF
- 调用项目里的固定工具
- 自动分类或预处理文本

示例：

```text
data-cleanup/
  SKILL.md
  scripts/
    normalize_csv.py
    validate_output.js
```

如果只是文字规则，不需要 `scripts/`。

## assets/

`assets/` 用来放模板、图片、素材或其他可复用文件。

常见内容：

- Word 模板
- PPT 模板
- 图片和 logo
- 邮件 HTML 模板
- 前端模板
- 示例文件

示例：

```text
weekly-report/
  SKILL.md
  assets/
    report-template.docx
    chart-style.png
```

## agents/openai.yaml

这是可选配置文件，可用于控制界面显示或自动触发策略。

常见用途是禁止隐式触发：

```yaml
policy:
  allow_implicit_invocation: false
```

这样 Codex 不会自动选择这个 skill，只有你明确说 `$skill-name` 时才使用。

## 推荐从简单开始

你现在可以先使用这种结构：

```text
.agents/skills/scene-a/
  SKILL.md
  references/
    rules.md
```

当某个 skill 变复杂时，再增加 `examples.md`、`scripts/`、`assets/` 等内容。
