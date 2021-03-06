# vagrant_lamp

## 環境

接続IPアドレス：`192.168.33.11`

* CentOS 7
* PHP 7.2
  * Xdebug
* Composer
* PHPUnit
* FuelPHP(oilコマンド)
* Apache
* Git
* MySQL 5.6

## マウントしているディレクトリ

ホストOS：`../`
ゲストOS：`/mnt/project`

## その他設定

* 日本時間設定
* SELinuxを無効に
* ファイアウォールを無効に
* `php.ini`と`httpd.conf`は用意したものを使用。デフォルトのものは`/mnt/project/backup`にコピーしている。

## How to use

cloneしたら、ディレクトリ名をvagrantに変更
```bash
mv vagrant_lamp vagrant
```

vagrant-vbguestプラグインをインストールしていない場合のみ以下を行う
```bash
vagrant plugin install vagrant-vbguest
```

立ち上げ
```bash
vagrant up
```
※追記：上記で起動した際、ディレクトリのマウントの際エラーになってしまっています。
```bash
The error output from the command was:

/sbin/mount.vboxsf: mounting failed with the error: No such device
```

対処法：ゲストOSでyumをアップデートさせる必要があります。
```bash
vagrant ssh

[ゲストOS]$ sudo yum -y update
```

vagrantをリロード
```bash
vagrant reload
```

これで、うまくいくはずです。（このような面倒なことをしなくてもいいように改善策調べ中）


## 立ち上げ後の確認

動作確認のため、以下ファイルを作成してある。
* `http://192.168.33.11`にアクセス。phpinfoが表示できていることを確認
* `http://192.168.33.11/lesson/`にアクセス。hellolessonと表示されることを確認

## プロジェクト作成時は、ドキュメントルートにシンボリックリンクを張る

```bash
ln -fs /mnt/project/＜プロジェクト名＞ /var/www/html/＜プロジェクト名＞
```

FuelPHPの場合

```bash
ln -fs /mnt/project/＜プロジェクト名＞/public /var/www/html/＜プロジェクト名＞
```
