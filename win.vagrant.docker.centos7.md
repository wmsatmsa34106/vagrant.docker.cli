```
REM https://app.vagrantup.com/martyV/boxes/centos7/versions/0.2.9 ... CentOS7.9 ベースの模様

MKDIR D:\WORK\centos7_vagrant
PUSHD D:\WORK\centos7_vagrant & REM PUSHD なら一挙に移動できる
REM vagrant -v & REM Vagrant 2.2.19 など
MKDIR data & REM デフォルト init 結果のパス
vagrant init martyV/centos7

git init

# 適切な差分

vagrant up
REM vagrant message.... ./win.vagrant.up.entos7.log.md
vagrant ssh
# 以降、vagrant のcentos7内部で
sudo yum -y upgrade
sudo yum -y update
# docker を使えるようにする
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install -y docker-ce docker-ce-cli containerd.io
sudo docker -v
sudo systemctl start docker
sudo systemctl enable docker
sudo curl -L https://github.com/docker/compose/releases/download/v2.5.1/docker-compose-$(echo `uname -s` | tr '[:upper:]' '[:lower:]')-`uname -m` -o /usr/local/bin/docker-compose ; # 2022/05., 05/18 rel.update
sudo chmod +x /usr/local/bin/docker-compose
sudo su -
docker-compose -v

# Hello.DockerCompose.world
mkdir -p /share/wkwk/2
pushd /share/wkwk/2
# https://qiita.com/KEINOS/items/43d9415e351d80f78c8b
curl -O https://keinos.github.io/hello-docker-compose/docker-compose.yml
docker-compose up
docker-compose down

- 
```