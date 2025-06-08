# プロジェクト運用ガイドライン

## AIアシスタントの活用

- AIアシスタント（GitHub Copilot等）を活用する場合は、指示内容や手動作業の切り分けを明確にする  
  例：画像リネームやリンク修正はAIに指示しつつ、最終確認・微調整は手動で行う

## ファイル・ディレクトリ運用ルール

- README.mdは概要・案内のみ記載し、詳細はdocs/配下に誘導
- docs/配下の各ドキュメントの役割
  - writing-style.md: 文体・表現ルール
  - article-guideline.md: 画像・ファイル管理、執筆ガイド
  - article-policy.md: 記事設計方針・ターゲット・構成
  - zenn-cli-usage.md: CLI操作・運用ルール
- 画像・GIFファイルは `images/記事slug/` に保存し、命名規則（セクション名や内容を反映）を徹底
- GIF画像は3MB以内に圧縮（推奨ツール: gifsicle 例: `gifsicle -O3 --colors 256 -o out.gif in.gif`）
- 記事ファイル・画像ファイルのリネームやリンク修正は、記事公開前に必ず確認・反映する

## 運用・執筆フローに関する補足

- 記事執筆後は、writing-style.md / article-guideline.md / article-policy.md の観点でセルフチェックを実施
- 公開後のフィードバックや修正依頼は、issueやコメント等で記録し、対応履歴を残す

---

（このファイルにはプロジェクト全体の運用方針・AI活用・ファイル構成ルールなど、上位方針のみを記載してください。実務的な執筆ガイドはarticle-guideline.mdに集約します）

