# structure.md — 作成する Vault 構造の定義

エージェントはこの構造を Vault ルートに作成すること。空フォルダには `.gitkeep` を置く。

```
{{VAULT}}/
├── CLAUDE.md                 # 全体ルール（憲法）。Claude系が最初に読む
├── AGENTS.md                 # Codex/他エージェント用。CLAUDE.md を参照
├── Memory.md                 # 【必須】オーナーの引き継ぎ書（事実・前提）。AIが起動時に必読
├── Home.md                   # 【必須】Vaultの玄関（ハブ／目次）。主要ノートへのリンク集
│
├── raw/                      # 【入力】整理せず放り込む素材。AIは読むだけ・削除改名しない
│   └── .gitkeep
│
├── wiki/                     # 【知識】AIが構造化して書くページ群
│   ├── index.md              #   全ページの目次（AIが自動更新）
│   └── moc/                  #   Map of Content（テーマ別の地図）
│       └── .gitkeep
│
├── reports/                  # 【出力】問いへの答え・調べものの成果物
│   └── .gitkeep
│
├── daily/                    # 日々のメモ（今日の1枚から始める）
│
├── outputs/                  # 最終成果物（ブログ/台本など）。ここだけフォルダ管理
│   └── .gitkeep
│
├── rules/                    # 運用ルール
│   ├── corrections.md        # 一度受けた修正指示の蓄積（次回以降も守る）
│   ├── mistakes.md           # AIのやらかし＋再発防止
│   ├── naming.md             # 命名規則＋4つの手がかり
│   └── lint.md               # 週次ヘルスチェック
│
└── templates/                # ノート雛形
    ├── daily.md
    ├── meeting.md
    ├── permanent.md
    ├── source.md
    └── moc.md
```

## 各場所の役割（一言）

| 場所 | 役割 | 書く人 |
|---|---|---|
| `Memory.md` | オーナーの引き継ぎ書（事実・前提・判断基準） | 人間（AIが追記補助） |
| `Home.md` | Vaultの玄関（主要ノートへの目次） | 人間＋AI |
| `raw/` | 素材の投入口（記事・議事録・メモ・PDF） | 人間 |
| `wiki/` | 構造化された知識 | AI |
| `reports/` | 問いへの答え | AI |
| `daily/` | 日々の記録 | 人間（AIが補助） |
| `outputs/` | 公開・提出する成果物 | 人間＋AI |
| `rules/` | 運用の取り決め | AI（人間が承認） |
| `templates/` | ノートの型 | 共有 |

## 設計の原則

- **整理は分類でなくリンクで**：`raw/` に放り込み、`wiki/` で `[[リンク]]` を張って繋ぐ。フォルダを増やさない。
- **入力と知識を分ける**：`raw/`（生）と `wiki/`（整理済み）を混ぜない。
- **答えを残す**：問いへの答えは `reports/` にファイル化し、次の問いの素材にする。
- **Obsidian 構文で書く**：wikilink・frontmatter・callout を使う（`obsidian-flavored-markdown` スキル）。

> 補足：この `structure.md` が定義するのは「ユーザーのVaultに作る構造」。リポジトリ直下の `skills/`（Agent Skills）と `.claude-plugin/`（配布マニフェスト）はVaultには入れず、エージェント側で使う。
