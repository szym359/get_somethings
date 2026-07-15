# Skill 触发方式

skill 有两类触发方式：显式触发和隐式触发。

## 显式触发

显式触发就是你直接点名使用某个 skill。

例如：

```text
用 $customer-reply 回复这段投诉
```

或者：

```text
请使用 $legal-risk-check 检查下面这段协议
```

显式触发最稳定，尤其适合你有很多场景 A/B/C/D，又不希望 Codex 自动猜错的时候。

## 隐式触发

隐式触发是 Codex 根据 `description` 判断是否应该使用某个 skill。

例如 skill 写了：

```markdown
description: 当用户需要处理退款投诉、售后沟通、客户安抚、客服回复时使用。
```

然后你说：

```text
帮我回复这个退款投诉：……
```

Codex 可能会自动使用这个 skill。

## description 必须写吗

必须写。

一个 skill 的 frontmatter 至少要有：

```markdown
---
name: skill-name
description: 什么时候应该使用这个 skill
---
```

即使你不想自动触发，也要写 `description`。

保守写法：

```markdown
description: 仅当用户明确要求使用 skill-name 时使用。
```

这种写法可以降低自动误触发概率。

## description 可以写中文吗

可以。

例如：

```markdown
description: 仅当用户明确要求使用 scene-a 时使用。用于 A 场景的话术、规则和处理流程。
```

建议：

- `name` 用英文小写和短横线
- `description` 可以中文
- 想自动匹配就写具体一点
- 只想手动触发就写保守一点

## name 和文件夹名可以不一致吗

可以，但不推荐。

例如：

```text
.agents/skills/customer-reply/SKILL.md
```

里面写：

```markdown
---
name: refund-support
description: 用于退款、售后、客服投诉回复。
---
```

这种情况下，真实触发名通常是：

```text
$refund-support
```

不是：

```text
$customer-reply
```

为了以后不混乱，推荐文件夹名和 `name` 保持一致。

## 控制不自动触发

如果你希望只能手动触发，可以在 skill 目录里添加：

```text
agents/openai.yaml
```

内容：

```yaml
policy:
  allow_implicit_invocation: false
```

同时把 `description` 写成：

```markdown
description: 仅当用户明确要求使用 skill-name 时使用。
```

这是一种比较稳的配置。
