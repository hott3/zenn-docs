---
title: "【UIデザイン】デザインシステムの原則からUIデザインを考える（Material Design 3）"
emoji: "🎓"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["ui", "designsystem", "materialdesign"]
published: true
---

# デザインシステムの原則からUIデザインを考える（Material Design 3）

スマホアプリやWebサイトを開発する時に、ユーザーが使いやすいようにUIデザインを考える必要があります。

**みなさんはUIデザインを考える時にどんなことを基準に考えていますか？**
デザインシステムにはユーザーの使いやすさについて原則が示されていて、原則に則ったUIデザインが行われています。

**この記事の目的は、デザインシステムの原則を知り、UIデザインを考える基準を増やすことです。**

:::message
この記事は[UIデザイン Advent Calendar 2023](https://qiita.com/advent-calendar/2023/ui_design)の1日目の記事です。
:::

## デザインシステムの原則とは

世の中に公開されているデザインシステムを確認すると、多くのデザインシステムが原則を定めていました。
原則にはプロダクトやサービスの軸となることが記載されていて、提供する体験に統一感を持たせることを目的にしているようです。

また、デザインシステムについて詳しく説明されている書籍^[[Design Systems ―デジタルプロダクトのためのデザインシステム実践ガイド](https://www.amazon.co.jp/Design-Systems-―デジタルプロダクトのためのデザインシステム実践ガイド-アラ・コルマトヴァ/dp/4862464122)]には以下のように記されています。

> 重要なのは、原則がどれほど効果的にデザイン思想を統一し、クリエイティブ面の方向性をチームに広められるかです。本書で言うところのデザイン原則とは、チームにとっての優れたデザインの本質をとらえた共有のガイドラインであり、同時に優れたデザインの作成方法に関する指南書です。
> 
> Design Systems ―デジタルプロダクトのためのデザインシステム実践ガイド | アラ・コルマトヴァ 著, 佐藤伸哉 監訳

原則はデザインシステムを構成する重要な要素のひとつで、デザインの方向性を示しています。
定めた原則に則りUIデザインを行うことで、チームが同じ方向を向いて一貫性のある開発を実現することができるようです。

つまり、**原則に基づいたUIデザインは、基準や方向性から乖離していないか明確にします。**


## Material Design 3の原則

今回、確認するMaterial Design 3はドキュメントやデザインリソース、開発に必要なライブラリが公開されているデザインシステムです。

Material Design 3では、Foundationsという項目で、原則が定められています。

> Foundations inform the basis of any great user interface, from accessibility standards to essential patterns for layout and interaction. 
> 訳）アクセシビリティの基準から、レイアウトやインタラクションに不可欠なパターンまで、あらゆる優れたユーザーインターフェースの基礎となる情報を提供します。
> 
> https://m3.material.io/foundations

:::details Material Design 3とは
Material Design 3（MD3）は、Googleが開発したデザインシステムです。
AndroidやGmailなどのGoogleアプリで利用されていて、モバイル、デスクトップ、ウェブなど、さまざまなデバイスに対応しています。

https://m3.material.io
:::

### Accessibility

人間の身体的な特徴を理解したうえで画面設計を行うことについて記載されています。
余分な設計を不要とし、ユーザーが対象を理解し操作するコストを減らすことが可能です。

小さなボタンは、（当然のことながら）操作しづらいので、**十分な大きさを確保したボタンが操作しやすい**と示されています。^[[Accessibility – Material Design 3](https://m3.material.io/foundations/accessible-design/accessibility-basics#28032e45-c598-450c-b355-f9fe737b1cd8)]

![](/images/ui-study-from-design-system/accessibility.png)

### Content design

UIに使用するテキストは誰でも理解できるテキストにすると記載されています。
テキストで何かを理解させるためには、画像に対して適切な代替テキストを使用したり、ユーザーが使用する言語の違いに気をつけたりすることが必要です。

他にも、**人の目線が移動する経路を理解することで、コンテンツの構成やレイアウトをわかりやすくできる**と示されています。^[[Style guide – Material Design 3](https://m3.material.io/foundations/content-design/style-guide/ux-writing-best-practices#3a833840-43db-4f6e-8133-c4665c17d176)]

![](/images/ui-study-from-design-system/content-design.png)

### Adaptive design

アダプティブデザインとは、さまざまなデバイスや画面サイズに対応したデザインのことです。

端末によって、ディスプレイサイズも異なりますし、アプリの表示に使用できる領域が異なる場合もあります。
たとえば、iPhoneのHome Indicatorや折りたたみ式デバイスなどは、端末ごとのディスプレイ仕様に留意する必要があります。

モバイル端末ではひとつのカラムで表示しますが、横幅の広いデスクトップ端末などでは、複数のカラムでコンテンツを表示する場合があります。**画面遷移や操作に応じて、注目するアイテムの表示サイズを切り替えることでユーザーが素早く理解できる**ことを示しています。^[[Applying layout – Material Design 3](https://m3.material.io/foundations/layout/applying-layout/window-size-classes#6e960b82-eff3-4f1b-92d3-5edb5e338f49)]

![](/images/ui-study-from-design-system/adaptive-design.png)


### Customizing Material

さまざまなプロダクトでブランドカラーやコンセプトカラーを、取り入れたいケースがあるかと思います。
Material Design 3では、開発者が任意のカスタマイズを可能にするデザインであることが示されています。

Material Design 3では[Color System](https://m3.material.io/styles/color/system/overview)が用意されていて、強調色やユーザーの注意を促す警戒色の利用方法が記載されています。
このColor schemesは、開発者が任意のカラーで再マッピングすることが可能になっているので、**ブランドイメージやユーザーの設定が反映しつつ、視認性が下がることを防ぎながらプロダクトに反映できる**ことが示されています。^[[Customizing Material – Material Design 3](https://m3.material.io/foundations/customization#06d3ef4e-0f76-411a-b7b0-08d17cc737be)]

![](/images/ui-study-from-design-system/customizing-material.gif)

### Design tokens

デザイントークンは、Material Designのカラーやフォントなどの値を定義したものです。
デザイントークンを定義することで、プロダクト全体の統一感を実現し、**エラーメッセージなど注意を促す色を統一するなど、ユーザーにわかりやすいUIを提供できる**ことを示しています。

Material Design 3では、3種類のデザイントークンが用意されています。
このデザイントークンを任意の値に更新することで、プロダクト全体でUI設計を更新したり、部分的に値を変更することを可能にしています。^[[Design tokens – Material Design 3](https://m3.material.io/foundations/design-tokens/how-to-read-tokens#efa90c6e-92da-4af3-8031-f0520540df25)]

![](/images/ui-study-from-design-system/design-token.png)

### Interaction states

Interaction statesとは、ユーザーが要素に触れる時や、操作する時に変化する要素の状態のことです。
ユーザーの操作に応じて状態が変化することで、プロダクトの動作状況をユーザー視覚的に伝達できます。
**ユーザーに視覚的に状態を伝えることで、ユーザーは手を動かさずに目的を達成するための操作を選択できます。**

:::details インタラクションデザインを知る

ソフトウェアの画面で状態変化を利用することで、人間が操作しやすいデザインを実現します。
このアプローチ方法はインタラクションデザインと呼ばれていて、実現することでユーザーの体験を向上させることができます。

> IxD プラクティスの中心にあるのは、「適切なインタラクティブ要素の選択によって人間関係の感覚を高める」という概念です。

https://www.uxpin.com/studio/jp/blog-jp/%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%A9%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3%E3%81%A8%E3%81%AF%EF%BC%9F/#:~:text=IxD%20%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9%E3%81%AE%E4%B8%AD%E5%BF%83%E3%81%AB%E3%81%82%E3%82%8B%E3%81%AE%E3%81%AF%E3%80%81%E3%80%8C%E9%81%A9%E5%88%87%E3%81%AA%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%83%96%E8%A6%81%E7%B4%A0%E3%81%AE%E9%81%B8%E6%8A%9E%E3%81%AB%E3%82%88%E3%81%A3%E3%81%A6%E4%BA%BA%E9%96%93%E9%96%A2%E4%BF%82%E3%81%AE%E6%84%9F%E8%A6%9A%E3%82%92%E9%AB%98%E3%82%81%E3%82%8B%E3%80%8D%E3%81%A8%E3%81%84%E3%81%86%E6%A6%82%E5%BF%B5%E3%81%A7%E3%81%99%E3%80%82
:::


Material Design 3では選択している状態か、押されている状態か、ドラッグしている状態か、ボタンの状態を表現する方法が示されています。^[[States – Material Design 3](https://m3.material.io/foundations/interaction/states/state-layers#ec68aa40-c1aa-410a-b677-e83f6f2ba021)]
他にも、操作の可否を示す状態もあるので、視覚的に動作状況を伝達するUIデザインを実現しています。

![](/images/ui-study-from-design-system/interaction-states.png)

## デザインシステムの原則を知り、UIデザインを考える基準を増やせたか

この記事では、デザインシステムの原則を確認して、その原則がUIデザインの基準になっていることを確認しました。
デザインシステムの原則に則ったUIデザインは、基準が明らかです。
「使いやすさ」について、原則を基にしたチームの協議や主観に頼らない検討を実現します。

今回は、Material Design 3を確認しましたが、他にも公開されているデザインシステムが多くあります。
ぜひ、他のデザインシステムも確認し、どのような基準でUIデザインが行われているか考えてみましょう💡

ユーザーが使いやすいプロダクト開発を実現するために、ぜひデザインシステムの原則を参考にしてみてください。

:::details 🌱 オマケ

今回、デザインシステムの原則を確認しましたが、他にもUIデザインの判断基準にできる分野がありました。
HCI（ヒューマン・コンピューター・インタラクション）について、参考になる記事があったのでオススメです。

https://qiita.com/SAKUA/items/3d276f4915eb66c9220a

https://about.yahoo.co.jp/info/blog/20230329/hci.html

:::