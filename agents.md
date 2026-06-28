# agents.md

このリポジトリで作業するエージェント向けのメモです。

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
- 外部サービスの公式アイコンは、可能な限り改変せず `public/icons/` から参照する

## Cloudflare Pages

Cloudflare Pages の設定は以下です。

```text
Build command: npm run build
Build output directory: dist
```

## 注意事項

- `node_modules/`, `dist/`, `.astro/` は生成物として扱う
- favicon関連ファイルは `public/` 直下に置く
- フッター左下の画像は `public/images/footer-peek.png` を参照している
- Links のサービスアイコンは `public/icons/` 配下を参照している
