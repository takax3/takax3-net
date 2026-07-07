# knowledge — takax3-net

再利用できる知見・ハマった問題と回避策。同じ失敗の再調査を防ぐためのファイル。

## CSS / レイアウト

- **`loading="lazy"` + 固有サイズなし + `position: absolute` はデッドロックする。** width/height 属性がない画像はサイズ 0 で交差判定に入らず、永遠に読み込まれない。装飾画像（footer-peek）には width/height 属性を必ず付ける。常時ビューポート内にある画像なら lazy 自体を外してよい。
- **`position: static` にすると absolute な子要素のアンカーが外れる。** footer-peek は `.site-footer` を基準に absolute 配置しているため、モバイルで sticky を解除するときは `static` ではなく `position: relative` にする（[global.css](../src/styles/global.css) の 720px メディアクエリ参照）。
- footer-peek のサイズは `.site-shell` の `--footer-peek-size` で管理し、`.content` の下パディングと連動させている。片方だけ変えると重なりが出る。

## 画像パイプライン

- 立ち絵の元データは 8K の VRChat スクショ（OneDrive\画像\VRChat）。**アルファチャネル透過あり**。プレビューで黒背景に見えても背景合成の結果なので、透過を潰さないこと。
- WebP 化は ffmpeg: `crop → scale=-2:高さ → libwebp q85`。`scale=-2` は**偶数丸めで幅が計算値とズレる**ので、width/height 属性は変換後の実寸（naturalWidth）で確認してから書く。
- PowerShell でのアルファ境界スキャンは、`Add-Type` での System.Drawing C# コンパイルが失敗する環境のため、**縮小してから GetPixel で走査**する方式を使う。

## Astro

- **Content Collections のスキーマ（src/content/config.ts）を変更したら `.astro/` を削除して dev サーバーを起動し直す。** コンテンツレイヤーのキャッシュに旧スキーマでパース済み（新フィールドが削ぎ落とされた）のデータが残り、dev サーバーの再起動だけでは反映されない。`astro build` は毎回同期するのでビルドは正しく出る — 「ビルドは正しいのに dev だけ古い」ときはまずこれを疑う。

## デプロイ / 運用

- Cloudflare Pages は main への push から**約60秒**で本番反映される。反映確認は本番 URL のタイトル文字列ポーリングと画像への HEAD リクエストで行った。
- ビルドが失敗した場合 Cloudflare Pages はデプロイしない（壊れたサイトが公開される事故は起きにくい）。それでも push 前にローカルで `npm run build` を通すこと。
