# EARTHIA Industries Co., Ltd.

福井・北陸を拠点とする清掃会社 EARTHIA Industries のコーポレートサイト。
ビルド不要の静的サイトで、GitHub Pages から配信します。

## 構成

```
index.html     サイト本体（HTML / CSS / JS を1ファイルに同梱）
images/        ヒーロースライド（slide1–5）とビフォーアフター写真（ba1–6）
.nojekyll      GitHub Pages の Jekyll 処理を無効化
```

ヒーローの動画4本は Higgsfield CDN（CloudFront）から直接読み込むため、
リポジトリには含まれません。

## ページの中身

- **ヒーロー** — 画像5枚と動画4本を7秒ごとに切り替えるシネマ風シーケンス。
  レターボックス、フィルムグレイン、Ken Burns、シーンごとのコピーを重ねています。
- **イントロ** — 「掃除文化を未来へ」のステートメント。
- **実績（ビフォーアフター）** — グリストラップ清掃6件。
  ハンドルをドラッグして施工前後を比較できます（マウス／タッチ対応）。

## 実装メモ

- **モバイルの動画 autoplay** — `muted` + `playsinline` + `webkit-playsinline` で
  iOS のインライン再生を許可し、さらに最初の `touchstart` / `click` で
  `manageMedia()` を呼び直して再生をかけ直します。
- **Sound On** — 右下のトグルで動画をアンミュートします。
  ミュート状態は `soundOn` が唯一の情報源で、`manageMedia()` はシーン切替のたびに
  `vid.muted = !soundOn` を適用します。ここを無条件に `true` にすると
  Sound On が次のシーンで解除されてしまうため注意してください。
- **ビフォーアフターの色補正** — 写真は彩度を落とし（`saturate` 0.25–0.3）、
  `.ba-slider::before` のネイビーのグラデーションで青寄りに寄せて、
  ヒーローのトーンと揃えています。

## ローカル確認

相対パスで画像を読むので、ファイルを直接開くのではなくサーバー経由で表示します。

```sh
python3 -m http.server 8000
# http://localhost:8000
```

## デプロイ

`main` ブランチのルートを GitHub Pages に指定すると、そのまま公開されます
（Settings → Pages → Source: Deploy from a branch → main / root）。

---

Designed by KOESA Co., Ltd.
