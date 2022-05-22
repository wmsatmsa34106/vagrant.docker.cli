```
REM https://app.vagrantup.com/martyV/boxes/centos7/versions/0.2.9 ... CentOS7.9 ベースの模様

MKDIR D:\WORK\centos7_vagrant
PUSHD D:\WORK\centos7_vagrant & REM PUSHD なら一挙に移動できる
REM vagrant -v & REM Vagrant 2.2.19 など
vagrant init martyV/centos7
vagrant up
REM vagrant message.... ./win.vagrant.up.entos7.log.md
vagrant ssh
# 以降、vagrant のcentos7内部で
sudo yum -y upgrade
sudo yum -y update

- 
```