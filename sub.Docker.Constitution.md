
- post script memo
    - sudo dnf upgrade
    - sudo dnf update
    - sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    - sudo dnf install -y docker-ce docker-ce-cli containerd.io
    - sudo docker -v
    - sudo systemctl start docker
    - sudo systemctl enable docker
    - # docker commpose
    - sudo curl -L https://github.com/docker/compose/releases/download/v2.5.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    - sudo chmod +x /usr/local/bin/docker-compose
    - sudo su -
    - docker-compose -v

- dockerCompose HelloWorld
    - https://qiita.com/KEINOS/items/43d9415e351d80f78c8b
    - pushd /vagrant/wkwk/02
    - docker-compose up
    - docker-compose down
