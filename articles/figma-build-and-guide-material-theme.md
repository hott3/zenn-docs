---
title: "【Figma】Material Themeのカラースキームとガイドの作成（MD3,Figma plugins）"
emoji: "🎨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["figma", "materialdesign",]
published: true
---

# 【Figma】Material Themeのカラースキームとガイドの作成（MD3,Material Theme Builder,Color Style Guide,Typography Style Guide）

![](/images/figma-build-and-guide-material-theme/thumnbail.png)

Material Theme Builderは、FigmaでMaterial Designテーマを作成するためのプラグインです。
このプラグインを使用すると、色、タイポグラフィ、その他のデザイン要素を定義することで、一貫した外観のUIを作成できます。

テーマを作成したら、Color Style GuideとTypography Style Guideを使用して、それぞれのスタイルガイドを表示します。
スタイルガイドには、テーマで使用されているすべての色とフォントがリストされています。
これらのスタイルガイドを作成することで、テーマを利用するチームメンバーの開発効率が向上します。


-----

## 使用したFigmaのプラグインについて

Material Theme BuilderはMaterial DesignのColor systemをサポートするプラグインです。
ドキュメントのResources^[https://m3.material.io/styles/color/overview#4f6a95eb-8f29-431b-8c05-c2de50e5103e]でも指定されています。

https://www.figma.com/community/plugin/1034969338659738588/Material-Theme-Builder

Color Style GuideとTypography Style Guideは、Figmaファイルに登録されたスタイルからデザインガイドを出力するプラグインです。

https://www.figma.com/community/plugin/941680506965181089/Color-Style-Guide

https://www.figma.com/community/plugin/965313760136371738/Typography-Style-Guide

他にも多くスタイルを管理するプラグインがありますが、出力操作とデザインガイドがシンプルでわかりやすかったため、今回はこちらの2つを使用しました。

## 作業したこと
 
今回やったことは以下のとおりです。

1. Material Theme Builderでオリジナルのテーマをスタイル機能に登録する
2. Color Style Guideでカラースタイルのガイドを作成する
3. Typography Style Guideでテキストスタイルのガイドを作成する
4. コンポーネントやデザインパーツを作成するときは、`theme-name/sys`のスタイルを指定する

## Material Theme Builderでオリジナルのテーマをスタイル機能に登録する

### プラグインから検索して使用する

![](/images/figma-build-and-guide-material-theme/material-theme-builder-01.png)

### 「Create theme」を選択する

![](/images/figma-build-and-guide-material-theme/material-theme-builder-02.png)

### 選択した時点でデフォルトの名前でスタイルが登録される

![](/images/figma-build-and-guide-material-theme/material-theme-builder-03.png)

:::message
「surfaces」と「state-layers」を使用する場合は設定を変更する必要があります。
:::

:::details 「surfaces」と「state-layers」の設定
Material Designでは、要素の状態やユーザーの操作に対応して要素の標高^[https://m3.material.io/styles/elevation/overview]や状態^[https://m3.material.io/foundations/interaction/states/overview]が表現されます。

surfaceのカラースタイルとstate-layerのカラースタイルを利用する場合は、以下の設定を有効にしてください。
![](/images/figma-build-and-guide-material-theme/material-theme-builder-04.png)
![](/images/figma-build-and-guide-material-theme/material-theme-builder-05.png)
:::

### PrimaryやSecondaryを上から順に使用したい色を指定する

以下のように、Material Theme Builderでは、任意のキーカラーを入力することでカラーロールのトーンを作成できます。

> By using Material Theme Builder, teams can input any key color to generate tones for custom color roles. In the diagram below, yellow, orange, and green are custom color inputs. A custom color input is translated into tones to automatically provide the range of tones that map to color roles.
>
> https://m3.material.io/styles/color/the-color-system/custom-colors#ecfd3a0d-00dc-470d-b2c3-457d9bd0f4f5

:::details 試しに使用したカラーコード
```
Primary         #025338 
Secondary       #535302
Tertiary        #380253
Error           #530210
Neutral         #4F5352
Neutral Variant #353837
```
:::


色を指定するとスタイルが更新されます。

![](/images/figma-build-and-guide-material-theme/material-theme-builder-06.png)


:::message alert
指定した色が`theme-name/sys/light/primary`や`theme-name/sys/light/secondary`に登録されるわけではないことに注意が必要です。
:::


:::details 指定した色はトーンに置き換えられる
指定したカラーはトーンに変換されて色の役割にマッピングされます。
入力した色と同じ値が`primary`や`secondary`にあてはまるわけではなく、アクセシビリティに考慮された組み合わせパターンが生成されたカラートーンの中から選ばれて、マッピングされます。

![](/images/figma-build-and-guide-material-theme/material-theme-builder-07.png)
*https://m3.material.io/styles/color/the-color-system/custom-colors#d2a8b8c2-3ce7-4245-a273-8b56deb35c07*

https://m3.material.io/foundations/accessible-design/patterns#f72f3851-5184-4132-b871-bc8224e062e2
:::



### 開発しているプラットフォーム似合わせてソースコードをでダウンロードできる

![](/images/figma-build-and-guide-material-theme/material-theme-builder-08.png)

### ビルドされたテーマの名前を変更する

登録されたカラースタイルとテキストスタイルをプロジェクトに応じて変更します。
以上で、オリジナルテーマのスタイル登録は完了です ✅

![](/images/figma-build-and-guide-material-theme/material-theme-builder-09.png)


## Color Style Guideでカラースタイルのガイドを作成する

### プラグインから「Color Style Guide」を選択する

![](/images/figma-build-and-guide-material-theme/color-style-guide-01.png)

### 選択することで「Colors」ページが作成される

プラグインを実行すると新規にページが作成されます。

![](/images/figma-build-and-guide-material-theme/color-style-guide-02.png)

### カラースタイルのガイド用のコンポーネントと一覧が作成されている

Colorsページは、スタイルガイド用のコンポーネントとインスタンスから構成されます。
プロジェクトに応じて不要な説明テキストはコンポーネントから非表示にしてもいいかもしれません💡
以上で、カラースタイルのガイド作成は完了です ✅

![](/images/figma-build-and-guide-material-theme/color-style-guide-03.png)

:::details 作成したカラースタイルガイドのプロトタイプ
@[figma](https://www.figma.com/proto/UWMVu2pSYk3BwHfuhcsxGZ/Build-%26-Guide-for-My-Material-Theme?type=design&node-id=3-4871&t=ajh2v52Sc1HoNX22-0&scaling=min-zoom&page-id=3%3A4870)
:::

## Typography Style Guideでテキストスタイルのガイドを作成する

### プラグインから「Typography Style Guide」を選択する

プラグインを実行すると新規にページが作成されます。

![](/images/figma-build-and-guide-material-theme/typography-style-guide-01.png)

### 選択することで「Typography」ページが作成される

TypographyページもColorsページと同様に、スタイルガイド用のコンポーネントとインスタンスから構成されます。
プロジェクトに応じて不要な説明テキストはコンポーネントから非表示にしてもいいかもしれません💡
以上で、テキストスタイルのガイド作成は完了です ✅

![](/images/figma-build-and-guide-material-theme/typography-style-guide-02.png)

### テキストスタイルのガイド用のコンポーネントと一覧が作成されている

![](/images/figma-build-and-guide-material-theme/typography-style-guide-03.png)

:::details 作成したテキストスタイルガイドのプロトタイプ
@[figma](https://www.figma.com/proto/UWMVu2pSYk3BwHfuhcsxGZ/Build-%26-Guide-for-My-Material-Theme?type=design&node-id=4-7533&t=ajh2v52Sc1HoNX22-0&scaling=min-zoom&page-id=4%3A7532)
:::


## コンポーネントやデザインパーツを作成するときは、`theme-name/sys`のスタイルを指定する

コンポーネントやデザインパーツを作成するときは、`theme-name/sys`のスタイルを指定します。
`theme-name/sys`に設定されているは、MD3内でSystem tokenと定義されているもので、デザイン言語が体系化されたトークンです。

つまり、色以外の属性や要素が考慮されたトークンにあたるため、コンポーネントやデザインパーツのプロパティにはこのトークンを指定します。

![](/images/figma-build-and-guide-material-theme/systems-token.png)
*https://m3.material.io/foundations/design-tokens/how-to-read-tokens#20829697-fd3d-4802-b295-96ba564f2e50*

:::details Component tokenについて
現在開発中のトークンが示唆されているため、指定するトークンは変わる可能性があります。
https://m3.material.io/foundations/design-tokens/how-to-read-tokens#9edb5a47-17f1-4067-96a3-403aee901e2c
:::

-----


## まとめ

以上でMaterial Themeのカラースキームとガイドの作成は完了です。✅
これらのスタイルガイドを作成することで、テーマを利用するチームメンバーの開発効率が向上します。

今回作成したスタイルガイドはFigma Communityに公開していますので、よろしければそちらもご参考ください。
https://www.figma.com/community/file/1278172974480012582

みなさんの開発効率の向上の参考になれば幸いです。


## 参考記事など

参考になりました🙇‍♂️

https://m3.material.io/
https://qiita.com/mkosuke/items/314242951766e413b4ab




