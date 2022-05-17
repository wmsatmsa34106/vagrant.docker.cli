- Windows10 以降の vagrant 環境のつくり方
    - base.VirtualBox
        - Windows の機能の有効化または無効化
        - hypervisor なWindows機能、次の３機能が有効の場合はすべて無効化
            1. Linux用Windowsサブシステム
            2. Hyperviser または、 Windows ハイパーバイザープラットフォーム
            3. 仮想マシンプラットフォーム
    - vagrant / win, virtualbox の組合せ . 2022.04頃
        - vagrant 2.2.19/ Windows10(Pro/ Home) /VirtualBox 6.1.14
            - VirtualBox : https://www.oracle.com/jp/virtualization/technologies/vm/downloads/virtualbox-downloads.html
                - Oracle.ja な VirtualBoxより取得が望ましい模様。
        - vagrant 2.2.19/ Windows11(Pro/ Home?) /VirtualBox 6.1.34
            - https://www.virtualbox.org/wiki/Downloads の『Windows hosts』リンクからゲットがおすすめな模様
                - 本家公式を取得が正しい模様。
    - その他
        - 適切な vagrant/ win/ virutalbox の組合せと、仮想系３機能全OFFなら vagrant plugin とかは特に選ぶことはなさそう。

- WSL2正式リリース以前のWindows10対応PCの場合は、WSL2利用のDockerよりHyperViserにした方が”幸せ”になれそう。
    - プリインストールが、Ver.21H1 とかまでのPCは無理臭い。
    - なんとなくストレージ（HDD・SSDのキャッシュなどの仕組みやバス企画や各種ファームなど）周りがWin11仕様でない場合はもれなくWSL２はあきらめた方が無難な使いかが出来そう。きっとBIOSとかファームをゴリゴリ書き換えられる”自作猛者”なら解決できるんじゃないかな（匙投げ）
    - 別にまとめる予定の、Dドライ項に構成したい場合もこっちの方が”筋”がよさそう
    - 新しもの付きで、QiitaでヤッホイなWSL２に試行錯誤していた１年半が何とも、、、（遠い目
        - きっと枯れた技術って素晴らしい★のだと思われる

- Windows10 以前
    - 気が向いたら