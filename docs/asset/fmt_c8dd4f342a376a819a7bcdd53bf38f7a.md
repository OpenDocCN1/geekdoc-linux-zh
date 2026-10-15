
- i. 当询问选择安装偏好时，输入 1. Start Now with Default Settings（使用默认设置开始）。在系统安装摘要中，确保`hdisk0`是唯一磁盘并输入 1 继续安装。显示安装进度。

- j. 安装过程完成并重启后，使用`padmin`用户登录。提示提供新密码。

成功登录后，您将进入 VIOS 命令行界面（CLI）。输入示例 3-1 所示的命令来接受许可。

```
$ license -accept
```

现在已可以使用新创建的 VIOS 软件在客户端分区上创建资源。

## 3.5 配置虚拟 I/O 服务器

在本节中，我们使用第 55 页的表 3-2 在客户端分区上配置 SCSI 设备。请参阅图 3-8 的基本配置。

![](img/8968f0cd21ddc37c_85_0.png)

带有 带有客户端分区的 VIOS

根据图 3-8，以下章节将引导您配置虚拟以太网和虚拟 SCSI 适配器。

### 3.5.1 命令行界面

VIOS 提供了一个受限 shell（CLI）。所有的 VIOS 配置应通过 CLI 完成：

- 设备管理（物理、虚拟和 LVM）

- 网络配置

- 软件安装和更新

- 安全

- 用户管理

- 维护任务

登录 VIOS 后，您将进入受限 Korn shell。受限 Korn shell 的工作方式与普通 Korn shell 相同，但具有以下限制：

- 无法更改当前工作目录。

- 无法设置 `SHELL`、`ENV` 或 `PATH` 变量。

- 无法指定包含 >、< 或 * 的命令。

由于这些限制，您无法直接将命令输出到文件，必须将输出通过到`tee`命令。

登录后，可以使用`help`命令获取支持的命令概述，如示例 3-2 所示。

示例 3-2 VIOS 支持的命令

```
$ help
```

安装命令

- `ioslevel`

- `license`

- `lssw`

- `oem_platform_level`

- `oem_setup_env`

- `remote_management`

- `updateios`

LAN 命令

- `cfggnl`

- `cfnamesrv`

- `entstat`

- `hostmap`

- `hostname`

- `lnetsvc`

- `lstcpip`

- `mktcpip`

- `chtcpip`

- `netstat`

- `optimenet`

- `ping`

- `rmtcpip`

- `startnetsvc`

- `stopnetsvc`

- `traceroute`

安全命令

- `lsfailedlogin`

- `sgcl`

- `viosecure`

- `mkldap`

- `ldapadd`

- `ldapsearch`

用户命令

- `chuser`

- `luser`

- `mkuser`

- `passwd`

- `rmuser`

维护命令

- `alt_root_vg`

- `backupsios`

- `booklist`

- `cattrapt`

- `chdate`

- `clang`

- `cfgassist`

- `cl_snmp`

- `diagmenu`

- `errlog`

设备命令

- `fsck`

- `invscout`

- `ldfware`

- `chdev`

- `logmnsg`

- `chpath`

- `lsfware`

- `cfgdev`

- `lslparinfo`

- `lsdev`

- `motd`

- `lsmap`

- `mount`

- `lspath`

- `pdump`

- `mkpath`

- `replphyvol`

- `mkdev`

- `restoregstruct`

- `mkvt`

- `save_base`

- `rmdev`

- `savevgstruct`

- `rmpath`

- `showmount`

- `rmdev`

- `shutdown`

- `rmvt`

- `snap`

- `snmp_info`

- `snmp_trap`

物理卷命令

- `startsyscdump`

- `lspv`

- `starttrace`

- `migratepv`

- `stoptrace`

- `sysstat`

逻辑卷命令

- `topas`

- `chlv`

- `unmount`

- `cplv`

- `viostat`

- `endlv`

- `wkdmgr`

- `lslv`

- `wkldagent`

- `mklv`

- `wkldout`

- `mklvcopy`

- `rmlv`

Shell 命令

- `awk`

- `cat`

卷组命令

- `chmod`

- `activatevg`

- `clear`

- `chvg`

- `cp`

- `deactivatevg`

- `crontab`

- `exportvg`

- `date`

- `extendvg`

- `ftp`

- `importvg`

- `grep`

- `lsvg`

- `head`

- `mirrors`

- `ls`

- `mkvg`

- `man`

- `redfvg`

- `mkdir`

- `reducevg`

- `more`

- `syncvg`

- `mv`

- `unmirroris`

存储池命令

```
chsp
lsssp
mkbdsp
mksp
rmbdsp
rm
sed
st
tail
tee
vi
wall
wc
who
```

监控命令

```
cfgsvc
lssvc
startsvc
stopsvc
```

要获取有关这些命令的进一步帮助，请使用示例 3-3 所示的`help`命令。

示例 3-3 帮助命令

```
$ help lsmap
Usage: lsmap [-adapterServerVirtualAdapter | -plcPhysicalLocationCode | 
[-all] [-type BackingDeviceType ... | -net]
[-field FieldName ...] [-fmt delimiter]
```

显示物理设备与虚拟设备之间的映射。

VIOS CLI 支持两种执行模式：

- 传统模式（Traditional mode）

- 交互模式（Interactive mode）

传统模式用于单命令执行。在此模式下，你从 shell 提示符运行一个命令。例如，要显示物理、逻辑和虚拟设备之间的映射，请输入 3-4 所示的命令。

示例 3-4 传统模式下的`ismap`命令

```
$ ioscli ismap -all
```

为了减少在传统 shell 级模式下的输入工作量，每个子命令都有一个别名（alias）。设置别名后，你无需像示例 3-5 所示那样输入`ioscli`命令。

示例 3-5 使用别名运行`ismap`命令

```
$ ismap -all
```

在交互模式下，用户通过执行不带任何子命令或参数的`ioscli`命令来获得`ioscli`命令提示符。从现在起，`ioscli`命令将一个接一个地运行，而无需每次都重新输入 ios ioscli 命令。例如，要进入交互模式，请输入示例 3-6 所示的命令。

示例 3-6 交互模式

```
$ ioscli
```

在交互模式下，要列出所有虚拟设备，输入示例 3-7 所示的`lmap`命令。

示例 3-7 交互模式下的命令

```
$ lmap -all
```

外部命令（如 `grep` 或 `sed`）无法在交互模式命令提示符下运行。你必须先输入 `quit` 或 `exit` 来退出交互模式。

### 3.5.2 镜像 VIOS rootvg

当 VIOS `rootvg` 安装完成后，可以使用以下命令将 VIOS `rootvg` 卷组镜像到第二个物理卷。这可以防止在磁盘故障时单 VIOS 分区设置受到影响。对于其他 VIOS 高可用性示例配置部署，请参考《Advanced POWER Virtualization on IBM System p Virtual I/O Server Deployment Examples》，REDP4224，该文档在线可用：

```
http://www.redbooks.ibm.com/abstracts/redp4224.html#7open
```

步骤显示了如何镜像 VIOS rootvg：

1. 使用 `extendvg` 命令将 `hdisk1` 包含在 `rootvg` 卷组中。适用 LVM 概念——你不能使用属于另一个卷组的 `hdisk`，且该磁盘的大小需要相等或大于目标磁盘。

2. 使用 3-8 所示的 `lspv` 命令，确认 `rootvg` 已扩展以包含 `hdisk1`。

> 示例 3-8 `lspv` 命令输出

| lspv | PVID | VG |
| --- | --- | --- |
| n STATUS `hdisk0` active | 00c18ea19cacb2a | `rootvg` |
| `hdisk1` active | 00c18ea1f04575 | `rootvg` |
| `hdisk2` | 00c18ea8ae5fd5d | NONE |
| `hdisk3` | 00c18ea8ae665c7 | NONE |
