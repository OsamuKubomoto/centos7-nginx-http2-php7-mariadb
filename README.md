# centos7-nginx-http2-php7-mariadb

Vagrant�ŗ����グ��2���VM�ŁAansible���g���ăv���r�W���j���O����playbook�����܂����B

## �J����

VirtualBox5.0.14
Vagrant1.8.1

## VM�̍\��

* WEB�T�[�o�idev�j192.168.33.10
* ansible�T�[�o�iansible�j 192.168.33.20

### OS�ƃ~�h���E�F�A�̃o�[�W����

* centos 7.2
* nginx 1.9.10
* php 7.0.2
* mysql(mariadb) 5.6.28

## ����

/provision/group_vars/all��K�X�C�����Ă��������B

## �\�z�菇

���z�}�V���N��

    $ vagrant up
    $ vagrant reload

ansible�T�[�o�Ƀ��O�C��

    $ vagrant ssh ansible

ansible���C���X�g�[��

    $ sudo yum -y install epel-release ansible

ssh���쐬

    $ ssh-keygen -t rsa
    ������͑S���G���^�[��OK

�閧���Őڑ��ł���悤�ɂ���

    $ ssh-copy-id vagrant@192.168.0.1
    Are you sure you want to continue connecting (yes/no)? yes
    vagrant@192.168.0.1's password: vagrant

�a�ʊm�F

    $ ansible -i provision/hosts dev -m ping

## provision���s

���z�X�g�}�V���Ŏ��s

    $ vagrant ssh ansible -c "ansible-playbook -i provision/hosts provision/site.yml"

�e�o�[�W�������m�F

    $ vagrant ssh dev -c "nginx -v"
    nginx version: nginx/1.9.10

    $ vagrant ssh dev -c "php -v"
    PHP 7.0.2 (cli) (built: Jan  6 2016 15:25:31) ( NTS )
    Copyright (c) 1997-2015 The PHP Group
    Zend Engine v3.0.0, Copyright (c) 1998-2015 Zend Technologies
        with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2015, by Zend Technologies

    $ vagrant ssh dev -c "mysql --version"
    mysql  Ver 14.14 Distrib 5.6.28, for Linux (x86_64) using  EditLine wrapper

�u���E�U�Ŋm�F

    https://192.168.33.10

F12�Ń��X�|���X�w�b�_������΁uX-Firefox-Spdy: h2�v�ƂȂ��Ă���http2�ł��邱�Ƃ��m�F�ł��܂��B