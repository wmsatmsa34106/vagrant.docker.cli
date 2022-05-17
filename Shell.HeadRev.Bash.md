- ざっと
```
PUSHD %AppData:C:=V:%\centos8\wkwk\BashAlpine
$ vagrant ssh
Last login: Sun May 15 11:00:37 2022 from 10.0.2.2
[vagrant@centos8 ~]$ sudo su -
Last login: Sun May 15 08:06:36 UTC 2022 on pts/0
[root@centos8 ~]# pushd /vagrant/wkwk/BashAlpine/
/vagrant/wkwk/BashAlpine ~
[root@centos8 BashAlpine]# docker-compose -f docker-compose.point_image.yml up -d
[root@centos8 BashAlpine]# docker-compose exec bash /innervagrant/1st.kick.bash
# defualt vagrant/vbox host/win mount path %AppData:C:=V:%\centos8\wkwk\BashAlpine
# bash.profile ini.,  1st. kick bat
# bash5.2b / 2022.05
```

- todo : to "UserLand Docker"
