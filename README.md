# takax3-net

Astroで作成した、ポートフォリオ兼技術ブログサイトの最小構成です。

自己紹介、実績・プロジェクト、技術ブログを掲載するための土台として作成しています。記事や実績はMarkdown/MDXで管理し、Astro Content Collectionsから一覧・詳細ページを生成します。

## ローカル開発

依存関係をインストールします。

```bash
npm install
```

開発サーバーを起動します。

```bash
npm run dev
```

## ビルド

静的ファイルを `dist` に出力します。

```bash
npm run build
```

## プレビュー

ビルド後の内容をローカルで確認します。

```bash
npm run preview
```

## コンテンツ管理

- ブログ記事: `src/content/blog`
- 実績・プロジェクト: `src/content/projects`
- Content Collections定義: `src/content/config.ts`

`src/content.config.ts` から `src/content/config.ts` の定義を読み込む構成にしています。

## Cloudflare Pages

Cloudflare Pagesでは以下を設定します。

```text
Build command: npm run build
Build output directory: dist
```

Node.jsはCloudflare Pages側で現行LTSを指定する想定です。必要に応じて、Cloudflare Pagesの環境変数で `NODE_VERSION` を指定してください。
