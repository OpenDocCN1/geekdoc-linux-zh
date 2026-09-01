
# Linux Mint 20 自助指南第二版：非官方且兼容所有 Linux Mint 20 版本

## 免责声明

书中的所有信息均按“原样”提供，不作任何保证。尽管在编写本书时已付出了无一的努力，但作者或出版者对因本书内容直接或间接导致或声称导致的任何损失或损害对任何个人或实体不承担任何责任。

书中的任何内容均非官方或赞助，且未获得商标所有者（无论开源还是闭源）的支持。

本书仅供客户的自我帮助和学习目的使用。

## 商标

书中出现了商标名称，例如 `Blizzard Battle.net`、`Microsoft`、`Youtube` 等，在书中使用这些名称无侵犯商标的意图，仅用于自我帮助或学习目的，并符合商标所有者的利益，已进行脱敏处理。

所有商标均归其各自所有者。

本书仅供购买者的自我帮助和学习目的使用。

书中的任何内容均非官方或赞助，且未获得商标所有者（无论开源还是闭源）的支持。

`Linux` 是 `Linus Torvalds` 在美国及其他国家的注册商标。

## 致谢

感谢我的家人，没有他们，这一切都不可能实现。

`Linus Torvalds` 是 `Linux` 的创建者和 `Linux` 商标的持有者，特此对此致谢，他并不支持或赞助本自我帮助类学习书。

`Linux®` 是 `Linus Torvalds` 在美国及其他国家的注册商标。

感谢 `Linux Mark Institute` 及社区开发并维护了 `Linux Mint`。

感谢 `Blizzard` 开发并发布了我真正喜爱并享受的《`World of Warcraft`》（魔兽世界）。

感谢 `WINE` 或 `Wine Is Not An Emulator` 兼容层。

感谢 `Lutris` 让安装和玩游戏及软件变得更加方便。

感谢 `Gabe Newell` 和 `Valve` 开发并发布了 `Steam Store`。

## 安装机器详情

本自我帮助学习指南的所有细节均已在裸机或直接在硬件上完成，而非虚拟机。

`Linux Mint 20.03` 的安装在一个手动分区的驱动上完成，配置如下：

- 53 GB 用于 `/` 或根分区

- 20 GB 用于交换分区 (`swap`)

- 我使用了来自 `Ubuntu 20.04.03 LTS` 安装的现有 `EFI` 分区

安装 `Linux Mint 20.03` 的电脑配置为：

- CPU：`Intel(R)Core(TM) i3-9100F CPU`

- 内存：16GB DDR4

- 主板：`MSI B365M PRO-VH REV 1.0`

- GPU 或显卡：`MSI Nvidia 1060 GTX 6GB`

- 显示器：`24" HP 24o Monitor`

- SSD：1618 GB，涵盖 `Samsung`、`PNY` 和 `SPCC` 硬盘

- 内部 HDD：9TB，涵盖 2 个 `Western Digital` 硬盘

- 外部 HDD：1TB `JMicron`

- 声卡：`USB 3.0 External Phoinkas Soundcard`

- 扬声器：`Amazon Basics 2.0 Speakers`

- 耳机：`Generic 2.0 Earphones`

- 耳机：`Kingston HyperX Cloud Alpha 3.5 MM`

- 键盘 1 & 2：`USB 2.0 Generic Mini Gaming Keyboard`、`USB 2.0 Basic Full Sized Keyboard`

- 鼠标：`USB 2.0 HP Wireless Mouse X200`、`USB 2.0 Basic Wired Mouse`

- 网络：`USB 3.0 Realtek Gigabit Adapter`、`Realtek Motherboard Gigabit PCI Port`

- 手机：`Samsung Smartphone`

- USB 集线器：`USB 3.0 External Phoinkas Soundcard`

- 打印机：`Epson Network Printer`

## 引言

本指南旨在作为 `Linux Mint 20.03` 的自我帮助指南。

为了增加您的安全性，您需要 `ENTER` 密码以完成此列表中的大多数步骤，因此请确保手头有密码。

在输入所有 `sudo` 命令和您的密码后，您可能需要按 `ENTER` 继续或按 `ESC` 取消。

请确保每天几天或根据您的意愿更新并升级您的 `Linux Mint 20.03`，以确保安全性和稳定性。

切勿使用 `sudo apt auto remove`，因为它可能会导致 `Linux Mint 20.03` 不稳定或损坏。

你应该按照说明输入内容以助于记忆，但如果您愿意，也可以复制和粘贴。

在下载 `.deb`、`.appimage`、`.jar`、`.targz`、`.taxxz` 等文件时，确保点击 `Keep`（保留）或 `Save File`（保存文件）。

## 关于作者

## 参考文献

### 音频编辑器

#### Ardour

`Ardour`

`Audacity`

`Kwave`

![](img/image00747.jpeg)

打开：软件管理器

输入或复制粘贴：

`ardour`

点击：`Ardour`

![](img/image00748.jpeg)

点击：安装

![](img/image00749.jpeg)

打开：终端

输入或复制粘贴：

```bash
sudo apt install ardour
```

按下：`ENTER`

#### Audacity

`Audacity`

![](img/image00750.jpeg)

打开：软件管理器

输入或复制粘贴：

`audacity`

点击：`Audacity`

![](img/image00751.jpeg)

点击：安装

![](img/image00752.jpeg)

打开：终端

输入或复制粘贴：

```bash
sudo apt install audacity
```

![](img/image00753.jpeg)

打开：Snap Store

输入或复制粘贴：

`audacity`

点击：`Audacity`

![](img/image00754.jpeg)

点击：安装

![](img/image00755.jpeg)

打开：终端

输入或复制粘贴：

```bash
sudo snap install audacity
```

按下：`ENTER`

#### Kwave

`Kwave`

![](img/image00756.jpeg)

打开：软件管理器

输入或复制粘贴：

`kwave`

点击：`Kwave`

![](img/image00757.jpeg)

##### Kwave

点击：安装

![](img/image00758.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install kwave
```

按下：`ENTER`

![](img/image00759.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
kwave
```

点击：`kwave`

![](img/image00760.jpeg)

点击：安装

![](img/image00761.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install kwave
```

按下：`ENTER`

### 云端备份

- `Insync`

- `overGrive`

#### Insync

![](img/image00762.jpeg)

前往：[`www.insynchq.com/downloads`](https://www.insynchq.com/downloads)

点击：安装程序（Installers）下方的框

点击：`Linux Mint`

点击：安装程序与包（Installers and Packages）下方的框

点击：`20.x`

点击：下载

保存至：`insync_3.7.1.50307-focal_amd64.deb`

前往：`insync_3.7.1.50307-focal_amd64.deb` 的下载路径

双击：`insync_3.7.1.50307-focal_amd64.deb`

![](img/image00763.jpeg)

点击：安装包

#### overGrive

![](img/image00764.jpeg)

前往：[`www.thefanclub.co.za/overgrive`](https://www.thefanclub.co.za/overgrive)

点击：`overGrive 3.3.13 - Debian|Ubuntu|Mint`

前往：下载 `overgrive_3.3.13_all.deb`

前往：`overgrive_3.3.13_all.deb` 的下载路径

双击：`overgrive_3.3.13_all.deb`

![](img/image00765.jpeg)

点击：安装包

### 云端办公套件

- `Google Docs`

- `Microsoft Office 365`

- `Zoho Docs`

#### Google Docs

![](img/image00766.jpeg)

打开：`Firefox`

前往：[`www.google.co.uk/docs/about/`](https://www.google.co.uk/docs/about/)

登录访问 Google Docs

#### Microsoft Office 365

![](img/image00767.jpeg)

打开：`Firefox`

前往：[`www.office.com/`](https://www.office.com/)

登录访问

#### Zoho Docs

![](img/image00768.jpeg)

打开：`Firefox`

前往：[`www.zoho.com/docs/`](https://www.zoho.com/docs/)

登录访问

### 通讯工具

- `Discord`

- `Pidgin`

- `Telegram`

#### Discord

![](img/image00769.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
discord
```

点击：`Discord`

![](img/image00770.jpeg)

点击：安装

![](img/image00771.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install discord
```

按下：`ENTER`

#### Pidgin

![](img/image00772.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
pidgin
```

点击：`Pidgin`

![](img/image00773.jpeg)

点击：安装

![](img/image00774.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install pidgin
```

按下：`ENTER`

#### Telegram

![](img/image00775.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
telegram
```

点击：`telegram-desktop`

![](img/image00776.jpeg)

点击：安装

![](img/image00777.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install telegram-desktop
```

按下：`ENTER`

### 兼容层

- `Anbox`

- `WINE Staging`

#### Anbox

![](img/image00778.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install --devmode --beta anbox
```

按下：`ENTER`

![](img/image00779.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap refresh --beta --devmode anbox
```

按下：`ENTER`

前往：更新 `Anbox`

#### WINE Staging

![](img/image00780.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo dpkg --add-architecture i386
```

按下：`ENTER`

![](img/image00781.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt update
```

按下：`ENTER`

![](img/image00782.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
wget -qO- https://dl.winehq.org/wine-builds/winehq.key | sudo apt-key add -
```

按下：`ENTER`

![](img/image00783.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt-add-repository 'deb http://dl.winehq.org/wine-builds/ubuntu bionic main'
```

按下：`ENTER`

![](img/image00784.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt update
sudo apt install --installcommends winehq-staging
```

按下：`ENTER`

### 加密货币钱包

- `Bitcoin-Core`

- `Coin Wallet`

- `Electrum`

#### Bitcoin-Core / Coin Wallet

![](img/image00786.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
bitcoin-core
```

点击：`bitcoin-core`

![](img/image00787.jpeg)

点击：安装

##### Coin Wallet（检查流程）

![](img/image00789.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
coin-wallet
```

点击：`Coin Wallet`

![](img/image00790.jpeg)

点击：安装

![](img/image00791.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install coin-wallet
```

#### Electrum

![](img/image00792.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
electrum
```

点击：`electrum`

![](img/image00793.jpeg)

点击：安装

![](img/image00794.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install electrum
```

### 数据恢复

- `R-Linux`

#### R-Linux

![](img/image00795.jpeg)

前往：[`www.r-studio.com/free-linux-recovery/shtml`](https://www.r-studio.com/free-linux-recovery/shtml)

点击：下载 Debian/Ubuntu 平台同行的 `R-Linux` (64 位)

保存至：`RLinux5_x64.deb`

前往：`RLinux5_x64.deb` 的下载路径

双击：`RLinux5_x64.deb`

![](img/image00796.jpeg)

点击：安装包

### 桌面环境

- `Cinnamon`

- `Gnome`

- `KDE Plasma`

- `Ubuntu Desktop`

#### Cinnamon

![](img/image00797.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install cinnamon
```

按下：`ENTER`

#### Gnome

![](img/image00798.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install gnome
```

按下：`ENTER`

#### KDE Plasma

![](img/image00799.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo add-apt-repository ppa:kubuntu-ppa/backports
```

按下：`ENTER`

![](img/image00784.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt update
sudo apt install kde-plasma-desktop
```

##### Tasksel (Ubuntu Desktop)

![](img/image0800.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install tasksel
```

按下：`ENTER`

![](img/image0801.jpeg)

打开：`Terminal`

输入或复制粘贴：



```bash
sudo tasksel
```

按下：`ENTER`

使用上下方向键导航到 Ubuntu desktop。

按下：`Space` 选择 `Ubuntu desktop`。

按下：`TAB` 直到选中 OK。

按下：`ENTER`

## 下载管理器

- `FireDM`
- `KGet`
- `uGet`

### FireDM

![](img/image0804.jpeg)

前往：[`github.com/firedm/FireDM/releases`](https://github.com/firedm/FireDM/releases)

点击：`FireDM-2022.2.5-x86_64.AppImage`

保存至：`FireDM-2022.2.5-x86_64.AppImage`

前往：`FireDM-2022.2.5-x86_64.AppImage` 的下载路径。

双击：`FireDM-2022.2.5-x86_64.AppImage`

![](img/image0805.jpeg)

集成并运行。

### KGet

![](img/image0806.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
kget
```

点击：`Kget`

![](img/image0807.jpeg)

点击：安装。

![](img/image0808.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install kget
```

### uGet

![](img/image0809.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
uget
```

点击：`Uget`

![](img/image0810.jpeg)

点击：安装。

![](img/image0811.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
uget
```

点击：`uget`

![](img/image0812.jpeg)

点击：安装。

![](img/image0813.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install uget
```

## 电子书阅读器

- `Calibre`
- `Fbreader`
- `Lucidor`

### Calibre

![](img/image0815.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
calibre
```

点击：`Calibre`

![](img/image0816.jpeg)

点击：安装。

![](img/image0817.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install calibre
```

```bash
sudo apt install imagemagick imagemagick-6-common imagemagick-6.q16 javascript-common libchm1 libjpeg-turbo-progs libjs-jquery libjs-sphinxdoc libjs-underscore libjxr-tools libjxr0 liblqr-1-0 libmagickcore-6.q16-6 libmagickcore-6.q16-6-extra libmagickwand-6.q16-6 libminizip1 libnetpbm10 libpodofo0.9.6 libqt5designer5 libqt5help5 libqt5positioning5 libqt5printsupport5 libqt5qml5 libqt5quick5 libqt5quickwidgets5 libqt5sql5 libqt5sql5-sqlite libqt5test5 libqt5webchannel5 libqt5webengine-data libqt5webengine5 libqt5webenginecore5 libqt5webenginewidgets5 libqt5xml5 libre2-5 netpbm optipng python3-apsw python3-chm python3-css-parser python3-cssselect python3-cssutils python3-dnspython python3-feedparser python3-html2text python3-html5-parser python3-html5lib python3-lxml python3-markdown python3-mechanize python3-msgpack python3-nose python3-pygments python3-pyqt5 python3-pyqt5.qtsvg python3-pyqt5.qtwebchannel python3-pyqt5.qtwebengine python3-regex python3-repoze.lru python3-routes python3-sip python3-webob python3-zeroconf
```

按下：`ENTER`

![](img/image00819.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin
```

按下：`ENTER`

## Fbreader

![](img/image00820.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
fbreader
```

点击：`Fbreader`

![](img/image00821.jpeg)

点击：`Install`

![](img/image00822.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install fbreader
```

按下：`ENTER`

![](img/image00823.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
fbreader
```

点击：`FBReader 2.0`

![](img/image00824.jpeg)

点击：`Install`

![](img/image00825.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install fbreader
```

按下：`ENTER`

## Lucidor

![](img/image00826.jpeg)

前往：[`lucidor.org/lucidor/download.php`](http://lucidor.org/lucidor/download.php)

点击下载 deb 包：`lucidor_0.9.15-1_all.deb`

下载：`lucidor_0.9.15-1_all.deb`

前往：`lucidor_0.9.15-1_all.deb` 的下载位置。

双击：`lucidor_0.9.15-1_all.deb`

![](img/image00827.jpeg)

点击：`Install Package`

## Elder Gaming、Dosbox、ResidualVM、ScummVM

### Dosbox

![](img/image00828.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
dosbox
```

点击：`Dosbox`

![](img/image00829.jpeg)

点击：`Install`

![](img/image00830.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install dosbox
```

按下：`ENTER`

![](img/image00831.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
dosbox
```

点击：`DOSBox Staging`

![](img/image00832.jpeg)

点击：`Install`

![](img/image00833.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install dosbox-staging
```

按下：`ENTER`

### ResidualVM

![](img/image00834.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
residualvm
```

点击：`Residualvm`

![](img/image00835.jpeg)

点击：`Install`

![](img/image00836.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install residualvm
```

按下：`ENTER`

![](img/image00837.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
residualvm
```

点击：`ResidualVM`

点击：`Install`

![](img/image00839.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install residualvm
```

按下：`ENTER`

### ScummVM

![](img/image00840.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
scummvm
```

点击：`Scummvm`

![](img/image00841.jpeg)

点击：`Install`

![](img/image00842.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install scummvm
```

按下：`ENTER`

![](img/image00843.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
scummvm
```

点击：`ScummVM`

![](img/image00844.jpeg)

点击：`Install`

![](img/image00845.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install scummvm
```

按下：`ENTER`

## 文件压缩与解压

### Engrampa / PeaZip

![](img/image00846.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
engrampa
```

点击：`Engrampa`

![](img/image00847.jpeg)

点击：`Install`

![](img/image00848.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install engrampa
```

按下：`ENTER`

![](img/image00849.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
p7zip-desktop
```

点击：`P7Zip - Desktop`

![](img/image00850.jpeg)

点击：`Install`

![](img/image00851.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install p7zip-desktop
```

按下：`ENTER`

### PeaZip（手动安装）

![](img/image00852.jpeg)

前往：[`peazip.github.io/peazip-linux.html`](https://peazip.github.io/peazip-linux.html)

点击：`DEB GTK2`

下载：`peazip_8.4.0.LINUX-GTK2-1_amd64.deb`

前往：`peazip_8.4.0.LINUX-GTK2-1_amd64.deb` 的下载位置。

双击：`peazip_8.4.0.LINUX-GTK2-1_amd64.deb`

![](img/image00853.jpeg)

点击：`Install Package`

## 编辑器

### Blender

![](img/image00854.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
blender
```

点击：`Blender`

![](img/image00855.jpeg)

点击：`Install`

![](img/image00856.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install blender
```

按下：`ENTER`

![](img/image00857.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
blender
```

点击：`Install`

### GIMP / GNU Image Manipulation Program

![](img/image00860.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
gimp
```

点击：`Gimp`

![](img/image00861.jpeg)

点击：`Install`

![](img/image00862.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install gimp
```

按下：`ENTER`

![](img/image00863.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
gimp
```

点击：`GNU Image Manipulation Program`

![](img/image00864.jpeg)

点击：`Install`

![](img/image00865.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install gimp
```

按下：`ENTER`

### Krita

![](img/image00866.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
krita
```

点击：`Krita`

![](img/image00867.jpeg)

点击：`Install`

![](img/image00868.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install krita
```

按下：`ENTER`

![](img/image00869.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
krita
```

点击：`Krita`

![](img/image00870.jpeg)

点击：`Install`

![](img/image00871.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install krita
```

按下：`ENTER`

### Pinta

![](img/image00872.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
pinta
```

点击：`Pinta`

![](img/image00873.jpeg)

点击：`Install`

![](img/image00874.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install pinta
```

按下：`ENTER`

![](img/image00875.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
pinta
```

点击：`Pinta`

![](img/image00876.jpeg)

点击：`Install`

![](img/image00877.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install pinta
```

按下：`ENTER`

### Inkscape

![](img/image00878.jpeg)

打开：`Software Manager`

输入或复制粘贴：

```bash
inkscape
```

点击：`Inkscape`

![](img/image00879.jpeg)

点击：`Install`

![](img/image00880.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install inkscape
```

按下：`ENTER`

![](img/image00881.jpeg)

打开：`Snap Store`

输入或复制粘贴：

```bash
inkscape
```

点击：`Inkscape`

![](img/image00882.jpeg)

点击：`Install`

## 视频直播

- `OBS Studio`

### OBS Studio

![](img/image00884.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install ffmpeg
```

按下：`ENTER`



```bash
sudo apt install ffmpeg
```

按下：`ENTER`

![](img/image00887.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install obs-studio
```

按下：`ENTER`

![](img/image00884.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install ffmpeg
```

按下：`ENTER`

![](img/image00888.jpeg)

打开：`Software Manager`

输入或复制粘贴：

`obs studio`

点击：`Obs-studio`

![](img/image00889.jpeg)

点击：`Install`

![](img/image00884.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install ffmpeg
```

按下：`ENTER`

![](img/image00890.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install obs-studio
```

按下：`ENTER`

## 媒体播放器

*   Parole
*   SMPlayer
*   VLC

### Parole

![](img/image00891.jpeg)

打开：`Software Manager`

输入或复制粘贴：

`parole`

点击：`Parole`

![](img/image00892.jpeg)

点击：`Install`

![](img/image00893.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install parole
```

按下：`ENTER`

### SMPlayer

![](img/image00894.jpeg)

打开：`Software Manager`

输入或复制粘贴：

`smplayer`

点击：`Smplayer`

![](img/image00895.jpeg)

点击：`Install`

![](img/image00896.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install smplayer
```

按下：`ENTER`

### VLC

![](img/image00897.jpeg)

打开：`Software Manager`

输入或复制粘贴：

`vlc`

点击：`VLC`

![](img/image00898.jpeg)

点击：`Install`

![](img/image00899.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install vlc
```

按下：`ENTER`

![](img/image00900.jpeg)

打开：`Snap Store`

输入或复制粘贴：

`vlc`

点击：`VLC`

![](img/image00901.jpeg)

点击：`Install`

![](img/image00902.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install vlc
```

按下：`ENTER`

## 现代游戏

*   Blizzard Battle.net
*   Lutris
*   Proton-QT
*   Steam
*   WINE

### Blizzard Battle.net

![](img/image00903.jpeg)

打开：`Lutris`

点击：`Community Installers`

点击：`Search Bar`

输入或复制粘贴：

`blizzard battle.net`

选择：`Blizzard Battle.net`

点击：`Install`

![](img/image00904.jpeg)

点击：`Install`

![](img/image00905.jpeg)

点击：`Install`

![](img/image00906.jpeg)

等待文件下载

![](img/image00907.jpeg)

点击：`Continue`

![](img/image00908.jpeg)

点击：`Install`

![](img/image00909.jpeg)

点击：`Create desktop shortcut`

点击：`Create application menu shortcut`

点击：`Close`

### Lutris

![](img/image00910.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo add-apt-repository ppa:lutris-team/lutris
```

按下：`ENTER`

![](img/image00784.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt update
```

按下：`ENTER`

![](img/image00911.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install lutris
```

按下：`ENTER`

### Proton-QT

![](img/image00912.jpeg)

前往：[`github.com/DavidoTek/ProtonUp-Qt/releases/tag/v2.5.0`](https://github.com/DavidoTek/ProtonUp-Qt/releases/tag/v2.5.0)

点击：`ProtonUp-Qt-2.5.0-x86_64.AppImage`

保存至：`ProtonUp-Qt-2.5.0-x86_64.AppImage`

前往：`ProtonUp-Qt-2.5.0-x86_64.AppImage` 下载所在

双击：`ProtonUp-Qt-2.5.0-x86_64.AppImage`

![](img/image00913.jpeg)

点击：`Integrate and run`

### Steam

![](img/image00914.jpeg)

打开：`Software Manager`

输入或复制粘贴：

`steam`

点击：`Steam`

![](img/image00915.jpeg)

点击：`Install`

![](img/image00916.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install steam
```

按下：`ENTER`

### WINE

![](img/image00780.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo dpkg --add-architecture i386
```

按下：`ENTER`

![](img/image00781.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt update
```

按下：`ENTER`

![](img/image00782.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
wget -qO -://dl.winehq.org/wine-builds/winehq.key | sudo apt-key add -
```

按下：`ENTER`

![](img/image00783.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt-add-repository 'deb http://dl.winehq.org/wine-builds/ubuntu/ bionic main'
```

按下：`ENTER`

![](img/image00784.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt update
```

按下：`ENTER`

![](img/image00785.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt-get install --install-recommends winehq-staging
```

按下：`ENTER`

## 点播

*   Amazon Music Unlimited
*   Apple Music
*   Spotify Client
*   Spotify
*   Tidal
*   Youtube Music

### Amazon Music

![](img/image00917.jpeg)

前往：[`www.amazon.com/music`](https://www.amazon.com/music)

### Apple Music

![](img/image00918.jpeg)

前往：[`music.apple.com`](https://music.apple.com)

### Spotify Client

![](img/image00919.jpeg)

前往：[`www.spotify.com`](https://www.spotify.com)

### Spotify

![](img/image00920.jpeg)

前往：[`www.spotify.com`](https://www.spotify.com)

### Tidal

![](img/image00921.jpeg)

前往：[`www.tidal.com`](https://www.tidal.com)

### Youtube Music

![](img/image00922.jpeg)

前往：[`music.youtube.com`](https://music.youtube.com)

## 音乐播放器

*   Audacious
*   Clementine

### Audacious

![](img/image00923.jpeg)

打开：`Software Manager`

输入或复制粘贴：

`audacious`

点击：`Audacious`

![](img/image00924.jpeg)

点击：`Install`

![](img/image00925.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install audacious
```

按下：`ENTER`

### Clementine

![](img/image00926.jpeg)

打开：`Software Manager`

输入或复制粘贴：

`clementine`

点击：`Clementine`

![](img/image00927.jpeg)

点击：`Install`

![](img/image00928.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install clementine
```

按下：`ENTER`

## 办公套件

*   LibreOffice
*   ONLYOFFICE Desktop Editors
*   OpenOffice
*   SoftMaker FreeOffice
*   WPS Office

### LibreOffice

![](img/image00929.jpeg)

打开：`Software Manager`

输入或复制粘贴：

`libreoffice`

点击：`LibreOffice`

![](img/image00930.jpeg)

点击：`Install`

![](img/image00931.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install libreoffice
```

按下：`ENTER`

![](img/image00932.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo add-apt-repository ppa:libreoffice/ppa
```

按下：`ENTER`

![](img/image00933.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt update
```

按下：`ENTER`

![](img/image00934.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt upgrade
```

按下：`ENTER`

### ONLYOFFICE Desktop Editors

![](img/image00935.jpeg)

打开：`Snap Store`

输入或复制粘贴：

`onlyoffice`

点击：`ONLYOFFICE Desktop Editors`

![](img/image00936.jpeg)

点击：`Install`

![](img/image00937.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install onlyoffice-desktopeditors
```

按下：`ENTER`

![](img/image00938.jpeg)

前往：[`www.onlyoffice.com/en/download-desktop.aspx?from=desktop`](https://www.onlyoffice.com/en/download-desktop.aspx?from=desktop)

点击：`DOWNLOAD DEB under Debian 8, Ubuntu 14.04 and higher`

保存至：`onlyoffice-desktopeditors_amd64.deb`

前往：`onlyoffice-desktopeditors_amd64.deb` 下载所在

双击：`onlyoffice-desktopeditors_amd64.deb`

![](img/image00939.jpeg)

点击：`Install Package`

### OpenOffice

![](img/image00940.jpeg)

前往：

链接：[`apprepo.de/appimage/openoffice`](https://apprepo.de/appimage/openoffice)

- 点击：`DOWNLOAD`
- 下载：下载 `OpenOffice.AppImage`
- 前往：`OpenOffice.AppImage` 的下载位置
- 双击：`OpenOffice.AppImage`

![](img/image00948.jpeg)

- 点击：`Integrate and run`

### SoftMaker FreeOffice

![](img/image00949.jpeg)

- 前往：[`www.freeoffice.com/en/download/applications`](https://www.freeoffice.com/en/download/applications)
- 点击：`Download Under Linux`
- 点击：基于 DEB 的系统的 `.deb` 包
- 下载：下载 `softmaker-freeoffice-2021_1042-01_amd64.deb`
- 前往：`softmaker-freeoffice-2021_1042-01_amd64.deb` 的下载位置
- 双击：`softmaker-freeoffice-2021_1042-01_amd64.deb`

![](img/image00950.jpeg)

- 点击：`Install Package`

### WPS Office

![](img/image00951.jpeg)

- 前往：[`www.wps.com/`](https://www.wps.com/)
- 点击：`Free Download`
- 点击：`Deb Package`
- 下载：下载 `wps-office_11.1.0.10920.XA_amd64.deb`
- 前往：`wps-office_11.1.0.10920.XA_amd64.deb` 的下载位置
- 双击：`wps-office_11.1.0.10920.XA_amd64.deb`

![](img/image00952.jpeg)

- 点击：`Install Package`

## PDF 阅读器

### Evince

- Okular

### Evince

![](img/image00953.jpeg)

- 打开：`Software Manager`
- 输入或复制粘贴：`evince`
- 点击：`Evince`

![](img/image00954.jpeg)

- 点击：`Install`

![](img/image00955.jpeg)

- 打开：`Terminal`
- 输入或复制粘贴：

```bash
sudo apt install evince
```

- 按回：`ENTER`

![](img/image00956.jpeg)

- 打开：`Snap Store`
- 输入或复制粘贴：`evince`
- 点击：`Evince`

![](img/image00957.jpeg)

- 点击：`Install`

![](img/image00958.jpeg)

- 打开：`Terminal`
- 输入或复制粘贴：

```bash
sudo snap install evince
```

- 按回：`ENTER`

### Okular

![](img/image00959.jpeg)

- 打开：`Software Manager`
- 输入或复制粘贴：`okular`



- 点击：`Okular`

![](img/image00960.jpeg)

- 点击：`Install`

![](img/image00961.jpeg)

- 打开：`Terminal`

- 输入或复制粘贴：

```bash
sudo apt install okular
```

- 按回：`ENTER`

![](img/image00962.jpeg)

- 打开：`Snap Store`

- 输入或复制粘贴：`okular`

- 点击：`Okular`

![](img/image00963.jpeg)

- 点击：`Install`

![](img/image00964.jpeg)

- 打开：`Terminal`

- 输入或复制粘贴：

```bash
sudo snap install okular
```

- 按回：`ENTER`

## 远程办公

### Citrix Workspace

### Microsoft Teams

### Zoom

### Citrix Workspace

![](img/image00965.jpeg)

- 前往：[`www.citrix.com/en-gb/downloads/workspace-app/linux/workspace-app-for-linux-latest.html`](https://www.citrix.com/en-gb/downloads/workspace-app/linux/workspace-app-for-linux-latest.html)

- 点击：`Download File under Citrix Workspace app for Linux (x86_64)`

- 下载：下载`icaclient_22.2.0.20_amd64.deb`

- 前往：`icaclient_22.2.0.20_amd64.deb`的下载位置

- 双击：`icaclient_22.2.0.20_amd64.deb`

![](img/image00966.jpeg)

- 点击：`Install Package`

### Microsoft Teams

![](img/image00967.jpeg)

- 打开：`Snap Store`

- 输入或复制粘贴：`microsoft teams`

- 点击：`Microsoft Teams (Insiders or Preview)`

![](img/image00968.jpeg)

- 点击：`Install`

### Zoom

![](img/image00784.jpeg)

- 打开：`Terminal`

- 输入或复制粘贴：

```bash
sudo apt update
```

- 按回：`ENTER`

![](img/image00969.jpeg)

- 打开：`Terminal`

- 输入或复制粘贴：

```bash
sudo apt install libglib2.0-0 libxcb-shape libxcb-shm libxcb-fixes libxcb-randr libxcb-image0 fontconfig libgl1-mesa-glx xi libsm6 renderx1 libcomposite1 sqlite3-0 libxcb-keysym1 ibus
```

- 按回：`ENTER`

![](img/image00970.jpeg)

- 前往：[`zoom.us/download?linux`](https://zoom.us/download?linux)

- 点击：Linux 版本

- 点击：相同的架构

- 点击：64 位

- 下载：`zoom_amd64.deb`

- 前往：`zoom_amd64.deb`的下载位置

- 双击：`zoom_amd64.deb`

![](img/image00971.jpeg)

- 点击：`Install`

## 安全

## 防火墙端口

### TCP 端口

`53`, `80`, `433`, `1119`, `1120`, `2099`, `3074`, `3075`, `3216`, `3478`, `3479`, `3569`, `3724`, `4000`, `5060`, `5062`, `5222`, `5223`, `6012`, `6112`, `6113`, `6114`, `6250`, `8080`, `8088`, `8094`, `8097`, `9946`, `9988`, `14000`, `14008`, `14020`, `14021`, `14022`, `14023`, `14024`, `17502`, `17503`, `17504`, `18000`, `18060`, `18120`, `22990`, `27900`, `28910`, `29900`, `42124`, `42125`, `42126`, `42127`, `42130`, `42210`, `42230`, `10000:19999`, `10000:20000`, `10000:29999`, `1024:1124`, `1119:1120`, `12000:65000`, `20000:20100`, `25000:25099`, `27014:27050`, `30000:30099`, `42100:42200`, `6112:6119`, `6113:6119`, `7777:7780`, `8393:8400`, `9960:9969`

### UDP 端口

`67`, `80`, `443`, `1119`, `1120`, `2099`, `3074`, `3075`, `3216`, `3478`, `3479`, `3569`, `3724`, `4000`, `5060`, `5062`, `5222`, `5223`, `6012`, `6112`, `6113`, `6114`, `6250`, `8080`, `8088`, `8094`, `8097`, `9946`, `9988`, `14000`, `14008`, `14020`, `14021`, `14022`, `14023`, `14024`, `17502`, `17503`, `17504`, `18000`, `18060`, `18120`, `22990`, `27900`, `28910`, `29900`, `42124`, `42125`, `42126`, `42127`, `42130`, `42210`, `42230`, `10000:19999`, `10000:20000`, `10000:29999`, `1024:1124`, `1119:1120`, `12000:65000`, `20000:20100`, `25000:25099`, `27014:27050`, `30000:30099`, `42100:42200`, `6112:6119`, `6113:6119`, `7777:7780`, `8393:8400`, `9960:9969`

![](img/image00985.jpeg)

### Clamtk

点击：安装

![](img/image00986.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt install clamtk-gnome
```

按下：`ENTER`

### Firetools

![](img/image00987.jpeg)

打开：`Software Manager`

输入或复制并粘贴：

```bash
firetools
```

点击：`Firetools`

![](img/image00988.jpeg)

点击：安装

![](img/image00989.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt install firetools
```

按下：`ENTER`

### Firejail

![](img/image00990.jpeg)

打开：`Software Manager`

输入或复制并粘贴：

```bash
firejail
```

点击：`Firejail`

![](img/image00991.jpeg)

点击：安装

![](img/image00992.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt install firejail
```

按下：`ENTER`

### GUFW

![](img/image00993.jpeg)

打开：`Software Manager`

输入或复制并粘贴：

```bash
gufw
```

点击：`Gufw`

![](img/image00994.jpeg)

点击：安装

![](img/image00995.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt install gufw
```

按下：`ENTER`

#### GUFW 设置多端口规则

![](img/image00996.jpeg)

打开：`Gufw` 或 `Firewall Configuration`

点击：`Rules`

点击：`+`

点击：`Simple`

选择：`TCP` 或 `UDP`

输入或复制并粘贴：

```text
21,22
```

点击：`Add`

#### GUFW 设置范围范围规则

![](img/image00997.jpeg)

打开：`Gufw` 或 `Firewall Configuration`

点击：`Rules`

点击：`+`

点击：`Simple`

选择：`TCP` 或 `UDP`

输入或复制并粘贴：

```text
4001:4002
```

点击：`Add`

#### GUFW 设置单端口规则

![](img/image00998.jpeg)

打开：`Gufw` 或 `Firewall Configuration`

点击：`Rules`

点击：`+`

点击：`Simple`

选择：`TCP` 或 `UDP`

输入或复制并粘贴：

```text
21
```

点击：`Add`

### UFW

![](img/image00999.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt install ufw
```

按下：`ENTER`

#### UFW 设置多端口及范围规则

![](img/image01000.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo ufw allow 21,22,4111:4112/tcp
```

按下：`ENTER`

对于 UDP 协议，将`/tcp`改为`/udp`

#### UFW 设置多端口规则

![](img/image01001.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo ufw allow 21,22/tcp
```

按下：`ENTER`

对于 UDP 协议，将`/tcp`改为`/udp`

#### UFW 设置范围端口规则

![](img/image01002.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo ufw allow 4111:4112/tcp
```

按下：`ENTER`

对于 UDP 协议，将`/tcp`改为`/udp`

#### UFW 设置单端口规则

![](img/image01003.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo ufw allow 21/tcp
```

按下：`ENTER`

对于 UDP 协议，将`/tcp`改为`/udp`

### 软件分发

- AppImageLauncher

- Flathub

- Flatpak

- Java JRE JDK

- Snap

- Snap Store

#### AppImageLauncher

![](img/image01004.jpeg)

访问：[`github.com/TheAssassin/AppImageLauncher/releases/tag/v2.2.0`](https://github.com/TheAssassin/AppImageLauncher/releases/tag/v2.2.0)

点击：`appimagelauncher_2.2.0-travis995.0f91801.bionic_amd64.deb`

前往：下载`appimagelauncher_2.2.0-travis995.0f91801.bionic_amd64.deb`

![](img/image01005.jpeg)

访问：`appimagelauncher_2.2.0-travis995.0f91801.bionic_amd64.deb`下载所在。

双击：`appimagelauncher_2.2.0-travis995.0f91801.bionic_amd64.deb`

点击：安装

![](img/image01006.jpeg)

点击：继续

#### Flathub

![](img/image01007.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
flatpak remote-add --if-exists flathub https://flathub.org/repo/flathub.flatpak
```

按下：`ENTER`

#### Flatpak

![](img/image00784.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt update
```

按下：`ENTER`

![](img/image0108.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt install flatpak
```

按下：`ENTER`

#### Java JRE JDK

![](img/image0109.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt install default-jdk default-jre
```

#### Snap

![](img/image0110.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo mv /etc/apt/preferences.d/nosnap ~/Documents/nosnap
```

按下：`ENTER`

![](img/image00784.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt update
```

按下：`ENTER`

![](img/image0111.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt install snapd
```

按下：`ENTER`

## Snap Store

![](img/image0112.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo snap install snap-store
```

按下：`ENTER`

### 系统设置

- 缩图

- AMD 驱动

- 自动挂载磁盘

- 更改内核版本

- 更改鼠标加速

- 更改音频设备

- 更改主题

- 启用 LibreOffice 

- 如何使用 Xed 阻止网站

- Nautilus 文件管理器

- 夜光

- Nvidia 驱动

- 可能段错误

- 设置默认文件类型

- 备用 DNS

- 启动应用程序

- 更新系统

#### 缩图

![](img/image0113.jpeg)

打开：`Windows`

点击：`Alt-Tab`

点击：Alt-Tab 切换器所在的框

点击：仅缩图

#### AMD 驱动

![](img/image0114.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo add-apt-repository ppa:kisak/kisak-mesa
```

按下：`ENTER`

![](img/image0115.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt update
```

按下：`ENTER`

![](img/image0116.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt-get upgrade
```

按下：`ENTER`

![](img/image0117.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt-get install mesa
```

按下：`ENTER`

![](img/image0118.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt-get install ppa-purge
```

按下：`ENTER`

![](img/image0119.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo ppa-purge ppa:kisak/kisak-mesa
```

按下：`ENTER`

![](img/image00784.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt update
```

按下：`ENTER`

![](img/image0941.jpeg)

打开：`Terminal`

输入或复制并粘贴：

```bash
sudo apt upgrade
```

按下：`ENTER`

#### 自动挂载磁盘

![](img/image0120.jpeg)

打开：`Disks`

选择：`Disk`

选择：`Volume`



点击：`Cog` 图标

点击：`Edit Options`

移动：`User Session Defaults` 所在的开关到左侧

点击：`OK`

## 更改内核版本

![](img/image0122.jpeg)

点击：`Play` 按钮

打开：`Update Manager`

点击：`View`

点击：`Linux Kernels`

![](img/image0124.jpeg)

可以选择继续或不继续

点击：`5.13`

点击：安装

## 更改鼠标加速

![](img/image0126.jpeg)

点击：`Yes`

打开：`Mouse and Touchpad`

移动：`Custom Acceleration` 所在的开关到右侧

移动：`Acceleration` 下方的开关一直滑到 `Fast`

## 更改音频设备

![](img/image0128.jpeg)

打开：`Sound`

点击：`Device` 切换到该音频设备

## 更改主题

![](img/image0129.jpeg)

打开：`Themes`

点击：`Controls` 所在的框

点击：`Mint-Y-Dark`

点击：`Desktop` 所在的框

点击：`Mint-Y-Dark`

确保与“启用”（`Enable`）和“自启动”（`Autostart`）同一行的框框已勾选

## Nvidia 驱动

![](img/image01038.jpeg)

1. 打开：`驱动管理器`（`Driver Manager`）

2. 选择：`nvidia-driver-510`

3. 点击：`应用更改`（`Apply Changes`）

![](img/image01039.jpeg)

4. 等待更改应用

![](img/image01040.jpeg)

5. 点击：`重启`（`Restart`）

## 可能的 Intel 声音卡杂声修复

![](img/image01041.jpeg)

1. 打开：`终端`（`Terminal`）

2. 输入或复制并粘贴：

```bash
sudo echo "options snd_hda_intel power_save=0" | sudo tee -a /etc/modprobe.d/audio_disable_powersave.conf
```

3. 按下：`回车键`（`ENTER`）

## 可能的 Parole 段错误修复

![](img/image01042.jpeg)

1. 打开：`文件`（`Files`）

2. 转到：`/home/mylinuxmintpc/.config/xfce4`

3. 选择：`parole`

4. 右键点击：`parole`

5. 点击：`删除`（`Delete`）

## 设置为文件类型的默认值

![](img/image01043.jpeg)

1. 右键点击：`文件`（`File`）

2. 点击：`属性`（`Properties`）

3. 点击：`打开方式`（`Open With`）

4. 点击：`应用程序`（`Application`）

5. 点击：`设为默认`（`Set as default`）

6. 点击：`关闭`（`Close`）

## 设置替代 DNS

![](img/image01044.jpeg)

1. 转到：[`www.quad9.net/`](https://www.quad9.net/)

2. 注意：`IPv4` 和 `IPv6` 地址

3. 打开：`网络`（`Network`）

![](img/image01045.jpeg)

4. 选择：`连接`（`Connection`）

5. 点击：`齿轮图标`（`Cog icon`）

![](img/image01046.jpeg)

6. 点击：`IPv4`

7. 将：与`自动`（`Automatic`）和`DNS`同一行的开关向左移动

8. 点击：`DNS` 下方的 `+` 按钮

9. 点击服务器旁边的第一个框

10. 输入或复制并粘贴：`9.9.9.9`

11. 点击服务器旁边的第二个框

12. 输入或复制并粘贴：`149.112.112.112`

13. 点击：`IPv6`

![](img/image01047.jpeg)

14. 点击：`IPv6`

15. 将：与`自动`（`Automatic`）和`DNS`同一行的开关向左移动

16. 点击：`DNS` 下方的 `+` 按钮

17. 点击服务器旁边的第一个框

18. 输入或复制并粘贴：`2620:fe::fe`

19. 点击服务器旁边的第二个框

20. 输入或复制并粘贴：`2620:fe::9`

21. 点击：`应用`（`Apply`）

### 其他可选替代 DNS 有：

* **Comodo Secure DNS**

    * [`www.comodo.com/secure-dns/switch/`](https://www.comodo.com/secure-dns/switch/)

    * `IPv4`: `8.26.56.26`, `8.20.247.20`

* **DNS.WATCH**

    * [`dns.watch/`](https://dns.watch/)

    * `IPv4`: `84.200.69.80`, `84.200.69.80`

    * `IPv6`: `2001:1608:10:25::1c04:b12f`, `2001:1608:10:25::9249:d69b`

* **OpenNIC Project**

    * [`www.opennic.org/`](https://www.opennic.org/)

    * `IPv4`: `94.247.43.254`, `194.36.144.87`, `151.80.222.79`, `91.217.137.37`

    * `IPv6`: `2a00:f826:8:1::254`, `2a03:4000:4d:c92:88c0:96ff:fec6:b9d`, `2001:470:1f15:b80::53`, `2001:67c:13e4:1::37`

## 启动应用程序

![](img/image01048.jpeg)

1. 打开：`启动应用程序`（`Startup Applications`）

2. 点击：`+`

3. 点击：`选择应用程序`（`Choose Application`）

![](img/image01049.jpeg)

4. 点击：`Firefox 浏览器`（`Firefox Web Browser`）

5. 点击：`添加应用程序`（`Add Application`）

![](img/image01050.jpeg)

1. 打开：`启动应用程序`（`Startup Applications`）

2. 点击：`+`

3. 点击：`自定义命令`（`Custom Command`）

![](img/image01051.jpeg)

4. 点击：与`名称`（`Name`）同一行的框

5. 输入或复制并粘贴：`Firefox`

6. 点击：与`命令`（`Command`）同一行的框

7. 输入或复制并粘贴：`firefox`

8. 点击：`添加`（`Add`）

## 更新系统

![](img/image01052.jpeg)

1. 打开：`更新管理器`（`Update Manager`）

2. 选择：`不从本地镜像下载`（`Not to download from Local Mirror`）

3. 选择：`更新管理器`（`To Update Manager`）

4. 点击：`刷新`（`Refresh`）

5. 点击：`安装`（`Install`）

![](img/image01053.jpeg)

6. 点击：`确定`（`OK`）

![](img/image01054.jpeg)

7. 等待更改应用

## 备份你的进度和文件

![](img/image01055.jpeg)

1. 按下：`Super` 或 `Meta` 键

2. 点击：`电源图标`（`Power Icon`）(向上)

![](img/image01057.jpeg)

3. 点击：`重启`（`Restart`）

## 系统实用

* `Bleachbit`

* `Boot Repair`

* `Czkawka`

* `GParted`

* `gpustat`

* `Grub Customizer`

* `HardInfo`

* `K4DirStat`

* `KDE Partition Manager`

* `Neofetch`

* `Psensor`

* `QDirStat`

* `Sweeper`

### Bleachbit

![](img/image01058.jpeg)

1. 打开：`软件管理器`（`Software Manager`）

2. 输入或复制并粘贴：`bleachbit`

3. 点击：`Bleachbit`

![](img/image01059.jpeg)

4. 点击：`安装`（`Install`）

![](img/image01060.jpeg)

5. 打开：`终端`（`Terminal`）

6. 输入或复制并粘贴：

```bash
sudo apt install bleachbit
```

7. 按下：`回车键`（`ENTER`）

## Boot Repair

![](img/image01061.jpeg)

1. 打开：`终端`（`Terminal`）

2. 输入或复制并粘贴：

```bash
sudo add-apt-repository ppa:yannubuntu/boot-repair && sudo apt update
```

3. 按下：`回车键`（`ENTER`）

![](img/image01062.jpeg)

4. 打开：`终端`（`Terminal`）

5. 输入或复制并粘贴：

```bash
sudo apt install -y boot-repair && boot-repair
```

6. 按下：`回车键`（`ENTER`）

## Czkawka

![](img/image01063.jpeg)

1. 打开：`软件 Store`（`Snap Store`）

2. 输入或复制并粘贴：`czkawka`

3. 点击：`Czkawka`

![](img/image01064.jpeg)

4. 点击：`安装`（`Install`）

![](img/image01065.jpeg)

1. 打开：`终端`（`Terminal`）

2. 输入或复制并粘贴：

```bash
sudo apt install bleachbit
```

3. 按下：`回车键`（`ENTER`）

## GParted

![](img/image01066.jpeg)

1. 打开：`软件管理器`（`Software Manager`）

2. 输入或复制并粘贴：`gparted`

3. 点击：`GParted`

![](img/image01067.jpeg)

4. 点击：`安装`（`Install`）

![](img/image01068.jpeg)

5. 打开：`终端`（`Terminal`）

6. 输入或复制并粘贴：

```bash
sudo apt install -y boot-repair && boot-repair
```

7. 按下：`回车键`（`ENTER`）

## gpustat

![](img/image01069.jpeg)

1. 打开：`软件管理器`（`Software Manager`）

2. 输入或复制并粘贴：`gpustat`

3. 点击：`gpustat`

## Grub Customizer

![](img/image01070.jpeg)

1. 打开：`终端`（`Terminal`）

2. 输入或复制并粘贴：

```bash
sudo add-apt-repository ppa:yannubuntu/boot-repair && sudo apt update
```

3. 按下：`回车键`（`ENTER`）

## HardInfo

![](img/image01071.jpeg)

1. 打开：`终端`（`Terminal`）

2. 输入或复制并粘贴：

```bash
sudo apt install -y boot-repair && boot-repair
```

3. 按下：`回车键`（`ENTER`）

## K4DirStat

![](img/image01072.jpeg)

1. 打开：`软件管理器`（`Software Manager`）

2. 输入或复制并粘贴：`k4dirstat`

3. 点击：`K4DirStat`

## KDE Partition Manager

![](img/image01073.jpeg)

1. 点击：`安装`（`Install`）

## Neofetch

![](img/image01074.jpeg)

1. 打开：`终端`（`Terminal`）

2. 输入或复制并粘贴：

```bash
sudo apt install bleachbit
```

3. 按下：`回车键`（`ENTER`）

## Psensor

![](img/image01075.jpeg)

1. 打开：`软件管理器`（`Software Manager`）

2. 输入或复制并粘贴：`psensor`

3. 点击：`Psensor`

## QDirStat

![](img/image01076.jpeg)

1. 点击：`安装`（`Install`）

## Stacer

![](img/image01077.jpeg)

1. 打开：`软件管理器`（`Software Manager`）

2. 输入或复制并粘贴：`stacer`

3. 点击：`Stacer`

## Sweeper

![](img/image01078.jpeg)

1. 点击：`安装`（`Install`）

## Openshot

![](img/image01103.jpeg)

## 软件管理器

打开：`Software Manager`

输入或复制粘贴：

`openshot`

点击：`OpenShot Video Editor`

![](img/image01104.jpeg)

点击：`Install`

![](img/image01105.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install openshot
```

按下：`ENTER`

# Shotcut

![](img/image01106.jpeg)

## 软件管理器

打开：`Software Manager`

输入或复制粘贴：

`shotcut`

点击：`Shotcut`

![](img/image01107.jpeg)

点击：`Install`

![](img/image01108.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install shotcut
```

按下：`ENTER`

![](img/image01109.jpeg)

## Snap Store

打开：`Snap Store`

输入或复制粘贴：

`shotcut`

点击：`shotcut`

![](img/image01110.jpeg)

点击：`Install`

![](img/image01111.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install shotcut
```

按下：`ENTER`

## 视频点播流媒体

* `Amazon Prime Video`

* `Disney+`

* `Netflix`

### Amazon Prime Video

![](img/image01112.jpeg)

前往：

[`www.amazon.co.uk/Amazon-Video/b?node=3010085031`](https://www.amazon.co.uk/Amazon-Video/b?node=3010085031)

登录访问

### Disney+

![](img/image01113.jpeg)

前往：

[`www.disneyplus.com/en-gb`](https://www.disneyplus.com/en-gb)

登录访问

### Netflix

![](img/image01114.jpeg)

前往：

[`www.netflix.com/gb/`](https://www.netflix.com/gb/)

登录访问

## 虚拟化

* `Virt-Manager`

* `Virtualbox`

* `Virtualbox Extension Pack`

### Virt-Manager

![](img/image01115.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virtinst virt-manager
```

按下：`ENTER`

### Virtualbox

![](img/image01116.jpeg)

打开：`Software Manager`

输入或复制粘贴：

`virtualbox`

点击：`Virtualbox`

![](img/image01117.jpeg)

点击：`Install`

![](img/image00784.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt update
```

按下：`ENTER`

![](img/image01118.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo apt install virtualbox
```

按下：`ENTER`

### Virtualbox Extension Pack

![](img/image01119.jpeg)

打开：`Software Manager`

输入或复制粘贴：

`virtualbox`

点击：`Virtualbox-ext-pack`

![](img/image01120.jpeg)

点击：`Install`

![](img/image01121.jpeg)

打开：`Terminal`

输入或复制粘贴：



# 安装软件

```bash
sudo apt install virtualbox-ext-pack
```

按下：`ENTER`

## 浏览器

- Chromium
- Firefox ESR
- Google Chrome
- Microsoft Edge
- Opera

### Chromium

![](img/image01122.jpeg)

打开：`Snap Store`

输入或复制粘贴：

`chromium`

点击：`chromium`

![](img/image01123.jpeg)

点击：`Install`

![](img/image01124.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install chromium
```

按下：`ENTER`

### Firefox ESR

![](img/image01125.jpeg)

前往：

[`www.mozilla.org/en-GB/firefox/all/#product-desktop-esr`](https://www.mozilla.org/en-GB/firefox/all/#product-desktop-esr)

点击：您想要下载哪个浏览器下方的框

点击：`Firefox Extended Support Release`

点击：选择您的首选安装程序下方的框

点击：`Linux 64-bit`

点击：选择您的首选语言下方的框

点击：`English (British)`

下载：`firefox-91.6.0esr.tar.bz2`

前往：`firefox-91.6.0esr.tar.bz2` 下载的位置

双击：`firefox-91.6.0esr.tar.bz2`

![](img/image01126.jpeg)

选择：`firefox`

点击：`Extract`

![](img/image01127.jpeg)

前往：

`/home/mylinuxmint/Applications`

点击：`Extract`

点击：`Close`

### Google Chrome

![](img/image01128.jpeg)

前往：

[`www.google.com/intl/en_uk/chrome/`](https://www.google.com/intl/en_uk/chrome/)

点击：`Download Chrome`

勾选：`64 bit.deb` (对于 Debian/Ubuntu) 同行的框

点击：`Accept and install`

下载：`google-chrome-stable_current_amd64.deb`

前往：`google-chrome-stable_current_amd64.deb` 下载的位置

双击：`google-chrome-stable_current_amd64.deb`

### Microsoft Edge

![](img/image01129.jpeg)

前往：

[`www.microsoft.com/edge/insider/`](https://www.microsoft.com/edge/insider/)

点击：`Download Edge`

勾选：`64 bit.deb` (对于 Debian/Ubuntu) 同行的框

点击：`Accept and install`

下载：`microsoft-edge-stable_current_amd64.deb`

前往：`microsoft-edge-stable_current_amd64.deb` 下载的位置

双击：`microsoft-edge-stable_current_amd64.deb`

### Opera

![](img/image01130.jpeg)

打开：`Snap Store`

输入或复制粘贴：

`opera`

点击：`opera`

![](img/image01131.jpeg)

打开：`Terminal`

输入或复制粘贴：

```bash
sudo snap install opera
```

按下：`ENTER`

## 选择：`TotalValue_Shadowlands`

点击：`提取`

前往：`World of Warcraft/_retail_/Interface/AddOns`

点击：`提取`

## 魔兽世界插件管理器

- `Ajour`
  - `Ajour`
  - `Ajour 删除插件`
  - `Ajour 删除变量`
  - `Ajour 安装插件`
  - `Ajour 新建插件目录`
- `Strongbox (强箱)`
  - `Strongbox`
  - `Strongbox 切换主题`
  - `Strongbox 删除插件`
  - `Strongbox 删除多个插件`
  - `Strongbox 安装插件`
  - `Strongbox 安装多个插件`
  - `Strongbox 新建插件目录`
- `wowmatrix`
  - `wowmatrix`
  - `wowmatrix 删除插件`
  - `wowmatrix 删除多个插件`
  - `wowmatrix 安装插件`
  - `wowmatrix 新建插件目录`
- `Wowup`
  - `Wowup`
  - `Wowup 删除插件`
  - `Wowup 删除多个插件`
  - `Wowup 安装插件`
  - `Wowup 新建插件目录`

### Ajour

![](img/image01148.jpeg)

前往：`https://github.com/ajour/ajour/releases/tag/1.3.2`

点击：`ajour-opengl.AppImage`

至：下载 `ajour-opengl.AppImage`

前往：`ajour-opengl.AppImage` 的下载位置

双击：`ajour-opengl.AppImage`

![](img/image01149.jpeg)

点击：`集成并运行`

### Ajour 删除插件

![](img/image01150.jpeg)

打开：`Ajour`

点击：`我的插件`

点击：`插件`

点击：`删除主计划 (Master Plan)`

![](img/image01151.jpeg)

点击：`确认删除`

### Ajour 删除变量

![](img/image01152.jpeg)

打开：`Ajour`

点击：`我的插件`

点击：`插件`

点击：`删除保存变量 (SavedVariables)`

![](img/image01153.jpeg)

点击：`确认删除`

### Ajour 安装插件

![](img/image01154.jpeg)

打开：`Ajour`

点击：`目录`

点击：`搜索框`

输入或复制粘贴：`master plan`

点击：`在与 Master Plan 相同的行中安装`

### Ajour 新建插件目录

![](img/image01155.jpeg)

打开：`Ajour`

点击：`选择目录`

![](img/image01156.jpeg)

前往：魔兽世界文件夹

点击：

- `_retail_`
- `_classic_`
- `_classic_era_`

点击：`Interface`

选择：`Addons`

点击：`确定`

## Strongbox

![](img/image01157.jpeg)

前往：`https://github.com/ogri-la/strongbox/releases/tag/5.0.0`

点击：`strongbox`

至：下载 `strongbox`

前往：`strongbox` 的下载位置

双击：`strongbox`

![](img/image01158.jpeg)

点击：`集成并运行`

### Strongbox 切换主题

![](img/image01159.jpeg)

打开：`Strongbox`

点击：`视图`

点击：`深色主题`

### Strongbox 删除插件

![](img/image01160.jpeg)

打开：`Strongbox`

点击：`已安装`

选择：`BlizzMove`

右键点击：`BlizzMove`

点击：`删除`

点击：`确定`

### Strongbox 删除多个插件

![](img/image01161.jpeg)

打开：`Strongbox`

按住 `Shift 并左键` 选择多个插件

右键点击：`选中的插件`

点击：`删除`

点击：`确定`

### Strongbox 安装插件

![](img/image01162.jpeg)

打开：`Strongbox`

点击：`搜索`

点击：`搜索框`

输入或复制粘贴：`Blizzmove`

点击：`在与 BlizzMove 相同的行中安装`

### Strongbox 安装多个插件

![](img/image01163.jpeg)

打开：`Strongbox`

点击：`搜索`

点击：`搜索框`

按住 `Shift 并右键` 选择多个要安装的插件

点击：`安装已选`

### Strongbox 新建插件目录

![](img/image01159.jpeg)

打开：`Strongbox`

点击：`文件`

点击：`新建插件目录`

![](img/image01156.jpeg)

前往：魔兽世界文件夹

点击：

- `_retail_`
- `_classic_`
- `_classic_era_`

点击：`Interface`

选择：`Addons`

点击：`确定`

## wowmatrix

![](img/image01164.jpeg)

前往：`https://www.wowmatrix.com/download`

点击：`Linux 64 位 免费下载`

至：下载 `wowmatrix.tar.gz`

前往：`wowmatrix.tar.gz` 的下载位置

双击：`wowmatrix.tar.gz`

![](img/image01165.jpeg)

选择：`wowmatrix`

点击：`提取`

![](img/image01166.jpeg)

前往：`/home/mylinuxmintpc/Applications`

点击：`提取`

### wowmatrix 删除插件

![](img/image01167.jpeg)

打开：`wowmatrix`

选择：`BetterWardrobe`

点击：`卸载`

![](img/image01168.jpeg)

点击：`永久删除`

### wowmatrix 删除多个插件

![](img/image01169.jpeg)

打开：`wowmatrix`

选择：`NeatPlates_Horizontal`

按住 `Shift 并左键`

点击：`卸载`

### wowmatrix 安装插件

打开：`wowmatrix`

点击：`获取插件`

点击：`搜索`

选择：`armory`

点击：`安装`

### wowmatrix 新建插件目录

打开：`wowmatrix`

前往：魔兽世界文件夹

点击：

- `_retail_`
- `_classic_`
- `_classic_era_`

点击：`Interface`

选择：`Addons`

点击：`确定`

## Wowup

前往：`https://github.com/ajour/ajour/releases/tag/1.3.2`

点击：`ajour-opengl.AppImage`

至：下载 `ajour-opengl.AppImage`

前往：`ajour-opengl.AppImage` 的下载位置

双击：`ajour-opengl.AppImage`

![](img/image01149.jpeg)

点击：`集成并运行`

### Ajour 删除插件

![](img/image01150.jpeg)

打开：`Ajour`

点击：`我的插件`

点击：`插件`

点击：`删除主计划`

![](img/image01151.jpeg)

点击：`确认删除`

### Ajour 删除变量

![](img/image01152.jpeg)

打开：`Ajour`

点击：`我的插件`

点击：`插件`

点击：`删除保存变量`

![](img/image01153.jpeg)

点击：`确认删除`

### Ajour 安装插件

![](img/image01154.jpeg)

打开：`Ajour`

点击：`目录`

点击：`搜索框`

输入或复制粘贴：`master plan`

点击：`在与 Master Plan 相同的行中安装`

### Ajour 新建插件目录

![](img/image01155.jpeg)

打开：`Ajour`

点击：`选择目录`

![](img/image01156.jpeg)

前往：魔兽世界文件夹

点击：

- `_retail_`
- `_classic_`
- `_classic_era_`

点击：`Interface`

选择：`Addons`

点击：`确定`

## Strongbox

![](img/image01157.jpeg)

前往：`https://github.com/ogri-la/strongbox/releases/tag/5.0.0`

点击：`strongbox`

至：下载 `strongbox`

前往：`strongbox` 的下载位置

双击：`strongbox`

![](img/image01158.jpeg)

点击：`集成并运行`

### Strongbox 切换主题

![](img/image01159.jpeg)

打开：`Strongbox`

点击：`视图`

点击：`深色主题`

### Strongbox 删除插件

![](img/image01160.jpeg)

打开：`Strongbox`

点击：`已安装`

选择：`BlizzMove`

右键点击：`BlizzMove`

点击：`删除`

点击：`确定`

### Strongbox 删除多个插件

![](img/image01161.jpeg)

打开：`Strongbox`

按住 `Shift 并左键` 选择多个插件

右键点击：`选中的插件`

点击：`删除`

点击：`确定`

### Strongbox 安装插件

![](img/image01162.jpeg)

打开：`Strongbox`

点击：`搜索`

点击：`搜索框`

输入或复制粘贴：`Blizzmove`

点击：`在与 BlizzMove 相同的行中安装`

### Strongbox 安装多个插件

![](img/image01163.jpeg)

打开：`Strongbox`

点击：`搜索`

点击：`搜索框`

按住 `Shift 并右键` 选择多个要安装的插件

点击：`安装已选`

### Strongbox 新建插件目录

![](img/image01159.jpeg)

打开：`Strongbox`

点击：`文件`

点击：`新建插件目录`

![](img/image01156.jpeg)

前往：魔兽世界文件夹

点击：

- `_retail_`
- `_classic_`
- `_classic_era_`

点击：`Interface`

选择：`Addons`

点击：`确定`

## wowmatrix

![](img/image01164.jpeg)

前往：`https://www.wowmatrix.com/download`

点击：`Linux 64 位 免费下载`

至：下载 `wowmatrix.tar.gz`

前往：`wowmatrix.tar.gz` 的下载位置

双击：`wowmatrix.tar.gz`

![](img/image01165.jpeg)

选择：`wowmatrix`

点击：`提取`

![](img/image01166.jpeg)

前往：`/home/mylinuxmintpc/Applications`

点击：`提取`

### wowmatrix 删除插件

![](img/image01167.jpeg)

打开：`wowmatrix`

选择：`BetterWardrobe`

点击：`卸载`

![](img/image01168.jpeg)

点击：`永久删除`

### wowmatrix 删除多个插件

![](img/image01169.jpeg)

打开：`wowmatrix`

选择：`NeatPlates_Horizontal`

按住 `Shift 并左键`

点击：`卸载`

### wowmatrix 安装插件

打开：`wowmatrix`

点击：`获取插件`

点击：`搜索`

选择：`armory`

点击：`安装`

### wowmatrix 新建插件目录

打开：`wowmatrix`

前往：魔兽世界文件夹

点击：

- `_retail_`
- `_classic_`
- `_classic_era_`

点击：`Interface`

选择：`Addons`

点击：`确定`

## Wowup

前往：`https://github.com/ajour/ajour/releases/tag/1.3.2`

点击：`ajour-opengl.AppImage`

至：下载 `ajour-opengl.AppImage`

前往：`ajour-opengl.AppImage` 的下载位置

双击：`ajour-opengl.AppImage`

![](img/image01149.jpeg)

点击：`集成并运行`

### Ajour 删除插件

![](img/image01150.jpeg)

打开：`Ajour`

点击：`我的插件`

点击：`插件`

点击：`删除主计划`



![](img/image01151.jpeg)

点击：`确认删除`

## Ajour 删除变量

![](img/image01152.jpeg)

打开：`Ajour`

点击：`我的插件`

点击：`插件`

点击：`删除保存变量`

![](img/image01153.jpeg)

点击：`确认删除`

## Ajour 安装插件

![](img/image01154.jpeg)

打开：`Ajour`

点击：`目录`

点击：`搜索框`

输入或复制粘贴：`master plan`

点击：`在与 Master Plan 相同的行中安装`

## Ajour 新建插件目录

![](img/image01155.jpeg)

打开：`Ajour`

点击：`选择目录`

![](img/image01156.jpeg)

前往：魔兽世界文件夹

点击：

- `_retail_`

- `_classic_`

- `_classic_era_`

点击：`Interface`

选择：`Addons`

点击：`确定`
