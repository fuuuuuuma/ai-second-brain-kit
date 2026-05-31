# AI Second Brain Kit 🧠

**このリポジトリをAIエージェントに渡すだけで、「AIが二度と記憶喪失しない第二の脳（Obsidian Vault）」の最適なファイル構造を自動で作ってもらえます。**

Claude Code / Codex / Cursor / Gemini など、ファイルを読み書きできるAIエージェントならどれでも動きます。
特別なアプリも課金も不要。中身はすべて Markdown（ただのテキストファイル）です。

---

## これは何？

AIを使っていて、こんな経験はありませんか。

- 新しい会話を開くたびに、自分の仕事の前提を毎回ゼロから説明し直している
- 一度「こう直して」と伝えたのに、次の会話ではまた同じミスを繰り返す
- メモは溜まるのに、どこに何を書いたか分からなくなる

これらは **AIの賢さの問題ではなく、「覚えておく場所」と「ルール」を渡していない構造の問題** です。

このキットは、その「覚えておく場所」と「ルール」を最初からセットで作ります。特徴は5つ。

1. **あなたの引き継ぎ書（Memory.md）＋ 玄関（Home.md）【必須】** — `Memory.md` はAIが起動時に必ず読む“あなたについての事実”（事業・体制・判断基準）。`Home.md` は主要ノートへの目次。この2枚が、毎回ゼロから説明する手間を消します。
2. **全体ルール（CLAUDE.md / AGENTS.md）** — AIがセッション開始時に必ず読む“憲法”。振る舞い・文体・安全ルールを1か所に集約。
3. **修正指示の自動蓄積（rules/corrections.md）** — 一度「こう直して」と言った内容が記録され、次回以降もAIが守る。言い直しが消えます。
4. **整理いらずの知識構造（raw / wiki / reports）** — 素材は放り込むだけ。構造化・リンク・整理はAIが担当します。
5. **同梱の Agent Skills** — `second-brain`（構築・運用）/ `obsidian-flavored-markdown`（正しいObsidian構文で書く）/ `web-clip`（Webをクリーンに取り込む）。Claude Code・Codex 等が自動で使えます（[Agent Skills 仕様](https://agentskills.io/specification)準拠）。

---

## 使い方（2通り）

### 方法A：リポジトリをエージェントに読ませる（おすすめ）

お使いのAIエージェントに、こう伝えるだけです。

```
https://github.com/fuuuuuuma/ai-second-brain-kit の SETUP.md を読んで、
その手順どおりに私の第二の脳（Obsidian Vault）を構築して。
```

または、ローカルにクローンしてフォルダごと渡します。

```bash
git clone https://github.com/fuuuuuuma/ai-second-brain-kit
cd ai-second-brain-kit
# このフォルダでお使いのエージェント（claude / codex など）を起動し、こう伝える：
#   「SETUP.md を読んで、私の Vault を構築して」
```

### 方法B：プロンプトをコピペする（クローン不要）

[PROMPT.md](PROMPT.md) の中身をまるごとコピーして、AIエージェントの入力欄に貼り付けるだけ。
エージェントが質問しながら、最適なファイル構造を組み立てます。

---

## 何が作られるのか

エージェントは [SETUP.md](SETUP.md) に従って、次のような構造をあなたのVaultに作ります。

```
MyBrain/                    ← あなたの Vault（保管庫）
├── CLAUDE.md               ← 全体ルール（憲法）。Claude系が最初に読む
├── AGENTS.md               ← Codex/他エージェント用（CLAUDE.md と同じ内容を指す）
├── Memory.md               ← ★必須：あなたの引き継ぎ書（事実・前提・判断基準）。AIが起動時に必読
├── Home.md                 ← ★必須：Vaultの玄関（主要ノートへの目次・ハブ）
├── raw/                    ← 整理せず素材を放り込む場所（AIは読むだけ）
├── wiki/                   ← AIが構造化して書く知識ページ
│   ├── index.md            ←   全ページの目次（AIが自動更新）
│   └── moc/                ←   Map of Content（テーマ別の地図）
├── reports/                ← 問いへの答え・調べものの成果物
├── daily/                  ← デイリーノート（今日の1枚から始める）
├── outputs/                ← ブログ・台本など最終成果物（ここだけフォルダ管理）
├── rules/
│   ├── corrections.md      ← ★一度受けた修正指示を蓄積（次回以降も守る）
│   ├── mistakes.md         ← ★AIのやらかし＋再発防止ルール
│   ├── naming.md           ← 命名規則＋AIが引き出すための4つの手がかり
│   └── lint.md             ← 週次ヘルスチェック（矛盾・重複・古い情報を掃除）
└── templates/              ← ノートの雛形（デイリー/議事録/概念/出典/MOC）
```

各ファイルの中身のひな型は [`templates/`](templates/) にあります。

> リポジトリ自体の構成は「Vaultに入る雛形（`templates/`）」と「エージェントが使うスキル（`skills/`）」に分かれています。`skills/` は Vault には入れず、エージェント側にインストールして使います。

---

## 同梱スキル（Agent Skills）と推奨インストール

このキットには、[Agent Skills 仕様](https://agentskills.io/specification)に沿った3つのスキルが同梱されています（Claude Code / Codex CLI などが自動認識）。

| スキル | 役割 |
|---|---|
| [`second-brain`](skills/second-brain) | Vaultの構築と毎セッションの運用（必読順・修正の蓄積・構造化・週次lint） |
| [`obsidian-flavored-markdown`](skills/obsidian-flavored-markdown) | wikilink / embed / callout / properties を正しく書く |
| [`web-clip`](skills/web-clip) | Webページを Defuddle でクリーンなMarkdownにして `raw/` へ |

プラグインとして入れる場合：

```
/plugin marketplace add fuuuuuuma/ai-second-brain-kit
/plugin install ai-second-brain@ai-second-brain-kit
```

### あわせて入れると強力（公式・Obsidian CEO 製）

より深い Obsidian 構文（**Bases** `.base` 動的データベース、**Canvas** `.canvas` 視覚マップ、**Obsidian CLI**、**defuddle**）は、公式スキル集を併用すると一段強化されます。

```
/plugin marketplace add kepano/obsidian-skills
/plugin install obsidian@obsidian-skills
```

→ [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills)（MIT）。本キットの `obsidian-flavored-markdown` / `web-clip` はこの要点を内製・要約したもので、公式を入れると Bases・Canvas・CLI まで扱えます。

---

## 設計の背景にある考え方

- **記憶の置き場が本質** — 「どのAIを使うか」より「記憶をどこに置くか」で差がつく。だからAIに依存しない Markdown のVaultに記憶を置く。
- **整理するな、繋げろ** — フォルダで細かく分類するほど続かない。素材は `raw/` に放り込み、構造化はAIに任せる（海外で広まった “LLM Wiki” 的な考え方）。
- **複利は「整える」から生まれる** — 足すだけでは誤りも溜まる。週次の `lint`（ヘルスチェック）で矛盾・重複・古い情報を掃除することで、使うほど賢くなる。
- **修正は資産化する** — 一度の「こう直して」を `corrections.md` に蓄積し、AIの恒久ルールに変える。

---

## 対応エージェント

ローカルのファイルを読み書きできるエージェントなら動きます。

| エージェント | 起点ファイル |
|---|---|
| Claude Code / Claude Desktop | `CLAUDE.md` |
| Codex | `AGENTS.md` |
| Cursor / Windsurf / その他 | `CLAUDE.md`（または `AGENTS.md`）を読ませる |

Obsidian は必須ではありませんが、`wiki/` のリンク構造やグラフを可視化できるため併用を推奨します（無料）。

---

## 着想・参考

- **Andrej Karpathy の "LLM Wiki"** — 「素材を放り込み、AIが構造化・整理する」中核思想。
- **[AgriciDaniel/claude-obsidian](https://github.com/AgriciDaniel/claude-obsidian)** — `raw/ → wiki/`、`index`・`hot` キャッシュ、`/wiki` 系コマンド等を参考にした先行実装（MIT）。
- **[kepano/obsidian-skills](https://github.com/kepano/obsidian-skills)** — Obsidian CEO（Stephan Ango）製の公式 Agent Skills（MIT）。Agent Skills 形式、Obsidian Flavored Markdown 規約、Defuddle 取り込みの要素を取り入れています。
- **`Memory.md`（オンボーディング文書）/ `Home.md`（ハブ）** — Obsidian×AIを解説する各種記事で共有されている定番構成を取り入れています。

このキットは上記を土台に、**日本語前提・エージェント中立（Claude/Codex/Cursor/Gemini）・修正指示の蓄積（corrections）** を足して再構成したものです。

## ライセンス

MIT License. 自由に複製・改変・再配布できます。
