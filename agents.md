# agents.md

このリポジトリで作業するエージェント向けのメモです。

作業開始時は次の順に読んでください:

1. このファイル（agents.md）— 作業ルールの正本
2. [PROGRESS.md](PROGRESS.md) — 現在地・次にやること・人間の判断待ち
3. [docs/SPECIFICATION.md](docs/SPECIFICATION.md) — サイトの方向性・スコープ
4. [docs/decisions.md](docs/decisions.md) — 決定済み事項（同じ論点を蒸し返さない）
5. [docs/knowledge.md](docs/knowledge.md) — 既知の問題・ハマりどころ

## プロジェクト概要

`takax3-net` は Astro で作成したポートフォリオ兼技術ブログサイトです。

- 静的サイトとしてビルドする
- Cloudflare Pages で公開する
- コンテンツは Markdown / MDX と Astro Content Collections で管理する
- デザインよりも、保守性・シンプルさ・拡張しやすさを優先する

## 主なコマンド

```bash
npm install
npm run dev
npm run build
npm run preview
```

変更後は、可能な限り `npm run build` を実行して確認してください。

## コミット方針

コミットメッセージは `feat: ...`、`fix: ...`、`docs: ...` のようなprefix形式にしてください。

## ディレクトリ構成

- `src/pages/`: ページルート
- `src/layouts/`: 共通レイアウト
- `src/styles/global.css`: グローバルCSS
- `src/content/blog/`: ブログ記事
- `src/content/projects/`: 実績・プロジェクト
- `src/content/config.ts`: Content Collections 定義
- `public/`: favicon、画像、アイコンなどの静的ファイル

## コンテンツ管理方針

ブログ記事や実績は、ページに直接書かず `src/content` 配下に Markdown / MDX として追加してください。

ブログ記事では `draft: true` の記事を一覧・詳細ページに出さない方針です。

## スタイル方針

- CSSは最小限にする
- 既存のクラスやレイアウトに合わせる
- 過度な装飾やアニメーションは追加しない
- スマホ表示で崩れないことを優先する
- UIアイコンは、Google Fonts の Material Symbols を優先して使用する
- 外部サービスの公式アイコンは、可能な限り改変せず `public/icons/` から参照する

## Cloudflare Pages

Cloudflare Pages の設定は以下です。

```text
Build command: npm run build
Build output directory: dist
```

## デフォルト判断ルール

仕様・方針に書かれていない事項に遭遇したら、**人間に質問せず**以下の順で判断して進む:

1. [docs/decisions.md](docs/decisions.md) に既決の類似論点がないか確認する
2. なければ、以下の優先軸で妥当なデフォルトを選ぶ:
   - 保守性・シンプルさ > 機能の豊富さ（YAGNI）
   - 既存のクラス・レイアウトのパターン踏襲 > 新しい書き方
   - スマホ表示が崩れない > デスクトップの見栄え
   - 静的生成で済む方法 > クライアントJSを増やす方法
3. 選んだ判断と理由を docs/decisions.md に「デフォルト採用」として記録する
4. 作業を続行する

人間に質問してよいのは下記の人間ゲート該当時のみ。その場合も PROGRESS.md の「人間の判断待ち」に選択肢+推奨案を書き、可能なら他のタスクに進む。

## 人間ゲート（taka の承認が必須の操作）

| # | ゲート | 備考 |
|---|---|---|
| G1 | **main への push（= 本番デプロイ）** | Cloudflare Pages が main への push で自動デプロイするため。ローカルコミットは自由 |
| G2 | サイトの方向性・スコープの変更 | docs/SPECIFICATION.md の変更 |
| G3 | 不可逆な削除・破壊的操作 | git 履歴の書き換え、公開済みコンテンツの削除 |
| G4 | 依存パッケージの追加・メジャー更新 | Astro 本体のメジャーアップデート含む |
| G5 | 認証・シークレット・Cloudflare Pages 設定の変更 | ビルド設定・カスタムドメイン含む |
| G6 | サイト名・名義・公開プロフィールに関わる文言の変更 | 恋ヶ窪タカノ / taka / たかにゃん の使い分け含む |

**これ以外の通常作業では人間の承認を待たない。**

## セッション終了時にやること

毎回必ず:

1. [PROGRESS.md](PROGRESS.md) を更新する（タスク状態 / 人間の判断待ち / 次のセッションでやること）
2. `npm run build` が通る状態でコミットする

該当する場合のみ（空更新はしない）:

- docs/decisions.md — 仕様外の判断をした場合
- docs/knowledge.md — 再利用できる知見・ハマりどころが得られた場合
- このファイル（agents.md）— 作業ルール自体を変えた場合

## 注意事項

- `node_modules/`, `dist/`, `.astro/` は生成物として扱う
- favicon関連ファイルは `public/` 直下に置く
- フッター左下の画像は `public/images/footer-peek.png` を参照している
- Links のサービスアイコンは `public/icons/` 配下を参照している
