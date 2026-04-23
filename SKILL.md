---
name: role-promo-card
description: >-
  Generates role/character promotional cards (角色宣传卡 / 推荐卡) end-to-end: collects
  role info in any format (chat, paste, file, CSV, or guided Q&A), drafts copy,
  builds a styled HTML card, runs QA, and optionally exports images. No
  pre-existing CSV or template required. Use when the user asks to 做角色宣传图,
  制作推荐卡, 批量出卡, 做角色介绍卡, 生成宣传长图, build character intro cards, or create
  role promotional visuals from any data source.
---

# Role Promo Card Generator

Turns role/character information into a styled, shareable promotional card.
Works with whatever the user has: a pasted description, a spreadsheet, a CSV,
or nothing at all (guided Q&A).

## Step 1 — Collect role information

Ask the user: "请描述你的角色，或直接粘贴资料（任意格式均可）。"

Accept input in any form:

| What the user provides | How to handle it |
|------------------------|-----------------|
| Free-text description | Extract fields directly |
| Pasted table / CSV rows | Parse rows into fields |
| File path | Read the file |
| "I don't have anything" | Run guided Q&A (see below) |

**Guided Q&A** (when user has no existing data):

Ask these questions one by one, skipping any already answered:

1. 角色叫什么？（姓名 / 代号）
2. 年龄 / 职业是什么？
3. 他/她最突出的性格特点是？
4. 这个角色面对什么困境或选择？
5. 你想让读者对这个角色产生什么感受？
6. 有没有想突出的金句或台词？（没有可跳过）
7. 给这个角色打 1-3 个标签（如：职场 / 情感 / 家庭）

Once all required fields are gathered, proceed to Step 2.

## Step 2 — Draft copy

Write copy for each card section. Default rules (user can override any):

| Section | Rule |
|---------|------|
| Identity intro | First person · ≤ 80 chars · structure: identity → conflict → action → stakes |
| Hook sentence | ≤ 20 chars · punchy, creates curiosity |
| Scene description | ≤ 30 chars · sets time/place/mood |
| Key dialogue / line | ≤ 40 chars · the emotional peak |
| Option A / B | ≤ 12 chars each · no line wraps · present a real dilemma |
| Tags | ≤ 3 · last tag visually highlighted |

Show draft and ask: "文案是否需要调整？" before generating HTML.

## Step 3 — Build HTML card

**If the user provides a template** → fill its placeholder slots.

**If no template exists** → generate a self-contained HTML file with:

- Clean card layout (max-width 480 px, mobile-friendly)
- Card 1: identity panel (role name + intro copy + tags)
- Card 2: scene panel (hook + scene + dialogue + options A/B)
- Neutral default color palette — tell the user which CSS variables to change
  for brand colors

Save as: `YYMMDD-role-promo-<role-name>.html`
If no output directory is specified, save in the current working directory.

## Step 4 — QA checklist

Before delivering:

- [ ] No text overflows card boundaries
- [ ] Option A/B each fits on one line
- [ ] Named relationships are explicit ("my manager" not "that person")
- [ ] Tags ≤ 3; last tag visually active
- [ ] No unfilled placeholders (`{{field}}`, `[TODO]`, etc.)

If something fails: adjust copy length first; change layout only as last resort.

## Step 5 — Export images (optional)

Ask: "需要导出图片吗？" If yes:

Use a headless browser or screenshot tool the user has available. If none is
available, show instructions for:
- **Chrome / Edge**: DevTools → "Capture node screenshot" on the card element
- **Python + playwright**: `page.locator(".card").screenshot(path="card.png")`

Export naming:
```
{sequence}-{card1|card2|full}-{role-name}.png
```

## Step 6 — Output summary

```
角色宣传卡已生成。

- 角色      : <name>
- 产出文件  : <path/filename.html>
- 图片导出  : 已完成 / 未进行
```

## Failure handling

| Situation | Action |
|-----------|--------|
| User can't describe the role | Offer to generate a fictional demo to show the format |
| Copy exceeds length limit | Rewrite automatically; highlight changed sections |
| HTML renders broken | Validate CSS variables; check for unclosed tags |
| No output directory access | Save to current working directory and report path |
