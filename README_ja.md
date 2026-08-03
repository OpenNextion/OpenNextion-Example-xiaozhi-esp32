# OpenNextion XiaoZhi AI チャットボット

([English](README.md) | [中文](README_zh.md) | [日本語](README_ja.md))

対応する OpenNextion ESP32-S3 タッチスクリーンを XiaoZhi AI 音声アシスタントにします。画面に合うファームウェアを書き込み、Wi-Fi に接続すれば、画面のタップまたは BOOT ボタンで会話を始められます。

<!-- MEDIA TODO — ヒーロー画像または動画。推奨パス: docs/images/opennextion-xiaozhi-hero.jpg
     完成したデスクトップケースに収めた、電源オンの OpenNextion パネルを表示。推奨幅: 820 px。 -->

<p align="center">
  <img src="docs/v1/OpenNextion-ONX2432G028.jpg" alt="OpenNextion ONX2432G028 2.8-inch touchscreen" width="390">
  <img src="docs/v1/OpenNextion-ONX3248G035.jpg" alt="OpenNextion ONX3248G035 3.5-inch touchscreen" width="390">
</p>

> このプロジェクトは [xiaozhi-esp32](https://github.com/78/xiaozhi-esp32) の OpenNextion ハードウェア向けポートです。以下の 2 機種のみを対象としています。

## 対応ハードウェア

| OpenNextion モデル | ディスプレイ | 向き | ファームウェアのボード名 | 状態 |
| --- | --- | --- | --- | --- |
| [ONX2432G028][onx2432g028] | 2.8 インチ静電容量式タッチ、240 × 320 | 縦向き | <code>OpenNextion-ONX2432G028</code> | 対応 |
| [ONX3248G035][onx3248g035] | 3.5 インチ静電容量式タッチ、320 × 480 | 縦向き | <code>OpenNextion-ONX3248G035</code> | 対応 |

**パネルに記載された型番と完全に一致するファームウェアだけを使用してください。ONX2432G028 と ONX3248G035 のファームウェアは相互に使用できません。**

このポートはディスプレイ、静電容量式タッチ、デュアルマイク、スピーカー、Wi-Fi をサポートします。2.4 GHz Wi-Fi が必要です。

## 始める前に

- 上表にある対応 OpenNextion パネル。
- 充電専用ではないデータ通信対応 USB ケーブル。
- Windows、macOS、または Linux のコンピューター。
- 2.4 GHz Wi-Fi ネットワーク。ESP32-S3 は 5 GHz 専用ネットワークには接続できません。
- 既定の XiaoZhi サービスを使う場合は [xiaozhi.me](https://xiaozhi.me) アカウント。

## クイックスタート

### 1. 正しいファームウェアを入手する

プロジェクトの [GitHub Releases](https://github.com/OpenNextion/OpenNextion-Example-xiaozhi-esp32/releases) から最新ファームウェアをダウンロードします。現在の <code>v2.2.6</code> 初回書き込みイメージは次のとおりです。

| パネル | ダウンロードするファイル |
| --- | --- |
| ONX2432G028 | [<code>xiaozhi_V2.2.6_merged_ONX2432G028_en_Jarvis.bin</code>](https://github.com/OpenNextion/OpenNextion-Example-xiaozhi-esp32/releases/download/v2.2.6/xiaozhi_V2.2.6_merged_ONX2432G028_en_Jarvis.bin) |
| ONX3248G035 | [<code>xiaozhi_V2.2.6_merged_ONX3248G035_en_Jarvis.bin</code>](https://github.com/OpenNextion/OpenNextion-Example-xiaozhi-esp32/releases/download/v2.2.6/xiaozhi_V2.2.6_merged_ONX3248G035_en_Jarvis.bin) |

ファイル名の <code>ONX...</code> 型番がパネルと一致するものだけを選択してください。他の XiaoZhi ボード用ファームウェアは使用しないでください。

### 2. パネルに書き込む

<!-- MEDIA TODO — 書き込み手順画像。推奨パス: docs/images/opennextion-xiaozhi-flashing.jpg
     USB 接続したパネルと、正しいモデルが選択された書き込みツールを表示。推奨幅: 620 px。 -->

1. データ通信対応 USB ケーブルでパネルをコンピューターへ接続します。
2. [初心者向け書き込みガイド][flashing-guide]に従い、対応する <code>.bin</code> ファイルをアドレス <code>0x0</code> に書き込みます。
3. 完了後、パネルが再起動するまで待ちます。

シリアルデバイスが表示されない場合は、USB ケーブルまたはポートを変更してください。充電専用ケーブルもあります。書き込みツールが接続できない場合は、BOOT と Reset ボタンでダウンロードモードにしてから再試行してください。

### 3. Wi-Fi を設定する

<!-- MEDIA TODO — Wi-Fi 設定画像。推奨パス: docs/images/opennextion-xiaozhi-wifi-setup.jpg
     Xiaozhi-xxxx ホットスポットおよび/または http://192.168.4.1 の設定ページを表示。推奨幅: 620 px。 -->

初回起動時、または保存済み Wi-Fi を使用できない場合、デバイスは <code>Xiaozhi-xxxx</code> という設定用ホットスポットを作成します。

1. スマートフォンまたはコンピューターで <code>Xiaozhi-xxxx</code> Wi-Fi に接続します。
2. 設定ページが自動的に開かない場合は <http://192.168.4.1> を開きます。
3. 2.4 GHz の自宅 Wi-Fi を選び、パスワードを入力します。
4. 保存し、デバイスが Wi-Fi へ接続して起動を続けるまで待ちます。

設定用ホットスポットはオープンネットワークです。信頼できる場所で設定し、完了後は設定モードを終了してください。

### 4. 有効化して会話を始める

<!-- MEDIA TODO — 有効化または利用画像。推奨パス: docs/images/opennextion-xiaozhi-activation.jpg
     有効化画面、またはタッチで会話を開始する様子を表示。推奨幅: 620 px。 -->

既定のファームウェアは [xiaozhi.me](https://xiaozhi.me) に接続します。画面の有効化案内に従い、その後 XiaoZhi コンソールにログインしてデバイスとモデル設定を管理します。

画面を 1 回タップするか **BOOT** ボタンを短く押すと会話を開始します。同じ操作でもう一度、現在の会話を終了できます。

## 日常操作

| 行いたいこと | 操作 |
| --- | --- |
| 会話の開始・終了 | 画面をタップするか、**BOOT** ボタンを短く押します。 |
| AI サービスの設定変更 | 有効化後、[xiaozhi.me](https://xiaozhi.me) コンソールへログインします。 |
| Wi-Fi の変更 | デバイスを再起動し、起動中に **BOOT** ボタンで設定モードに入り、ホットスポット設定を完了します。 |
| 誤った・壊れたファームウェアからの復旧 | 対応するパネル型番用の完全な USB ファームウェアパッケージを書き込み直します。 |
| ファームウェアの更新 | パネル型番が明記された更新パッケージだけを使用し、そのリリースノートに従います。 |

## XiaoZhi サービスと AI モデルの設定

既定サービスでデバイスを有効化した後、[xiaozhi.me](https://xiaozhi.me) コンソールでデバイスと利用可能な AI モデルの設定を管理します。サービスの選択、利用可能なモデル、アカウント設定はパネルのファームウェアではなくコンソールで管理されます。

セルフホストサービスや別のバックエンドを使う場合は、XiaoZhi プロトコルに対応したサーバーを導入し、そのサーバーの文書に従って設定してください。

- [xiaozhi-esp32-server](https://github.com/xinnan-tech/xiaozhi-esp32-server)（Python）
- [xiaozhi-esp32-server-java](https://github.com/joey-zhou/xiaozhi-esp32-server-java)（Java）
- [xiaozhi-server-go](https://github.com/AnimeAIChat/xiaozhi-server-go)（Go）

## トラブルシューティング

### コンピューターがパネルを見つけられない

データ通信対応 USB ケーブルを使用し、別の USB ポートも試してください。それでも表示されない場合は、お使いの OS に必要な USB シリアルドライバーをインストールしてください。

### 書き込み時に接続できない

USB を抜き差しして再試行してください。必要なら BOOT と Reset ボタンでダウンロードモードにしてから書き込みを開始します。

### Wi-Fi に接続できない

選択したネットワークが 2.4 GHz を提供していることと、パスワードが正しいことを確認してください。起動中に **BOOT** ボタンを押して設定モードへ入り、<code>Xiaozhi-xxxx</code> に接続して再設定します。

### 画面が正しくない、またはタッチが反応しない

誤ったファームウェアが書き込まれている可能性があります。USB で正しいパネル型番用の完全なパッケージを書き込み直してください。2 機種のファームウェアは交換できません。

## ケースと画像

<!-- MEDIA TODO — 最終的な取付写真と公開 3D モデルへのリンクを追加。
     推奨パス:
       docs/images/onx2432g028-xiaozhi-enclosure.jpg
       docs/images/onx3248g035-xiaozhi-enclosure.jpg
     各モデルについて、パネルを 3D プリントケースに収めた斜めからの写真を 1 枚追加。 -->

デスクトップケースの写真とダウンロード可能な 3D プリントファイルは後で追加します。

| モデル | 3D プリントケース |
| --- | --- |
| ONX2432G028 | リンク追加予定 |
| ONX3248G035 | リンク追加予定 |

## 開発者向け

通常の利用には開発環境は不要です。ファームウェアを変更する場合、またはリリース済みファームウェアがない場合のみ、ソースからビルドしてください。

1. VS Code または Cursor 用 ESP-IDF 拡張をインストールし、ESP-IDF 5.4 以降を使用します。
2. プロジェクトディレクトリで ESP32-S3 ターゲットを選択し、設定を開きます。

~~~sh
idf.py set-target esp32s3
idf.py menuconfig
~~~

3. <code>menuconfig</code> で <strong>Board Type</strong> を開き、パネルに対応する項目を 1 つだけ正確に選択します。

   - 2.8 インチパネル: <strong>OpenNextion ONX2432G028</strong>
   - 3.5 インチパネル: <strong>OpenNextion ONX3248G035</strong>

   設定を保存して <code>menuconfig</code> を終了します。画面サイズが近い他のボードを選択しないでください。

4. ビルドして書き込みます。

~~~sh
idf.py build
idf.py flash monitor
~~~

ボードファイルは [main/boards/OpenNextion_ONX2432G028](main/boards/OpenNextion_ONX2432G028) と [main/boards/OpenNextion_ONX3248G035](main/boards/OpenNextion_ONX3248G035) にあります。

### 開発者ドキュメント

- [Custom board guide](docs/custom-board.md) — ボードの追加とハードウェアサポートの変更。
- [MCP usage guide](docs/mcp-usage.md) と [MCP protocol](docs/mcp-protocol.md) — AI サービスへデバイス機能を公開。
- [MQTT + UDP protocol](docs/mqtt-udp.md) と [WebSocket protocol](docs/websocket.md) — カスタムバックエンドを統合。
- [BluFi provisioning](docs/blufi.md) — 既定のホットスポットではなく Bluetooth で Wi-Fi 設定。

## 謝辞とライセンス

本プロジェクトは [xiaozhi-esp32](https://github.com/78/xiaozhi-esp32) に基づき、[MIT License](LICENSE) で公開されています。第三者コンポーネントには個別のライセンス表示がある場合があります。

第三者ファームウェアの書き込みは、デバイス損傷やデータ損失のリスクを伴います。書き込み前に、ファームウェアがパネルの型番に一致することを確認してください。

[flashing-guide]: https://ccnphfhqs21z.feishu.cn/wiki/Zpz4wXBtdimBrLk25WdcXzxcnNS
[onx2432g028]: https://nextion.tech/wiki/onx2432g028/
[onx3248g035]: https://nextion.tech/wiki/onx3248g035/
