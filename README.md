# centos7-nginx-http2-php7-mariadb

Vagrant�ŗ����グ��2���VM�ŁAansible���g���ăv���r�W���j���O����playbook�����܂����B

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
