

## NIS 客户端

为了让主机能够使用网络上的 NIS，首先需要在该主机上指定 NIS 域名。此外，你的 NIS 客户端还需要知道 NIS 服务器的名称。如果你安装 Linux 的网络中已经运行了 NIS，你可能在安装过程中已经输入了这些信息。

### 指定 NIS 域和服务器

你可以使用 authconfig-gtk 工具来指定 NIS 域名和服务器，你可以从“系统设置”窗口访问该工具。在该窗口中，选择 Authentication（认证）。这将打开认证配置窗口。在“用户信息”面板中，点击“配置 NIS”按钮，打开一个对话框，你可以在其中输入 NIS 域名称以及 NIS 服务器名称。请务必也在“用户信息”面板中启用 NIS。NIS 域将保存在 /etc/sysconfig/network 文件中，而 NIS 服务器则保存在 /etc/yp.conf 文件中。

### 访问服务器

然后，网络上的每个 NIS 客户端主机都需要运行 ypbind NIS 客户端以访问服务器。在客户端的 /etc/yp.conf 文件中，你需要指定它将使用的 NIS 服务器。以下条目将引用位于 192.168.1.1 的 NIS 服务器：

```
ypserver 192.168.1.1
```

或者，你可以指定 NIS 域名称及其使用的服务器：

```
domain mydomain.nis server servername
```

authconfig-gtk 工具将为使用 turtle.mytrek.com 服务器和 myturtle.nis NIS 域在 /etc/yp.conf 中创建以下条目：

```
domain myturtles.nis server turtle.mytrek.com
```

要启动 NIS 客户端，请运行 ypbind 脚本：

```
service ypbind start
```

然后，为了检查一切是否正常工作，你可以使用 ypcat 尝试列出 NIS 密码文件：

```
ypcat passwd
```

你可以使用 ypcat 列出任何 NIS 配置文件。ypwhich 命令将显示你的客户端正在使用的 NIS 服务器的名称。yppmatch 可用于查找配置文件中的特定条目。

```
ypmatch cecelia passwd
```

用户可以使用 yppasswd 命令更改 NIS passwd 文件中的密码。其工作原理与 passwd 命令相同。你还需要运行 yppasswd 守护进程。

### 使用 nsswitch.conf 指定配置文件

为了确保客户端针对特定配置文件访问 NIS 服务器，你应该在 `/etc/nsswitch.conf` 文件的相应条目中指定 **nis**。 **nisplus** 选项指的是 NIS 版本 3。**nis** 选项用于指代较旧的 NIS 版本 2。`/etc/nsswitch.conf` 文件指定了主机应该在哪里查找某些类型的信息。例如，以下条目表示先检查本地配置文件（**files**），然后再检查 NIS 服务器（**nisplus**）以获取密码数据：

```
passwd: files nisplus
```

**files** 指定意味着首先使用系统自身的文件，即本地主机上的文件。**nis** 表示查找 NIS 文件中的条目，即访问 NIS 服务器。**nisplus** 表示使用由 NIS+ 服务器维护的 NIS+ 文件。**dns** 表示执行 DNS 查询；它只能用于包含主机名的文件，如 **hosts**。以下是一些标准条目：

```
passwd: files nisplus
shadow: files nisplus
group: files nisplus
hosts: files nisplus dns
bootparams: nisplus [NOTFOUND=return] files
ethers: files
netmasks: files
networks: files
protocols: files nisplus
rpc: files
services: files nisplus
netgroup: files nisplus
publickey: nisplus
automount: files nisplus
aliases: files nisplus
```

## 分布式网络文件系统

对于像 Linux 集群这样的超大型分布式系统，Linux 还支持分布式网络文件系统，例如 Coda、Intermezzo、红帽全局文件系统（GFS 和 GFS 2）以及并行虚拟文件系统（PVFS2）。这些系统基于 NFS 的基本概念以及 RAID 技术，构建一个在大型网络上的多个主机上实现的文件系统，实际上是在非常低的层次上将相同的文件系统分布到不同的主机上（见表 38-3）。你可以将其视为一种跨网络主机实现的 RAID 阵列，而不仅仅是在单个系统上。各主机不再依赖其自身硬盘上的文件系统，而是共享同一个使用不同分布式服务器上的硬盘组成的分布式文件系统。这提供了对主机可用存储空间的更 efficiently 的使用，同时也提供了更集中的文件系统管理。

| 网站 | 名称 |
| :--- | :--- |
| fedoraproject.org/wiki/Tools/GFS | Fedora GFS 资源和链接 |
| www.pvfs.org | 并行虚拟文件系统，PVFS2（开源） |
| sourcereare.org/gfs | 全局文件系统（Fedora 和商业版本） |
| www.coda.cs.cmu.edu ftp.coda.cs.cmu.edu/pub/coda/linux | Coda 文件系统，断开的移动访问（实验性） |
| www.inter-mezzo.org | Intermezzo（开源） |
| clusterfs.com | Lustre |

**表 38-3** 分布式文件系统

### 并行虚拟文件系统 (PVFS)

并行虚拟文件系统 (PVFS) 使用管理服务器来管理不同 I/O 服务器上的文件系统，从而实现分布式网络文件系统。管理服务器维护文件系统信息，包括访问权限、目录结构和元数据信息。对文件的访问请求由管理服务器的客户端提交。然后管理服务器在客户端和持有请求文件数据的 I/O 服务器之间建立连接。读取和写入等访问操作随后直接在客户端和 I/O 服务器之间执行。PVFS 可以使用内核模块透明地实现，以利用内核的虚拟文件系统。这样，PVFS 文件系统就可以像任何其他文件系统一样由客户端挂载。在 PVFS 实现中，文件系统被组织成数据条带，类似于 RAID 阵列，但条带分布在网络上的不同主机上。文件作为条带集合进行访问，这些条带可以分布在整个网络中。

PVFS 的一个新版本，称为 PVFS2，目前可以从 www.pvfs.org 获取。你可以从那里下载源代码。PVFS 是与克莱姆森大学并行体系结构实验室和阿贡国家实验室数学与计算机科学部门合作的项目。

PVFS 管理服务器使用两个配置文件：pvfs2-fs.conf 和 pvfs2-server.conf。你使用配置脚本 pvfs2-genconfig 创建这些文件。脚本会提示你输入配置信息，如协议、端口、日志文件和存储目录。要配置集群网络，务必输入将作为 I/O 服务器运行的主机。

管理服务器是 pvfs2-server。要管理服务器，首先将 pvfs2-server 服务脚本放入 /etc/init.d 目录。然后你可以使用 service 命令配合该脚本来启动和停止服务器。要让服务器自动运行，请使用 chkconfig 或 system-config-services 将其开启。

在 I/O 服务器上，你运行 pvfs2-server 脚本创建存储空间，然后启动服务器。I/O 服务器使用 /etc/pvfs2-fs.conf 配置文件。你可以使用 pvfs2-server 脚本让服务器自动开启。

在将使用 PVFS 系统的客户端上，你需要安装文件系统配置信息和访问工具。每个客户端都需要一个 PVFS 守护进程 pvfs2-client，以及其支持模块和库。文件系统挂载配置可以保存在 /etc/pvfs2tab 中，但你可以直接将条目放置在 /etc/fstab 文件中。要挂载 PVFS 文件系统，你也可以在 mount 命令中使用 -t 选项和 pvfs2 类型。PVFS2 提供了一组自己的文件命令，如 pvfs2-ping、pvfs2-cp 和 pvfs2-ls，用于列出和访问其文件系统上的文件。

客户端可以通过内核模块直接访问 Linux 文件系统，或者使用 MPI-IO 接口来访问 PVFS2 文件系统；后者需要重新编译并使用 libpvfs2 库，但为并行应用提供了更好的性能。PVFS2 中的并行支持是通过消息传递接口 (MPI) 实现的，该接口由 ROMIO (www-unix.mcs.anl.gov/romio) 和 MPICH2 (www-unix.mcs.anl.gov/mpi/mpich2) 支持，这些工具来自阿贡国家实验室的 MCS 部门。

> *注意：为了充分利用 PVFS，应用程序应该是 PVFS 启用的，这样它们的文件数据会被条带化，以便在 PVFS 系统上更好地使用。*

### Coda

Coda 由卡内基梅隆大学开发，作为一个实验性项目，尽管它可以免费获取。它的一些功能包括支持移动计算、访问控制和带宽适应。你可以从 www.coda.cs.cmu.edu 获取有关 Coda 的信息。你可以从 ftp.coda.cs.cmu.edu/pub/coda/linux 下载某些版本为 Fedora 和 Red Hat 提供的 RPM 软件包。

使用内核模块与虚拟文件系统接口，可以从客户端上的 Coda 目录（通常是 /coda）访问分布式的 Coda 文件。Coda 会在客户端上维护经常访问的文件的缓存，以提高效率。该缓存由一个名为 Venus 的缓存管理器维护，它处理所有文件系统请求。缓存的使用允许对文件进行断开的操作，让用户可以在本地处理文件，然后稍后与主服务器更新。断开连接的操作非常适合移动计算，因为笔记本电脑可能会在一段时间内与网络断开连接。用户经常使用的文件对应的数据库（称为 hoods）也维护在服务器上，以促进更新。

要配置客户端，你需要 coda-debug-client 软件包。使用 venus-setup 脚本配置客户端，然后使用 venus 守护进程启动 Coda。对于服务器，你需要安装 coda-debug-server 软件包并运行 venus-setup 来配置你的服务器。

### 红帽全局文件系统 (GFS 和 GFS 2)

红帽已将全局文件系统 (GFS) 作为开源免费可用的分布式网络文件系统发布。最初的 GFS 版本包含在 Fedora 4 和 5 中。从 Fedora Core 6 开始，包含 GFS 的新版本 GFS 2，使用类似的配置和管理工具集，以及原生内核支持。与各种看似不相关的软件包不同，GFS 2 仅通过三个软件包实现：gfs2-utils、cman 和 lvm-cluster。对 GFS 2 的原生内核支持提供了大部分的内核级操作。

分布式网络文件系统基于 NFS 的基本概念以及 RAID 技术，构建一个在大型网络上的多个主机上实现的文件系统，实际上是在非常低的层次上将相同的文件系统分布到不同的主机上。你可以将其视为一种跨网络主机实现的 RAID 阵列，而不仅仅是单一

