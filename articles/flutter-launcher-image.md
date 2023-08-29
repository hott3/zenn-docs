---
title: "【Flutter】アプリアイコンに必要な画像と追加方法（flutter_launcher_icons,Figma）"
emoji: "🌠"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["flutter", "figma",]
published: true
---

# アプリアイコンに必要な画像と追加方法

どのアプリでもホーム画面に表示するためのアイコン画像が必要になります。
iOSとAndroid両方のアイコン画像を追加できるパッケージを使ってみました。

https://pub.dev/packages/flutter_launcher_icons

また、アイコン画像を追加するにはOSに依存した作業が必要になります。
OSに依存する画像の仕様を理解することと、パッケージを使用することで、作業をシンプルにできました。


## やったこと

### 事前準備

:::details 動作環境
flutter 3.7.7
iOS 16
Android 13
:::

- 画像を知る
- 画像を用意する
- flutter_launcher_iconsのインストール
- flutter_launcher_iconsの設定


### 追加作業

- `flutter_launcher_icons`の実行


## 画像を知る

### iOSで使用されるアイコン画像

Appleのガイドラインを確認するとアプリアイコンの画像に仕様が定められていることがわかります。

![](/images/flutter-launcher-image/guideline-ios-icon-01.png)

https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/

App Storeで使用する画像は1024x1024のサイズです。
他の項目も確認すると、画像のサイズは1024x1024が一番大きく、
他のサイズについては自動で小さなものを生成できるとあります。

> You need to provide a large version of your app icon, measuring 1024x1024 pixels, to display in the App Store. You can let the system automatically scale down your large app icon to produce all other sizes,

つまり、iOSのアイコンに必要な画像は以下のとおりです。

- 1つのレイヤーで構成されていること
- 透過度は使用しないこと
- 四角い画像であること
- 1024x1024のサイズ

### Androidで使用されるアイコン画像

android developerサイトを確認すると、アダプティブアイコンの記載があります。

> Android 8.0（API レベル 26）では、アダプティブ ランチャー アイコンが導入され、デバイスモデルごとに異なる図形を表示できるようになりました。

https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive?hl=ja

アダプティブアイコンとは、バックグランドとフォアグラウンドの2つのレイヤーで構成されています。
レイヤーを組み合わせ、デバイスごとのマスクに切り取られたイメージが画面に表示されます。

公式ドキュメントのイメージ図がわかりやすかったので、転載します。

> 図 2: アダプティブ アイコンは 2 つのレイヤとマスクを使って定義されます。

![](https://developer.android.com/guide/practices/ui_guidelines/images/NB_Icon_Layers_3D_03_ext.gif)

Androidアイコンは、2つの画像が必要です。

- background
    - 108dpx108dp
    - 外側の4辺の18dpは、視覚効果のために使用される
- foreground
    - 108dpx108dp
    - 72dpx72dpの中にロゴやイメージを設置する

monoさんの過去の記事が参考になりました🙇‍♂️

https://gist.github.com/mono0926/38561024c187b8bb359f5445e9b0e900#file-android_adaptive_icon-md

Figma CommunityにMaterial Designのファイルもありますので、参考になるかと思います。

https://www.figma.com/community/file/1131374111452281708/Android-App-Icons


## 画像を用意する

Figmaを用いて前述の条件に対応した画像を作成しました。
（使用した画像はFigma CommunityのUI Kitから参照して編集したものです。）

:::details icon_ios.png
![](/images/flutter-launcher-image/icon_ios.png =250x)
:::

:::details icon_adaptive_foreground.png
![](/images/flutter-launcher-image/icon_adaptive_foreground.png =250x)
:::

:::details icon_adaptive_background.png
![](/images/flutter-launcher-image/icon_adaptive_background.png =250x)
:::

作業用のファイルをFigma Communityに公開しているので、よければご参考ください💡

作業用のファイル内で行う作業は下記のとおりです。

- アイコン用の画像を用意する
- フレーム内に画像を設置する
- プレビューを参考に位置を調整する
- exportして、画像データをダウンロードする

https://www.figma.com/community/file/1232673757056185299/Icon-Template-for-flutter_launcher_icons(iOS-Icon-and-Android-Adaptive-Icon)


## flutter_launcher_iconsのインストール

- インストールコマンドの実行をします

`flutter pub add flutter_launcher_icons`

https://pub.dev/packages/flutter_launcher_icons

## flutter_launcher_iconsの設定

- `pubspec.yaml`に設定を追加します

```
flutter_icons:
  ios: true
  image_path: "assets/images/launcher/icon_ios.png"
  remove_alpha_ios: true
  android: true
  adaptive_icon_background: "assets/images/launcher/icon_adaptive_background.png"
  adaptive_icon_foreground: "assets/images/launcher/icon_adaptive_foreground.png"
```

### `remove_alpha_ios`の指定について

前述の通り、AppleのガイドラインでiPhoneのアイコンには透過画像が利用はできないことがわかりました。
そのため、`flutter_launcher_icons`の設定では`remove_alpha_ios: true`と記載します。

## `adaptive_icon_xxx`について

パッケージのドキュメントの通り、 `adaptive_icon_background`と`adaptive_icon_foreground`は両方指定する必要があります。

> adaptive_icon_background: The color (E.g. "#ffffff") or image asset (E.g. "assets/images/christmas-background.png") which will be used to fill out the background of the adaptive icon.

> adaptive_icon_foreground: The image asset which will be used for the icon foreground of the adaptive icon Note: Adaptive Icons will only be generated when both adaptive_icon_background and adaptive_icon_foreground are specified. (the image_path is not automatically taken as foreground)

## `flutter_launcher_icons`の実行

- `flutter_launcher_icons`を実行します

`flutter pub run flutter_launcher_icons:main`

```
$ flutter pub run flutter_launcher_icons:main
This command is deprecated and replaced with "flutter pub run flutter_launcher_icons"
  ════════════════════════════════════════════
     FLUTTER LAUNCHER ICONS (v0.13.1)                               
  ════════════════════════════════════════════
  

⚠ Warning: flutter_icons has been deprecated please use flutter_launcher_icons instead in your yaml files
• Creating default icons Android
• Overwriting the default Android launcher icon with a new icon
• Creating adaptive icons Android
• Overwriting default iOS launcher icon with new icon
No platform provided

✓ Successfully generated launcher icons
```

## アプリアイコンの反映を確認

無事、反映されていることを確認しました。

![](/images/flutter-launcher-image/check-result-ios.png =250x)

![](/images/flutter-launcher-image/check-result-android.png =250x)


## 利用時に検討した点

### iOSで画像が反映されない

iOSの場合はキャッシュが発生するために、反映されないことがあります。
アプリのアンインストールや端末の再起動で対処できました。

## 公式ドキュメント

- flutter_launcher_icons

https://pub.dev/packages/flutter_launcher_icons

- App icons

https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/

- アダプティブアイコン

https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive?hl=ja

- Android App Icon(Material Design)

https://www.figma.com/community/file/1131374111452281708/Android-App-Icons


## 参考

参考になりました🙇‍♂️

https://medium.com/flutter-jp/icon-935d637d2da0

https://gist.github.com/mono0926/38561024c187b8bb359f5445e9b0e900#file-android_adaptive_icon-md

https://note.com/nviveto/n/n4a4e0377a97b

## まとめ

アイコンを追加するための作業と必要な画像情報をまとめました。
アイコンの設定作業はアプリを制作する度に必要な作業です。
ご参考いただけると幸いです。