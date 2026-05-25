---
type: concept
tags:
  - 精灵
  - 数据抓取
  - BWIKI
  - workflow
summary: 从 BWIKI rocom 站点批量获取洛克王国精灵核心数据的标准化流程
source_file: ""
updated: 2026-05-21
---

# 从洛克 WIKI 获取精灵数据

## 概述

从 **BWIKI rocom**（洛克王国：世界）站点自动抓取精灵核心数据，输出为标准化格式。

**数据源**：`https://wiki.biligame.com/rocom/{精灵名称}`

> ⚠️ rocom = 洛克王国：世界（手游版），与原版端游数据不同。

## 输出格式（6 项）

每只精灵统一输出以下字段：

```
## {精灵名称}

- **属性**：{单属性 / 属性1 + 属性2}
- **种族值**（{总和}）：精力 X / 物攻 X / 魔攻 X / 物防 X / 魔防 X / 速度 X
- **特性**：{特性名} — {效果简述}
- **被克制**：{弱点属性列表}
- **抵抗**：{优势属性列表}
```

## 执行步骤

### Step 1: WebFetch 抓取

```
URL: https://wiki.biligame.com/rocom/{UTF-8编码的精灵名}
Prompt: 提取名称、编号、属性、种族值(6维+总和)、特性(名称+效果)、被克制属性、抵抗属性、身高体重
```

### Step 2: 回退策略

WebFetch 返回空或不完整时，使用 `agent-browser`：

```bash
agent-browser open "https://wiki.biligame.com/rocom/{名称}"
agent-browser wait --load networkidle
agent-browser snapshot   # 用正则提取 StaticText/InlineTextBox 数值
agent-browser close
```

> snapshot 中文在终端会乱码，但数值全部可读；中文需用 WebFetch 补充确认。

### Step 3: 格式化输出

按固定 6 项模板输出，不多不少。

## 已收录精灵

| 精灵 | 属性 | 种族值和 | 特性 |
|------|------|----------|------|
| [[雪影娃娃]] | 冰 + 萌 | 617 | 捉迷藏 |
| [[火神]] | 火 | 613 | 助燃 |
| [[水泡壳]] | 水 | 594 | 缩壳 |
| [[魔力猫]] | 草 | 613 | 氧循环 |
| [[岚鸟]] | 翼 | 570 | 顺风 |

## 注意事项

- 站点标识符必须是 **rocom**，不是 rocokingdom（空壳）或 roco（重定向）
- 页面不存在时返回 404，换名字重试即可
- 特性字段若页面未填写则标注"未知"
