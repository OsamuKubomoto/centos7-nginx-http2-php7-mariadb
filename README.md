# centos7-nginx-http2-php7-mariadb

Vagrantで立ち上げた2台のVMで、ansibleを使ってプロビジョニングするplaybookを作りました。

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
