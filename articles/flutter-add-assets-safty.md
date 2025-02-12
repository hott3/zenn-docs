---
title: "【Flutter】画像を効率的に追加する方法（flutter_gen）"
emoji: "📂"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["flutter"]
published: true
---

# 画像を効率的に追加する方法

アプリを実装する際に、画像やフォントをassetsに追加することがあります。
追加した画像やフォントを反映する際に、`assets/images/...` や `NotoSans` など、ソースコード上で文字列の指定が必要です。
文字列の指定 → リロード → 反映の確認のように手順がいくつか発生するので、手順の途中でタイポが発生するかもしれません。
そこで、文字列指定の簡略化とタイポ防止のために、`flutter_gen`を使用してみました。

https://pub.dev/packages/flutter_gen

## やったこと

### 事前準備

- `flutter_gen`の有効化

### 追加作業

- pubspec.yamlに記載
- `fluttergen`の実行
- 画像パスの指定
- フォントの指定


## `flutter_gen`の有効化

- `flutter_gen`のコマンドを有効化するために下記のコマンドを実行

`dart pub global activate flutter_gen`


:::message
シェルにパスの追加が必要です。
:::


## pubspec.yamlに記載

- pubspec.yamlに追加するassetsを記載します

今回は、下記のような画像とフォントを使用します。

```yaml
  assets:
    - assets/images/user
    - assets/images/post

  fonts:
    - family: NotoSansJP
      fonts:
        - asset: assets/fonts/Noto_Sans_JP/NotoSansJP-Regular.otf
          weight: 400
        - asset: assets/fonts/Noto_Sans_JP/NotoSansJP-Bold.otf
          weight: 700
```


## `fluttergen`の実行

- `fluttergen`を実行します

```
$ fluttergen                                                                
FlutterGen v5.2.0 Loading ... project-name/pubspec.yaml
Generated: /project-name/lib/gen/assets.gen.dart
Generated: /project-name/lib/gen/fonts.gen.dart
FlutterGen finished.
```

## 画像パスの指定

- 自動生成されたClassを使用してパスを指定します

`Assets.~`と入力するとサジェストが出てくるので、
タイポの心配なくパスを指定できます。🙌

![](/images/flutter-add-assets-safty/add-assets-image.png)

## フォントの指定

- 自動生成されたClassを使用してフォントを指定できます

生成されたClassは`FontFamily`でプロパティを指定するだけです。


![](/images/flutter-add-assets-safty/add-assets-fontfamily.png)


## 公式ドキュメント

- 画像の追加

https://docs.flutter.dev/development/ui/assets-and-images

- フォントの追加

https://docs.flutter.dev/cookbook/design/fonts


## 利用時に検討した点

### 自動生成されるディレクトリ名を変えたい

> FlutterGen also support generating other style of Assets class:

`pubspec.yaml`に記載して生成されるディレクトリのパスを指定できます。

https://pub.dev/packages/flutter_gen#configuration-file

```yaml
# pubspec.yaml
flutter_gen:
  output: lib/gen/ # Optional (default: lib/gen/)
  line_length: 80 # Optional (default: 80)
```


### enum内では、Assetsクラスのパスを利用できない

enumクラスの定義にはconstが必要です。
加えて、constの引数には定数式が必要なために`Assets`クラスを利用できません。

https://dart.dev/tools/diagnostic-messages?utm_source=dartdev&utm_medium=redir&utm_id=diagcode&utm_content=non_const_generative_enum_constructor#non_const_generative_enum_constructor

https://dart.dev/tools/diagnostic-messages?utm_source=dartdev&utm_medium=redir&utm_id=diagcode&utm_content=const_with_non_constant_argument#const_with_non_constant_argument



### SVGファイルのパス指定でFlutterGenを利用したい

Flutterには、SVGファイルの表示する機能が含まれていないため、表示するためにはパッケージの導入が必要になります。
FlutterGenを利用する際には、`pubspec.yaml`に記載を追加することで、SVGファイルのパス指定を行えるようになります。

```yaml
## pubspec.yaml
flutter_gen:
  integrations:
    flutter_svg: true
```

呼び出し例は下記のように、`.svg`を記述します。

```dart
Widget build(BuildContext context) {
  return Assets.images.logo.svg(
    width: 120,
    height: 120,
  );
}
```


## 参考

参考になりました🙇‍♂️

https://wasabeef.medium.com/fluttergen-25149caea94f

https://zenn.dev/mamushi/scraps/aa3e57f6c8fa09

https://qiita.com/minako-ph/items/2104cbebda5dfa924748

## まとめ

指定を効率化することでロジックに集中できます。
ご参考いただけると幸いです。