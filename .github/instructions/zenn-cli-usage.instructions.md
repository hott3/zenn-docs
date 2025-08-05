---
applyTo: '**'
---

# Zenn CLI 運用ルール

## 基本コマンド

- 記事の新規作成: `npx zenn new:article`
- ブックの新規作成: `npx zenn new:book`
- プレビュー: `npx zenn preview`

## 記事作成フロー

1. `npx zenn new:article`で記事ファイル作成
2. ファイル名・slugは内容がわかるものにリネーム可
3. `articles/`配下に保存
4. テンプレートを活用し執筆


## 記事内容の確認・案内に関する運用ルール

1. 記事の内容を確認する際は、必ずZenn CLIのプレビュー機能（`npx zenn preview`）を使い、ブラウザで内容を表示する
2. 記事の内容確認を促す場合は、プレビュー用コマンド（`npx zenn preview`）を実行し、確認用URL（`http://localhost:8000`）を明示する
3. 記事や公開URLを案内する際は、必ず作成した記事のスラッグ（例: `articles/figma-make-trial-dinner-menu-app`）を付与して案内する

## プレビュー

- `npx zenn preview`でローカルプレビュー
- ブラウザで http://localhost:8000 を開く

## 公開

1. メタデータの`published: true`に変更
2. GitHubリポジトリにコミット・プッシュ
3. Zennと連携していれば自動で公開

## 記事削除フロー

1. `articles/`から該当ファイルを削除し、コミット・プッシュ
2. Zennのダッシュボードで削除を行う

## その他

- 画像は`images/記事slug/`に保存し、記事内から相対パスで参照
- 下書きは`published: false`で管理
- 既存記事の修正もコミット・プッシュで反映
- 詳細は[公式ガイド](https://zenn.dev/zenn/articles/zenn-cli-guide)参照

---

この命令ファイルが参照されていることを確認するために、返答の最初に「🌱 zenn-cli-usage」と記載してください。
作業を終えた後、作業内容が上記の命令を遵守していることを確認し、遵守されていない箇所があれば修正を行ってください。
その後、返答の最後に「🌻 zenn-cli-usage」と記載してください。

