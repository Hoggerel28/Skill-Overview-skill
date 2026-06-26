---
name: skill-overview
description: Pre-work selection gate for choosing plugins, skills, and subagents before development, creation, debugging, analysis, configuration, installation, deployment, or other multi-step tasks. Use when a user wants help deciding what capability to use, when multiple skills/plugins may apply, when a skill or plugin is explicitly mentioned but related options may also matter, or when Chinese explanations of available capabilities are needed. Before using other plugins/skills/subagents, list candidates in Chinese, grouped by type with unified numbering, then pause and wait for the user to choose.
---

# Skill Overview

## 目标

先选能力，再做任务。

帮用户看清可能用到的插件、技能和 subagent，避免自动隐式匹配到不合适的能力。

这是选择门，不是执行门。输出候选清单后必须暂停，等用户用编号确认，再继续真正执行任务。

## 输出要求

1. 先用一句话复述任务目标。
2. 把候选项分成三块：插件、技能、subagent。
3. 所有候选项连续编号，不要分区重置编号。
4. 每项都用中文写清用途、推荐度、适合边界。
5. 主动点名的插件/技能也要继续补充相关候选项。
6. 输出后暂停，等用户用编号确认。
7. 用户确认前，不要进入开发、创作、批量修改、安装、部署、付款、授权、发送消息或删除操作。

### 选择面板格式

```md
任务目标：...

--- 插件 ---
| 编号 | 名称 | 推荐度 | 中文说明 | 建议 |
|---:|---|---|---|---|

--- 技能 ---
| 编号 | 名称 | 推荐度 | 中文说明 | 建议 |
|---:|---|---|---|---|

--- Subagent ---
| 编号 | 名称 | 推荐度 | 中文说明 | 建议 |
|---:|---|---|---|---|

推荐组合：...
请回复编号，例如：选 1、2；或回复 不使用，直接继续。
```

如果某个区域没有合适候选项，写：暂无明显需要。

## 推荐度规则

- 高：几乎直接匹配任务，明显能提高成功率。
- 中：可能有帮助，但不是必须。
- 低：仅在用户偏好或特殊场景下使用。

避免为了凑数列太多项。普通任务优先列 3-8 个候选；复杂任务最多列 12 个左右。

## 主动调用插件或技能时

当用户已经主动提到 `@插件`、`$技能` 或链接到某个技能时，也必须做选择面板：

- 把用户主动点名的项放在前面。
- 翻译它的英文简介或已知用途为中文。
- 继续补充可能遗漏的相关插件、技能、subagent。
- 明确说明主动点名项是否足够，是否建议搭配其他项。

如果无法读取某个技能的完整说明，只根据当前可见的名称和描述做保守判断，并标注不确定。

## Subagent 选择

只有当任务明显适合并行、跨领域或需要专家分工时才推荐 subagent。

示例：

- 前端界面：frontend-developer、ui-designer、ui-fixer
- 后端接口：backend-developer、api-designer
- 架构梳理：code-mapper、microservices-architect
- 测试质量：test-engineer、qa-engineer，如果存在
- 安全审查：security-auditor，如果存在
- 文档整理：documentation-writer，如果存在

如果用户的全局规则要求并行前先询问，必须先问用户是否开启多代理并行。

## 安全和确认

遇到下面事项时，必须额外提醒并等待确认：

- 删除文件或目录
- 付款、购买、订阅
- 授权、登录、写入密钥、暴露 token
- 发送消息、发邮件、发评论、提交 PR
- 部署到生产环境
- 批量修改大量文件

如果用户贴出密钥、token、Cookie、身份证号、银行卡等敏感信息，要提醒其安全风险，并建议撤销或更换。

## 与 Superpowers 的关系

除非用户明确输入 `/superpowers:`，或明确要求启用 Superpowers 流程，不要自动进入 Superpowers 工作流。

如果用户明确要求使用 Superpowers，再把相关 Superpowers 技能列入选择面板，并等待用户确认。

## 输出风格

- 默认简体中文。
- 不啰嗦，不堆术语。
- 给出清楚可选项。
- 不要假装有系统级强制能力。
- 如果此技能无法保证优先触发，要坦诚说明：它只能提高命中率，真正稳定需要配合 AGENTS.md 或用户主动 `$skill-overview`。
