---
name: second-brain
description: This skill should be used when the user wants to build, set up, or operate an AI "second brain" — a persistent memory vault (Obsidian-compatible Markdown) that lets an AI agent resume work without re-explaining context, remembers correction instructions across sessions, and auto-organizes raw material into structured knowledge. Trigger on requests like "build my second brain", "set up an Obsidian vault for AI", "give my AI persistent memory", or "make AI stop forgetting".
license: MIT License. Copyright (c) 2026 fuuuuuuma.
---

# Second Brain — 構築と運用

AIエージェントの「外部記憶」となる Vault（Obsidian互換のMarkdown）を構築・運用するスキル。
目的は3つ：(1) 新しいセッションでも前提説明なしに再開できる、(2) 一度の修正指示が次回以降も守られる、(3) 素材を放り込むだけで構造化される。

## 構築するとき（初回）

1. ユーザーに4点だけ聞く：業務ドメイン / 使うエージェント / 言語（既定:日本語）/ Vaultの場所（既定:`~/MyBrain`）。
2. 次の構造を作る（詳細手順は同梱の `SETUP.md`、各ファイルのひな型は `templates/` を参照）：
   - **必須**：`Memory.md`（オーナーの引き継ぎ書＝事実）、`Home.md`（玄関/目次）、`CLAUDE.md`＋`AGENTS.md`（ルール＝憲法）
   - `raw/`（放り込む）→ `wiki/`（AIが構造化）→ `reports/`（答え）、`daily/`、`outputs/`
   - `rules/`：`corrections.md`（修正指示の蓄積）/ `mistakes.md`（再発防止）/ `naming.md`（命名と4手がかり）/ `lint.md`（週次点検）
3. ノートは Obsidian Flavored Markdown で書く（`obsidian-flavored-markdown` スキル参照）。
4. 作成物を報告し、「最初の一歩（raw/ に素材→『整理して』）」を案内する。

## 運用するとき（毎セッション）

起動時に必ず `CLAUDE.md → Memory.md → rules/corrections.md → rules/mistakes.md → wiki/index.md` の順で読む。そのうえで：

- **修正の資産化**：訂正されたら即 `rules/corrections.md` に3行（日付/指摘/今後）で追記し、以降は恒久的に守る。
- **失敗の記録**：同じ失敗を指摘されたら `rules/mistakes.md` に追記＋再発防止ルール。
- **素材の構造化**：`raw/` を読み `wiki/` に概念ページ化、`[[リンク]]`で繋ぎ `wiki/index.md` を更新（`raw/` は読み取り専用）。
- **答えはファイルに**：重要な答えは `reports/` に残し `wiki/` へリンク。
- **週次の手入れ**：`rules/lint.md` の観点で矛盾・重複・古い情報を洗い出す（`web-clip` で素材を増やしたら特に）。
- **破壊的操作の前に確認**：削除・上書き・大量改名は必ず確認。

## 関連スキル

- `obsidian-flavored-markdown` … ノートを正しい Obsidian 構文（wikilink/embed/callout/properties）で書く
- `web-clip` … WebページをクリーンなMarkdownにして `raw/` に取り込む

より深い Obsidian 構文（Bases `.base` / Canvas `.canvas` / Obsidian CLI）は、公式の
[kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) を併せてインストールすると強化される。
