---
title: "【Flutter】記事のテンプレート（flutter_native_splash）"
emoji: "📂"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["flutter", "",]
published: false
---

# タイトル

スプラッシュ画像は、アプリを起動するときに表示されてで、準備中であることを知らせます。
スプラッシュ画像を設定するには、画像をassetsフォルダに追加し、コードで指定する必要があります。
ただし、サイズや解像度にも注意が必要で手間と感じることがあります。

`flutter_native_splash`を使用して、コマンドの実行で必要な画像の作成と設定を行います。


https://pub.dev/packages/flutter_native_splash






## やったこと

### 事前準備

- 画像のサイズ確認
- 画像の用意
- パッケージのインストール

### 追加作業

- 画像ファイルの設置
- コマンドの実行
- 反映の確認

## 画像のサイズ確認

まずはスプラッシュ画像に使用する画像を用意します。
今回、使用した画像のサイズは下記のとおりです。

1024x
aaax


自動生成のもとになる画像のサイズについて、ドキュメントには記載がないために、
他の方々の記事を参考にサイズを指定しました。

:::message
メッセージをここに
:::

https://github.com/jonbhanson/flutter_native_splash/issues/89

https://zenn.dev/flutteruniv_dev/articles/20220406-061305-flutter-native-splash

https://qiita.com/kokogento/items/12c44b6350ed8056c97e

- 作業

```
flutter_native_splash:
  color: '#888888'
  image: 'assets/images/splash_icon/splash_icon-768x768.png'
  android_12:
    icon_background_color: '#888888'
    image: 'assets/images/splash_icon/splash_icon-1152x1152.png'
```



コマンド結果の内容

```
$ flutter pub run flutter_native_splash:create
[Android] Creating default splash images
[Android] Creating default android12splash images
[Android] Creating dark mode android12splash images
[Android] Updating launch background(s) with splash image path...
[Android]  - android/app/src/main/res/drawable/launch_background.xml
[Android]  - android/app/src/main/res/drawable-v21/launch_background.xml
[Android] Updating styles...
[Android]  - android/app/src/main/res/values-v31/styles.xml
[Android]  - android/app/src/main/res/values-night-v31/styles.xml
[Android]  - android/app/src/main/res/values/styles.xml
[iOS] Creating  images
[iOS] Updating ios/Runner/Info.plist for status bar hidden/visible
Web folder not found, skipping web splash update...
╔════════════════════════════════════════════════════════════════════════════╗
║                                 WHAT IS NEW:                               ║
╠════════════════════════════════════════════════════════════════════════════╣
║ You can now keep the splash screen up while your app initializes!          ║
║ No need for a secondary splash screen anymore. Just use the remove()       ║
║ method to remove the splash screen after your initialization is complete.  ║
║ Check the docs for more info.                                              ║
╚════════════════════════════════════════════════════════════════════════════╝

✅ Native splash complete.
Now go finish building something awesome! 💪 You rock! 🤘🤩
Like the package? Please give it a 👍 here: https://pub.dev/packages/flutter_native_splash
```




反映の確認時にはキャッシュがあることを確認した

パケージの[ドキュメント](https://pub.dev/packages/flutter_native_splash#i-see-a-flash-of-the-wrong-splash-screen-on-ios)にも記載されている

> This is caused by an iOS splash caching bug, which can be solved by uninstalling your app, powering off your device, power back on, and then try reinstalling.

## 手順2

- 作業

## 手順3

- 作業

## 公式ドキュメント

- flutter_native_splash

https://pub.dev/packages/flutter_native_splash

- ドキュメント2

https://google.com

## 利用時に検討した点

### 検討した点1

- 作業1


## 参考

参考になりました🙇‍♂️

https://zenn.dev/flutteruniv_dev/articles/20220406-061305-flutter-native-splash


ダミー画像作成に使用したツール
（いつもありがとうございます）

https://placehold.jp/

画像編集に使用

https://www.figma.com

## まとめ


まとめました。
ご参考いただけると幸いです。