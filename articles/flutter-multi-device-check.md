---
title: "【Flutter】複数のプレビュー画面を同時に確認する（VSCode,launch.json）"
emoji: "📲"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["flutter","vscode"]
published: true
---

# 複数のプレビュー画面を同時に確認する

実装した画面のレイアウトを確認する際に、複数の端末でデバッグして確認することがあります。
デバッグ起動 → 確認 → デバッグ起動 → 確認 → デバッグ起動... と手間がかかるので、
シミュレーターを複数同時に立ち上げたり、シミュレーター内でプレビューを切り替える方法をまとめてみました。

## やったこと

- iOSシミュレーターの追加
- Androidシミュレーターの追加
- 複数のシミュレーターで同時にデバッグする設定
- 端末内にデバイスプレビューを表示する方法


## iOSシミュレーターの追加

- Simulator > File > Open Simulator > 端末を選択

![](/images/flutter-multi-device-check/add-ios-device-01.png)

- 参考になりました🙇‍♂️

https://zenn.dev/ryota_iwamoto/articles/simulator_switch_for_androidstudio


## Androidシミュレーターの追加

- Android Studio > ︙ > Create device > 端末を選択

![](/images/flutter-multi-device-check/add-android-device-01.png)

- 設定値など細かく記載があり、参考になりました🙇‍♂️

https://akira-watson.com/android/avd-manager.html

## 複数のシミュレーターで同時にデバッグする設定

ここではVSCodeを利用した方法を記載します

- `flutter devices`で`deviceId`確認

![](/images/flutter-multi-device-check/debug-multi-devices-01.png)

- VSCodeのlaunch.jsonに記載

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "device-check-android",
            "request": "launch",
            "type": "dart",
            "deviceId": "xxxxxx" // flutter devicesで確認した値
        },
        {
            "name": "device-check-iPhone",
            "request": "launch",
            "type": "dart",
            "deviceId": "xxxxxx" // flutter devicesで確認した値
        },
        {
            "name": "device-check-iPad",
            "request": "launch",
            "type": "dart",
            "deviceId": "xxxxxx" // flutter devicesで確認した値
        },
    ],
    "compounds": [
        {
            "name": "All Devices", // 追加するコマンドの名前
            "configurations": [ // 起動に使用する設定を指定する
                "device-check-android",
                "device-check-iPhone",
                "device-check-iPad",
            ],
        }
    ]
}
```

- VSCodeの実行とデバッグから、launch.jsonに追加した`All Devices`を選択

![](/images/flutter-multi-device-check/debug-multi-devices-02.png)

- 複数の端末が起動される

![](/images/flutter-multi-device-check/debug-multi-devices-03.png)


https://github.com/flutter/flutter/wiki/Multi-device-debugging-in-VS-Code

https://zenn.dev/ioridev/articles/7201841bd1749f
## 端末内にデバイスプレビューを表示する方法

`device_preview`パッケージを使用します。
一つの画面内に複数の端末の表示を切り替えることができます。

https://pub.dev/packages/device_preview


- パッケージ追加後に`DevicePreviw`で、`MyApp`をラップする

```
void main() {
  runApp(
    DevicePreview(
      builder: (context) => const MyApp(),
    ),
  );
}
```

- 画面右のサイドバーのDevice model 設定から端末を選択

![](/images/flutter-multi-device-check/run-device-preview-01.png)


:::message
`DevicePreview`にoptionを設定することで初期設定を指定することもできます。
詳しくはドキュメントに記載があります。
:::

https://aloisdeniel.github.io/flutter_device_preview/#/content/usage/options



## まとめ

複数の画面を確認する方法がいくつかありますが、ご参考いただけると幸いです。