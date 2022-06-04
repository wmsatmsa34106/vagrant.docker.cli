- ### google.com/search?q=kubernetes+centos8
- # 本気の設定はこちらだ（だと思う）
- # https://ja.linux-console.net/?p=871
- # https://qiita.com/yasubehe/items/51a05688d1f66d51531e ... 一部はこちらの設定流用
- ### 今回は、簡易にこう
- # https://genchan.net/it/virtualization/7595/
- # google.com/search?q=k8s+centos8+%2Fetc%2Fsysconfig%2Fkubelet
- # google.com/search?q=swapoff+centos8+起動時設定
- ### DockerDesktop の k8s と同様に物理１台に構成したい
- # google.com/search?q=kubernetes+centos8+一台構成
- # google.com/search?q=kubernetes+flannel
- sudo dnf -y update --nobest
```bash
 Last metadata expiration check: 0:14:20 ago on Sat 04 Jun 2022 01:46:50 AM UTC.
 Dependencies resolved.
 Nothing to do.
 Complete!
```
- sudo su -
```bash
sudo cat << EOF > /etc/sysconfig/kubelet
KUBELET_EXTRA_ARGS="--cgroup-driver=cgroupfs"
EOF

cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
        https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```
- exit
- cat /etc/sysconfig/kubelet
```bash
 KUBELET_EXTRA_ARGS="--cgroup-driver=cgroupfs"
```
- cat /etc/yum.repos.d/kubernetes.repo
```bash
 [kubernetes]
 name=Kubernetes
 baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
 enabled=1
 gpgcheck=1
 repo_gpgcheck=1
 gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
 exclude=kube*
```
- sudo swapoff -a
- sudo setenforce 0
- # swapoff のサービス反映
- # firewall 無効化
- 
- sudo dnf install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
- sudo systemctl enable kubelet
- sudo systemctl start kubelet
- 
- ### 本物の複数台構成の k8s ならこういう設定
- # https://qiita.com/ishida0503/items/427472f76fefc1e62b47
- 
- ### 一台で
- ### https://genzouw.com/entry/2020/01/25/001110/1905/
- ### # おまけ # https://garafu.blogspot.com/2019/06/build-k8s-single-master-cluster.html
- ### 参考資料
- ### # https://speakerdeck.com/hhiroshell/kubernetes-network-fundamentals-69d5c596-4b7d-43c0-aac8-8b0e5a633fc2?slide=34?title="整理しながら理解するKubernetesネットワークの仕組み / Kubernetes Network Fundamentals - Speaker Deck"
- kubeadm version
```json
 kubeadm version: &version.Info{Major:"1", Minor:"24", GitVersion:"v1.24.1", GitCommit:"3ddd0f45aa91e2f30c70734b175631bec5b5825a", GitTreeState:"clean", BuildDate:"2022-05-24T12:24:38Z", GoVersion:"go1.18.2", Compiler:"gc", Platform:"linux/amd64"}
```
- # https://none06.hatenadiary.org/entry/2022/05/28/025115

[vagrant@centos8 02]$ cat /proc/cpuinfo | grep processor
processor       : 0
processor       : 1
[vagrant@centos8 02]$ swapon -s
[vagrant@centos8 02]$ sudo swapoff -a
[vagrant@centos8 02]$ swapon -s
[vagrant@centos8 02]$ sudo cp -p /etc/fstab{,_`date +%Y%m%d`}
[vagrant@centos8 02]$ ls -l /etc/fstab*
-rw-r--r--. 1 root root 773 Jun  4 00:23 /etc/fstab
-rw-r--r--. 1 root root 773 Jun  4 00:23 /etc/fstab_20220604
[vagrant@centos8 02]$ sudo sed -i /swap/s/^/#/g /etc/fstab
[vagrant@centos8 02]$ diff /etc/fstab{,_`date +%Y%m%d`}
14c14
< #/dev/mapper/cl_centos8-swap none                    swap    defaults        0 0
---
> /dev/mapper/cl_centos8-swap none                    swap    defaults        0 0
[vagrant@centos8 02]$ uname -n
centos8.localdomain

 sudo dnf list -q kubelet kubeadm kubectl
Installed Packages
kubeadm.x86_64          1.24.1-0                 @kubernetes
kubectl.x86_64          1.24.1-0                 @kubernetes
kubelet.x86_64          1.24.1-0                 @kubernetes

### https://none06.hatenadiary.org/entry/2022/05/28/025115
### google.com/search?q=firewalld+is+active%2C+please+ensure+ports+%5B6443+10250%5D+are+open+or+your+cluster+may+not+function+correctly

[vagrant@centos8 02]$ sudo systemctl daemon-reload
[vagrant@centos8 02]$ sudo systemctl restart kubelet



