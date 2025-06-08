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
