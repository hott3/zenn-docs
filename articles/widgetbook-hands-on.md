---
title: "【Widgetbook】UIコンポーネントから開発しよう（Flutter,ハンズオン）"
emoji: "✨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Widgetbook","Flutter", "デザインシステム", "ハンズオン"]
published: true
---

# WidgetbookでUIコンポーネントから開発しよう

![WidgetbookでUIコンポーネントから開発しよう](/images/widgetbook-hands-on/thumbnail.gif)

## Widgetbookとは

Flutterを用いたアプリケーション開発において、UIコンポーネントの管理は非常に重要です。
[Widgetbook](https://docs.widgetbook.io/)は、FlutterのWidgetをカタログのように一覧表示し、個々のWidgetの動作を簡単に確認できるライブラリです。
シミュレーター上でWidgetを操作しているかのように、ブラウザ上でさまざまな状態のWidgetを視覚的に確認できます。

Widgetbookを使うことで、以下のような事が可能になります。

- ビジネスロジックと分離してUIコンポーネントの開発を進める
- 異なるデバイスのレイアウトや、ダークモード/ライトモードの表示などを確認
- Widgetbookの操作画面をデプロイしデザイナーとフィードバックを共有

この記事では、**Widgetbookプロジェクトの用意とユースケースの追加、アドオンの活用、ノブの活用について**解説します。
ぜひ、FlutterのUIコンポーネント開発に役立ててください👇

1. [サンプルプロジェクトの紹介](#サンプルプロジェクトの紹介)
2. [Widgetbookプロジェクトの用意](#Widgetbookプロジェクトの用意)
3. [ユースケースの追加](#ユースケースの追加)
4. [開発環境の整備](#開発環境の整備)
5. [アドオンの活用](#アドオンの活用)
6. [ノブの活用](#ノブの活用)
7. [Widgetbook活用方法の考察](#Widgetbook活用方法の考察)

:::message
この記事は「[Flutter Advent Calendar 2024](https://qiita.com/advent-calendar/2024/flutter)シリーズ 2」22日目の記事です🎄

シリーズ 2
21日目： [Flutterでポケポケみたいなカード風エフェクトのパッケージつくってみた #個人開発 - Qiita](https://qiita.com/oh-yeah-sea-kit2/items/3155d42dc516ae5b1149) by [oh-yeah-sea-kit2](https://qiita.com/oh-yeah-sea-kit2)さん
22日目： 【Widgetbook】UIコンポーネントから開発しよう（Flutter,ハンズオン） ← 今ここ
23日目： [[Flutter] 静的解析の設定を入れる (flutter_lints) #GitHub - Qiita](https://qiita.com/grhg/items/4210e5b4fd196026d03a) by [grhg - Qiita](https://qiita.com/grhg)さん

シリーズ 1
21 日目：[非同期初期化が必要なRiverpodプロバイダの初期化方法](https://zenn.dev/altiveinc/articles/riverpod-provider-initialization) by [村松龍之介](https://zenn.dev/riscait)さん
22 日目：[Pub workspaces を使ってみた](https://zenn.dev/kosukesaigusa/articles/dart-pub-workspaces) by [Kosuke Saigusa](https://zenn.dev/kosukesaigusa)さん
23 日目：[Bluesky投稿専用クライアントをつくった #Flutter - Qiita](https://qiita.com/hidea/items/2fb221b898faa5b6a9c3) by [ひであ](https://qiita.com/hidea) さん
:::

## サンプルプロジェクトの紹介

この記事で紹介している手順はサンプルプロジェクトで実施したものをもとに作成しています。
そのサンプルプロジェクトをGitHubに公開しています。

https://github.com/hott3/widgetbook_trial

## Widgetbookプロジェクトの用意

### 任意のディレクトリにプロジェクトを作成

ここで作成したプロジェクトがアプリプロジェクトとなります。

```:terminal
flutter create widgetbook_trial --empty
```

### Widgetbookプロジェクトをサブプロジェクトとして作成

アプリプロジェクトを作成後、Widgetbookプロジェクトをサブプロジェクトとして作成します。

```:terminal
cd widgetbook_trial
flutter create widgetbook --empty --platforms web
```

:::message
この記事ではサブプロジェクトとしてWidgetbookのプロジェクトを作成しています。
公式ドキュメントの[Quick Start - Widgetbook](https://docs.widgetbook.io/guides/quick-start)にもサブプロジェクトとして作成する方法が紹介されています。
:::

### Widgetbookプロジェクトの`pubspec.yaml`を編集

[Widgetbookパッケージ](https://pub.dev/packages/widgetbook)と名前衝突を避けるために、作成したWidgetbookプロジェクトの`pubspec.yaml`を編集します。

```diff yaml:widgetbook/pubspec.yaml
- name: widgetbook
+ name: widgetbook_workspace
```

### Widgetbookプロジェクトで使用するパッケージを追加

Widgetbookプロジェクトで使用するパッケージを追加します。

```:terminal
cd widgetbook
flutter pub add widgetbook widgetbook_annotation dev:widgetbook_generator dev:build_runner
```

追加したパッケージは以下の通りです。

- [widgetbook | Flutter package](https://pub.dev/packages/widgetbook)
- [widgetbook_annotation | Dart package](https://pub.dev/packages/widgetbook_annotation)
- [widgetbook_generator | Dart package](https://pub.dev/packages/widgetbook_generator)
- [build_runner | Dart package](https://pub.dev/packages/build_runner)


### Widgetbookプロジェクトのパス依存関係にアプリプロジェクトを追加

Widgetbookプロジェクトのパス依存関係に、アプリプロジェクトを追加します。
依存関係を追加することで、Widgetbookプロジェクトの開発時にアプリプロジェクトのコードを参照できるようになります。
アプリプロジェクトのコードを複製せずにimport文を追加することができるので二重管理の手間は起こりません。

```diff yaml:widgetbook/pubspec.yaml
dependencies:
+  widgetbook_trial:
+    path: ../
```

ここでフォルダ構造を確認する^[`tree`コマンドに[tree — Homebrew Formulae](https://formulae.brew.sh/formula/tree)を使用しています]と以下のようになります。
`widgetbook_trial`がアプリプロジェクトを開発するフォルダ、`widgetbook`フォルダがWidgetbookプロジェクトを開発するフォルダです。

```:terminal
widgetbook_trial $ tree -L 2
.
├── README.md
├── analysis_options.yaml
├── lib
│   └── main.dart
├── pubspec.lock
├── pubspec.yaml
├── web
│   ├── favicon.png
│   ├── icons
│   ├── index.html
│   └── manifest.json
├── widgetbook
│   ├── README.md
│   ├── analysis_options.yaml
│   ├── lib
│   ├── pubspec.lock
│   ├── pubspec.yaml
│   ├── web
│   └── widgetbook.iml
└── widgetbook_trial.iml

7 directories, 14 files
```


## ユースケースの追加

次にWidgetbookプロジェクトでUIコンポーネントを確認できるようにアプリプロジェクトとWidgetbookプロジェクトにファイルを追加します。

### アプリプロジェクトにUIコンポーネントを追加

アプリプロジェクトに`thanks_button.dart`を追加します。

![](/images/widgetbook-hands-on/thanksbutton-image.png)

```dart:widgetbook_trial/lib/thanks_button.dart
import 'package:flutter/material.dart';

class ThanksButton extends StatelessWidget {
  const ThanksButton({super.key});

  @override
  Widget build(BuildContext context) {
    return OutlinedButton.icon(
      onPressed: () {
        showDialog<String>(
            context: context,
            builder: (BuildContext context) => Dialog(
                  child: Padding(
                    padding: const EdgeInsets.all(16.0),
                    child: Text(
                      'どういたしまして！',
                      textAlign: TextAlign.center,
                    ),
                  ),
                ));
      },
      icon: Icon(Icons.favorite),
      label: Text('ありがとう！'),
    );
  }
}
```

### Widgetbookプロジェクトにユースケースを追加

Widgetbookプロジェクトに`ThanksButton`を表示するためのユースケースを追加します。


```dart:widgetbook/lib/thanks_button.dart
import 'package:flutter/material.dart';
import 'package:widgetbook_annotation/widgetbook_annotation.dart' as widgetbook;
import 'package:widgetbook_trial/thanks_button.dart';

@widgetbook.UseCase(name: 'Default', type: ThanksButton)
Widget buildThanksButtonUseCase(BuildContext context) {
  return ThanksButton();
}

```

### Widgetbookプロジェクトの`main.dart`を編集

Widgetbookプロジェクトの`main.dart`を以下のように書き換えます。


```diff dart:widgetbook/lib/main.dart
import 'package:flutter/material.dart';
+import 'package:widgetbook/widgetbook.dart';
+import 'package:widgetbook_annotation/widgetbook_annotation.dart' as widgetbook;
+
+import 'main.directories.g.dart';

void main() {
- runApp(const MainApp());
+ runApp(const WidgetbookApp());
}

-class MainApp extends StatelessWidget {
- const MainApp({super.key});
+@widgetbook.App()
+class WidgetbookApp extends StatelessWidget {
+ const WidgetbookApp({super.key});

  @override
  Widget build(BuildContext context) {
-   return const MaterialApp(
-     home: Scaffold(
-       body: Center(
-         child: Text('Hello World!'),
-       ),
-     ),
+   return Widgetbook.material(
+     directories: directories,
    );
  }
}
```

Widgetbookプロジェクトの`main.dart`を書き換えると以下のようなファイルになります。


```dart:widgetbook/lib/main.dart
import 'package:flutter/material.dart';
import 'package:widgetbook/widgetbook.dart';
import 'package:widgetbook_annotation/widgetbook_annotation.dart' as widgetbook;

// まだ存在しないファイルですが、次のステップで生成されます
import 'main.directories.g.dart';

void main() {
  runApp(const WidgetbookApp());
}

@widgetbook.App()
class WidgetbookApp extends StatelessWidget {
  const WidgetbookApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Widgetbook.material(
      // まだ未定義ですが、次のステップで生成されます
      directories: directories,
    );
  }
}

```

:::message alert
> Target of URI hasn't been generated: 'main.directories.g.dart'.
Try running the generator that will generate the file referenced by the URI.

> Undefined name 'directories'. Try correcting the name to one that is defined, or defining the name.

存在しないファイルや未定義の変数があるのでエラーが出ますが、次のステップで生成されるので無視してください。
:::

### Widgetbookプロジェクトでビルドランナーを実行

ビルドランナーを実行して、`directories`を含んだ`main.directories.g.dart`を生成します。

```
cd widgetbook
dart run build_runner build -d
```

:::details ファイルの編集を監視して自動でビルドする場合
```
dart run build_runner watch -d
```
:::

### Widgetbookプロジェクトの実行

これでWidgetbookプロジェクトの準備が完了したので実行してみます。

```
flutter run -d chrome
```

Widgetbookが立ち上がった後に、画面左側のペインから`ThanksButton`をクリックします。
以下のように`ThanksButton`が表示されれば成功です🎉🎉🎉

![](/images/widgetbook-hands-on/widgetbook-run-trial.png)


## 開発環境の整備

Widgetbookの実行が確認できたところで、この後の開発を効率的に行うために開発環境を整備します。

### WidgetbookプロジェクトにmacOSプラットフォームを追加

FlutterをWebのプラットフォームで実行する場合、ホットリロードが機能しません。^[Flutter Webはホットリスタートをサポートしていますが、ホットリロードはサポートしていません。[参照](https://docs.flutter.dev/tools/hot-reload#:~:text=Flutter%20web%20currently%20supports%20hot%20restart%20but%20not%20hot%20reload.)]
ホットリロードを有効にして開発するために、macOSのプロジェクトを追加します。※macOSユーザーのみ

```
cd widgetbook
flutter create --platforms macos .
```

### VSCodeのデバッグ環境を設定

VSCodeを利用している場合、`launch.json`を追加することでデバッグ環境の設定と実行を効率的に行うことができます。
以下のファイルを`.vscode/launch.json`として作成することで、さきほどの実行コマンドを叩く必要がなく、VSCodeの「実行とデバッグ」メニューからWidgetbookプロジェクトを実行できます。

```json:.vscode/launch.json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "debug widgetbook",
            "request": "launch",
            "type": "dart",
            "program": "widgetbook/lib/main.dart",
            "flutterMode": "debug",
        },
    ]
}
```

## アドオン

Widgetbookには確認画面の設定を動的に変更できるアドオンが用意されています。
Widgetbookで用意されているアドオンを使用することで異なる端末のレイアウト確認やテーマの切り替え、テキストのサイズ変更などが可能になります。

### アドオンの追加方法

`widgetbook/lib/main.dart`を編集して、Widgetbookに用意されているいくつかのアドオンを追加してみます。


```diff dart:widgetbook/lib/main.dart
  @override
  Widget build(BuildContext context) {
    return Widgetbook.material(
      directories: directories,
+     addons: [
+       DeviceFrameAddon(
+         initialDevice: Devices.ios.iPhone13,
+         devices: [
+           Devices.ios.iPhone13,
+           Devices.ios.iPhone13ProMax,
+           Devices.android.mediumPhone,
+         ],
+       ),
+       MaterialThemeAddon(
+         themes: [
+           WidgetbookTheme(name: 'Light', data: ThemeData.light()),
+           WidgetbookTheme(name: 'Dark', data: ThemeData.dark()),
+         ],
+       ),
+       TextScaleAddon(
+         min: 0.5,
+         max: 3.0,
+         divisions: 5,
+       ),
+       BuilderAddon(
+         name: 'Scaffold & SafeArea',
+         builder: (context, child) {
+           return Scaffold(
+             body: SingleChildScrollView(
+               child: SizedBox(
+                 width: double.infinity,
+                 child: SafeArea(
+                   child: child,
+                 ),
+               ),
+             ),
+           );
+         },
+       ),
+     ],
    );
  }
```

### `DeviceFrameAddon`

`DeviceFrameAddon`はデバイスの枠を切り替えるアドオンです。
ここで指定したデバイスの枠が表示されるのでプロジェクトに合わせて必要なデバイスの画面を用意できます。

![](/images/widgetbook-hands-on/deviceframeaddon-demonstration.gif)

### `MaterialThemeAddon`

`MaterialThemeAddon`はテーマを切り替えるアドオンです。
最初から用意されている`ThemeData`だけでなく、`ThemeData`を拡張することでオリジナルのテーマを追加することもできます。

![](/images/widgetbook-hands-on/materialthemeaddon-demonstration.gif)

### `TextScaleAddon`

`TextScaleAddon`はテキストのサイズを切り替えるアドオンです。
端末の設定で変更されるテキストサイズのテストに利用することができるので、アクセシビリティ対応の確認に利用できます。

![](/images/widgetbook-hands-on/textscaleaddon-demonstration.gif)

### `BuilderAddon`

`BuilderAddon`はユースケースをラップするWidgetを指定できるアドオンです。
ここで指定したWidgetがユースケースをラップするので、`Scaffold`や`SafeArea`などの毎回呼び出すWidgetを指定しておくことができます。

### その他のアドオン

他にも用意されているアドオンがあり、公式ドキュメントに詳細が記載されています。
言語設定のアドオンは、異なる言語のテキストが反映されたときにUIコンポーネントがどのように表示されるか確認するのに便利そうです。

> ### Available Addons
> Widgetbook comes equipped with a variety of ready-to-use Addons:
> 
> - Theme Addon: Provides theming options.
>   - Material Theme Addon
>   - Cupertino Theme Addon
>   - Custom Theme Addon
> - Device Frame Addon: Facilitates previewing use-cases on specific device sizes.
> - Localization Addon: Enables testing across different locales.
> - Text Scale Addon: Supports varying text scales and aids in accessibility testing.
> - Alignment Addon: Enables centering the use-case within the workbench.
> - Grid Addon: Enables displaying a pixel grid.
> 
> 引用）[Addons - Widgetbook](https://docs.widgetbook.io/addons)



## ノブ

Widgetbookにはユースケースに渡すパラメータをその場で変更できるノブが用意されています。
Widgetbookで用意されているノブを利用することで、さまざまな条件や入力に基づいてUIコンポーネントを調整できるので、UIコンポーネントの動作確認やデザイン検証が効率的に行えます。

### ノブの追加方法

#### アプリプロジェクトのWidgetにプロパティを追加 

まず、アプリプロジェクトの`thanks_button.dart`にプロパティを追加します。

```diff dart:lib/thanks_button.dart
class ThanksButton extends StatelessWidget {
- const ThanksButton({super.key});
+ const ThanksButton({
+   super.key,
+   required this.buttonLabel,
+   required this.responseText,
+   required this.color,
+   required this.textStyle,
+ });
+
+ final String buttonLabel;
+ final String responseText;
+ final Color color;
+ final TextStyle textStyle;

  @override
  Widget build(BuildContext context) {
    return OutlinedButton.icon(
      onPressed: () {
        showDialog<String>(
            context: context,
            builder: (BuildContext context) => Dialog(
                  child: Padding(
                    padding: const EdgeInsets.all(16.0),
                    child: Text(
-                     'どういたしまして！',
+                     responseText,
                      textAlign: TextAlign.center,
                    ),
                  ),
                ));
      },
-     icon: Icon(Icons.favorite),
-     label: Text('ありがとう！'),
+     icon: Icon(Icons.favorite, color: color),
+     label: Text(buttonLabel, style: textStyle.copyWith(color: color)),
    );
  }
}
```

#### Widgetbookプロジェクトのユースケースにノブを追加

Widgetbookプロジェクトのユースケースにノブを追加します。
追加したノブを使って、`ThanksButton`のプロパティに指定します。

```diff dart:widgetbook/lib/thanks_button.dart
@widgetbook.UseCase(name: 'Default', type: ThanksButton)
Widget buildThanksButtonUseCase(BuildContext context) {
- return ThanksButton();
+ final buttonLabel = context.knobs.string(
+   label: 'Button Label',
+   initialValue: 'ありがとう！',
+ );
+ final responseText = context.knobs.string(
+   label: 'Response Text',
+   initialValue: 'どういたしまして！',
+ );
+ final color = context.knobs.color(
+   label: 'Color',
+   initialValue: ThemeData().colorScheme.primary,
+ );
+ final textStyleOption = [
+   _TextStyleOption(
+     optionLabel: 'Large',
+     textStyle: TextStyle(
+       fontSize: 14,
+     ),
+   ),
+   _TextStyleOption(
+     optionLabel: 'Medium',
+     textStyle: TextStyle(
+       fontSize: 12,
+     ),
+   ),
+   _TextStyleOption(
+     optionLabel: 'Small',
+     textStyle: TextStyle(
+       fontSize: 11,
+     ),
+   ),
+ ];
+ final textStyle = context.knobs.list(
+   label: 'TextStyle',
+   initialOption: textStyleOption[0],
+   labelBuilder: (option) => option.optionLabel,
+   options: textStyleOption,
+ );
+
+ return ThanksButton(
+   buttonLabel: buttonLabel,
+   responseText: responseText,
+   color: color,
+   textStyle: textStyle.textStyle,
+ );
+ }
+ 
+ class _TextStyleOption {
+   const _TextStyleOption({
+     required this.optionLabel,
+     required this.textStyle,
+   });
+ 
+   final String optionLabel;
+   final TextStyle textStyle;
}
```

#### String Knob

`context.knobs.string()`はテキストを変更するノブです。
Widgetbookの画面上でテキストを入力することで、`ThanksButton`のプロパティを変更できます。

![](/images/widgetbook-hands-on/stringknob-demonstration.gif)

#### Color Knob

`context.knobs.color()`は色の値を変更するノブです。
Widgetbookの画面上で色を選択することで、`ThanksButton`のプロパティを変更できます。

![](/images/widgetbook-hands-on/colorknob-demonstration.gif)

#### List Knob

`context.knobs.list()`はリストから値を選択するノブです。
リストの選択肢には任意の型を使用できます。
Widgetbookの画面上でリストから値を選択することで、`ThanksButton`のプロパティを変更できます。

![](/images/widgetbook-hands-on/listknob-demonstration.gif)

#### その他のノブ

他にも用意されているノブがあり、公式ドキュメントに詳細が記載されています。

> | Type | Regular Knob | Nullable Knob |
> | ---- | ---- | ---- |
> | bool | boolean | booleanOrNull |
> | int | int.input | int.input |
> | int | int.slider | int.slider |
> | double | double.input | doubleOrNull.input |
> | double | double.slider | doubleOrNull.slider |
> | String | string | stringOrNull |
> | Duration | duration | durationOrNull |
> | DateTime | dateTime | dateTimeOrNull |
> | Color | color | colorOrNull |
> | T | list | listOrNull |
> 
> 引用）[Knobs - Widgetbook](https://docs.widgetbook.io/knobs)

## Widgetbook活用方法の考察

### 開発体制に与える影響

この記事ではエンジニアがUIコンポーネントを開発する際に、Widgetbookを利用する手順を解説しました。
開発したWidgetbookプロジェクトをデプロイしてGitHub PagesやFirebase Hostingにデプロイすることで、エンジニア以外のメンバーにもUIコンポーネントの確認を共有できます。
機能の仕様を調整しながらUIコンポーネントを先行して開発を進めるなど、柔軟な開発を進めることができるのもWidgetbookの特徴です。
もちろん機能の開発段階に進んだとき、UIコンポーネントの調整/修正を行う可能性もあります。
その際は、もとのアプリプロジェクトのコードを依存関係で連携しているので、アプリプロジェクトの作業はWidgetbookプロジェクトに反映させることができます。

### ユースケースを追加する手間

UIコンポーネントはアプリプロジェクトの中で行われますが、Widgetbookプロジェクトにユースケースを追加する手間がかかります。
たとえば、既存のUIコンポーネントにプロパティが追加された場合、ユースケースを編集して追加されたプロパティに対応する必要があります。
たとえば、新規のUIコンポーネントを追加された場合、どのようなUIコンポーネントなのか利用イメージを想定してユースケースを追加する必要があります。
私はこれらの作業は反復的で手間を感じる作業に感じています。

調べていると、VSCodeに[Widgetbook Entries Generator](https://marketplace.visualstudio.com/items?itemName=LeanCode.widgetbook-generator)という拡張機能があることを知りました。
この拡張機能はユースケースを追加するプロセスを自動化し、手動で設定する時間のかかる作業を効率化できるようです。

https://leancode.co/blog/moving-flutter-widgets-to-widgetbook

UIコンポーネントが少ない場合や重要なUIコンポーネントのみを管理する場合は、まずは手動でユースケースを追加しておき、その後に拡張機能の利用を検討するのも良いかもしれません。

## 参考記事など

参考になりました🙇‍♂️

https://zenn.dev/natoring/articles/3d6638ab499117
https://zenn.dev/imajoriri/articles/6b10a2351fe887
https://qiita.com/Ryota-Nakamura-317/items/b381230a890133dd611b
https://light11.hatenadiary.com/entry/2024/08/05/191249
https://kakehashi-dev.hatenablog.com/entry/2024/09/24/110000


## まとめ

Widgetbookを利用してUIコンポーネントから開発する手順をまとめました。
UI/UXを重視したユーザー体験の向上にはUIコンポーネントの管理が重要です。
ビジネスロジックと分離してUIコンポーネントの開発が必要になったとき、試してみてはいかがでしょうか。
ぜひこの記事をご参考くださいませ💡
もし参考になったところや、疑問に感じたところがあればコメントください🌻