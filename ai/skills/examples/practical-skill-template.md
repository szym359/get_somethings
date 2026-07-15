# 实用 Skill 模板

适合规则较多、需要引用资料的场景。

目录：

```text
.agents/skills/customer-reply/
  SKILL.md
  references/
    rules.md
    examples.md
  agents/
    openai.yaml
```

`SKILL.md`：

```markdown
---
name: customer-reply
description: 用于客服回复、投诉处理、退款沟通、售后安抚和用户情绪处理。
---

# Customer Reply

处理客服回复时：

1. 先判断用户诉求和情绪强度
2. 读取 `references/rules.md`
3. 如需参考语气，读取 `references/examples.md`
4. 回复时先承认问题，再给解决路径
5. 不承诺超出政策的补偿
6. 输出最终可直接发送给用户的回复
```

`references/rules.md`：

```markdown
# 客服回复规则

- 语气礼貌、克制、具体
- 不使用夸张承诺
- 不把责任推给用户
- 先说明能做什么，再说明不能做什么
- 必要时给出下一步操作方式
```

`references/examples.md`：

```markdown
# 示例

用户：我申请退款三天了还没有结果。

回复：理解你等待处理结果时会比较着急。我先帮你确认当前进度。如果订单已经进入审核流程，通常会在规定时间内完成处理；如果需要补充信息，我会一次性说明需要你提供的内容。
```

`agents/openai.yaml`：

```yaml
policy:
  allow_implicit_invocation: false
```

使用方式：

```text
用 $customer-reply 回复下面这段投诉：……
```
