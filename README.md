# role-promo-card

A Cursor Agent Skill that generates role/character promotional cards (角色宣传卡) end-to-end — no CSV, no template required.

## What it does

- Collects role info in **any format**: free-text, pasted table, file, or guided Q&A
- Drafts copy for each card section (identity intro, hook, scene, dialogue, options, tags)
- Generates a **self-contained HTML card** — creates a default template if you don't have one
- Runs a QA checklist before delivery
- Optionally exports images via browser screenshot or Playwright

## Installation

1. Copy the `role-promo-card/` folder into your Cursor skills directory:
   - **Windows**: `C:\Users\<you>\.cursor\skills\`
   - **macOS / Linux**: `~/.cursor/skills/`

2. Restart Cursor.

That's it — no other setup needed.

## Usage

In any Cursor chat, just say:

> 帮我做一张角色宣传卡

or

> 制作推荐卡 / 批量出卡 / 做角色介绍图

The agent will guide you from there, asking only for what it needs.

## Customization

- **Bring your own template**: point the agent to any HTML file with placeholder slots
- **Override copy rules**: paste your own length/tone spec at any point in the conversation
- **Brand colors**: the generated default template exposes CSS variables you can change

## License

MIT
