
- post script memo
    - sudo dnf upgrade
    - sudo dnf update
    - # if "curl: (6) Couldn't resolve host.."
    - # https://qiita.com/bz0/items/7d4bac34c6cdada59b94
    - # sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
        - sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    - sudo dnf install -y docker-ce docker-ce-cli containerd.io
    - sudo docker -v
    - sudo systemctl start docker
    - sudo systemctl enable docker
    - # etc.
    - # https://docs.docker.com/engine/install/centos/
    - # http://docs.docker.jp/engine/installation/linux/docker-ce/centos.html#install-using-the-repository
    - # https://download.docker.com/linux/centos/
    - # docker commpose
    - sudo curl -L https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-$(echo `uname -s` | tr '[:upper:]' '[:lower:]')-`uname -m` -o /usr/local/bin/docker-compose ; # 2022/05., 06/04 rel.update
    - # https://github.com/docker/compose/releases/
    - sudo chmod +x /usr/local/bin/docker-compose
    - sudo su -
    - docker-compose -v

- dockerCompose HelloWorld
    - https://qiita.com/KEINOS/items/43d9415e351d80f78c8b
    - pushd /vagrant/wkwk/02
    - docker-compose up
    - docker-compose down
    - # 事前に、後続の最低限の Dockerの一般権限実行を対応
    - # vagrant user でも DockerCompose したい場合
    - ### google.com/search?q=sudo%3A+docker-compose%3A+command+not+found
    - # https://qiita.com/mtsiga/items/f90a3b8edd3ab58de376
    - sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
    - # 他
    - # https://kamihikouki.hatenablog.com/entry/2016/11/12/012345
    - # ただし、この設定だと "error message" が表示される状態なのでsudoする（未解決）
    - sudo docker-compose up
    - sudo docker-compose down
    - # error message.
     ```bash
      Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json?all=1&filters=%7B%22label%22%3A%7B%22com.docker.compose.project%3D02%22%3Atrue%7D%7D&limit=0": dial unix /var/run/docker.sock: connect: permission denied
     ```


- Docker を Vagrant ユーザで使いたい
    - # google.com/search?q=docker+centos8+wheel+root以外で実行
    - 多分本気でするにはこちら
        - https://docs.docker.jp/engine/security/rootless.html
        - https://access.redhat.com/documentation/ja-jp/red_hat_enterprise_linux/8/html-single/building_running_and_managing_containers/index
    - 簡易で、Wheelで権限を与える（k8sの構築も楽そう？<やっつけ>だと思う）
    - ## unskilled.site/dockerグループにユーザを登録してsudoなしでdockerコマンド/
    - cat /etc/group | grep docker
     ```bash
      docker:x:990:
     ```
    - cat /etc/group | grep vagrant
     ```bash
      vagrant:x:1000:
     ```
    - sudo usermod -aG docker vagrant

