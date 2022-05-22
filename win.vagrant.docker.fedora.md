```CMD.EXE
MKDIR D:\WORK\fedora
PUSHD D:\WORK\fedora & REM PUSHD なら一挙に移動できる
vagrant -v & REM Vagrant 2.2.19 など
vagrant init fedora/36-cloud-base --box-version 36-20220504.1 & REM ./work.Fedra.md
REM vagrant box list & REM boxomatic/centos-stream-9 (virtualbox, 20220501.0.1)
MKDIR share
REM vagrant init boxomatic/centos-stream-9
git init
echo "# vagrant.docker.cli" >> README.md
git add README.md
git commit -m "1st. commit"
git checkout -b vagrant_work
git add Vagrantfile
git commit -m "vagrant init. , fedora/36-cloud-base."
REM edit
git diff
|| diff --git a/Vagrantfile b/Vagrantfile
|| index 0e7f4de..a2286d0 100644
|| --- a/Vagrantfile
|| +++ b/Vagrantfile
|| @@ -32,7 +32,7 @@ Vagrant.configure("2") do |config|
|| 
||    # Create a private network, which allows host-only access to the machine
||    # using a specific IP.
|| -  # config.vm.network "private_network", ip: "192.168.33.10"
|| +  config.vm.network "private_network", ip: "192.168.33.33"
|| 
||    # Create a public network, which generally matched to bridged network.
||    # Bridged networks make the machine appear as another physical device on
|| @@ -43,7 +43,7 @@ Vagrant.configure("2") do |config|
||    # the path on the host to the actual folder. The second argument is
||    # the path on the guest to mount the folder. And the optional third
||    # argument is a set of non-required options.
|| -  # config.vm.synced_folder "../data", "/vagrant_data"
|| +  config.vm.synced_folder "./share", "/share"
|| 
||    # Provider-specific configuration so you can fine-tune various
||    # backing providers for Vagrant. These expose provider-specific options.
vagrant up
REM vagrant message.... ./win.vagrant.up.entos9.log.md
vagrant box list & REM fedora/36-cloud-base      (virtualbox, 36-20220504.1)
vagrant ssh
# 以降、vagrant のcentos9内部で

bing|google : "Failed Units: 1 NetworkManager-wait-online.service fedora vagrant"
https://qiita.com/yunano/items/8636a6dd6becad84920d

[systemd]
Failed Units: 1
  NetworkManager-wait-online.service
[vagrant@fedora ~]$

sudo dnf -y upgrade
sudo dnf -y update
cat /etc/redhat-release; # Fedora release 36 (Thirty Six)
# Docker を dnfインストール構成していく todo task Dockerの"UserLand"化
# ./sub.Docker.Constitution.md より
ping download.docker.com
# sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
sudo dnf install -y docker-ce docker-ce-cli containerd.io
sudo docker -v
sudo systemctl start docker
sudo systemctl enable docker
sudo curl -L https://github.com/docker/compose/releases/download/v2.5.1/docker-compose-$(echo `uname -s` | tr '[:upper:]' '[:lower:]')-`uname -m` -o /usr/local/bin/docker-compose ; # 2022/05., 05/18 rel.update
sudo chmod +x /usr/local/bin/docker-compose
sudo su -

[vagrant@fedora ~]$ sudo su -
[systemd]
Failed Units: 1
  NetworkManager-wait-online.service

docker-compose -v
mkdir -p /share/wkwk/2
pushd /share/wkwk/2
# https://qiita.com/KEINOS/items/43d9415e351d80f78c8b
docker-compose up
docker-compose down

systemctl start NetworkManager-wait-online.service
exit

sudo su -
exit

sudo systemctl enable NetworkManager-wait-online.service
```
