
我将在第 5 章中详细介绍整体 DHCP 配置，但在在这里我让 DHCP 回答对 `10.1.1.0/255.255.255.0` 子网的查询。我列出了网络上的两个 DNS 服务器以及要使用的路由器。`dynamic-boot` 行定义了此 DHCP 服务器将分配的 IP 地址范围。在这种情况下，我将分配 `10.1.1.50` 到 `10.1.1.99` 之间的地址。`next-server` 行配置了 TFTPD 使用的 IP 地址，以便任何通过 PXE 启动的主机通过 TFTPD 获取其启动加载程序（在本例中为服务器）。`filename` 告诉它要检索的文件名。关于这将在下一节中详细介绍。

显然，调整此示例配置以匹配你特定网络的设置，然后输入 `sudo service dhcp3-server start` 启动 DHCP 服务器。你应该看到：

```
$ sudo service dhcp3-server start
# Starting DHCP server dhcpd                                     [OK]
```

如果服务因为配置文件中的错误未能启动，你应该会在屏幕输出上看到对该错误的引用。在 `dhcpd.conf` 文件中追踪该行，并寻找行尾缺失的分号或你可能犯的任何语法错误。

## TFTP

一旦设置好 DHCP 服务器，下一步是安装 TFTP-server：

```
$ sudo apt-get install tftpd-server
```

TFTP 的配置文件位于 `/etc/tftpd.conf`。默认情况下，它从 `/var/tftp` 提供文件。你应该确保该目录存在并具有正确的权限：

```
$ sudo mkdir -p /var/tftp
sudo chmod 777 /var/tftp
```

现在 TFTP 服务器准备好了，我们需要将 PXE 启动文件移动到 `/var/tftp` 目录。我们将使用之前下载的 tarball 来提取文件。

## 配置 Pelinux

虽然我之前提供的示例是一个很好的起点，但当你想要自动化服务器安装时，你最终需要设置一个 PXE 启动服务器来管理此过程。毕竟，你真的想手动去每台新服务器并插入 CD-ROM 吗？如果你的服务器在另一个大陆，或者你有 200 台服务器要安装呢？通过 PXE 启动部署，你的新服务器将从网络启动，从 PXE 服务器下载镜像，然后开始安装过程——全部通过网络完成。

Ubuntu tarball 的很棒的一点是它为你设置了一个良好的 PXE 启动环境，带有菜单，大部分工作已经为你完成了。你只需要调整默认设置使其指向你的 Kickstart 文件。用你喜欢的文本编辑器打开 `/var/tftpboot/ubuntu-installer/i86/casper/precfg`，你会看到以下行：

```
default install
label install
menu default
```

此 tarball 包含了 `pxelinux.0` 二进制文件以及位于 `ubuntu-installer` 目录下的 `pxelinux.cfg` 配置文件。当 pxelinux 加载时，它会查找名为 `default` 的文件并使用它。

### PXE 启动服务器部署 115

```
kernel ubuntu-installer/i386/linux
append vga=normal initrd=ubuntu-installer/i386/initrd.gz --
quiet
label cli
```

```
menu label ^Command-line install
kernel ubuntu-installer/i386/linux
append tasks=standard pkgsel/language-patterns-
pkgsel/install-language-support-vga=normal initrd-ubuntu-
installer/i386/initrd.gz -- quiet
```

默认行（`default`）表示，如果用户在启动提示符处按回车，将加载标记为 `install` 的部分。`label install` 部分定义了用户可以选择的特定配置。每个部分都以 `label` 开始，定义了另一种配置。当你查看此配置文件时，你会看到已经为你设置了许多不同的标签。你可以通过在启动提示符处输入特定标签并按回车，在不同部分之间进行选择。虽然我可以直接按回车来选择上方标记为 `install` 的部分（因为它是默认设置），但我也可以在启动提示符处输入 `install` 并按回车。

我们所需要的更改默认启动选项，使其也指向我们的 Kickstart 文件。为了做到这一点，我只需将我的选项添加到 `append` 行中。文件的开头部分从这样变为如下所示：

```
default install
label install ^Install
menu default
kernel ubuntu-installer/i386/linux
append vga=normal initrd=ubuntu-installer/i386/initrd.gz --
quiet
```

```
default install
label install
menu label ^Install
menu default
kernel ubuntu-installer/i386/linux
append vga=normal initrd=ubuntu-installer/i386/initrd.gz
ks=http://10.1.1.5/ks.cfg -- quiet
```

保存更改并退出文本编辑器。Pselinux 现在已配置完成，你准备好进入最后一步了。

## Web

过程的最后一步是设置 Web 服务器来托管你的 Kickstart 文件、`preseed` 文件以及你可能有的任何自定义脚本。首先安装 `apache2` 包，它将提供你的 Web 服务器软件及其所有必要的依赖项：

```bash
$ apt-get install apache2
```

`apache2` 包将自动设置并启动一个默认目录为 `/var/www` 的运行 Web 服务器。我在这里不会涵盖 Apache 的任何高级配置，因为我们只需要一个 Web 服务器来托管几个文本文件。此时，你需要做的是将你的 `ks.cfg` 文件移动到此服务器的 `/var/www` 下。你只需要为 PXE 启动制作一个 `ks.cfg` 文件。由于我们不会从 CD-ROM 下载文件，我们需要告诉 Kickstart 文件从 Ubuntu 镜像获取文件，因此请找到并修改读取这一行：

```
cdrom
```

修改为：

```
url --url http://us.archive.ubuntu.com/ubuntu
```

> 注意：由于此服务器将直接从 Ubuntu 镜像拉取所有软件包，安装时间无疑会比从 CD-ROM 安装长。如果你计划进行大量的自动化 Ubuntu 安装，可能想要考虑设置自己的 Ubuntu 归档镜像。

在继续之前，尝试通过 Web 浏览器或使用如 `wget` 的工具访问你的 `ks.cfg` 文件，确保 Apache 正在提供该文件。如果你无法访问该文件，请检查 `/var/log/apache2/error.log` 中的 Apache 错误日志寻找可能错误的线索，并检查 `ks.cfg` 的权限以确保它是全局可读的。如果不是，输入 `chmod+r ks.cfg` 使变得可读。

## 测试你的 PXE 服务器

此时，你应该准备好通过新安装来测试你的 PXE 服务器。关于如何设置服务器进行 PXE 启动，并没有单一的指令。

### PXE 启动服务器部署 117

在某些服务器上，只需按下功能键获取启动选项列表并选择网络启动。在其他服务器上，你需要进入 BIOS 并更改启动顺序。还有一些服务器提供一个可以自动网络启动的功能键。你需要研究如何让你的特定服务器进行网络启动，并确保它与你的 PXE 启动服务器处于同一个子网。

一旦你的服务器通过 PXE 启动，你将看到如图 4-3 所示的 Ubuntu 。由于我们设置了默认标签使用我们的 Kickstart 选项启动，我们只需要按回车即可。

> 注意：即使这种自动化安装也需要一些用户交互，你至少需要在每次启动提示符处按回车来开始安装。从某种意义上说，这是一种安全机制，因为如果六个月后你的某一台服务器重启并进行网络启动会怎样？如果完全是自动化的，该服务器将重新开始安装并可能覆盖其所有当前文件——这可能是一件非常糟糕的事情。对于某些组织来说，这种行为是理想的（特别是对于相同机器的大集群）。它们将机器分在不同的部门，这样除非它们想连接，否则网络就不会连接；如果连接了，它们绝对希望它执行重装。如果你想要一个除了开启服务器外不需要用户交互的 100% 自动化安装（这意味着它永远不会超时），只需将数字改为 1，任何启动并获取该配置文件的服务器都将在一次性超时后自动加载默认标签。

![](img/4615e4cf34951)

图 4-3：Ubuntu PXE 启动菜单

## 自定义安装

在部署方面，一种方案并不适用于所有人。另一种区分不同安装类型的实用方法是使用“快捷代码”（cheat codes，我借用了 Knoppix 的名称）。快捷代码是你你在命令行输入的选项，它会被传递给系统。启动提示符的有趣之处在于，提示符上的所有内容在安装过程中都可以通过 `/proc/cmdline` 文件访问。如果你想创建自定义快捷代码，你只需要提供一个

这是一种安装前或安装后的脚本，它可以解析 `/proc/cmdline` 并这些设置存储在环境变量中。然后你可以在脚本中引用这些环境变量，并根据它们对安装前或安装后的过程进行自定义更改。

例如，假设我们在启动提示符处定义了两个调试代码：`type`，用于标记服务器类型（Web、MySQL、DNS），以及 `myraid`，告知系统是否应该使用 RAID。与其设置三个不同的 Kickstart 文件，我可以使用单个 Kickstart 文件，在其安装前脚本中编写逻辑来解析这些选项并据此更改设置。这里是一个安装前脚本示例，它可以解析 `/proc/cmdline` 文件，设置环境变量，并根据它们执行特殊操作。

```
%pre
for i in `cat /proc/cmdline`; do
  echo $i | grep -iq MYTYPE=
  if [ $? -eq 0 ]; then
    export MYTYPE=`echo $i | awk -F=" '{print $2;}'`
  fi
  echo $i | grep -iq MYRAID=
  if [ $? -eq 0 ]; then
    export MYRAID=`echo $i | awk -F=" '{print $2;}'`
  fi
done
```

```
if [ $MYTYPE == "web" ]; then
  # 修改 web 服务器的预设设置
elif [ $MYTYPE == "mysql" ]; then
  # 修改 mysql 服务器的预设设置
elif [ $MYTYPE == "dns" ]; then
  # 修改 dns 服务器的预设设置
fi
```

```
if [ $MYRAID ]; then
  # 修改 RAID 的预设设置
fi
```

现在在启动提示符处，如果我想设置一个带有 RAID 的 MySQL 服务器，我可以输入 `install mytype=mysql myraid=1`。同样，这种方法的优势是它允许你维护单一 Kickstart 文件，其中包含更改特定服务器类型设置的逻辑。这种方法的缺点是，随着时间的推移，生成的 Kickstart 文件可能会变得非常大且复杂。

## DHCP 选择

如果你的组织为服务器租用或使用静态 DHCP 分配，这种方法非常有效。在静态 DHCP 租用下，DHCP 服务器会在每次自动启动时或根据主机的 MAC 地址为每个请求 IP 地址的主机分配 IP。通常在这种设置下，你的服务器每当从网络启动时都会自动安装新镜像。你会发现这种方法在大规模集群或服务器在获取操作系统之前已进行物理安装的环境非常流行。一旦你更改 pxelinux 配置以自动安装默认镜像，你的 DHCP 配置文件将控制每台服务器。管理员要在服务器上安装 Ubuntu，只需将其连接到网络并开启电源即可。

在这种情况下，你在 `/var/lib/tftpboot` 下创建多个目录，每个目录都包含 `netboot.tar.gz` 的解压副本。如果我想为 Web、MySQL 和 DNS 服务器设置三个独立的配置，我会执行以下操作：

```
$ cd /var/lib/tftpboot
$ sudo wget
http://archive.ubuntu.com/ubuntu/dists/hardy/main/installer-i386/current/images/netboot/netboot.tar.gz
$ sudo mkdir mysql dns
$ cd web
$ sudo tar -xvf netboot.tar.gz
$ cd ../mysql
$ sudo tar -xzvf netboot.tar.gz
$ cd ../dns
$ sudo tar -xzvf netboot.tar.gz
```

现在，我会更改这些子目录下的 `pxelinux.cfg/default` 文件以反映我想更改的任何特殊设置。此外，如果我想让安装完全不需要用户交互，我会编辑 `pxelinux.cfg/default` 配置并将 `TIMEOUT` 值设置为 `1`，这样在一秒后它将自动启动安装过程。再次，如果你使用这种方法，请采取适当措施，防止机器意外网络启动并覆盖其设置。

一旦设置了 TFTP 服务器，大部分配置将在 DHCP 服务器上完成。我需要修改 `/etc/dhcp3/dhcpd.conf` 文件，根据哪个 MAC 地址请求租用，将其指向这些子目录中的特定 Linux 文件。对于每个 MAC 地址，我会添加一个独立的部分。下面我添加了三个特定的服务器，分别指向 Web、MySQL 或 DNS 配置：

```
host web1 {
  hardware ethernet 00:0c:cc0:ff:ee:00;
  option host-name "web1"
  fixed-address 10.1.1.101;
  filename "/web/pxlinux.0"
}
host mysql1 {
  hardware ethernet 00:0c:cc0:ff:ee:01;
  option host-name "mysql1"
  fixed-address 10.1.1.101;
  filename "/mysql/pxlinux.0"
}
host dns1 {
  hardware ethernet 00:0c:cc0:ff:ee:02;
  option host-name "dns1"
  fixed-address 10.1.1.101;
  filename "/dns/pxlinux.0"
}
```

这种方法的主要缺点是，需要在 TFTP 服务器上维护多个 pxlinux 配置文件。另一个缺点是，在安装任何内容之前必须查询每台服务器的 MAC 地址。

# DNS 服务器 127

`91.189.94.8.` DNS 服务器维护着一个对其拥有权威性的名称和 IP 地址的本地目录，因此，如果你向 DNS 服务器查询它对其拥有权威性的名称的 IP 地址，它通常会返回该答案。许多 DNS 服务器还提供递归查询。通过递归查询，DNS 服务器本身可能不包含你正在寻找的记录，但正如你所知道，它可以连接互联网并为你找到答案。

在 Ubuntu 上有许多提供 DNS 服务的程序，但最常用的一直以来都是 BIND——BIND，BIND 是 Berkeley Internet Name Domain（伯克利互联网命名域）的缩写，它具有许多高级功能，但许多功能通常伴随着更复杂的配置文件。老实说，让大多数管理员感到困惑的仅仅是从零开始构建 BIND 服务器，但正如你将看到的，Ubuntu 已经替为你完成了这些最繁重的工作。

## 安装 BIND

在 Ubuntu 下有几种方法安装 BIND。在初始安装 Ubuntu 期间，你可以从服务器类型列表中选择 DNS Server。如果你已经安装了 Ubuntu，可以使用 `sudo tasksel` 进入相同的菜单。一旦你选择了 DNS Server 并点击 OK，`bind9` 和 `bind9-doc` 包将自动为你下载并安装。或者，你也可以直接运行

```
$ apt-get install bind9 bind9-doc
```

你将发现（这也是我接下来要详细介绍的内容）是，一旦安装了 Ubuntu BIND 包，你实际上就已经拥有了一个完全配置并可以正常运行的名称服务器，至少可以作为递归查询的缓存名称服务器。示例配置文件、根区域文件、本地区域甚至 rnd 密钥都已经为你配置好了。

## Ubuntu 约定

Ubuntu 的 BIND 使用了一些关键文件约定，取决于你使用过哪些其他 Linux 发行版，这些可能与你习惯的有所不同。以下是 Ubuntu 的关键文件位置：

- `/etc/bind/`

此目录包含名为 `named.conf` 的 BIND 主配置文件，以及任何单独的区域文件。任何新的主区域文件也应该存储在此目录中，或者如果你有许多区域文件想要组织，可以存储在 `/etc/bind` 下的子目录中。

- `/etc/bind/named.conf`

这是 BIND 的主配置文件，你在此处更改 BIND 的选项和行为。BIND 的所有单独区域文件（包含名称和 IP 信息的文件）也在此处引用。BIND 中启用的主要选项包含在一个名为 `/etc/bind/named.conf.options` 的单独文件中。

- `/etc/bind/db.*`
