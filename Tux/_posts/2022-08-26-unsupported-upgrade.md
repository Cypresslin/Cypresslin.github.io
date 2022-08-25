---
title:  "Linux 筆記 - 升級已不再支援的 Ubuntu 作業系統"
subtitle: ""
categories: []
---

# 升級已不再支援的 Ubuntu 作業系統
這是將一台機器上官方已經不再提供支援的 Ubuntu 作業系統升級過程的筆記，一段時間得做一次但太久沒弄就忘了，想想還是寫下來的好。
開始之前先講一下 Ubuntu 作業系統的命名規則跟生命週期吧。

## Ubuntu 作業系統的命名規則
Canonical 固定在每年的四月、十月也就是每半年會推出一版新的 Ubuntu 作業系統，版號就是當時的年份跟月份，例如 22.04 就是 2022 年 4 月所推出的版本。而版本名稱將會是英文形容詞 + 名詞的組合，例如 22.04 版本名稱為 Jammy Jellyfish，在下個版本將會按照 A-Z 的字母順序使用另一組名字：22.10 Kinetic Kudu

## Ubuntu 作業系統的生命週期
除了每兩年在四月推出的長期支援版本（Long-Term Support, LTS）如 20.04、22.04 至少都有五年的支援之外，其餘版本都只有九個月的生命週期。一旦時間到了它就是一個產品生命週期結束（End-Of-Life, EOL）的版本，Canonical 將不再提供更新。

這裡可以查到關於產品週期的說明：[The Ubuntu lifecycle and release cadence](https://ubuntu.com/about/release-cycle)

## 作業系統 EOL 了怎麼辦
當作業系統 EOL 了，此時電腦應該會通知你並且問你要不要升級（雖然還是可以繼續使用啦但個人不是很建議，主要是會拿不到最新的安全性更新，時間越久風險可能越高。）

## 透過命令列手動升級作業系統
除了透過圖形界面的 Software Updater 來進行升級之外，也可以用 `do-release-upgrade` 這個指令來升級作業系統，在開始前系統會要求你把所有能更新的套件先更新完：

    $ sudo do-release-upgrade
    Checking for a new Ubuntu release
    Please install all available updates for your release before upgrading.

這邊只要下 `sudo apt update && sudo apt dist-upgrade` 把該更新的東西更新一下後再次執行 `sudo do-release-upgrade` 即可。

官方所提供的升級教學：[Upgrade Ubuntu desktop](https://ubuntu.com/tutorials/upgrading-ubuntu-desktop#1-before-you-start)


但如果你的版本真的很舊，舊到差了兩個版本以上（以此例來說是要將作業系統從 21.04 升級，後面的 21.10 也已經 EOL 了所以是要直接升級到 22.04），那麼你可能會遇到有套件待更新但無法從線上套件庫下載的問題：

    $ sudo do-release-upgrade
    Checking for a new Ubuntu release
    Your Ubuntu release is not supported anymore.
    For upgrade information, please visit:
    http://www.ubuntu.com/releaseendoflife

    Please install all available updates for your release before upgrading.

    $ sudo apt dist-upgrade
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    Calculating upgrade... Done
    The following packages were automatically installed and are no longer required:
      libnvpair3linux libuutil3linux libzfs4linux libzpool4linux
    Use 'sudo apt autoremove' to remove them.
    The following packages will be upgraded:
      accountsservice alsa-ucm-conf apache2-dev bind9-dnsutils bind9-host bind9-libs busybox-initramfs busybox-static cloud-init command-not-found debootstrap icu-devtools libaccountsservice0 libasound2
      libasound2-data libcaca0 libicu-dev libicu67 libmysqlclient21 libnetplan0 libnss-mymachines libnss-systemd libnss3 libnvpair3linux libpam-systemd libpq5 libpulse0 libpython3.9 libpython3.9-dev
      libpython3.9-minimal libpython3.9-stdlib librados2 librbd1 libruby2.7 libsystemd0 libudev1 libuutil3linux libvirt-clients libvirt-daemon libvirt-daemon-config-network libvirt-daemon-config-nwfilter
      libvirt-daemon-driver-qemu libvirt-daemon-system libvirt-daemon-system-systemd libvirt0 libzfs4linux libzpool4linux lintian linux-base linux-libc-dev netplan.io openssh-client openssh-server
      openssh-sftp-server openssl python3-commandnotfound python3-lxml python3-pil python3-problem-report python3.9 python3.9-dev python3.9-minimal ruby2.7 sosreport systemd systemd-container systemd-sysv
      tzdata ubuntu-advantage-tools udev ufw update-notifier-common usrmerge vim vim-common vim-runtime vim-tiny xxd
    78 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
    44 standard security updates
    Need to get 70.5 MB/71.8 MB of archives.
    After this operation, 210 kB of additional disk space will be used.
    Do you want to continue? [Y/n] 
    Ign:1 http://ports.ubuntu.com/ubuntu-ports hirsute-updates/main s390x libsystemd0 s390x 247.3-3ubuntu3.7
    Ign:2 http://ports.ubuntu.com/ubuntu-ports hirsute-updates/main s390x libnss-systemd s390x 247.3-3ubuntu3.7
    Err:3 http://ports.ubuntu.com/ubuntu-ports hirsute-updates/main s390x libvirt-daemon s390x 7.0.0-2ubuntu2.2
      404  Not Found [IP: 185.125.190.39 80]
    Err:4 http://ports.ubuntu.com/ubuntu-ports hirsute-updates/main s390x libvirt-daemon-driver-qemu s390x 7.0.0-2ubuntu2.2
      404  Not Found [IP: 185.125.190.39 80]
    Err:5 http://ports.ubuntu.com/ubuntu-ports hirsute-updates/main s390x libvirt0 s390x 7.0.0-2ubuntu2.2
      404  Not Found [IP: 185.125.190.39 80]

這是因為這些套件都已經不在這台伺服器上了，請先手動更新 /etc/apt/source.list 的內容，把裡面出現的 http://archive.ubuntu.com/ubuntu 改成 http://old-releases.ubuntu.com/ubuntu/ 即可。只要改網址就好，其他像是 codename 那些不要動。

而因為我手邊這台機器是 s390x 架構的機器，所以它套件庫的網址也不大一樣，不過大同小異一樣是把：

    deb http://ports.ubuntu.com/ubuntu-ports/ hirsute main restricted
    deb-src http://ports.ubuntu.com/ubuntu-ports/ hirsute main restricted

改成：

    deb http://old-releases.ubuntu.com/ubuntu/ hirsute main restricted
    deb-src http://old-releases.ubuntu.com/ubuntu/ hirsute main restricted

改好後請跑一遍 `sudo apt update` 來更新套件清單，再跑 `sudo apt dist-upgrade` 即可安裝那些待更新的套件。搞定之後就可以跑 `sudo do-release-upgrade` 升級到最近一個有支援的版本囉！

如果你都有乖乖升級的話應該是不會遇到這個問題啦XD

Reference: [https://help.ubuntu.com/community/EOLUpgrade](https://help.ubuntu.com/community/EOLUpgrades)
