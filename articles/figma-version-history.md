---
title: "【Figma】Version Historyの利用（バージョン管理）"
emoji: "🔖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["figma",]
published: true
---

# Version Historyの利用

![](/images/figma-version-history/figma-version-history.png)


プロダクト開発において、デザインファイルの安全な運用は重要です。変更理由の明確化や、過去の状態への復元など、さまざまなメリットがあります。
この記事では、FigmaのVersion History機能を利用して、デザインファイルのバージョン管理を行う方法を紹介します。


## Version History とは

Version Historyを利用すると、デザインファイルのその時点のデータをバージョンとして保存できます。
保存されたバージョンを確認することで、過去の作業履歴の確認や復元を行うことができます。

たとえば、以下のようなケースでVersion Historyを利用することがあります。

- 作業後にバージョンを保存し、作業内容のログを管理する
- 任意のタイミングで名前をつけてバージョンを保存し、あとで参照する
- 過去のバージョンのデザインデータを確認し、これから行うデザイン作業の参考にする
- 仕様変更があった際に、過去のバージョンのデザインデータを復元し、新しくデザイン作業を行う


ただし、Figmaを利用しているプランによってVersion Historyの機能に制限がある^[2023年9月 記事執筆時点]ので注意が必要です。

- スタータープランのVersion Historyは30日間のバージョンのみ利用可能
- プロフェッショナル以上のプランのVersion Historyは無制限に利用可能

詳しくは、公式のヘルプページをご確認ください。

https://help.figma.com/hc/ja/articles/360040328273-Choose-a-Figma-Plan


## デザインデータのバージョンを管理するメリットについて

前述のようにVersion History機能は、ファイルの変更履歴を記録しバージョン管理を行う機能です。
この機能を利用することで、以下のような2つのメリットがあると考えています。

### バージョンを基準にすることで、チームメンバーと変更内容について議論することができる

ファイルの変更履歴をタイムライン形式で簡単に確認することができるので、いつ、誰が、どのような変更を行ったかを簡単に確認できます。
デザインファイルの変更履歴をチームメンバーに共有することで、変更内容の把握や議論を行うことができます🙋‍♂️

### チームメンバー複数人で変更内容を管理することができる

過去のデザインデータを確認し、状況に応じて任意のバージョンに戻すことができます。
必要になったら復元することができるので、不要になったデザインデータを余分に残しておく必要はありません。
余分なデザインデータを削除することで、必然とデザインデータを整理できます。
そのため、日頃のデザイン作業の効率化にもつながります✨

### デザインデータの運用方法について協議を行う必要がある

他にもバージョン管理を行うメリットはいくつもあるかと思いますが、
チームメンバーと協議しながら、プロダクトに合わせたバージョン管理体制を構築していくことが重要だと考えます💡
以下、Version Historyの操作方法を紹介するので、ご参考ください。




## Version Historyの操作方法

### バージョンの保存方法


1. バージョン履歴を表示する
	![](/images/figma-version-history/add-version-01.png)
2. 追加するバージョンの説明を入力する
	![](/images/figma-version-history/add-version-02.png)
3. 保存される
	![](/images/figma-version-history/add-version-03.png)
4. バージョン履歴を非表示にする
	![](/images/figma-version-history/add-version-04.png)



:::message
編集中に `⌘ + ⌥ + S`を押しても、バージョンを保存できます。
:::



### バージョンの確認方法

1. バージョン履歴を表示して、確認したいバージョンを選択する
	![](/images/figma-version-history/check-version-01.png)
	↓ 選択したバージョン時点のデザインが表示される
	![](/images/figma-version-history/check-version-02.png)
2. フィルターアイコンから自動バージョンを非表示にすると、意図的に保存したバージョンだけ表示されるので確認しやすい
	![](/images/figma-version-history/check-version-03.png)


### バージョンの復元方法

:::message alert
バージョンからデザインファイルを復元する方法は二通りありますが、後者は運用しているデザインファイルを大きく変更してしまう可能性があります。
:::

- 過去のバージョンを選択し、新しいデザインファイルとしてデザインファイルを新規作成する方法
	![](/images/figma-version-history/restore-version-01.png) 
- 過去のバージョンを選択し、現在のデザインファイルを過去のバージョンに書き換える方法	
	![](/images/figma-version-history/restore-version-02.png)



### コンポーネントごとのversionの確認

Dev mode^[2023年中はオープンベータ機関のため無料のプランでも利用できます。詳しくは、https://www.figma.com/ja/dev-mode/]を使用するとコンポーネント単位でバージョンを確認できます。
キャプチャのようにコンポーネントの差分を確認できるFigmaファイルを作成しましたので、ご参考ください💡
https://www.figma.com/file/D7bbqeiXzXFtbclE0dtU6Y/Version-History-Trial?type=design&node-id=0-1&mode=design&t=2ON1axuROfY9Y1fQ-0

1. Dev modeを表示し、コンポーネントを選択する
2. インスペクトタブから「変更内容を比較」を選択する
	![](/images/figma-version-history/difff-component-01.png)
3. プロパティの差分を確認する
	![](/images/figma-version-history/difff-component-02.png)


## Version Historyの操作方法の補足

### 復元操作を行うと現在のバージョンはどうなるか

前述の復元操作で示した「このバージョンを復元」を実行した際に、復元前のバージョンはどうなるかを確認しました。
「このバージョンを復元」を実行するとデザインファイルが書き換わってしまいますが、復元操作前のバージョンは残っていました。
つまり、復元操作を行っても復元前のデータに戻すことが可能です😌
![](/images/figma-version-history/what-happen-after-restore-operation.gif)


### 参考記事

以下の記事を参考にしました🙇‍♂️

https://note.com/smikami/n/ne2511e1113b3
https://dev.classmethod.jp/articles/versioning-in-figma-at-cm-study-meeting-in-okayama/


### まとめ

Version History機能を利用することで、デザインファイルのバージョン管理を行うことができます。
バージョン管理を適切に利用することで変更理由を明確にしたり、過去のデザインデータを復元したり、さまざまなメリットがあります。

プロダクト開発を効率的に、合理的に、そして快適に進めていくためにも試してみてはいかがでしょうか🙋‍♂️

もし参考になったところや、疑問に感じたところがあればコメントください🌻


