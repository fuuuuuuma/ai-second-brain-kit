---
name: web-clip
description: This skill should be used when the user wants to capture a web page / article / docs into their second brain vault as clean Markdown — stripping ads, navigation, and sidebars to save tokens. Trigger on "clip this URL", "save this article to my vault", "ingest this page into raw/", or when gathering source material for the knowledge base.
license: MIT License. Copyright (c) 2026 fuuuuuuma. Uses Defuddle (MIT, kepano).
---

# Web Clip — Webページを raw/ に取り込む

外部記事・ドキュメントを**クリーンなMarkdown**にして Vault の `raw/` に保存するスキル。
広告・ナビ・サイドバーを除去してトークンを節約し、後段で `wiki/` に構造化しやすい素材にする。

## 取り込み手順

1. Defuddle CLI でページ本文だけを抽出する：

```bash
# 標準出力に出す
npx defuddle-cli parse https://example.com/article

# raw/ にファイル保存（命名は rules/naming.md に合わせる）
npx defuddle-cli parse https://example.com/article -o "raw/2026-05-31-出典-記事タイトル.md"

# メタデータ付きで取りたいとき
npx defuddle-cli parse https://example.com/article --json
```

2. 保存したファイルの先頭に、出典の frontmatter を付ける（`templates/notes/source.md` 準拠）：

```markdown
---
type: 出典
status: 処理済み
date: 2026-05-31
topic: テーマ
source_url: https://example.com/article
---
```

3. ユーザーに「`raw/` に取り込んだ。`wiki/` に整理しますか？」と確認し、希望があれば `second-brain` スキルの構造化に渡す。

## 注意

- `raw/` は読み取り専用扱い（後から削除・改名しない）。取り込み時のみ書き込む。
- ブラウザ拡張の **Obsidian Web Clipper** でも同じことが手動でできる（ワンクリックで `raw/` へ）。CLIは自動化向け。
- Defuddle は [kepano/defuddle](https://github.com/kepano/defuddle)（MIT）。公式の
  [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) にも `defuddle` スキルがある。
