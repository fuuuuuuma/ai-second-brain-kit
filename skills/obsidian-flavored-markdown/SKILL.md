---
name: obsidian-flavored-markdown
description: This skill should be used when creating or editing notes inside an Obsidian-compatible vault, to write correct Obsidian Flavored Markdown — wikilinks, embeds, callouts, YAML properties (frontmatter), tasks, highlights, and block references. Use whenever writing .md notes for a second brain / Obsidian vault so links resolve and metadata is queryable.
license: MIT License. Copyright (c) 2026 fuuuuuuma. Incorporates conventions from kepano/obsidian-skills (MIT, Stephan Ango).
---

# Obsidian Flavored Markdown — ノートの書き方

この Vault のノートは Obsidian Flavored Markdown（CommonMark/GFM の上位互換）で書く。
AIが書くノートが「リンクで繋がり、メタデータで絞り込める」状態になるための最小規約。

## ① Wikilinks（内部リンクは必ずこれ）

```markdown
[[ノート名]]
[[ノート名|表示テキスト]]
[[ノート名#見出し]]
[[ノート名#^ブロックID]]
```
- Vault内のリンクは Markdownリンクでなく **wikilink** を使う（リネームに追従する）。
- 外部URLだけ `[表示](https://example.com)` を使う。

## ② Embeds（埋め込みは `!` を付ける）

```markdown
![[ノート名]]
![[ノート名#見出し]]
![[image.png]]
```

## ③ Properties（frontmatter＝AIが絞り込む鍵）

ファイル先頭に YAML で置く（最上部・他要素より前）。この Vault の標準プロパティ：

```markdown
---
type: 概念        # daily / meeting / 概念 / 出典 / MOC / report など
status: 進行中    # 進行中 / 完了 / 保留 / 参照用  ← 絞り込みで最重要
date: 2026-05-31
topic: テーマ名
tags: [topic/テーマ, status/進行中]
---
```
- `tags` は frontmatter では `#` を付けない。`/` で階層化（`status/進行中`）。
- プロパティ名にスペースを使わない。`rules/naming.md` の4手がかり（type/when/topic/status）と一致させる。

## ④ Callouts（強調ブロック）

```markdown
> [!note]
> 補足。

> [!warning]
> 注意点。

> [!tip]- 折りたためる（- で初期折りたたみ）
> 中身。
```
主な種類：`note` `tip` `info` `warning` `danger` `success` `question` `quote` `example` `abstract(tldr)`。

## ⑤ そのほか

- ハイライト `==強調==` / 取り消し `~~削除~~`
- タスク `- [ ]` / `- [x]`
- コメント（読書ビューで非表示）`%%メモ%%`
- 数式 `$inline$` / `$$block$$`
- ブロック参照：行末に `^id` を置くと `[[ノート#^id]]` で参照可能

## さらに深い構文

Bases（`.base` 動的データベース）、Canvas（`.canvas` 視覚マップ）、Obsidian CLI は、公式の
[kepano/obsidian-skills](https://github.com/kepano/obsidian-skills)（MIT・Obsidian CEO 製）を
インストールすると専用スキルで扱える。本スキルはその要点（Markdown/properties）を内製・要約したもの。
