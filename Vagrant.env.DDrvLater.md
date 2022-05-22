- C ドライブ以外に収容していろいろとポータビリティや、システム圧迫を避けたいです(ハイ)という内容
    - ここ数年(2022年ごろ)はなくなったけど、Cドライブを128GByte(1000*1000GB計算)にしようっていうあの妙なこだわり仕様っていったい何なんだろ？
- 対応すること
    - vagrant はDドライブへ明示的にインストール
    - VirtualBoxはインストール後に立ち上げて、VBox収容パスをCドライブ以外に変更しておく
        - まさか、パスのつくり方の解説は不要とは思っている。
    - vagrantのワーク領域・お砂場はすべて、Cドライブ以外に
        - おススメはこうかな？
            - `` %AppData:C:={Drive letters other than C drive}:% ``

- その他
    - ${HomePath}/.vagrant.d も移動しないといけないことに気が付いた
    - bing|google : vagrant .vagrant.d windows
        - keyword's
            - vagrant box windows ローカル
            - vagrant box パス取得
            - vagrant box windows 格納パス
        - https://qastack.jp/programming/14733681/vagrant-d-outside-of-the-home-folder
            - memo : https://stackoverflow.com/programming/14733681/vagrant-d-outside-of-the-home-folder/23582609#23582609    
        - http://orca8.blogspot.com/2014/08/vagrantd.html
            - .vagrant.dフォルダの場所を変更する | orca8の備忘録


