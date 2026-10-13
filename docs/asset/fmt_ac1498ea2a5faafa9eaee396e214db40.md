
查找 IP 地址（基于获取的主机名）的过程由名称服务切换（`/etc/nsswitch.conf`）文件中的 `hosts` 关键字的配置决定。可以从 DNS、NIS（hosts.byname 映射）、NIS+（hosts 表）或 `/etc/hosts` 文件中获取。有关 `/etc/hosts` 文件的格式，请参见 `hosts(4)`。

### TFTP 守护进程（in.tftpd）

`/usr/sbin/in.tftpd` 守护进程为 SPARC 安装客户端提供了一种使用 TFTP 从安装/引导服务器获取引导映像的简单方法。与标准 FTP 不同，TFTP 不需要用户身份验证（账户名和密码）即可访问文件。引导映像通常存储在 `/tftpboot` 目录下。

### NFS 服务器守护进程（nfsd）

`/usr/lib/nfs/nfsd` 守护进程通过 NFS 提供对 Solaris 8 发行版文件的网络访问。这些文件由 `rpc.bootparamd` 守护进程提供的引导参数标识。

### 引导参数服务器守护进程（rpc.bootparamd）

`/usr/sbin/rpc.bootparamd` 守护进程提供引导安装客户端所需的 NFS 共享名称和其他信息。信息的来源由名称服务切换（`/etc/nsswitch.conf`）文件中的 `bootparams` 关键字的配置决定。可以从 NIS（bootparams 映射）、NIS+（bootparams 表）或 `/etc/bootparams` 文件中获取。有关 `/etc/bootparams` 文件的格式，请参见 `bootparams(4)`。

![](img/b957f979417d9f16274c2eb52c8f2c9f_455_0.png)

由于支持网络安装（无论是否使用 JumpStart）需要这四个守护进程，因此 `add_install_client` 命令在配置网络安装客户端时，会根据需要在安装/引导服务器上配置并启动它们。

## 使用 JumpStart 自动化安装

JumpStart 功能提供了一种自动安装 Solaris 操作系统的机制。两种 JumpStart 方法分别是 JumpStart 和 Custom JumpStart。

![](img/b957f979417d9f16274c2eb52c8f2c9f_456_0.png)

JumpStart 不仅能够自动化安装，还可以用于自动化安装大量配置相同的系统。例如，如果需要使用相同配置安装 100 个系统，JumpStart 提供了一种简化此任务的方法。

JumpStart 使您能够通过将 Solaris 发行版 CD 插入本地 CD-ROM 驱动器并给系统加电或通过网络引导，自动在新 SPARC 平台上安装 Solaris 操作系统。安装的软件由默认配置文件决定，该文件基于硬件型号和硬盘大小选择。无法手动选择安装的软件。

所有新 SPARC 平台都预装了 JumpStart 引导映像。可以使用 `re-preinstall(1M)` 命令将此引导映像复制到现有 SPARC 平台。

自定义 JumpStart 使您能够通过将 Solaris 发行版 CD 插入本地 CD-ROM 驱动器并给系统加电或通过网络引导，自动在新 SPARC 或 Intel x86 平台上安装 Solaris 操作系统。安装的软件由自定义配置文件决定。使用此方法，您可以以相同方式自动安装多组系统。自定义配置文件以及其他 JumpStart 配置文件位于 JumpStart 配置目录中。

## JumpStart 配置目录

JumpStart 配置目录包含用于自定义 JumpStart 安装的文件。它为相似系统组的安装提供了一种自动化系统配置阶段的方法。该目录可以位于软盘上，称为 *配置文件软盘*，或位于网络服务器上，称为 *配置文件服务器*。配置文件服务器通过网络提供对自定义 JumpStart 配置文件的访问，并消除了在安装大量系统时创建和分发多个配置文件软盘的需要。JumpStart 目录中的两种基本文件类型是规则文件和一个或多个配置文件。

![](img/b957f979417d9f16274c2eb52c8f2c9f_456_1.png)

第二部分考试 (CX-310-012) 继续将 *配置文件* 称为 *类文件*，尽管它在 Solaris 2.6 系统文档中早已更名。当您看到引用类文件的 JumpStart 问题时，请牢记这一点。

### 规则文件

规则文件是一个文本文件，其中包含一个条目或规则，用于描述要自动安装的每个系统或系统组。每个规则基于一个或多个属性标识系统（或系统组），并标识一个唯一的配置文件，该文件为该系统或系统组提供配置详细信息。

每条规则由一个或多个关键字和值组成，后面跟着 begin 脚本的名称、配置文件和 finish 脚本（全部以制表符或空格分隔）。关键字（及关联值）包括以下内容：

- `any`
- `arch` (后跟处理器类型值)
- `disksize` (后跟磁盘名称值)
- `hostaddress` (后跟 IP 地址值)
- `hostname` (后跟主机名值)
- `memsize` (后跟物理内存值)
- `model` (后跟平台名称值)

每条规则指定一个或多个这些关键字及关联值，以唯一标识一个系统或系统组。

在关键字和值之后是 begin 脚本的名称。这是一个在安装开始之前执行的 Bourne shell 脚本。如果不需要 begin 脚本，则应使用连字符代替。接下来是 JumpStart 配置目录中配置文件的名称，该文件为该系统或系统组提供配置详细信息。在配置文件之后是 finish 脚本的名称，这是一个在安装完成后执行的 Bourne shell 脚本。如果不需要 finish 脚本，则应使用连字符代替。

以下示例显示了规则文件中的几个条目：

```
hostname sample_host    -          host_class   set_root_pw
network 192.22.43.0 \
        karch sun4c    -          net192_sun4c  -
arch i386              x86-begin  x86-class     -
any  -                 -          any_machine   -
```

第一个条目列出了名为 sample_host 的主机的 JumpStart 安装。没有指定 begin 脚本，使用 host_class 文件作为配置文件或类文件，安装后调用 finish 脚本 set_root_pw 来设置 root 账户的密码。

第二个条目实际上列在两行上。第一行末尾的反斜杠 (`\`) 字符将该条目续到下一行。对于位于网络 192.22.43.0 上且为 SPARC sun4c 平台的系统，使用 net192_sun4c 配置文件或类文件。未指定 begin 或 finish 脚本。

第三个条目适用于所有 i386 或 Intel 兼容平台。首先执行 x86-begin 脚本，然后使用 x86-class 配置文件或类文件来指导安装。未指定 finish 脚本。

第四个条目提供了默认设置。其他规则未涵盖的任何系统都使用 any_machine 配置文件安装。未指定 begin 或 finish 脚本。

### 配置文件

配置文件（或类文件）是一个文本文件，定义如何在系统上安装 Solaris 8 软件。与规则文件一样，配置文件包含指导安装的关键字和关联值，例如：

- `boot_device` (后跟用作引导设备的分区)
- `cluster` (后跟要安装、添加或删除的软件组名称)
- `filesys` (后跟要挂载的远程文件系统的路径名和挂载点)
- `install_type` (后跟安装类型：initial_install 或 upgrade)
- `package` (后跟要添加或删除的软件包名称)
- `partitioning` (后跟磁盘分区类型：default、existing 或 explicit)
- `root_device` (后跟用作根设备的分区)
- `system_type` (后跟系统类型：standalone 或 server)

以下列出了 Solaris 8 发行版 CD 上作为 JumpStart 示例提供的 any_machine 配置文件的内容：

```
install_type   initial_install
system_type    standalone
partitioning   default
cluster        SUNWCuser
cluster        SUNWCXgl delete
package        SUNWaudio add
filesys        any 40 swap
filesys        any 50 /opt
```
