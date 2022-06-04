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

### 22'06/01 やっぱり壊れた、、、＜退避して再Box配置。。。原因追及用？

```CMD.EXE
vagrant box add generic/centos8
---
==> box: Loading metadata for box 'generic/centos8'
    box: URL: https://vagrantcloud.com/generic/centos8
This box can work with multiple providers! The providers that it
can work with are listed below. Please review the list and choose
the provider you will be working with.

1) docker
2) hyperv
3) libvirt
4) parallels
5) virtualbox
6) vmware_desktop

Enter your choice: 5
==> box: Adding box 'generic/centos8' (v4.0.2) for provider: virtualbox
    box: Downloading: https://vagrantcloud.com/generic/boxes/centos8/versions/4.0.2/providers/virtualbox.box
    box:
    box: Calculating and comparing box checksum...
==> box: Successfully added box 'generic/centos8' (v4.0.2) for 'virtualbox'!
---
vagrant up
---
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Checking if box 'generic/centos8' version '3.6.14' is up to date...
==> default: A newer version of the box 'generic/centos8' is available and already
==> default: installed, but your Vagrant machine is running against
==> default: version '3.6.14'. To update to version '4.0.2',
==> default: destroy and recreate your machine.
Your VM has become "inaccessible." Unfortunately, this is a critical error
with VirtualBox that Vagrant can not cleanly recover from. Please open VirtualBox
and clear out your inaccessible virtual machines or find a way to fix
them.
---
vagrant destroy
---
    default: Are you sure you want to destroy the 'default' VM? [y/N] y
Your VM has become "inaccessible." Unfortunately, this is a critical error
with VirtualBox that Vagrant can not cleanly recover from. Please open VirtualBox
and clear out your inaccessible virtual machines or find a way to fix
them.
---
# VirtualBox のダッシュボードで適切なVboxの構成を削除&整理

vagrant destroy
---
==> default: VM not created. Moving on...
---

vagrant up
---
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'generic/centos8'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'generic/centos8' version '4.0.2' is up to date...
==> default: Setting the name of the VM: centos8_default_1654302154682_70909
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 80 (guest) => 8888 (host) (adapter 1)
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default:
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Mounting shared folders...
    default: /vagrant => D:/WORK/centos8
==> default: Detected mount owner ID within mount options. (uid: 1000 guestpath: /vagrant)
==> default: Detected mount group ID within mount options. (gid: 1000 guestpath: /vagrant)
---

vagrant ssh
# 以降、vagrant のcentos8内部で
sudo dnf -y upgrade
sudo dnf -y update
# Docker を dnfインストール構成していく todo task Dockerの"UserLand"化
# ./sub.docker.constitution.md
ls -al /share/wkwk/02; # この辺りに Hello DockerCompose を構成

# k8s も使えるようにしよう
# ./sub.K8s.Constitution.md
```