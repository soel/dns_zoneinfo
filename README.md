dns_zoneinfo
============

## これは何?
bind の named.conf から zone 名を抽出し、一覧をファイルとして出力します
前回実行時と差分があった場合、差分をメールにて出力します

## 主な特徴
- cron で使用することで運用中の bind のコンフィグ状態を日々把握できます

## インストール
1. git clone
  ```bash
  git clone https://github.com/soel/dns_zoneinfo.git
  ```

## 使い方
1. zoneinfo.sh の編集
  以下を記述する
  HOST=hostname
  TYPE=slave or master
  CONF=name.conf の場所あるいは zone ファイルの場所
  UCBMAIL=/bin/mail
  TMP=/tmp
  STATEDIR=前回実行時の情報を残しておくディレクトリ
  NOTIFY="mailaddress"

  記入例
  ```bash
  HOST=dns01.example.com
  TYPE=master
  CONF=/var/named/chroot/var/etc/named.conf
  UCBMAIL=/bin/mail
  TMP=/tmp
  STATEDIR=/var/log/named/
  NOTIFY="soel@example.com"
  ```
1. 実行
  ```bash
  ./zoneinfo.sh
  ```

1. ファイル生成
  STATEDIR で指定したディレクトリへ zoneinfo というファイルが生成され、zone 名一覧が記述されています

## その他情報
- zoneinfo.sh を /etc/cron.daily へ置くことで毎日の情報を取得できます
- 抽出できる形式は
  ```bash
  zone "zone name" IN {
  ```
  の zone name に該当する部分です

## ライセンス
- LICENSE.txt をご覧ください
- MIT ライセンスです
