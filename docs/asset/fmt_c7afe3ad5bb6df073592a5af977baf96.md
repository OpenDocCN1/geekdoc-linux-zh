
```
xconfig --card="NVIDIA GeForce FX (generic)" --videoram=131072 \
        --hysync=31.5-37.9 --vysync=50-70 --resolution=800x600 \
        --depth=16 --startxonboot --defaultdesktop gnome
```

对于大多数现代硬件，您不需要设置这两个命令中的任意一个，因为 Fedora 在大多数情况下会自动配置显卡和显示器。

可选的 `network` 命令允许您配置 Fedora 系统到网络的网络接口。示例告诉您的计算机从 DHCP 服务器获取其 IP 地址和相关网络信息（`--bootproto dhcp`）。如果您想分配特定的 IP 地址，请使用 `--bootproto static` 选项。然后根据系统需求更改 IP 地址（`--ip`）、子网掩码（`--netmask`）、网关的 IP 地址（`--gateway`）以及 DNS 服务器的 IP 地址（`--nameserver`）。您还可以添加主机名（`--hostname`）。

> **注意：** 尽管 `network` 值似乎分三行显示，但所有值必须在同一行上。

```
network --device eth0 --bootproto dhcp
```

或者

```
network --device=eth0 --bootproto static --ip=192.168.0.1 \
        --netmask 255.255.255.0 --gateway 192.168.0.1 \
        --nameserver 192.168.0.254 --hostname duck.example.com
```

同样，对于大多数现代硬件，通常不需要 `network` 命令。

`rootpw` 命令将密码设置为紧随其后的单词（在下面的示例中为 `password`）。让这个密码处于明文状态是一个安全风险，因此您应该在 Linux 安装完成后更改此密码（使用 `passwd` 命令）。您也可以选择添加加密后的密码（`--iscrypted`）。

```
rootpw password
```

或者

```
rootpw --iscrypted                (line continues...)
$6$NtBq.5029fdfd412699$GfCCHdJEdPbgdc3.T/0e3hqNmqr1wMR/fYsd6rErFI3j0/dfGnOAS9QLj6nvb47PHjN.0UWZV3Ect.X3Md8B3jjJ1/B.
```

`firewall` 命令允许您设置 Fedora 系统使用的默认防火墙。默认值为 enabled（如果防火墙已开启）。您也可以将防火墙设置为 disabled（没有防火墙）。（这些值在本章前面介绍安装过程时有过说明。）如示例所示，您可以选择指示在特定接口上没有来自主机计算机的限制（`--trust eth0`）。您还可以允许单独的服务（`--service=ssh`）或特定的端口：协议对（`--port 1234:udp`）。

```
firewall --enabled --trust=eth0 --service=ssh --port=1234:udp
```

必需的 `authconfig` 命令设置用于保护用户密码的身份验证类型。`--enablashadow` 选项启用 `/etc/shadow` 文件来存储您的密码。`--passalgo=sha512` 选项启用基于 SHA512 的密码加密。（通常两个选项会一起使用。）

```
authconfig --enablashadow --passalgo=sha512
```

`selinux` 命令指示是否启用安全增强型 Linux（Security Enhanced Linux）。以下行显示其处于启用并强制状态：

```
selinux --enforcing
```

`timezone` 命令为 Linux 系统设置时区。此处显示的默认值为美国，纽约（`America/New_York`）。`--utc` 选项指示计算机的硬件时钟设置为 UTC 时间。如果您没有设置时区，则使用 US/Eastern。

```
timezone --utc America/New_York
```

`bootloader` 命令设置引导加载程序的位置（默认为 GRUB）。例如，`--location=mbr` 将 GRUB 添加到主引导记录。（使用 `--location=none` 可避免添加 GRUB。）`driveorder` 选项描述首先查找主引导记录的硬盘。您还可以使用 `append` 选项（`--append hdd=ide=0`）在启动时读取内核选项，或使用可选的 GRUB 密码（`--password=GRUBpassword`）。

```
bootloader --location=mbr --driveorder=sda --append="rhgb quiet" --password=GRUBpassword
```

## 分区与软件包

分区是新安装所必需的，对于升级则是可选的。下面的代码示例来自 `ks.cfg` 文件。`clearpart --linux` 值用于移除第一块硬盘（`--drive=sda`）上现有的 Linux 分区（或使用 `--all` 清除所有分区）。`part /boot`、`/` 和 `swap` 为每个分区分配设置文件系统类型（`-fstype`）和分区名称（`onpart`）。你还可以设置分区大小（`-size`）为所需的兆字节数。你也可以为分区创建卷组（`volgroup`）和单个逻辑卷（`logvol`）条目。如果你想使用这些命令，需要取消注释最后四行。

```
# The following is the partition information you requested
# Note that any partitions you deleted are not expressed
# here so unless you clear all partitions first, this is
# not guaranteed to work

#clearpart --linux --drive=sda
#part /boot --fstype ext3 --size=100 --ondisk=sda
#part / --fstype ext3 --size=700 --grow --ondisk=sda
#part swap --size=128 --grow --maxsize=256 --ondisk=sda
```

要指示安装哪些软件包，请使用 `$packages` 命令开始一个章节。（下面有几个示例。）可以指定整个安装组、单个组或单个软件包。在 `$packages` 行中，你可以指示是否通过安装由你选中的软件包所需的依赖项来解决依赖关系（`--resolvedeps`）。在 `$packages` 之后，使用 `@` 符号开始一个软件包组条目，并将每个单独的软件包名称放在单独的一行上。这里是一个示例：

> **提示：** 你可以在 Fedora 安装 DVD 上找到软件包组和单独软件包的列表。在 `repodata` 目录中找到 `comps.xml` 文件。然而，如果你从安装 Fedora 后生成的 `anaconda-ks.cfg` 文件开始，你可能已经拥有一组想要安装的软件包。

```
$packages --resolvedeps
@base
@editors
@games
@graphical-internet
@kde-desktop
@office
@sound-and-video
.
.
.
xfdsprgs
mttools
samba
-nano
@gimp
@nupkg2
$end
```

注意：`*packages*` 命令不支持升级。在升级期间安装新软件包的最佳替代方法是将必要的命令添加到 `*post*` 部分。这完全模拟了你在升级后手动执行的操作，但它是自动进行的。

`*post*` 命令启动安装后部分。之后，你可以添加任何要在安装完成后运行的 shell 命令。一件有用的事情是为安装期间想要添加的用户添加 `useradd` 命令。你还可以使用 `usermod` 命令来添加用户的密码。（关于创建加密密码的信息，请参见第 21 章。）注意，默认情况下没有 `*post*` 部分。

```
*post*
/usr/sbin/useradd jake
chfn -f 'John W. Jones' jake
/usr/sbin/usermod -p '$1$kQUMYbF0qh79wBCxnTuaH.' Jake
```

此时，你应该拥有一个可用的 `ks.cfg` 文件。

### 安装 kickstart 文件

一旦创建了 `ks.cfg` 文件，你需要将其放置在执行安装的计算机可以访问的位置。通常，你会将该文件放置在网络上可访问的计算机或硬盘上。你也可以将文件放置在软盘或 CD 上。

要将文件复制到软盘，创建一个 DOS 软盘并如下复制文件：

```
# mcopy ks.cfg a:
```
