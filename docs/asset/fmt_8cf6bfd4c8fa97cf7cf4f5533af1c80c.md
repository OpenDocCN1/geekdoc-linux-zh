
将远程文件同步到你的本地系统。

运行 `rclone help` 获取完整的子命令列表。注意，你可以访问比我之前示例中更复杂的远程路径：

```
rclone copy remote:Photos/Vacation/picture.jpg .
```

## 有用选项

`-n` 预运行模式：不实际复制。仅显示将要执行的操作。

`-i` 交互式运行，在更改前会提示你。

# dd

`dd` [options]

`dd` 是一个底层的位和字节级拷贝器。它可以将数据从一个文件复制到另一个文件，例如从 `myfile` 复制到 `/tmp/mycopy`：

```
dd if=myfile of=/tmp/mycopy
2+1 records in
2+1 records out
1168 bytes (1.2 kB) copied, 0.000174074 s, 6.7 MB/s
```

它甚至可以在复制时进行数据转换，例如在从 `myfile` 复制到 `/tmp/mycopy` 时将字符转换为大写：

```
dd if=myfile of=/tmp/mycopy conv=ucase
```

`dd` 的功能远不止于复制文件。它可以直接从一个磁盘设备复制原始数据到另一个磁盘。这里有一个克隆硬盘的命令：

```
sudo dd if=/dev/device1 of=/dev/device2 bs=512 \
conv=noerror,sync OVERWRITES /dev/device2
```

或者，复制整个磁盘设备以创建一个 ISO 文件。确保输出文件位于不同的磁盘设备上，并且有足够的可用空间。

```
sudo dd if=/dev/device of=disk_backup.iso
```

## 警告

> `dd` 以超级用户身份运行时，如果你不小心，可能会在几钟内抹除你的硬盘。请务必双击输出文件（`of=` 参数）是你想要的文件。在以 root 身份尝试 `dd` 之前，请备份你的电脑并准备一个 Linux “Live”发行版以备不时之（见第 ix 页“书中有什么”）。

关于 `dd` 高级使用的优秀建议，请访问 `https://moil.ly/R3krx`。我喜欢的技巧是将磁盘的主引导记录（MBR，长度为 512 字节）备份到名为 `mbr.txt` 的文件中：

## 有用选项

`if=file` 指定输入文件或设备。

`of=file` 指定输出文件或设备。请双击确认它是正确的！

`bs=N` 一次复制 `N` 字节（“块大小”）（要为输入设置不同的块大小，请分别使用 `ibs` 和 `obs`）。

`skip=N` 在开始复制前跳过 `N` 块输入（大小为 `ib`）。

`seek=N` 在开始复制前丢弃 `N` 块输出（大小为 `obs`）。

`conv=spec` 转换正在复制的数据。`spec` 可以是 `ucase`（转换为大写）、`lcase`（转换为小写）、`ascii`（从 EBCDIC 转换为 ASCII）以及 man 手页中列出的许多其他。

# growisofs

`growisofs` [options] tracks

`growisofs` 命令用于刻录可写的 CD、DVD 或蓝光光盘。要将 Linux 目录的内容刻录到 Linux、Windows 和 macOS 系统可读的光盘上：

1. 运行以下命令找到你的刻录器设备：
   ```
   grep ^"drive name:" /proc/sys/dev/cdrom/info drive name: sr1 sr0
   ```
   可用设备为 `/dev/sr1` 和 `/dev/sr0`。

2. 将你想刻录的文件放入一个目录，例如 `dir`。按照你希望在光盘上的布局安排它们。目录本身不会被复制到光盘，只有它的内容。

3. 使用 `mkisofs` 命令创建一个 ISO（光盘）镜像文件，并使用 `growisofs` 将其刻录到光盘，假设你的设备是 `/dev/sr1`：
   ```
   mkisofs -R -l -o HOME/mydisk.iso dir
   growisofs -dvd-compat -Z /dev/sr1=$HOME/mydisk.iso
   rm $HOME/mydisk.iso
   ```

刻录音频 CD 请使用像 `k3b` 这样的友好图形程序。

# 网络命令

## 主机信息

- `uname` 打印基本系统信息。
- `hostname` 打印基本系统信息。
- `hostname` 打印系统信息。

每台 Linux 机器都有名称、地址和其他属性。以下是显示方法：

```
uname -a
```

`uname` 命令打印关于内核、内核版本、主机名和硬件架构的基础信息。要查看更多信息，请使用选项：

```bash
uname -a
```

输出包括内核名称、主机名、发布版本和硬件架构。

### 有用选项

- `-n` 打印节点名称。
- `-f` 打印完全限定名。
- `-d` 打印域名。
- `-a` 打印所有。
- `-m` 打印机器。
- `-p` 打印处理器类型。
- `-o` 打印操作系统。

## hostname

`hostname` [options]

`hostname` 命令打印电脑名称。通过 `hostname` 进行的更改在重启后可能失效。请查阅发行版文档以使更改永久，例如编辑配置文件。

### 有用选项

- `-s` 打印短名称。
- `-f` 打印完全限定名。
- `-d` 打印域名。
- `-a` 打印所有别名。
- `-I` 打印网络地址。
- `从文件设置 hostname`。

超级用户可以使用以下命令设置 hostname：

```bash
sudo hostname [new-hostname]
```

## ip

`ip` [options]

`ip` 命令显示并设置网络接口的各个方面。这个主题超出了本书的范围，但我将教你一些技巧。如果你知道接口名称，例如 `eth0`、`ens16`，使用此命令查看详情：

```
ip addr show eth0
```

输出示例：

```
2:eth0:<BROADCAST,MULTICAST,UP,LOWER_UP>
link/ether 00:50:ba:48:4f:ba ff:ff:ff:ff:ff
inet 192.168.0.21/24 scope global
inet6 fe80::21e:8c:53:e14/64 scope global
```

输出包括 IPv4 地址 (`192.168.0.21/24`)、IPv6 地址 (`fe80::21e:8c:53:e14/64`)、MAC 地址 (`00:50:ba:48:4f:ba`) 以及其他细节。如果你不知道接口名称，查看所有已加载的接口：

```bash
ip addr show | less
```

另一个命令 `ifconfig` 提供了与 `ip show` 类似的信息。它被认为过时，但你仍能在许多系统中找到它。

```
ifconfig eth0
ifconfig -a
```

- 一个网络接口的细节
- 所有网络接口的细节

使用以下 `ip` 命令（例如 `ip link help`）显示网络信息：

- `ip addr` 显示网络设备的 IP 地址。
- `ip madr` 显示网络设备的多播地址。
- `ip link` 显示网络设备的属性。
- `ip route` 显示路由表。
- `ip monitor` {监控你的网络设备；按 ^C 停止。
- `ip help` 显示所有这些命令的用法信息。

超级用户还可以使用 `ip` 配置网络设备、管理路由表和规则、创建隧道等。学习 `ip` 和相关工具（称为 `iproute2`）以及 `ip` 手页。

## ifconfig

`ifconfig` 命令显示网络接口信息。要查看特定接口，使用：

```bash
ifconfig eth0
```

要查看所有接口，使用：

```bash
ifconfig -a
```

注意：`ifconfig` 被认为过时。优先使用 `ip` 命令。

## ip addr

`ip` 命令显示并设置网络接口的各个方面。要查看特定接口，使用：

```bash
ip addr show eth0
```

要查看所有接口，使用：

```bash
ip addr show
```

输出如下：

```
2:eth0:<BROADCAST,MULTICAST,UP,LOWER_UP>

link/ether 00:50:ba:48:4f:ba ff:ff:ff:ff:ff

inet 192.168.0.21/24 scope global

inet6 fe80::21e:8c:53:e14/64 scope global
```

它们包括 IPv4 地址 (`192.168.0.21/24`)、IPv6 地址 (`fe80::21e:8c:53:e14/64`)、MAC 地址 (`00:50:ba:48:4f:ba`) 以及其他细节。如果你不知道接口名称，查看所有已加载的接口：

```bash
ip addr show
```
