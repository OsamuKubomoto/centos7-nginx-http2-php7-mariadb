# centos7-nginx-http2-php7-mariadb

Vagrantで立ち上げた2台のVMで、ansibleを使ってプロビジョニングするplaybookを作りました。

## 開発環境

VirtualBox5.0.14
Vagrant1.8.1

## VMの構成

* WEBサーバ（dev）192.168.33.10
* ansibleサーバ（ansible） 192.168.33.20

### OSとミドルウェアのバージョン

* centos 7.2
* nginx 1.9.10
* php 7.0.2
* mysql(mariadb) 5.6.28

## 準備

/provision/group_vars/allを適宜修正してください。

## 構築手順

仮想マシン起動

    $ vagrant up
    $ vagrant reload

ansibleサーバにログイン

    $ vagrant ssh ansible

ansibleをインストール

    $ sudo yum -y install epel-release ansible

ssh鍵作成

    $ ssh-keygen -t rsa
    ※質問は全部エンターでOK

秘密鍵で接続できるようにする

    $ ssh-copy-id vagrant@192.168.0.1
    Are you sure you want to continue connecting (yes/no)? yes
    vagrant@192.168.0.1's password: vagrant

疎通確認

    $ ansible -i provision/hosts dev -m ping

## provision実行

※ホストマシンで実行

    $ vagrant ssh ansible -c "ansible-playbook -i provision/hosts provision/site.yml"

各バージョンを確認

    $ vagrant ssh dev -c "nginx -v"
    nginx version: nginx/1.9.10

    $ vagrant ssh dev -c "php -v"
    PHP 7.0.2 (cli) (built: Jan  6 2016 15:25:31) ( NTS )
    Copyright (c) 1997-2015 The PHP Group
    Zend Engine v3.0.0, Copyright (c) 1998-2015 Zend Technologies
        with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2015, by Zend Technologies

    $ vagrant ssh dev -c "mysql --version"
    mysql  Ver 14.14 Distrib 5.6.28, for Linux (x86_64) using  EditLine wrapper

ブラウザで確認

    https://192.168.33.10

F12でレスポンスヘッダを見れば「X-Firefox-Spdy: h2」となっていてhttp2であることが確認できます。