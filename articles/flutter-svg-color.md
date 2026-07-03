---
title: "【Flutter】Figmaで書き出したSVGファイルの色を変える方法（flutter_svg）"
emoji: "📂"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["flutter", "figma",]
published: false
---

# Figmaで書き出したSVGファイルの色を変える方法

アプリを作成する際にアイコン画像を使用する場面は多いです。
実装する際に適切なサイズの画像を指定しないと粗く表示されてしまいます。
しかし、SVG画像を利用することで、
サイズを引き伸ばしても見た目が粗くならず、色を動的に変化させることが可能です。


## やったこと

### 事前準備

- SVG画像を知る
- SVG画像を用意

### 追加作業

- SVG画像を`assets`に追加
- `flutter_svg`で表示
- フィルターを指定して色を変える


## SVG画像を知る

- SVG画像とは

> SVG は XML ベースのベクター グラフィックです。これらは、任意の画面でレンダリングできる数値と座標に基づく形状です。SVG はピクセルに依存しないため、画質に影響を与えることなく任意のサイズにスケーリングできます。また、透過性もサポートします。 （訳：Google Translate）

https://help.figma.com/hc/en-us/articles/13402894554519#:~:text=%E3%83%AC%E3%82%A4%E3%83%A4%E3%83%BC%E3%81%AE%E3%81%BF)-,SVG%20(%E3%82%B9%E3%82%B1%E3%83%BC%E3%83%A9%E3%83%96%E3%83%AB%20%E3%83%99%E3%82%AF%E3%82%BF%E3%83%BC%20%E3%82%B0%E3%83%A9%E3%83%95%E3%82%A3%E3%83%83%E3%82%AF%E3%82%B9),-SVG%20%E3%81%AF%20XML



## SVG画像を用意する

- SVG画像を用意

Flutterのデフォルトで用意されているMD3のResourcesを確認すると、
GoogleFontsにデータが用意されていることがわかります。

https://m3.material.io/styles/icons/overview#912ecccf-3fd8-4fe6-8142-458c5cc1a34f

https://fonts.google.com/icons

利用したいアイコンを選択して、
右下のSVGダウンロードボタンからSVG画像を取得できます。

- もしくは、FigmaからSVG画像をexportすることも可能です。

> 

https://help.figma.com/hc/article_attachments/13406331886359

引用）

https://help.figma.com/hc/ja/articles/360040028114-Figma%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B%E3%82%A8%E3%82%AF%E3%82%B9%E3%83%9D%E3%83%BC%E3%83%88%E3%81%AE%E3%82%AC%E3%82%A4%E3%83%89

## 手順2

- 作業

## 手順3

- 作業

## 公式ドキュメント

- Figmaからのエクスポート

https://help.figma.com/hc/ja/articles/360040028114-Figma%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B%E3%82%A8%E3%82%AF%E3%82%B9%E3%83%9D%E3%83%BC%E3%83%88%E3%81%AE%E3%82%AC%E3%82%A4%E3%83%89

- flutter_svg

https://pub.dev/packages/flutter_svg


- Flutter

https://api.flutter.dev/flutter/widgets/ColorFiltered-class.html

https://api.flutter.dev/flutter/dart-ui/BlendMode.html


## 利用時に検討した点

### 検討した点1

- 作業1


## 参考

参考になりました🙇‍♂️

https://google.com

## まとめ

まとめました。
ご参考いただけると幸いです。