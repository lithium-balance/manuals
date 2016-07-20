Lubuntu
=======
`Lubuntu 16.04`を`LIVA MINI PC KIT (LIVA-C0-2G-64G-W)`にインストールして運用中。(2016/07/01現在)  
`Ubuntu`は重かった...


インストールしたもの
--------------------
* Atom
* Vivaldi
* XRDP
* rdesktop


### Atom ###
公式サイトから.debファイルをダウンロードしてインストール。


### Vivaldi ###
公式サイトからダウンロードしてインストール。


### XRDP ###
0.9.0をインストール。  
色々やっていたので、以下の手順があっているのかは不明。

#### インストール ####
以下の手順でインストールした。  
参考: https://xrdp.vmeta.jp/X11RDP-o-Matic

    cd ~
    mkdir tmp
    cd tmp
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install git
    git clone https://github.com/scarygliders/X11RDP-o-Matic.git
    cd X11RDP-o-Matic
    sudo ./X11rdp-o-matic.sh --justdoit

インストールが完了したかは、以下のコマンドにて確認。

    dpkg -l xrdp x11rdp

#### 描画設定 ####
以下の手順で描画設定をした。

    sudo ./RDPsesconfig.sh

#### アンインストール ####
まだ実施していないが、いつか実施するときのためのメモ。  
普通のパッケージと同様、以下のどちらかを実施すればよい。

    apt-get remove [hoge]
    apt-get --purge remove [hoge]

#### 起動不良を解決 ####
設定ファイルのパスがDebian系と合っていないので、修正。

`sudo vi /lib/systemd/system/xrdp.service`

    [Unit]
    Description=xrdp daemon
    Requires=xrdp-sesman.service
    After=syslog.target network.target xrdp-sesman.service
    
    [Service]
    Type=forking
    PIDFile=/var/run/xrdp.pid
    #EnvironmentFile=/etc/sysconfig/xrdp
    ExecStart=/usr/sbin/xrdp $XRDP_OPTIONS
    ExecStop=/usr/sbin/xrdp $XRDP_OPTIONS --kill
    
    [Install]
    WantedBy=multi-user.target

`sudo vi /lib/systemd/system/xrdp-sesman.service`

    [Unit]
    Description=xrdp session manager
    After=syslog.target network.target
    StopWhenUnneeded=true
    
    [Service]
    Type=forking
    PIDFile=/var/run/xrdp-sesman.pid
    #EnvironmentFile=/etc/sysconfig/xrdp
    ExecStart=/usr/sbin/xrdp-sesman $SESMAN_OPTIONS
    ExecStop=/usr/sbin/xrdp-sesman $SESMAN_OPTIONS --kill
    
    [Install]
    WantedBy=multi-user.target

上記の編集後、下記のコマンドを実行する。

    sudo systemctl daemon-reload
    sudo systemctl enable xrdp.service

rsakeys.iniがなぜか存在していなかったので作成

    sudo xrdp-keygen xrdp

#### 失敗した手順 ####
色々失敗した軌跡  
順不同  
何度も失敗した...

    sudo apt-get install xrdp xvfb lxde
    sudo apt-get install xrdp xvfb vnc4server lxde-common
    echo "lxsession -s LXDE -e LXDE" > .xsession
    sudo service xrdp restart
    sudo /etc/init.d/xrdp restart
    cd ~
    sudo apt-get install lxde
    echo "lxsession -s LXDE -e LXDE" > ~/.xsession
    echo "lxsession -s Lubuntu -e LXDE" > ~/.xsession

以下でリセットした

    sudo apt-get --purge remove xrdp xvfb vnc4server


### rdesktop ###
`apt-get install rdesktop` でインストール。


以下はまだ
----------
* Pandoc導入  
  `sudo apt-get install pandoc`  
  `markdown-preview-pandoc`パッケージをインストール
* samba導入

