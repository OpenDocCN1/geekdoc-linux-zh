
GpsDrive 是一个导航系统，设计用于在可缩放地图上显示您的 GPS 位置（参见图 9.4）。虽然它可以完全独立于 Kismet 作为一个独立的映射程序使用，但它也能很好地与 Kismet（以及 MySQL）集成，在地图上显示 Kismet 网络数据。此外，它还支持通过 `festival` 进行语音输出（`flite` 也适用）；因此，你甚至可以让人工语音 GpsDrive 在发现新网络时告知你。如果你的 GPS 接收器支持 `gpsd`（或 `gpsdold`），那么它应该也能与 GpsDrive 配合使用。

### 图 9.4 GpsDrive 主页

![](img/d6ac176c353d2b7687c1186a140180a1_233_0.png)

## 安装

安装 `GpsDrive` 假设你已将 BackTrack 3 Beta（或其他 Linux 发行版）安装到硬盘上。你还需要以下软件包：`gpsd`、`GTK+-2.x`（最好 >=2.2.x）、`pango`、`atk`、`pcre`、`xadvel`（X11 开发包）、`gettext`、`librypt`、`glibc`、`gcc >=3.x` 以及 `make`。在许多情况下，这些软件包中的一部分或全部已经安装。无论如何，你最好事先检查，以避免任何问题。最后，`GpsDrive` 需要结构化查询语言（SQL）支持以与 Kismet 进行接口交互。对于 BackTrack，MySQL 已经安装；在其他发行版中，你可能需要自行安装。

**警告**

在 Debian 和 Slackware 发行版（包括 BackTrack）中，如果没有 `gcc 3.x`，`GpsDrive` 将无法正确编译。不幸的是，`slapt-get` 在 BackTrack 3 Beta 中开箱即用并不正常工作，因此你需要手动升级 `gcc`（http://gcc.gnu.org/），然后编译 `GpsDrive`。或者，你可以直接下载 `GpsDrive` 的预编译版本。

### 从源代码安装

要从源代码安装，请从 `GpsDrive` 网站（http://www.gpsdrive.de/）下载源代码。当前的稳定版本（尽管较旧）是 `v2.09`。然后执行以下操作：

```bash
tar -zxvf gpsdrive-2.09.tar.gz
cd gpsdrive-2.09
./configure
make
make install
```

**注意**

如果你不需要对 Garmin GPS 协议的支持，请在配置时使用 `--disable-garmin` 参数。

### 从软件包安装

作为替代方案，你可能希望选择一个已经编译好的 `GpsDrive` 软件包。根据你使用的发行版不同，软件包安装步骤可能有所不同。你可以在 http://slackware-current.net/package.php?id=345 找到一个兼容 Slackware（也兼容 BackTrack）的 `GpsDrive` 软件包（注意该版本已编译进 Garmin GPS 协议）。要安装（参见图 9.5）：

```bash
installpkg gpsdrive-2.09-i586-1.tgz
```

### 图 9.5 从软件包安装 GpsDrive

![](img/d6ac176c353d2b7687c1186a140180a1_235_0.png)

要启动，输入 `gpsdrive`。

## MySQL

虽然 `GpsDrive` 单独使用运行良好，但它需要 SQL 支持才能正确地与 Kismet 接口交互。正如之前所述，你的特定 Linux 版本上可能安装也可能没有安装 MySQL；我们将使用 BackTrack，其中已经安装了 MySQL。

即使已经安装了 MySQL，如果你以前从未使用过它，可能看起来有点吓人。别担心！Remote-Exploit 论坛（http://forums.remote-exploit.org/）用户 Dr.GrEeN 创建了一个小脚本，它将为你完成所有操作。只需将代码复制并粘贴到一个新文件中（这里我们将其命名为 `start-mysql`）：

```bash
#!/bin/sh
#
#### Backtrack Mysql Startup Script by Dr_Gr33n ####
#
option=6

echo "Welcome to the Dr_Gr33n's Backtrack 2 Mysql Startup Script"
#
echo "1) Start Small Server"
echo "2) Start Medium Server"
echo "3) Start Huge Server"
echo "4) Check Mysql is running"
echo "5) Stop Mysql"
echo "0) Exit"
read option
case $option in
1) echo "Starting Small Server"
    cp /etc/my-small.cnf /etc/my.cnf
    chown -R root .
    chown -R mysql /var
    chown -R mysql /var/lib/mysql
    /usr/bin/mysql_install_db --user=root
    /usr/bin/mysqld_safe --user=root &
    su
    mysql;;
2) echo "Starting Medium Server"
    cp /etc/my-medium.cnf /etc/my.cnf
    chown -R root .
    chown -R mysql /var
    chown -R mysql /var/lib/mysql
    /usr/bin/mysql_install_db --user=root
    /usr/bin/mysqld_safe --user=root &
    su
    mysql;;
3) echo "Starting Large Server"
    cp /etc/my-huge.cnf /etc/my.cnf
    chown -R root .
    chown -R mysql /var
    chown -R mysql /var/lib/mysql
    /usr/bin/mysql_install_db --user=root
    /usr/bin/mysqld_safe --user=root &
    su
    mysql;;
4) echo "Checking Mysql is running"
    /usr/bin/mysqladmin -u root -p version
    cd /root;;
5) echo "Stop Mysql Server"
    /usr/share/mysql/mysql.server stop
    cd /root;;
0) echo "*** Bye ***"
    ;;
*) exit ;;
esac
```

保存该文件，并别忘了执行 `chmod 755`。当你运行该文件时，它会提供三个选项：这些选项（小、中、大）都经过测试，看起来运行正常。

## Kismet + GpsDrive + MySQL

一旦你安装好所有软件，就可以开始了。首先，手动启动 MySQL，或使用名为 `start-mysql` 的 Dr_GrEeN 脚本。这将在 `3306` 端口（默认端口）上启动 MySQL。接下来，启动 GPS 守护进程（例如，`gpsd -p /dev/ttyUSB0`）。然后，启动 Kismet。最后，启动 `GpsDrive`（只需输入 `gpsdrive`）。在 `GpsDrive` 界面的左侧，务必勾选“使用 SQL”。这对于确保 Kismet 的网络存储在 MySQL 中并在 `GpsDrive` 中正确显示至关重要。

> **注意**
>
> 尽管你之前已经启动了 `gpsd`，但可能需要在 `GpsDrive` 内部点击启动按钮。

## 地图

你会很快注意到 `GpsDrive` 并不附带任何（有用的）地图，因此你需要自己获取。获取地图有两种方法：

- 在 `GpsDrive` 中，点击“下载地图”按钮。这将打开一个对话框窗口（参见图 9.6），允许你指定坐标和比例尺。请记住，这是一次下载一张地图（在某一比例下），如果你试图获取较大区域的多张不同比例尺地图，这可能很耗时。

> `GpsDrive` 会将地图着色为黄色，以指示将由特定比例尺地图下载的区域。更改比例尺显然会改变下载区域；请记住，比例尺越大，细节越多，但覆盖区域越小，反之亦然。

![](img/d6ac176c353d2b7687c1186a140180a1_238_0.png)

- `GpsDrive` 附带一个 perl 脚本 `gpsfetchmap.pl`，它自动化了一次下载多张地图的过程（参见图 9.7）。输入 `gpsfetch-map.pl --help` 查看可用选项。你肯定想阅读所有可用选项，以确保你为正确的位置获取正确比例尺的地图！
