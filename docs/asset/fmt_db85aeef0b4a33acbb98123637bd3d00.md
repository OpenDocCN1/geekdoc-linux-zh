
这是一个通常不安装在主机和节点上的发行版，而是以 LiveCD 模式运行。它不用于永久运行的集群，而是用于快速临时转换为教室或工作站计算集群。该发行版基于 Debian。请注意，它不再处于活跃开发状态，或者可能已经过时。

你可以安装主机镜像以便永久运行，并根据需要加载节点。该发行版中几乎没有集群监控和管理功能。由于该发行版的目的是在下班后运行一个或多个任务，通常不需要管理。镜像的更改与大多数 LiveCD 发行版一样进行，因此添加软件包、更新和配置更改需要手动完成。

## 第 25 章 开箱即用的堆栈与部署系统

这里是一个 PelicanHPC 会话的示例。从 LiveCD/LiveUSB 启动。在弹出的菜单中，选择“Start Debian Live”。下一个屏幕是“Pelican Setup”，系统将提示你选择 `/home` 目录的位置。默认建议将其放置在 RAM 中的虚拟磁盘上。如果你需要在重启之间保存 `/home` 目录的状态，可以指定挂载命令来挂载预格式化的 `/` 分区。如果你是首次启动，最好不要更改任何内容只需按“Enter”，启动后打开 `/home/user/pelican_config` 文件，该文件描述了不同的家目录挂载配置。

下一个设置屏幕是提示复制 `/home` 目录的初始设置。如果使用默认设置启动，选择“Yes”；如果你为 `/home` 使用持久存储，则应仅在首次启动时复制这些数据。下一步是为用户 `user` 设置密码。删除“PleaseChangeMe!”并输入新密码。之后，下载将继续并出现登录提示 `login):`。输入名称“user”和你输入的输入的密码。如果你更倾向于在图形化环境中工作，输入 `startx`，将加载 Xce 图形环境。

要启动你的集群，输入 `pelican_setup` 命令。程序将提示你选择对应于集群网络的网络接口。请小心，因为该网络上有一个 DHCP 服务器，如果你指定错误的接口，可能会干扰你的常规网络。

程序的下一个屏幕提示你选择所需的服务。如果你已就绪并确定选择了正确的接口，点击“Yes”。服务启动后，将出现一个屏幕邀请启动计算节点。选择“Yes”并开始开启电源或重启计算节点。确保节点通过网络启动。一旦启动，计算节点屏幕应显示“This is a PelicanHPC compute node.”和标准提示符。

在所有计算节点启动后，`pelican setup` 程序将显示节点数量。如果一切顺利，点击“Yes”。在下一个屏幕上，程序将提供有关新创建集群计算的简要信息。点击“OK”，将运行简单的集群性能测试，程序结束。

`/home/user/bhosts` 文件包含你的集群节点列表和其他一些参数。如果你需要添加或删除计算节点，运行 `pelican_restart_hpc` 命令，该命令会自动完成这些任务。如果你需要额外的软件包，可以使用 `apt-get` 命令交付。请记住下载的系统是基于 Debian 的，因此使用 deb 包即可。如果你愿意，可以创建一个包含所需软件包的自己的 PelicanHPC 镜像（详情请参见文档）。默认情况下，PelicanHPC 包含了并行版本的 Linpack 和 Octave 以及 OpenMPI。

项目网站 - https://sourceforge.net/projects/pelicanhpc/

## 简要总结

为了解决简单的典型任务并不总是需要“真正的”超级计算机；Beowulf 类集群就足够了，即从临时材料组装，或者你可以简单地在晚上使用空闲教室或办公室的电脑。一个不需要花费时间安装（或完全不需要安装）的现成堆栈对此目的非常有用。应该记住，这种解决方案的灵活性远低于安装所有的。

## 第 25 章 开箱即用的堆栈与部署系统

该系统是基于 Debian 的，因此使用 deb 包即可。如果你愿意，可以创建一个包含所需软件包的自己的 PelicanHPC 镜像（详情请参见文档）。默认情况下，PelicanHPC 包含了并行版本的 Linpack 和 Octave 以及 OpenMPI。

项目网站 - https://sourceforge.net/projects/pelicanhpc/

## 简要总结

为了解决简单的典型任务并不总是需要“真正的”超级计算机；Beowulf 类集群就足够了，即从临时材料组装，或者你可以简单地在晚上使用空闲教室或办公室的电脑。一个不需要花费时间安装（或完全不需要安装）的现成堆栈对此目的非常有用。应该记住，这种解决方案的灵活性远低于安装所有的。

## 第 26 章

# 集群管理系统 – xCAT 及其他

由于你的集群包含许多节点，它需要跟踪它们的名称、地址，`xCAT`（集群管理工具）由 IBM 开发，并自2007年起开源。它不是一个发行版，而是一个管理系统。

`xCAT` 可以：

- 创建下载操作系统镜像
- 自动执行安装
- 通过 IPMI、ILO 等协议管理节点
- 维护 TFTP、DNS 和 DHCP 信息

`xCAT` 更改 NFS、DHCP 和 TFTP 设置而不保留原始设置。小心，配置文件将被覆盖。更新不会自动发生，仅通过相应的命令进行。

## 搜索关键词

- HPC, LiveCD, LiveUSB, beowulf, knoppix, pelicanhpc

## 第 26 章 集群管理系统 – XCAT 及其他

首先，让我们运行 `tabdump site` 命令。这里是负责整个集群设置的表名称。以下是此类输出的示例（删除了部分行）：

```
1 #key,value,comments,disable
2 "domain", "mycluster",,,
3 "instaldir", "/install",,,
4 "ipmiretries", "3", "3",,,
5 "ipmitimeout", "2", "2",,,
6 "master", "10.0.5.1",,,
7 "forwarders", "8.8.8.8,4.4.4.4",,,
8 "nameserver", "10.0.5.1",,,
9 "Syncdfiledir", "/var/xcat/syncfiles",,,
10 "nodesyncfiledir", "/var/xcat/node/syncfiles",,,
11 "ftptdir", "/ftboot",,,
12 "xcatconf", "/etc/xcat",,,
13 "timezone", "Europe/London",,,
```

该结构非常简单：第一行包含字段列表，其中前两个——`key` 和 `value` 最为关键。第 2 行指定了通用域名；第 3、9、10、11 和 12 行是包含关键文件的目录；第 4 和 5 行指定了 IPMI 参数；第 6 行是 xCAT 头服务器的地址；第 7 和 8 行是外部和内部 DNS 服务器的地址。第 13 行指定了时区；可能需要将其更改为你需要的时区。

使用 `lsdef -t site -1` 命令也可以获取相同的信息，但显示方式更为简洁：

```
Object name: clustersite
domain=mycluster
forwarders=8.8.8.8,4.4.4.4
instaldir=/install
ipmiretries=3
ipmitimeout=2
master=10.0.5.1
```

你可以使用 `tabedit` 命令更改表中的数据——这将打开一个由 `EDITOR` 变量定义的编辑器，你可以编辑表中的行或多行。如果你只需要更改一个键，或者在脚本中执行，`chtab` 命令将非常有用。以下是其用法示例：

```
chtab key=tftpd site.value=/tftpboot
```

由于某些描述可能会影响多个表，因此存在 `chdef` 命令。以下是其用法示例：

```
chdef -t node=node01 groups=all,compute
```

在这里我们更改了类型为 "node"名为 `node01` 的对象，并指定它现在是 "all" 和 "compute" 组的成员。此更改将同时影响节点和组的描述。

对于某些对象（如节点），有专门的命令，可以这样执行之前的操作：

```
nodech node01 groups="all, compute"
```

`lsdef` 命令有一个 `-z`，可以保存当前对象的描述，编辑后可以使用 `mkdef -z` 命令加载回：

```
lsdef -z node01 > /tmp/n01.stanza
vi /tmp/n01.stanza mkdef -z
cat /tmp/n01.stanza -z
```

`xCAT` 支持哪些对象？以下是部分列表：

- `site` (集群)
- `node` (节点)
- `group` (节点组)
- `network` (子网)
- `osdistro` (操作系统发行版)
- `osimage` (操作系统镜像)
- `route` (路由描述)
