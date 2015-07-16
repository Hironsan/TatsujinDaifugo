# Brain	Hacker
Brain Hackerは、Web上でブレインストーミングをするためのアプリケーションです。
匿名でブレインストーミングを行うことができるので、相手を気にせず、自由に意見を出すことができます。
また、褒める機能と思考支援機能を持つAIを搭載することで、楽しく、創造的なブレインストーミングを可能にします。

# 目次
- [動作環境](#動作環境)
- [インストール方法](#インストール方法)
- [実行方法](#実行方法)
- [使い方](#使い方)

##動作環境
動作環境は以下の通りです。
* OS: Windows 7 or Ubuntu 14.04
* 言語: Python 3.4
* DBMS: PostgreSQL 9.4

Brain_hacker/settings.pyを変更することで、MySQL等の使用も可能です。

##インストール方法
インストール方法では、アプリケーションの実行に必要なモジュールのインストール方法、
使用している外部APIキーの設定方法について説明します。

### モジュールのインストール
Brain Hackerを動作させるために必要なモジュールは以下のコマンドでインストールできます。
```shell
$ pip install -r requirements.txt
```

### 外部APIキーの設定
思考支援機能を使うためには、以下の2つのAPIキーが必要になります。
* [Yahoo キーフレーズ抽出](http://developer.yahoo.co.jp/webapi/jlp/keyphrase/v1/extract.html)
* [Docomo 固有表現抽出](https://dev.smt.docomo.ne.jp/?p=docs.api.page&api_name=language_analysis&p_name=api_2#tag01)

APIキーはそれぞれ、
* handlers/agent/keyword_extraction.py
* handlers/agent/named_entity_extraction.py
の中の、keyidに記述してください。


##実行方法
実行方法では、データベースの設定、ポートの設定、アプリケーションの実行方法について説明します。
### データベースの設定
Brain_Hacker/settings.pyで、データベースの設定を行います。以下はPostgreSQLにおける設定例です。
```python
DATABASES = {
    'default': {
        'ENGINE': 'postgresql+psycopg2',
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': '*****',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

設定が終わったら、以下のコマンドを実行して、データベースにテーブルを作成します。
```shell
$ cd models
$ python user.py
$ python group.py
$ python room.py
```


### ポートの設定
Brain_Hacker/settings.pyで、アプリケーションを動作させるポートの設定を行います。以下が設定例です。
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
### ユーザ登録 & ログイン
* トップページ

![LOGIN](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/01_BrainHacker_TopPage.GIF)

* ユーザ登録

SIGN UPボタンからユーザ登録を行うことができます(ユーザ名，メールアドレス，パスワードの入力が必要)

![SIGNUP](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/02_signup.png)

* ログイン

登録したユーザでログイン(ユーザ登録直後は自動で，その後は右上のLoginからログイン画面に飛べます)

![LOGIN](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/03_login.png)

### 「Groups」から「グループの作成」

* ログイン後のトップページ

右上がログインユーザ名になります

![LOGIN](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/04_after_login.png)

* Groups画面

![GROUPS](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/08group.png)

* グループの作成

グループの作成ボタンからグループを作成できます

![GROUPS](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/09_make_group.png)

グループ作成

![MAKE_GROUPS](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/make_group.png)

下のエリアに新しいグループが作成されます

* グループページ

グループ名をクリックすることでグループのグループページへ遷移します

![GROUP_INFO](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/10_groupinfo.png)

* メンバーの招待

グループページでメンバーボタンをクリックするとグループに所属するユーザ一覧が表示されます

ユーザ一覧内の右上のメンバーを追加するボタンから新しいメンバーを追加できます

![ADD_MEMBER](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/add_nemmember.png)

### 作成したグループ内で「部屋の作成」

* 部屋の作成

グループページの部屋ボタンから部屋を作成できるページに遷移できます

部屋の作成ボタンから部屋を作成できます

![ROOM_catalog](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/make_room.png)

部屋作成

![MAKE_ROOM](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/room.png)


### 作成した部屋でブレインストーミング

* 部屋に入る

部屋作成ページ内で作成した部屋の名前をクリックすることでブレインストーミングを行う部屋に入ることができます

![IN_ROOM](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/in_room.png)

* 付箋の追加・編集・削除

左下の＋をクリックすることでアイデアを書くための付箋を出すことができます

![ADD_STICKY](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/add_sticky.png)

付箋はダブルクリックで編集することができます

付箋にマウスオーバすると出てくる付箋右上の×ボタンで付箋を削除できます

付箋はドラッグ・ドロップで動かすことができます

これら付箋に対するアクションはすべてリアルタイムで同じ部屋にいる人たちに反映されます

* 匿名のチャット

右下のチャットボックスでテキストチャットを匿名で行うことができます

![CHAT](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/chat.png)

### 思考支援機能

* アイデアを褒める

付箋を編集したら左下に何か出てきました

![TAMA_HOMERU](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/tama1.png)

彼は我々のブレインストーミングを手助けしてくれる「たまにゃん」です

たまにゃんはアイデアを出すと褒めてくれます

また、自分からほかの人のアイデアを褒めることもできます

褒める方法は付箋にマウスオーバすると出てくるサムズアップをクリックです

![I_HOMERU](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/HOMERU.png)

* 発想の転換

たまにゃんは褒めること以外にも発想の転換を促してくれます

![TAMA_TENKAN](https://raw.github.com/wiki/Hironsan/Brain_Hacker/images/tama2.png)
