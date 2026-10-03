
```
default via 192.168.1.1 metric 100 dev ens33
192.168.1.0/24 dev ens33 scope link proto kernel metric 0
192.168.1.160/24 dev ens33 scope link proto kernel metric 0
```

默认路由的作用：目标 IP 地址或网络不在路由表中，数据会被发送到默认网关。例如，中的默认网关是 `192.168.1.1`。

## 表 8-14 网络设备配置文件常用配置项

| 配置项 | 默认值 | 介绍 |
| --- | --- | --- |
| `HWADDR` | 无 | 设备硬件地址有如下格式的一个 12 字节的十六进制列表 `AA:BB:CC:DD:EE:FF`。 |
| `ONBOOT` | `yes` | 值表示是否在启动时激活网络接口（或者该配置文件是否能够自动连接），可以如下值：<br>—`yes`—是<br>—`no`—否 |
| `BOOTPROTO` | `none` | 接口 IPv4/IPv6 参数配置方法。可以如下值：<br>—`none`/`static`—手动配置此主机网络<br>`dhcp`—使用 DHCP 配置此主机网络。 |
| `DNS1`, `DNS2`, ... | 无 | DNS 服务器的 IP 地址列表，只有前 3 个以下 `DNS1-3` 是生效的。 |
| `DOMAIN` | 无 | 搜索域列表。 |
| `IPADDR`, `IPADDR1`, `PREFIX1`, ... | 无 | 静态 IP 地址和子网码列表：接口可以配置多个 IP 地址，例如：<br>`IPADDR=10.5.5.23`<br>`PREFIX=24`<br>`IPADDR=1.1.1.2`<br>`PREFIX=16` |
| `GATEWAY` | 无 | 网关 IP 地址。 |
| `PEERDNS` | 无 | 是否通过 DHCP 服务器获取的或者静态的 DNS 信息写入系统 DNS 的全局配置文件 `/etc/resolv.conf`，可以如下值：<br>—`yes`—是<br>—`no`—否 |
| `DEFROUTE` | 无 | 是否将网络接口作为路由的默认路由，可以如下：<br>—`yes`—是<br>—`no`—否 |
| `DEVICETYPE` | 无 | 表示此连接接口的类型，此处仅应用到该接口上，如使用该配置项指定设备，那么该配置文件可以应用到任意适配的接口上。 |
| `DEVICE` | 无 | 表示此连接接口的名称。 |
| `IPV6INIT` | 无 | 表示是否配置 IPv6 网络参数，可以如下值：<br>—`yes`—是<br>—`no`—否 |
| `NM_CONTROLLED`(*) | `yes` | 表示此网络接口是否允许 NetworkManager 进行配置，可以如下值：<br>—`yes`—是<br>—`no`—否 |
| `PEERROUTES`(*) | `yes` | 是否从 DHCP 服务器获取用于定义的路由的默认路由信息的条目，可以如下值：<br>—`yes`—是<br>—`no`—否 |
| `IPV4_FAILURE_FATAL`(*) | 无 | 当 IPv4 和 IPv6 配置都可用时，IPv4 配置失败时视为设备激活，可以如下值：<br>—`yes`—是<br>—`no`—否 |
| `NAME`(*), `UUID`(*) | 无 | 用户易读的连接名，往往也对应配置文件 `ifcfg` 的后续连接所对应的配置文件的全局唯一标识。 |

## 8.3 知识点 resolv.conf and hosts

在本节中，将介绍两个网络相关的系统全局配置文件。这两个文件都与域名解析相关，分别是 `/etc/resolv.conf` 文件和 `/etc/hosts` 文件。

### 1. resolv.conf 文件

`/etc/resolv.conf` 是 DNS 客户端配置文件，用于设置 DNS 服务器的 IP 地址和 DNS 域名，还可以包含主机名的搜索列表。其格式非常简单，每行一个配置项开头，后接一个或多个带有空格的值，其配置项如表 8-15 所示。

#### 表 8-15 resolv.conf 配置项

| 配置项 | 值 |
| --- | --- |
| `nameserver` | DNS 服务器 IP 地址。其中，域名服务器是按照文件中顺序查询的，且只有当第一个 `nameserver` 没有响应时才查找下面的 `nameserver`，最多配置 3 个 `nameserver`。 |
| `domain` | 指定本地主机名。`domain` 默认为主机名中的域名部分，如果主机名中不包含域名，那么默认就是“.”作为其默认值。许多应用程序需要用到本地名。 |
| `search` | 表示查询的搜索列表。`search` 的值是域名指定的本地主机名，也可以指定域名为主主机名解析。域名之间用空格隔开。当查询的主机名在 DNS 查询时，会在该列表中加上主机名如 `nmbdsdev.cn`，变成 `ping.nmbdsdev.cn`。 |

其中主要的是 `nameserver` 配置项，其他配置项都是可选的。清单 8-56 所示一个 `/etc/resolv.conf` 的内容。

#### 清单 8-56

```
domain nmbdsdev.cn #指定本地主机名nmbdsdev.cn
search nmbdsdev.cn intranet.nmbdsdev.cn #指定的两个主机名
nameserver 172.18.14.1
nameserver 172.18.14.2 #指定的两个 DNS 服务器地址
```

> **注意**
>
> * 在 NM 网络管理时，`/etc/resolv.conf` 中的内容可能是由 NM 在开机时自动生成的，其中的域名值会来自本地/主机名指定主机名中的域名；`nameserver` 值会来自本地接口配置的 DNS 值或来自 DHCP 指定。
> * 建议修改配置的 DNS 或主机名之前来修改 `/etc/resolv.conf`。

如果想进一步了解 `/etc/resolv.conf` 文件更新更详细的信息，可以通过 `man 5 resolv` 查看该文件的文档。

### 2. hosts 文件

`hosts` 文件是 RHEL/CentOS 使用在本地快速解析 IP 地址与域名之间的文件，负责将主机名映射到相应的 IP 地址。`hosts` 文件通常用于补充或小型网络中 DNS 的功能，用户可以直接对 `/etc/hosts` 文件进行控制。

一般情况下，`hosts` 文件的每一行代表一个主机，由 3 个字段组成，每部分都空格隔开，格式如清单 8-57 所示。

#### 清单 8-57

```
ip 地址  主机名/域名（主机名别名，该字段可以省略）
```

在默认情况下，`/etc/hosts` 包含两行，分别为指定 IPv4 网络中环接口的主机（默认 `localhost`），如清单 8-58 所示。

#### 清单 8-58

```
127.0.0.1 localhost
::1 localhost
```

> **注意**
>
> 在执行 DNS 查询时，`/etc/hosts` 文件的优先级高于 DNS 服务器，即先本地 `/etc/hosts` 文件查询，如果找不到再 DNS 服务器请求。

下面出一个 `/etc/hosts` 文件的范例，如清单 8-59 所示。

#### 清单 8-59

```
127.0.0.1 localhost
::1 localhost
```

## 8.4 任务

完成了本次任务，应对 CentOS 中的硬盘、分区和文件系统有一些了解。现在你能够：

- 部署并启用 NetworkManager (NM)。
- 查看网络接口状态和详情。
- 激活和断开设备。
- 为网络设备创建默认路由。
- 修改主机名。
- 使用 `ip` 命令查看网络属性。

同时你应该已经了解相关知识：

- NM 相关概念。
- 连接、接口的概念。
- 命令行用于配置和接口设备。
- DHCP 的基本概念。
- IP 地址、默认网关、DNS 服务器和默认路由。

# 9 管理软件

## 任务场景

这次任务是要为 PC 安装测试需要的软件。在前面的任务中，你已经使用了 `yum` 安装了一些软件，但对于如何管理软件并没有一个认知，希望通过这个任务，学习一下 CentOS 管理软件的知识，为以后解决软件相关问题打下基础。接下来一起完成软件的任务，同时掌握 CentOS 中的软件包概念、原理和命令。

### 9.1 任务介绍

任务需求明确，为了 PC 安装表 9-1 所示的 5 个开发软件。你要通过不同的方法来完成，积累软件管理知识和技能。

| 序号 | 软件名 |
| --- | --- |
| 1 | `finger` 命令 |
| 2 | `gnuplot` |
| 3 | Python 环境 |
| 4 | Sublime Text 编辑器 |
| 5 | MPlayer 播放器 |

### 9.2 任务实施

#### 9.2.1 RPM软件包安装

RPM (Red Hat Package Manager) 是 Linux 中使用最广泛的软件包管理器，最早由红帽开发和维护，现在由开源社区维护。RPM 目前是 Linux 标准的管理系统，也是 RHEL、CentOS、Fedora、OpenSUSE 等发行版本中默认的软件管理器。首先，需要获取这些软件的 RPM 软件包，后面详细说明 `rpm` 命令。

> **注意**
>
> 下载 RPM 软件包有如下 3 种途径：
>
> - 可以从官方网站获取，但官方网站可能会提供源码或 `yum` 源，很少直接 RPM。
> - 可以到 `rpmfind` 网站下载。
> - 可以到 CentOS、Fedora、EPEL、rpmfusion 软件仓库镜像站查询，在国内可以使用阿里云镜像、网易镜像站或者清华大学镜像站。

对于初学者，可以尝试在 `rpmfind` 网站下载 RPM 包：打开 `rpmfind` 网址，在首页直接搜索。根据操作系统的版本，在其中选择版本的 RPM 包。这里选择 `x86_64` 版本，单击接受并安装，将软件下载到本地磁盘上。也可以用 `wget` 工具下载。

#### 清单 9-1 安装

```
wget https://rpmfind.net/linux/fedora/releases/29/Everything/x86_64/Packages/f/finger-0.17-63.fc29.x86_64.rpm
```

下载的安装包名为 `finger-0.17-63.fc29.x86_64.rpm`。下载完成后，使用的命令就是 `rpm`。首先加上 `-q` 选项查询系统中是否安装了 `finger`，如果没有任何输出，则表示未安装。

#### 清单 9-2 查询

```
rpm -q finger
```

> 用 `rpm` 命令安装软件时，发现已经安装了该版本的软件，且该版本被其他软件依赖或独占。如果是该版本，`rpm` 命令将无法覆盖或更新。如果没有发现 `finger`，就可以开始安装。安装需要更改权限，先切换到 `root` 用户，用 `rpm` 命令加上 `-ivh` 选项。其中 `-i` 表示安装；`-v` 表示详细信息；`-h` 表示安装进度。

#### 清单 9-3 安装

```
$ su
rpm -ivh finger-0.17-63.fc29.x86_64.rpm
警告：finger-0.17-63.fc29.x86_64.rpm: 头V3 RSA/SHA256 Signature, 密钥 ID 9d2b6f1: NOKEY
准备中...
正在安装...
######################################## [100%]
1:finger-0.17-63.fc29######################################## [100%]
```

运行到 100%，安装完成了。但是在安装过程中，`rpm` 命令给出了一个警告，可能是下载的 GPG 签名与系统中现有的 GPG 钥不同。简单来说，该警告表示该包并非 CentOS 官方颁发的。

> - GPG 签名是一种 RHEL/CentOS 下的安全机制，用于确保安装软件的完整可靠性。
> - 在生产环境中安装这个包（如网络下载的软件包），不要轻易忽略。
> - 解决方法是找到软件包发行者的 GPG 钥，导入系统。

查询 `finger` 是否安装。

# 任务 9 管理软件

如果软件包未安装或有更新，那么就开始查找软件并解析软件的依赖性，输出：`yum` 在名为 `updates` 的仓库中找到了 Python 和其依赖的 `python-libs` 这两个软件包，并确定了下载大小。在回复“Y”同意下载事后，它会下载这两个软件包，安装后，就会显示“完成”字样，表示软件包已经安装成功了。

## 注意

- 严格来说，这里使用的是 `yum` 的客户端，下载安装的软件包都来自 `yum` 的服务器，也是 `yum` 软件仓库。

所谓“软件仓库”其实是一个本地目录，包含了软件包和索引文件。`yum` 可以在仓库中定位并找到正确的 RPM 软件包。

CentOS 默认的软件包安装版本如下：

- Base: CentOS 的软件包，发行版上的内容相同。
- Updates: Base 中软件包的更新版本。
- Extras: 其他附加的软件包。

接下来用 `yum` 来安装最后一个软件包，若不意外，`yum` 会显示如清单 9-9 所示的信息。

# 清单 9-9

```bash
# yum install mplayer
没有软件包 mplayer。
错误：无须任何处理
```

非常简单：在 CentOS 中，`yum` 默认的软件源是 CentOS 的官方软件仓库，官方的软件仓库中没有 MPlayer 这个软件，所以需要添加包含 MPlayer 的 `yum` 仓库才能安装了。

## 注意

CentOS 官方软件仓库中，由于版权协议和稳定性考虑，排除了很多的软件，如 MPlayer、Eclipse 等。

## 9.2.3 添加 yum 软件仓库

要添加一个 `yum` 软件仓库，必须在系统的 `/etc/yum.repos.d/` 目录下创建一个仓库的描述文件。该文件指定扩展名为 `.repo` 扩展，此通常也被称为 repo 文件。

一个在 `yum` 配置文件中定义了多个仓库，其中内容是每个仓库的位置，也意味着将读取到仓库中的软件包和其他相关信息（在本书的知识点 3 中将对 repo 文件进行更详细说明）。

仓库维护者会在网站上公布仓库的 repo 文件和对应的校验该仓库 RPM 签名的 GPG 公钥。添加一个软件包简单的方法就是将仓库的 repo 文件下载到系统的 `/etc/yum.repos.d/` 目录下，然后用 GPG 公钥命令导入系统。

## 注意

依靠仓库维护者一有机会提供添加该仓库的具体说明，如果没有，则按照说明来。

本任务要安装的 Sublime Text 在官方网站上提供了软件的 `yum` 仓库，且给出了具体添加说明，如图 9-5 所示。因此，这里按照该说明为 `yum` 添加 Sublime Text 的软件仓库，如清单 9-10 所示。

# 清单 9-10

```bash
# rpm -v --import https://download.sublimetext.com/sublimehq-rpm-pub.gpg
# yum-config-manager --add-repo https://download.sublimetext.com/repo/stable/x86_64/sublime-text.repo
正在添加仓库来自: https://download.sublimetext.com/repo/stable/x86_64/sublime-text.repo
正在抓取文件 http://download.sublimetext.com/repo/stable/x86_64/sublime-text.repo 到 /etc/yum.repos.d/sublime-text.repo
```

图 9-5 Sublime Text 官网上的 repo 添加说明

其中用命令 `rpm --import` 导入 GPG 公钥（`rpm` 的用法包含本任务的知识点 2），接着用 `yum-config-manager --add-repo` 命令引入 repo 文件（`yum` 的用法包含本任务的知识点 4）。接下来就可以用 `yum` 安装 Sublime Text 了，如清单 9-11 所示。

# 清单 9-11

```bash
# yum install sublime-text
```

安装完成后，可以在“应用程序”→“编程”菜单中找到 Sublime Text（如图 9-6 所示），点击打开即可。

图 9-6 从菜单中打开 Sublime Text

# 任务 9 管理软件

接下来，安装 MPlayer。该软件在 RPM Fusion 仓库中有收录，为此添加 RPM Fusion 的软件仓库。首先，打开 `rpmfusion` 官方网站，网站中提供了便于添加仓库的 RPM 软件包。

## 注意

仓库维护者会在网站上提供一个 RPM 安装包，供用户快速安装仓库版本并按照其安装和配置添加 RPM Fusion 的软件仓库。系统使用的是 CentOS 7，因此按照“RHEL 7 or compatible CentOS”下列的指南完成（如清单 9-12 和图 9-7）。

# 清单 9-12

```bash
# sudo yum localinstall --nogpgcheck https://download.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm https://download.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-7.noarch.rpm
```

## 注意

`localinstall` 在 `yum` 中已经被废弃（可用但不建议使用），一般用 `install` 替代。在执行完毕后，系统中添加了 3 个软件仓库 `rpmfusion-free`、`rpmfusion-nonfree`，具体见表 9-2。

# 表 9-2 rpmfusion 各仓库介绍

| 仓库名称 | 介绍 |
| :--- | :--- |
| `rpmfusion-free` | 该仓库均为开源软件，由于其他原因未收录到 RHEL 或 Fedora 的官方仓库。 |
| `rpmfusion-nonfree` | 该仓库的软件包并非开源，且由于其他原因未收录到 RHEL 或 Fedora 的官方仓库。 |
| `epel` | 该仓库是 EPEL 的仓库，rpmfusion 依赖于该仓库。 |
