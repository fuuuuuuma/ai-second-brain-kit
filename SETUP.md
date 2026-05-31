# SETUP.md — エージェント実行手順書

> **AIエージェントへ**：このファイルはあなた（AIエージェント）への指示書です。
> 以下のステップを順番に実行し、ユーザー専用の「第二の脳（Obsidian Vault）」を構築してください。
> 各テンプレートの中身は `templates/` 配下にあります。読み込んで、`{{プレースホルダ}}` をユーザーの回答で置き換えて配置してください。

---

## ゴール

ユーザーが、新しいセッションでも前提説明なしに作業を再開でき、一度伝えた修正指示が恒久的に守られ、素材を放り込むだけで知識が構造化・整理されていく Vault を完成させる。

---

## Step 0. 4つだけ質問する（既に分かっていれば省略可）

ユーザーに次の4点を聞く。答えが返らない・任せると言われたら、各項目の既定値で進める。

1. **業務ドメイン** — 何について第二の脳を作るか（例：AIエージェント研究 / 動画制作 / 営業 / 学習）。既定：「汎用ナレッジ」
2. **使うエージェント** — Claude Code / Codex / Cursor / その他。既定：Claude Code（`AGENTS.md` も併せて置く）
3. **言語** — 既定：日本語（固有名詞・コードは原語のまま）
4. **Vault の場所** — 既定：このリポジトリ内、または `~/MyBrain`

> 質問は一度にまとめて聞く。1問ずつ往復しない。

---

## Step 1. フォルダ構造を作る

`templates/structure.md` に定義された構造を、Vault のルートに作成する。

```
{{VAULT}}/
├── CLAUDE.md
├── AGENTS.md
├── Memory.md        ← 【必須】オーナーの引き継ぎ書
├── Home.md          ← 【必須】Vaultの玄関（目次）
├── raw/
├── wiki/
│   ├── index.md
│   └── moc/
├── reports/
├── daily/
├── outputs/
├── rules/
│   ├── corrections.md
│   ├── mistakes.md
│   ├── naming.md
│   └── lint.md
└── templates/
    ├── daily.md
    ├── meeting.md
    ├── permanent.md
    ├── source.md
    └── moc.md
```

`Memory.md` と `Home.md` は **必須**。Vault ルートに必ず作成する（省略しない）。
空フォルダには `.gitkeep` を置く（`raw/` `reports/` `outputs/` `wiki/moc/`）。

---

## Step 2. 憲法（全体ルール）を設置する

1. `templates/CLAUDE.md` を読み込む。
2. `{{OWNER}}` `{{DOMAIN}}` `{{LANG}}` などのプレースホルダを Step 0 の回答で埋める。
3. Vault ルートに `CLAUDE.md` として保存する。
4. `templates/AGENTS.md` を Vault ルートに `AGENTS.md` として保存する（Codex/他エージェント用。内容は CLAUDE.md を参照する1枚）。

> **最重要**：CLAUDE.md には「セッション開始時に `Memory.md` → `rules/corrections.md` → `rules/mistakes.md` を必ず読む」「ユーザーに訂正されたら必ず `rules/corrections.md` に追記する」というルールが含まれている。ここを省略しないこと。

---

## Step 2.5. Memory.md と Home.md を設置する（必須）

この2ファイルは**必須**。省略しない。

1. `templates/Memory.md` を読み込み、Step 0 の回答（業務ドメイン／使うエージェント／言語／判断基準・文体）でプレースホルダを埋め、Vault ルートに `Memory.md` として保存する。
   - これはオーナーの「引き継ぎ書（オンボーディング文書）」。AIが起動時に最初に読む**事実の置き場**。空欄が残ってもよいので、まず作って配置する。
2. `templates/Home.md` を Vault ルートに `Home.md` として保存する。
   - Vaultの玄関（ハブ／目次）。`Memory` `CLAUDE` `wiki/index` `rules/*` などへのリンクが既に入っている。
   - 日付プレースホルダ `{{YYYY-MM-DD}}` はユーザー環境の今日の日付で埋める（推測しない）。

---

## Step 3. ルール群を設置する

`templates/rules/` の4ファイルを `{{VAULT}}/rules/` にコピーする。

- `corrections.md` … 一度受けた修正指示の蓄積先（最初は空＋フォーマットのみ）
- `mistakes.md` … AIのやらかし＋再発防止ルール（最初は空＋フォーマットのみ）
- `naming.md` … 命名規則と「AIが引き出すための4つの手がかり（種類 / 時期 / 主題 / 状態）」
- `lint.md` … 週次ヘルスチェックの観点

---

## Step 4. ノート雛形を設置する

`templates/notes/` の5ファイルを `{{VAULT}}/templates/` にコピーする
（`daily.md` / `meeting.md` / `permanent.md` / `source.md` / `moc.md`）。

---

## Step 5. 初期ノートを生成する

1. `wiki/index.md` を作る（見出しと「ここにAIが目次を追記していく」旨のプレースホルダ）。
2. `daily/` に今日のデイリーノートを1枚作る（`templates/daily.md` ベース、日付は `{{TODAY}}` をユーザー環境の今日の日付で）。
   - 日付はユーザーに確認するか、ユーザー環境のコマンドで取得する。推測で埋めない。
3. `wiki/moc/` に、Step 0 のドメインに沿った最初の MOC を1枚作る（例：ドメインが「動画制作」なら `wiki/moc/動画制作.md`）。

> ノートを書くときは Obsidian Flavored Markdown の規約に従う（同梱スキル `obsidian-flavored-markdown` 参照）：内部リンクは `[[wikilink]]`、メタは frontmatter（type/status/date/topic/tags）、強調は callout `> [!note]`。

---

## Step 5.5. スキルを案内する（任意・推奨）

ユーザーが Claude Code / Codex を使う場合、次を案内する（必須ではない）。

- 本キット同梱スキル：`second-brain`（構築・運用）/ `obsidian-flavored-markdown`（構文）/ `web-clip`（取り込み）。リポジトリを読ませている時点で利用可能。
- さらに深い Obsidian 構文（Bases `.base` / Canvas `.canvas` / Obsidian CLI / Defuddle）が欲しければ、公式の [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) のインストールを薦める：
  ```
  /plugin marketplace add kepano/obsidian-skills
  /plugin install obsidian@obsidian-skills
  ```

---

## Step 6. 動作確認と引き継ぎ

1. 作成したファイル一覧をユーザーに報告する（絶対パス）。**`Memory.md` と `Home.md` が作成されていることを必ず確認**する。
2. `Memory.md` の空欄が多い場合は、「ここを埋めるほどAIの回答が良くなる」と一言添える。
3. 次の「最初の一歩」を案内する：
   - `raw/` に素材（記事・メモ・議事録）を放り込む
   - 「raw/ を読んで wiki/ に整理して」と頼む
   - 困ったら `daily/` に今日の1枚を書くところから
3. 「一度直してほしいことを言えば `rules/corrections.md` に記録され、次回から守ります」と伝える。

---

## 運用ルール（構築後、あなた＝エージェントが常に守ること）

- **セッション開始時**：`CLAUDE.md` → `Memory.md` → `rules/corrections.md` → `rules/mistakes.md` → `wiki/index.md` の順に読む。
- **Memory / Home の保守**：オーナーの前提・進行中・判断基準が変わったら `Memory.md` を更新する。重要ノート・MOC・進行中の案件が増えたら `Home.md` にリンクを1行足す。
- **ユーザーに訂正されたら**：その場で `rules/corrections.md` に3行で追記する（フォーマットは同ファイル参照）。
- **同じ失敗を指摘されたら**：`rules/mistakes.md` に追記し、再発防止ルールを書く。
- **素材を渡されたら**：`raw/` に置き、`wiki/` に概念ページとして構造化し、`wiki/index.md` を更新する。WebページのURLを渡されたら `web-clip` スキル（Defuddle）でクリーンに取り込む。
- **ノートを書くとき**：Obsidian Flavored Markdown に従う（`[[wikilink]]`・frontmatter・callout）。詳細は `obsidian-flavored-markdown` スキル。
- **問いに答えるとき**：結論をファイル（`reports/`）として残し、参照した `wiki/` ページにリンクする。
- **`raw/` は読み取り専用**：削除・改名しない。
- **命名と分類**：`rules/naming.md` に従う。フォルダで細かく分類しない（`outputs/` を除く）。
- **週に一度**：`rules/lint.md` の観点で `wiki/` を点検し、矛盾・重複・古い情報を洗い出す。
- **破壊的操作の前**：削除・上書き・大量改名はユーザーに確認する。
