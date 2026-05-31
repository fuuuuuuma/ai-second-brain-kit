# PROMPT.md — そのまま貼れるプロンプト

クローンせずに使いたい場合は、以下のブロックをまるごとコピーして、
お使いのAIエージェント（Claude Code / Codex / Cursor / Gemini など）の入力欄に貼り付けてください。

---

```
あなたはこれから、私専用の「第二の脳（Obsidian Vault）」を構築します。
目的は、(1) 新しい会話でも前提説明なしに作業を再開できること、
(2) 私が一度伝えた修正指示が次回以降も自動で守られること、
(3) 素材を放り込むだけで知識が構造化・整理されていくこと、の3つです。

# まず4つだけ質問してください（まとめて1回で）
1. 業務ドメイン（何についての第二の脳か）
2. 使うエージェント（Claude Code / Codex / Cursor / その他）
3. 言語（既定：日本語、固有名詞とコードは原語のまま）
4. Vault を作る場所（既定：~/MyBrain）

# 次に、以下の構造を作ってください
MyBrain/
├── CLAUDE.md        # 全体ルール（憲法）。セッション開始時に必ず読む
├── AGENTS.md        # Codex等向け。CLAUDE.md を参照する1枚
├── Memory.md        # 【必須】オーナーの引き継ぎ書（事実・前提・判断基準）。起動時に必読
├── Home.md          # 【必須】Vaultの玄関（主要ノートへの目次・リンク集）
├── raw/             # 整理せず素材を放り込む（あなたは読むだけ・削除改名しない）
├── wiki/            # あなたが構造化して書く知識ページ
│   ├── index.md     #   全ページの目次（あなたが自動更新）
│   └── moc/         #   Map of Content（テーマ別の地図）
├── reports/         # 問いへの答え・成果物
├── daily/           # デイリーノート
├── outputs/         # ブログ・台本など最終成果物（ここだけフォルダ管理）
├── rules/
│   ├── corrections.md  # 一度受けた修正指示を蓄積（次回以降も守る）
│   ├── mistakes.md     # あなたのやらかし＋再発防止ルール
│   ├── naming.md       # 命名規則＋引き出すための4手がかり（種類/時期/主題/状態）
│   └── lint.md         # 週次ヘルスチェックの観点
└── templates/       # ノート雛形（daily/meeting/permanent/source/moc）

# Memory.md と Home.md は必須です（省略しない）
- Memory.md：私の引き継ぎ書。事業/活動の概要・体制・進行中・よく使うツール・目標・判断基準・文体を、上の4つの質問の答えで埋める。空欄が残ってもよいのでまず作る
- Home.md：Vaultの玄関。Memory / CLAUDE / wiki/index / rules/* / daily / wiki/moc / reports へのリンクを集めた目次にする

# CLAUDE.md には必ず次のルールを含めてください
- セッション開始時に CLAUDE.md → Memory.md → rules/corrections.md → rules/mistakes.md → wiki/index.md の順で読む
- 私の前提・進行中・判断基準が変わったら Memory.md を更新し、重要ノートが増えたら Home.md にリンクを足す
- 私に訂正されたら、その場で rules/corrections.md に3行（日付 / 指摘内容 / 今後の動き）で追記する
- 同じ失敗を指摘されたら rules/mistakes.md に追記し、再発防止ルールを書く
- 素材を渡されたら raw/ に置き、wiki/ に概念ページとして構造化し、index.md を更新する
- 問いに答えるときは結論を reports/ にファイルで残し、参照した wiki/ ページにリンクする
- フォルダで細かく分類しない（outputs/ を除く）。整理は naming.md に従う
- 週に一度 lint.md の観点で wiki/ を点検し、矛盾・重複・古い情報を洗い出す

# 命名規則（naming.md に書く内容）
- ファイル名は「YYYY-MM-DD-種類-主題.md」
- 各ノート冒頭に frontmatter で type / status / date / topic / tags を持たせる
- 探すときの手がかりは4つ：種類(type) / 時期(when) / 主題(topic) / 状態(status)

# 最後に
作ったファイルの一覧（パス）を報告し、「最初の一歩」（raw/ に素材を入れて
『整理して』と頼む）を案内してください。日付は推測せず、私に確認するか
私の環境の今日の日付を使ってください。破壊的操作の前には必ず確認してください。
```

---

> より詳しい手順書は [SETUP.md](SETUP.md)、各ファイルのひな型は [`templates/`](templates/) にあります。
