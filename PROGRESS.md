# PROGRESS — takax3-net

現在地と次にやることの正本。セッション終了ごとに必ず更新する（agents.md「セッション終了時にやること」）。

## 現在の Phase

リデザイン Phase 2 まで完了・本番反映済み（2026-07-05）。Phase 3 に着手中（2026-07-07: プロジェクト記事3本追加、heroImage スキーマ・rank 表示順制御を導入）。

## タスク一覧

状態: `Done` / `WIP` / `Todo` / `Blocked`（Blocked は理由を必ず書く）

各タスクに**完了条件**と**確認方法**を書く。両方を満たしたときだけ Done にできる。

| ID | 優先度 | 状態 | 内容 | 完了条件 | 確認方法 | 備考 |
|---|---|---|---|---|---|---|
| T-001 | P0 | Done | Phase 1: デザイン基盤（配色・フォント・カード・タグ） | global.css にトークン一式が定義され全ページに適用 | 本番で確認済み | 2026-07-05 デプロイ |
| T-002 | P0 | Done | Phase 2: トップページ再設計（ヒーロー・Featured Project・Latest Posts） | index.astro が新レイアウトで表示される | 本番で確認済み | 2026-07-05 デプロイ |
| T-003 | P1 | WIP | Phase 3: projects/blog に `heroImage` スキーマ追加とカードのサムネイル表示 | 一覧カードに画像が出る。heroImage 未設定の記事も崩れない | `npm run build` + 一覧ページ目視 | projects の heroImage スキーマ・詳細ページ表示・Featured カード参照は実装済み（2026-07-07）。残りは一覧カードのサムネイル表示と blog 側 |
| T-004 | P1 | Todo | Phase 3: プロジェクト status バッジの色分け（公開中/開発中など） | status 値ごとに色が変わる | 一覧・詳細ページ目視 | 現在は一律アンバー |
| T-005 | P2 | Todo | Phase 3: 記事詳細（.prose）の見出し・引用・リンクの装飾強化 | 見出し/blockquote/コードにテーマが適用 | hello-world 記事で目視 | |
| T-006 | P2 | Todo | Phase 4: View Transitions（Astro ClientRouter）導入 | ページ遷移がフェードする。JS 無効でも動作 | dev サーバーで遷移確認 | G4 相当の依存追加はなし（Astro 標準） |
| T-007 | P2 | Todo | Phase 4: OGP 画像・メタタグ整備 | OGP 画像と og:/twitter: メタが全ページに出る | メタタグ検証ツール | |
| T-008 | P3 | Todo | Phase 4: footer-peek のスクロール連動アニメーション | reduced-motion 環境では動かない | dev サーバーで目視 | |
| T-009 | P3 | Todo | RSS・sitemap の追加 | /rss.xml と /sitemap-index.xml が生成される | ビルド出力確認 | @astrojs/rss 追加は G4（人間ゲート） |
| T-010 | P0 | Done | Google AdSense 所有権確認メタタグと ads.txt の追加 | 全ページ head に `google-adsense-account` メタタグが出て、`/ads.txt` が公開される | `npm run build` + `dist/index.html` / `dist/ads.txt` 確認 | 2026-07-05 対応。広告配信用 JavaScript は未導入 |
| T-011 | P0 | Done | プロジェクト記事3本追加（LLM Chat Bot / 読み上げ Bot / まめトレード）＋ rank 表示順制御 ＋ 詳細ページの heroImage 表示・一覧への導線 | 記事が公開され、DojiOnee が Featured に固定される | dev サーバー・ビルド出力で確認済み | 2026-07-07。本文は人間が編集済み |
| T-012 | P1 | Done | プロジェクト記事追加: Usagi-Chat（VC 音声対話 Bot） | 記事が一覧・詳細に表示される | `npm run build` で確認済み | 2026-07-07。本文は人間が編集済み。他の workspace 候補は見送り（トレード系はまめトレードに集約） |

## 人間の判断待ち

人間が**即決できる形**（選択肢+AI推奨案）で書く。ここに書いたらAIは他タスクに進む。

| 論点 | 選択肢 | AIの推奨と理由 | ゲート | 記載日 |
|---|---|---|---|---|
| （なし） | | | | |

## 次のセッションでやること

1. T-003 の残り（一覧カードのサムネイル表示、blog 側の heroImage）を進める
2. T-004（status バッジの色分け）— status 語彙は「運用中 / 休止中 / 研究中」で確定済み（docs/decisions.md）

## 完了した Phase の記録

| Phase | 完了日 | 主な成果 |
|---|---|---|
| リデザイン Phase 1 | 2026-07-05 | デザイントークン・フォント・カード/タグ/バッジのスタイル基盤 |
| リデザイン Phase 2 | 2026-07-05 | トップページ再設計（2カラムヒーロー・Featured Project・Latest Posts）、サイト名を「恋ヶ窪タカノの実装室」に変更 |
