<h1 align="center">
  passivbot
</h1>

![passivbot Version](https://img.shields.io/badge/passivbot-0.0.1-blue)

## BybitとBinance Futuresで動作するトレーディングボット

:warning: **ご自身の責任でご利用ください** :warning:

## Overview

ボットの目的は、時間をかけてトークンを蓄積することです

先物市場で働くマーケットメーカーボットで、現在の価格の上下に複数のPost-Only設定で指値注文を出します。

取引のwebsocket(※1)ライブ配信を聞き、継続的に注文を更新します。

(※1：Webにおいて双方向通信を低コストで行うための仕組み。httpの双方向通信アップグレード版)

可能であれば、ヘッジモードを使用します。


### 要求事項

- Python >= 3.8
- [requirements.txt](requirements.txt) 依存するPythonパッケージ

### 依存するPythonパッケージ（ライブラリ）のSetup

```bash
    pip install -r requirements.txt
```

### 使い方:

#### 取引所のBybit先物とBinance先物をサポートし、サポートされている場合はヘッジモードを使用します。

1. [api-keys.json](api-keys.json)というファイルにあなたのapiキーとシークレットを追加します。
2. ```bash
   python3 start_bot.py {account_name} {symbol} {path/to/config.json}
   ```

例:

```bash
python3 start_bot.py binance_01 XMRUSDT configs/live/binance_xmrusdt.json
```

#### dockerで起動

[docker-compose.yml](docker-compose.yml)のexchangeとuser_nameでコマンドを修正し、`docker-compose up -d`(バックグラウンドで実行する場合は-d)で起動します。
生成されたコードやファイルはすべてオリジナルのgitフォルダにあります。

#### botの停止

botを停止させるには、`do_long`と`do_shrt`の両方を`false`に設定します。
botは、既存のポジションがすべて閉じられるまで、新しいポジションを開くことなく、通常通りに動作します。

#### Telegramの設定

このbotは、Telegramを介してbotとのインターフェイスを提供しています。
これを設定するには、Telegramのbotトークンとchat-idが必要です。
これらを入手したら、api-keys.jsonファイルで指定された個々のアカウントに対してTelegramを有効にします。
api-keys.jsonファイルにはTelegramの設定例がありますので、それを参考にしてください。
もし、あるアカウントにTelegramの設定が存在しない場合、Telegramは起動時に無効になります。

セットアップ方法については https://docs.microsoft.com/en-us/azure/bot-service/bot-service-channel-connect-telegram?view=azure-bot-service-4.0

チャットIDを取得するには、Telegramで@getmyid_botとチャットを開始してください。

Telegramでは、いくつかのコマンドやメッセージが提供されていますので、Telegramチャットで`/help`コマンドを発行して
すべてのオプションを見ることができます。

### ドキュメント[WIP], 下記のwikiを参照してください:

https://github.com/enarjord/passivbot/wiki

### Resources

- Repository of settings and their backtesting results: https://github.com/JohnKearney1/PassivBot-Configurations

### [Changelog](changelog.md)

### License

Released freely without conditions.
Anybody may copy, distribute, modify, use or misuse for commercial,
non-commercial, educational or non-educational purposes, censor,
claim as one's own or otherwise do whatever without permission from anybody.

## Backtester

A backtester is included

1. modify `configs/backtest/default.hjson` as desired
2. run with `python3 backtest.py {path_to_live_config_to_test.json}`
3. optional args: `-b or --backtest-config`: use different backtest config

Will use numba's just in time compiler to speed up backtesting.

## Optimizer

To optimize a configuration by iterating multiple backtests,

1. modify `configs/backtest/default.hjson` and `configs/optimize/default.hjson` as desired
2. run with `python3 optimize.py`
3. optional args: `-b or --backtest-config`: use different backtest config
4. optional args: `-o or --optimize-config`: use different optimize config
5. optionally make optimizer start from given candidate(s) by adding kwarg `--start {path_to_starting_candidate.json}`
   if pointing to a directory, will use all .json files in that directory as starting candidates

See [wiki](https://github.com/enarjord/passivbot/wiki) for more info on backtesting and optimizing

## Live settings

- [Binance](live_configs/binance_default.json)
- [Bybit](live_configs/bybit_default.json)

## Support the project

### Feel free to make a donation to show support of the work

- XMR: `49gUQ1jasDK23tJTMCvP4mQUUwndeLWAwSgdCFn6ovmRKXZAjQnVp2JZ2K4UuDDdYMNam1HE8ELZoWdeJPRfYEa9QSEK6XZ`

- Nano: `nano_1nf3knbhapee5ruwg7i8sqekx3zmifdeijr8495t9kgp3uyunik7b9cuyhf5`

- EOS: `nbt4rhnhpjan`

- XLM: `GDSTC6KQR6BCTA7BH45B3MTSY52EVZ4UZTPZEBAZHJMJHTUQQ5SM57S7`

- USDT TRC20 (Binance): `TJr3KYY8Bz7wRU7QLwoYQHk88LcaBJqQN5`

### Referrals

- [Bybit](https://www.bybit.com/en-US/register?affiliate_id=16464&language=en-US&group_id=0&group_type=1)
- [Binance](https://www.binance.cc/en/register?ref=TII4B07C)
