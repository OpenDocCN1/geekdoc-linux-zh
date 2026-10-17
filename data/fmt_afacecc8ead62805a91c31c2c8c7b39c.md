
### apt-get remove name1 ...

卸载指定的软件包。

### apt-get source name

安装包的源代码。

### apt-get update

更新 `sources.list` 中指定的存档的软件包列表。（更多细节见 `apt update`。）

### apt-get upgrade

如果软件包源中有较新版本，则更新所有已安装的。

`apt-get` 命令的详细行为由选项控制：

#### apt-get -d --download-only

仅下载包到 `/var/cache/apt/archives` 目录，但不进行安装。

#### apt-get --no-install-recommends

不安装推荐包。

#### apt-get -s --simulate

模拟安装，但不进行任何更改。

#### apt-get -y --assume-yes

对所有问题回答“是”，以便在脚本中使用命令。

## 示例

以下更新命令展示了你可以如何使用 `apt-get`：

```
root apt-get update && apt-get dist-upgrade
(执行完整更新)
root# apt-get remove -y emacs
(无询问删除 emacs)
```

## apt-key 命令

尽管 `apt-key` 命令在无数网络手册中被提到，但它是过时的。在过去，该命令帮助管理软件包源的密钥。通常以 `apt-key add keyfile` 的形式执行。

该命令在当前的发行版中不再可用。密钥文件现在必须手动保存在 `/etc/apt/trusted.gpg.d` 目录下。此外，在 `/etc/apt/sources.list` 或 `/etc/apt/sources.d` 中指定软件包源时，必须使用 `signed-by:` 显式引用密钥文件：

```
## /etc/apt/sources.d/myrepo.list
deb [signed-by=/etc/apt/trusted.gpg/myrepo.asc] https://apt.myrepo.com ...
```

## aptitude [options]

Debian 特有的 `aptitude` 命令安装、更新和删除软件包，并访问像 `apt` 和 `apt-get` 这样的 APT 基础设施。与相比的优势

这两个命令的区别在于，`aptitude` 在安装过程中会记住依赖包，并在卸载时自动删除它们。

所有包管理功能都以命令的形式执行（例如，`aptitude install package name`）。基础命令与 `apt-get` 中的命令对应，并在那里有有描述。然而，`aptitude` 中没有提供 `check` 和 `autoremove` 命令。强大的 `search` 命令可以实现此目的。

此外，你也可以通过在不带任何额外参数的情况下直接启动程序，在控制中使用带有文本用户界面的程序。使用键盘快捷键 `Ctrl+T` 选择菜单。尽管有菜单，但 `aptitude` 的用法并不十分直观，大多数用户像使用 `apt-get` 一样，仅使用 `aptitude` 来运行单个命令。

大多数发行版默认没有安装 `aptitude`，在使用它之前必须通过 `apt` 或 `apt-get` 进行安装。

### aptitude search

`aptitude search` 为搜索软件包数据库提供了全面的选项。在最简单的形式下，你可以使用 `aptitude search 搜索词` 来搜索名称包含该搜索词的包。你可以使用 `~` 加字母来构建各种搜索标准。例如，`~i` 将搜索限制为已安装的包，`~U` 显示可用更新的包。`-F` 选项允许你控制搜索结果的哪些细节在特定宽度的列中显示。

其他许多搜索选项请参见 `/usr/share/doc/aptitude/README` 以及下页页：

`www.debian.org/doc/manuals/aptitude/ch02s04s05.en.html`

## 示例

以下两个命令首先安装 `mysql-server` 包，然后再次将其删除。值得注意的是，第二个命令删除了几乎所有与 `mysql-server` 一起安装的依赖包（但是，独立于服务器的客户端和库会被保留）。

```
root# aptitude install mysql-server
The following NEW packages will be installed:
libcgi-fast-perl{a} libcgi-pm-perl{a} libevent-core-2.1-7{a} ...
mysql-server mysql-server-8.0{a} mysql-server-core-8.0{a}
0 packages upgraded, 19 newly installed
...
```

```
root# aptitude remove mysql-server
The following packages will be REMOVED:
libcgi-fast-perl{u} ... mysql-server-core-8.0{u}
0 packages upgraded, 0 newly installed, 19 to remove
```

以下命令提供了所有已安装包的列表。包组或包源指定在第一列（`%20s, Source`，列宽为20个字符），包名指定在第二列。

```
user$ aptitude search ~i -F "%20s %p"
utils               adduser
admin             adwaita-icon-theme
games              aisleriot
..
```

你可以使用 `egrep` 从结果中过滤源自 Ubuntu 软件包源 `universe` 或 `multiverse` 的包。

```
user$ aptitude search ~i -F "%20s %p" | egrep "universe|multiverse"
universe/admin      aptitude
universe/admin      aptitude-common
universe/introspection  girl1.2-gtk-vnc-2.0
universe/editors      joe
universe/libs        libburn4
..
```

## arp [options] [hosts/ipaddresses/network]

来自 `net-tools` 包的 `arp` 命令有助于管理 `地址解析协议`（ARP）的缓存。该缓存包含本地网络设备列表，并允许分配它们的 MAC 地址。在没有任何额外参数的情况下，该命令返回当前缓存内容。使用 `-n` 选项，显示相应的 IP 地址而不是主机名。

```
user$ arp
Address            HWtype Hwidth      Flags Mask Iface
fritz.box           ether 3c:37:12:b7:a1:cb C       enp0s1
Archer-C6.fritz.box ether d08:b6:4f:19:af C enp0s1
m3.fritz.box ether 80:a9:97:32:c5:d7 C enp0s1
BRN0018BA99C5DA4.fritz ether 00:1b:a9:9c:5d:a4 C enp0s1
```

```
user$ arp -n
Address HWype HWaddress Mask Iface
192.168.178.10 ether 3c:37:12:b1:cb C enp0s1
192.168.178.21 ether d08:b6:4f:19:af C enp0s1
192.168.178.146 ether 80:a9:97:32:c5:d7 C enp0s1
192.168.178.20 ether 00:1b:a9:9c:5d:a4 C enp0s1
```

## arp-scan [options] [hosts/ipaddresses/network]

`arp-scan` 向指定的主机或 IP 地址发送地址解析协议（ARP）数据包并显示得到的响应。`arp-scan` 提供了一种极其快速的方法来发现哪些主机或 IP 地址正在运行活动设备以及它们拥有哪些 MAC 地址。

## atq

`atq` 列出所有设置在未来某个时间执行的作业。如果由 `root` 用户运行 `atq`，它将显示所有用户的作业；否则，仅显示其自身的作业。

## atrm n

`atrm` 根据编号删除指定的作业。你可以使用 `atq` 来确定所有设置在未来执行的作业编号。

## attr [options] files

`attr` 确定或更改指定文件或目录的扩展访问属性。这仅在文件系统支持扩展属性（EAs）时才有效。对于 `ext3/ext4` 文件系统，必须使用挂载选项 `user_xattr`。
