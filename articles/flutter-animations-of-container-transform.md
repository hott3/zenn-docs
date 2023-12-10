---
title: "【Flutter】Container transformな画面遷移（animations,motion）"
emoji: "🌊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["flutter", "materialdesign", "ui"]
published: true
---

# 【Flutter】Container transformな画面遷移（animations,motion）

アニメーションを取り入れたUIは、とても身近でよく目にするものです。

- 画面遷移で横にスライドする
- 下から新しいコンテンツが現れる
- **コンテンツを押したら詳細画面が展開する**

![Containertransformな画面遷移](/images/flutter-animations-of-container-transform/flutter-animations-of-container-transform.gif)

これらのUIは、自然な表現で画面内の変化を滑らかにします。
アプリの動線を見せることでユーザーに画面遷移の仕組みを理解してもらうのに役立ちます。

この記事では、アニメーションを使用したUIを実装し、ユーザーが理解しやすい画面遷移を検討します。

:::message
この記事は[Flutter Advent Calendar 2023](https://qiita.com/advent-calendar/2023/flutter)の10日目の記事です。
:::

## アプリを便利にするアニメーションとは

アニメーションを表現するにはいくつもの方法が存在します。
その中でも、アプリを便利にするアニメーションにはどのようなものがあるでしょうか。

Flutter 3.16からデフォルトになった^[[What’s new in Flutter 3.16. Material 3 by default, Impeller preview… | by Kevin Chisholm | Flutter | Nov, 2023 | Medium](https://medium.com/flutter/whats-new-in-flutter-3-16-dba6cb1015d1#:~:text=Material%203%20is%20the%20new%20default)]Material Design 3の中から、Transitionsを確認したところ、**Container transform**というアニメーションが示されていました。^[[Container transform - Motion – Material Design 3](https://m3.material.io/styles/motion/transitions/transition-patterns#b67cba74-6240-4663-a423-d537b6d21187)]


![Containertransformな画面遷移](/images/flutter-animations-of-container-transform/container-transform.gif)

:::details Material Design 3とは
Material Design 3（MD3）は、Googleが開発したデザインシステムです。
AndroidやGmailなどのGoogleアプリで利用されていて、モバイル、デスクトップ、ウェブなど、さまざまなデバイスに対応しています。

https://m3.material.io
:::

この**Container transform**は、画面遷移の開始状態と終了状態をシームレスに接続するため、遷移前と遷移後の要素間に強い関係を表現できます。
要素間の関係を表現することで、ユーザーが画面遷移の仕組みを理解しやすくなります。

## Flutterで実装する

この**Container transformな画面遷移**を実装する方法を調べました。

### Flutter公式の対応状況と対応パッケージ

FlutterのissueにはMaterial Design 3をサポートするためのissueがありますが、Container transformなどのTransitionsはまだ対応していないようです。

https://github.com/flutter/flutter/issues/116526

そのため、今回はMaterial Design 3のResources^[[Resources - Motion – Material Design 3](https://m3.material.io/styles/motion/overview#79091b43-b231-4ab8-9b89-509c95d2bcde)]に記載されているパッケージを試しました。

https://pub.dev/packages/animations

### animationsパッケージを使用する

animationsパッケージはFlutter公式から提供されているパッケージです。
Flutter公式YouTubeチャンネルに紹介動画もあります。

https://www.youtube.com/watch?v=HHzAJdlEj1c


### 実装例

実際に実装した画面がこちらです。

![Containertransformな画面遷移](/images/flutter-animations-of-container-transform/flutter-animations-of-container-transform.gif)


https://github.com/hott3/flutter_animation/blob/efe9000564e8837c513355fc4f47bd4b8172285a/lib/main.dart#L47-L62


`OpenContainer`を利用し、展開前のWidgetと展開後のWidgetを指定します。
`closedBuilder`には、展開前のWidgetを指定します。
`openBuilder`には、展開後のWidgetを指定します。

`animations`パッケージはContainer transformだけでなく、他のTransitionsも実装できます。

- Shared axis
- Fade through
- Fade

Flutterの公式のissueにMaterial Design 3のTransitionsの対応状況が記載されています。
そのissueの対応状況によっては、別の実装方法が示されるかもしれませんが、よければご参考ください。

## まとめ

みなさんは画面遷移を実装する時には、どのような実装をしていますか。
コンテンツや機能が多いアプリは画面設計が複雑になり、ユーザーがアプリの仕組みを理解しにくくなるかと思います
画面遷移のアニメーションを活用することで、不快感を与えることなくユーザーに理解してもらいやすくすることが可能です。

もし参考になったところや、疑問に感じたところがあればコメントやいいねをください🌱
画面遷移パターンを追加していきたいと思います🌻
