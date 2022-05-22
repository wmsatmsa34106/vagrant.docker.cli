```CMD.EXE
MKDIR D:\WORK\centos8
PUSHD D:\WORK\centos8 & REM PUSHD なら一挙に移動できる
vagrant -v & REM Vagrant 2.2.19 など
vagrant box add generic/centos8 & REM https://pocketcode.net/virtualbox-vagrant-centos8 ,,, 2022Q2
vagrant box list & REM generic/centos8 (virtualbox, 3.6.14)
MKDIR share
vagrant init generic/centos8
git init
echo "# vagrant.docker.cli" >> README.md
git add README.md
git commit -m "1st. commit"
git checkout -b vagrant_work
git add Vagrantfile
git commit -m "vagrant init. , generic/centos8."
REM edit
git diff
|| diff --git a/Vagrantfile b/Vagrantfile
|| index db38691..e6e7ff0 100644
|| --- a/Vagrantfile
|| +++ b/Vagrantfile
|| @@ -32,7 +32,7 @@ Vagrant.configure("2") do |config|
|| 
||    # Create a private network, which allows host-only access to the machine
||    # using a specific IP.
|| -  # config.vm.network "private_network", ip: "192.168.33.10"
|| +  config.vm.network "private_network", ip: "192.168.33.13"
|| 
||    # Create a public network, which generally matched to bridged network.
||    # Bridged networks make the machine appear as another physical device on
|| @@ -43,7 +43,7 @@ Vagrant.configure("2") do |config|
||    # the path on the host to the actual folder. The second argument is
||    # the path on the guest to mount the folder. And the optional third
||    # argument is a set of non-required options.
|| -  # config.vm.synced_folder "../data", "/vagrant_data"
|| +  config.vm.synced_folder "./share", "/share"
vagrant up
REM vagrant message.... ./win.vagrant.up.entos8.log.md
vagrant ssh
# 以降、vagrant のcentos8内部で
sudo dnf -y upgrade
sudo dnf -y update
# Docker を dnfインストール構成していく todo task Dockerの"UserLand"化
# ./sub.docker.constitution.md
ls -al /share/wkwk/02; # この辺りに Hello DockerCompose を構成
```

