# 達人大富豪
「達人大富豪」は、Web上での大富豪プログラミングを通じて、達人プログラマを目指すWebアプリケーションです。


# 目次
- [動作環境](#動作環境)
- [インストール方法](#インストール方法)
- [実行方法](#実行方法)
- [使い方](#使い方)

## アーキテクチャ
### システム構成
* 開発言語
 * Python 3.4, JavaScript
* フレームワーク
 * Tornado
* DB
 * PostgreSQL 9.4
* 対象ブラウザ
 * Google Chrome, FireFox

### モデル構成

### 通信方式


##インストール方法
インストール方法では、アプリケーションの実行に必要なモジュールのインストール方法について説明します。

### モジュールのインストール
TatsujinDaifugoを動作させるために必要なモジュールは以下のコマンドでインストールできます。
```shell
$ pip install -r requirements.txt
```

##実行方法
実行方法では、データベースの設定、ポートの設定、アプリケーションの実行方法について説明します。
### データベースの設定
TatsujinDaifugo/settings.pyで、データベースの設定を行います。以下はPostgreSQLにおける設定例です。
```python
DATABASES = {
    'default': {
        'ENGINE': 'postgresql+psycopg2',
        'NAME': 'xxxxx',
        'USER': 'xxxxx',
        'PASSWORD': 'xxxxx',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

設定が終わったら、以下のコマンドを実行して、データベースにテーブルを作成します。
```shell
$ cd models
```


### ポートの設定
TatsujinDaifugo/settings.pyで、アプリケーションを動作させるポートの設定を行います。以下が設定例です。
```python
define('port', default=8888, help="run on the given port", type=int)
```
設定例では、デフォルトのポート番号を8888にしています。それ以外にも、ポート番号は実行時に指定することもできます。

### アプリケーションの実行
アプリケーションは以下のコマンドで実行します。
```shell
$ python app.py
```
また、実行時にポート番号を指定することで、指定したポート番号でアプリケーションを実行することができます。
以下では、ポート番号に8000番を指定して実行しています。
```shell
$ python app.py --port=8000
```
アプリケーションをポート番号8888番で起動後、ブラウザで[http://127.0.0.1:8888/](http://127.0.0.1:8888/)にアクセスして
トップページが表示されることを確認します。


## 使い方
Coming Soon
