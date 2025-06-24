---
title: "【OSS活動入門】OSS活動を始めるためのGitHub基本操作（フォークからプルリクまで）"
date: "2025-06-25"
emoji: "🧑‍💻"
type: "tech"
topics: [OSS, GitHub]
published: true
---

![【OSS活動入門】OSS活動を始めるためのGitHub基本操作（フォークからプルリクまで）](/images/github-workflow-getting-started-for-oss/thumnbnail.jpeg)

専門的な知識や高度な技術を使わなくても、小さなところからOSS活動できるように記事を作成しました。
OSS活動を始めようと思っている方の参考になりましたら幸いです🙇‍♂️


## 記載していること

1. リポジトリを自分の作業場に持ってくる
2. 最初の貢献（コントリビュート）に挑戦する
3. OSS活動を始めるためのGitHub基本操作について


## リポジトリを自分の作業場に持ってくる
まずは、OSS開発の第一歩である「フォーク」と「クローン」をやってみます。

### フォーク(Fork)する

ここでは自分の「作業場」となるリポジトリを作成するために、対象のリポジトリを「フォーク」します。
フォークすることで、リポジトリの完全なコピーが自分のGitHubアカウントで管理できるリポジトリとして作成されます。

1. 対象のリポジトリにブラウザでアクセスする
2. 画面の右上にある「Fork」ボタンをクリックする
	![Forkボタンをクリックする](/images/github-workflow-getting-started-for-oss/fork-button.png)
3. 「Create fork」ボタンをクリックする
	- 任意のリポジトリ名を入力できる
	- ここではフォーク元のリポジトリと同じ名称を使用した
	![Create forkボタンをクリックする](/images/github-workflow-getting-started-for-oss/create-fork-button.png)
4. 自身のリポジトリに追加される
	- 例）`https://github.com/{your_name}/{repository_name}`

今後、変更はこのリポジトリに対して行います。

:::message
他者が管理しているリポジトリをクローンするだけではそのリポジトリにプッシュできません。
フォークしてから自分のリポジトリとしてコピーし、それをクローンすることでコードを修正したり、機能を追加したりして、その変更を元のリポジトリに変更を提案（プルリクエスト）を作成できます。
:::


### クローン(Clone)する

ここではフォークして作成された自分のリポジトリを、PCのローカル環境にダウンロードします。

1. フォークした自分のリポジトリにアクセスする
2. 「<> Code」ボタンをクリックし、表示されたURLをコピーする
	- この記事ではHTTPS形式のURLを選択する
	- ![copyからcloneする](/images/github-workflow-getting-started-for-oss/code-copy-clone-url.png)
3. PCでターミナル（またはコマンドプロンプト）を開く
4. 作業したいディレクトリに移動して、以下のコマンドを実行する
	- `$ git clone コピーしたURL`


### フォークを同期する


すぐには差分は発生していないかと思いますが元のリポジトリ（フォーク元のリポジトリ）で変更があった場合に、それを自分の作業場にも反映できるように同期する手順についても確認しておきます。

同期する方法はいくつかあります。

https://docs.github.com/ja/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork

ここでは2つとりあげます。
- GitHubのGUIでフォークを同期する方法
- コマンドラインからフォークのブランチを同期する


#### GitHubのGUIでフォークを同期する手順

1. GitHub でアップストリームリポジトリと同期するフォーク先のリポジトリのメインページにアクセスする
2. コードが表示されているページで、ブランチを選択するボタンの近くに、本家のリポジトリとの状態を示すメッセージが表示される
3. もしあなたのフォークが本家より遅れている場合、メッセージが表示される
4. その隣の `[Sync fork]` というボタンをクリックすると、プルダウンメニューが表示される
5. ここに本家から取り込まれる変更内容の概要が表示されるので、内容を確認して緑色の `[Update branch]` ボタンをクリックする



#### コマンドラインからフォークのブランチを同期する手順

本家リポジトリの変更を取り込めるように設定 (Upstream設定)します。

:::message
`git remote add upstream <URL>` というコマンドは、あなたのローカルリポジトリに対して、「フォーク元のリポジトリは upstream です」と登録することです。
フォークした後も更新される可能性があるため、その更新を利用しながら作業したり、コンフリクトを起こしにくくするために設定します。
:::


1. ターミナルを開き、クローンしたディレクトリに移動する
	```terminal
	# クローンしたディレクトリに移動する
	cd {ディレクトリのパス}
	```
2. リモートリポジトリの一覧を確認する
	```terminal
	$ git remote -v
	origin	https://github.com/{your_name}/{repository_name}.git (fetch)
	origin	https://github.com/{your_name}/{repository_name}.git (push)
	```
3. フォーク元リポジトリにブラウザでアクセスする
4. 「<> Code」ボタンをクリックし、表示されたURLをコピーする
5. フォーク元のリポジトリをリモートリポジトリに追加する
	```terminal
	// 参考
	$ git remote add upstream https://github.com/ORIGINAL-OWNER/ORIGINAL-REPOSITORY.git
	// コピーペーストを利用して作成するコマンド
 	$ git remote add upstream {コピーしたURLをペースト}
	```
6. リモートリポジトリの一覧を確認する
	```terminal
	 $ git remote -v
	origin	https://github.com/{your_name}/{repository_name}.git (fetch)
	origin	https://github.com/{your_name}/{repository_name}.git (push)
	upstream	https://github.com/{target_name}/{repository_name}.git (fetch)
	upstream	https://github.com/{target_name}/{repository_name}.git (push)
	```

https://docs.github.com/ja/pull-requests/collaborating-with-pull-requests/working-with-forks/configuring-a-remote-repository-for-a-fork

Upstream設定が完了していれば、以下のコマンドを実行します。
```terminal
# 本家の最新の状態に更新
git fetch upstream
git checkout main
git merge upstream/main
```

:::message
もしコンフリクトが起きても慌てず解消しましょう。
後述のブランチを切り分けることでコンフリクトは起きにくくなると思いますが、なにかしらで起こる可能性はあります。
慌てず解消できるものとしてとらえて、丁寧に確認しながら解決しましょう。
:::


:::details upstreamとはどういう意味か？
`upstream`とは「上流」という意味の英単語です。
`upstream`はOSS開発において慣習的に使用されていて「本家」のリポジトリを指します。
本家の変更（川の上流からの流れ）を取り込むために設定します。
:::

:::details upstreamとoriginの違い
`origin`は`git clone`を実行したときにクローン元のリポジトリに対して自動的に付けられるデフォルトの名前です。
今回のフォークしてからクローンするワークフローでは、`origin` は自分自身のGitHub上のリポジトリになります。
:::	


## 最初の貢献（コントリビュート）に挑戦する
いきなり大きな変更をすることは難しいと感じます。
なので簡単なことから始めて、一連の流れを体験してみましょう。

### issueを立てる

OSS開発では、何か作業を始める前に「こんな問題がある」「こんな機能を追加したい」といった提案を issueとして登録します。
対応することが明確になるように、なるべく小さな内容で対応内容がわかるようにissueを立てます。

たとえば、練習レベルの簡単なテーマ案を考えてみるとこんなイメージです💡
- ドキュメントの改善提案
	- README.md ファイルを読んでみて、誤字脱字を見つけたり、「この説明を追記した方が分かりやすいのでは？」といった改善案をIssueとして立ててみる
- 簡単な改善提案
	- アプリを動かしてみて、「ここのテキストを少し変えたい」「このボタンの色を変えてみてはどうか」といった、簡単な改善を提案してみる

実際にissueを立ててみます。

1. フォーク元のリポジトリにブラウザでアクセスする
2. フォーク元のリポジトリの 「Issues」タブを確認して、既に同じ内容のissueがないか確認する
3. 「New issue」ボタンをクリックする
4. TitleとDescriptionを入力する
	- Issueのタイトルはどんな対応が必要かイメージできるようにわかりやすく示します
	- Issueの説明はどこを修正したいのか、修正の意図や目的をわかりやすく示します
	- 可能ならIssueの中に具体的な修正箇所や修正例を挙げると意図が伝わりやすくスムーズなコミュニケーションが可能です
	- ![issueを入力する](/images/github-workflow-getting-started-for-oss/issue-input.png)
5. 「Create」ボタンをクリックしてIssueを作成する



### 簡単な修正でプルリクエストを送ってみる

Issueを立てたら、次はコードの修正をします。
変更内容やコミットメッセージは、フォーク元のリポジトリをメンテナンスしている人が確認することがあります。
変更したい意図や作業の記録は読みやすいものを心がけましょう。

様々なGitクライアントがあるので、詳細なGit操作はここでは説明しません。


#### ブランチ (Branch) を作成する
修正作業は、必ず新しいブランチを作成して行います。
フォークしたリポジトリの`main`ブランチで直接作業しないようにするためです。
	? なぜmainブランチで直接作業しないのか？
		フォークしたリポジトリの`main`ブランチは、本家の変更をいつでもスムーズに受け入れられる状態にしておく必要があるためです。
		そのため、機能開発を行うときはブランチをわけて作業を行い、`main`ブランチとは切り離しておくことが重要です。

以下、リポジトリとブランチの対応イメージを図で示します。

```Mermaid
graph TD
	subgraph "本家リポジトリ (upstream)"
		U_Main("main<br>公式の作業記録")
	end

	subgraph "あなたのフォーク (origin)"
		O_Main("main<br>本家と同じ状態を保つ<br><b>※ここでは作業しない</b>")
		
		subgraph "作業スペース"
			direction LR
			featA("feature/A")
			featB("fix/B")
		end
		
		O_Main -- "作業ブランチを作成" --> featA
		O_Main -- "作業ブランチを作成" --> featB
	end

	%% ワークフローの矢印
	U_Main -- "<b>【同期】</b><br>本家の変更を<br>自分のmainに取り込む" --> O_Main
	
	featA -- "<b>【貢献】</b><br>作業内容を<br>プルリクエスト" --> U_Main
	featB -- "<b>【貢献】</b><br>作業内容を<br>プルリクエスト" --> U_Main
```


ブランチ名は、`fix/readme-typo` (READMEのタイポ修正) や `feature/add-new-color-theme` (新しいカラーテーマの追加) のように、作業内容がわかる名前にしておくと、issueで目的から離れにくい発散しにくい作業にまとまられそうです。

今回私は対応内容に合わせて以下のようにブランチ名を検討しました。
- `fix/readme-typo-3`
	- 「fix/」で修正系の作業であることを明示
	- 「readme-typo」で内容を簡潔に表現
	- 作成したissue番号の「3」を末尾につけて関連付け

#### コードを修正する
実際にissueに記載した内容に対応する作業を行います。
例えば、以下のような簡単な修正をイメージです。
- README.md の誤字を修正する
- コード内のコメントを追加・修正する
- アプリ内の表示テキストを少しだけ変更する

#### コミット (Commit) & プッシュ (Push)する
修正が完了したら変更内容を記録（コミット）します。
- この時にコミットメッセージを分かりやすく書くと自身の作業内容や意図が明確になります。


:::message
Conventional Commits^[[Conventional Commits](https://www.conventionalcommits.org/ja/v1.0.0/)]というコミットメッセージを読みやすくするために整理された仕様があるので参考にしてみましょう
:::

コミットしたら自分のリポジトリ（フォークしたリポジトリ）にアップロード（プッシュ）します。
- Upstream設定が完了している場合、プッシュ先の候補に`upstream`が表示されるかもしれません。プッシュするのは自分のリポジトリである`origin`になります。
 
```terminal
# ご自身のGitHubリポジトリにプッシュコマンド例
git push origin <ブランチ名>
```

#### プルリクエスト (Pull Request) の作成する
プッシュが完了すると、自分のGitHubリポジトリのページに「Compare & pull request」というボタンが表示されます。
これをクリックし、プルリクエスト（「この変更を本家に取り込んでください」というお願い）を作成します。
このときプルリクエストの説明を具体的に書くと、レビューする側がわかりやすくなります。
- タイトルの書き方
	- 何をしたのかが簡潔にわかるように書く
	- 例）README.md のタイポを修正
- 内容の書き方
	- どのIssueに対応するものか
	- どのような変更をしたのか
	- なぜこの変更が必要だと思ったのか

https://docs.github.com/ja/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork

:::message
自分のGitHubのリポジトリにプルリクエストを作成するとフォーク元のリポジトリにも反映されません。
プルリクエストを「作成」しただけでは、フォーク元の本家リポジトリのコード（mainブランチなど）は一切変更されません。
:::

## レビューへの対応

プルリクエストを送った後、メンテナーからコメントが付くことがあります。
- これはコードをより良くするための貴重なフィードバックです。

コメントには感謝を伝えましょう！（例: "Thank you for your review!"）
指摘内容について質問があれば遠慮なく質問して、よりよい開発にしていきましょう。
指摘を受けてコードを修正したら、「修正しました、再度確認をお願いします」と返信します。


## OSS活動を始めるためのGitHub基本操作について

OSS活動はハードルが高く感じます。
ハードルが高く感じる理由として、「多くの知らないことが存在する状態」がひとつの原因と考えられます。
世界には自分より優秀なエンジニアが多いと感じることは日常茶飯事です。
自分が知らない高度に感じる技術で実現されているプロジェクトも多いです。
その中で「OSS活動を始める」ということは「多くの知らないことが存在する状態」です。

今回私が書いた記事でGitHubの基本操作について知り、「知らないこと」が少しでも知ったら嬉しい限りです。
専門的な知識や高度な技術を使わなくても、小さなところからOSS活動できるようにトライしてみましょう💡


記事の内容に不備や誤りがありましたら、コメントいただけますとありがたいです🙇‍♂️


## 参考記事など

参考になりました🙇‍♂️

https://qiita.com/y-vectorfield/items/b955617712f3b66359f2
https://zenn.dev/acntechjp/articles/114abccf5eecf0
https://zenn.dev/nekocodex/articles/ab915845d300c6
