
```
$ swap -s
Filename Size Used Priority
dev/das1 partition 259956 0 -1
dev/dasdr1 partition 519924 0 -2
```

优先级较高的设备将被优先使用；如果优先级相等，则使用优先级顺序中的下一个。使用默认值，第一个 VDISK `300` `/dev/das1` 获得优先级 `-1`，第二个 VDISK `301` `/dev/dasdr1` 在第一个用满后使用。你也可以在 `/etc/fstab` 交换设备中指定 `pri=nn`。

- 4. 你可以选择确认其他项。

至此，你已成功安装了黄金镜像。此镜像通常会被关机或退出。

你现在已准备好将黄金镜像克隆到新服务器上。

- 为 minidisks 格式化 DASD
- 手动克隆虚拟机
- 克隆一个新虚拟机
- 克隆另外三个虚拟机
- 检查系统状态

参考第 50 页第 4.6.2 节“为 minidisks 格式化 DASD”，DASD 已格式化为用于控制器和黄金镜像的 minidisks。可以使用 `CPFMTXA` 一次格式化一个 DASD，而 `CPFFOR` 配合 `CPFMTXA` 可以格式化多个 DASD。要定义具有 3390 个卷的用户 ID，需要 7 个卷（本例中还有一个可用）。请参考第 117 页第 2.7.2 节“z/VM DASD 表格”获取指导。

### 格式化 DASD 步骤

- 1. 在 `2750` 登录到 `MAINT`。
- 2. 查询用于剩余 Linux ID 的设备。

```
== das51-das57
DASD D51 ND51, DASD D52 ND52, DASD D53 ND53, DASD D54 ND54
DASD D55 ND55, DASD D56 ND56, DASD D57 ND57
```

- 3. 挂载用于控制器、CMS 磁盘和黄金镜像的卷。在本例中，DASD 地址为：

```
== das51-das57
ATTACH TO MAINT
```

- 4. 使用 `perm` 参数对这些卷调用 `CPFFOR` 命令：

```
== cpformat=<das51-das57> as perm
```
格式化以下 DASD：

Target ID OwnerID Vol-ID Start Size

MAINT DAS51 DAS51 3390 MDA51 0 3399

Target ID OwnerID Vol-ID Start Size

MAINT DAS52 DAS52 3390 MDA52 0 3399

Target ID OwnerID Vol-ID Start Size

MAINT DAS53 DAS53 3390 MDA53 0 3399

Target ID OwnerID Vol-ID Start Size

MAINT DAS54 DAS54 3390 MDA54 0 3399

Target ID OwnerID Vol-ID Start Size

MAINT DAS55 DAS55 3390 MDA55 0 3399

Target ID OwnerID Vol-ID Start Size

MAINT DAS56 DAS56 3390 MDA56 0 3399

Target ID OwnerID Vol-ID Start Size

MAINT DAS57 DAS57 3390 MDA57 0 3399

警告 - 这将破坏数据！

确定要将 DASD 格式化为 PERM 吗 (y/n)?

y

...

DASD51-DAS57 DETACHED

DASD51-DAS57 ATTACHED TO MAINT

DASD 状态：

Target ID OwnerID Vol-ID Start Size

MAINT DAS51 DAS51 3390 MDA51 0 3399

MAINT DAS52 DAS52 3390 MDA52 0 3399

MAINT DAS53 DAS53 3390 MDA53 0 3399

MAINT DAS54 DAS54 3390 MDA54 0 3399

MAINT DAS55 DAS55 3390 MDA55 0 3399

MAINT DAS56 DAS56 3390 MDA56 0 3399

使用 `DETACH` 命令从 `MAINT` 卸载这七卷：

```
== det <da51-da57>
DAS51-DETACHED
```

将新 DASD 挂载到 `SYSTEM` 以用于 minidisks：

```
== att <da51-da57> system
DAS51 ATTACHED TO SYSTEM MMDA51
DAS52 ATTACHED TO SYSTEM MMDA52
DAS53 ATTACHED TO SYSTEM MMDA53
DAS54 ATTACHED TO SYSTEM MMDA54
DAS55 ATTACHED TO SYSTEM MMDA55
DAS56 ATTACHED TO SYSTEM MMDA56
DAS57 ATTACHED TO SYSTEM MMDA57
```

这七个 DASD 卷现在可用于 `USER DIRECT` 文件中的 minidisks。在下一次 IPL 后，在标签匹配 `SYSTEM CONFIG` 文件中 `*User_Volume_Include*` 语句指定的模式之前，它们将可用。

## 9.1.1 为虚拟机定义新用户 ID

在此处你在 z/VM 中定义一个新用户 ID `LINUX0`，并将黄金镜像克隆到它：

- 1. 登录 `MAINT` 并编辑 `USER DIRECT` 文件以添加更多 Linux ID。

```
== user direct c
```

- 2. 转到文件末尾并添加以下 5 行。在本例中，用户 ID 将为 `LINUX01`，密码为 `LINX4VM`。它默认内存为 256 MB，但可以设置为 1 GB。它将只有 G（普通用户）。它将有两个 3338 柱体（约 2.2 GB）minidisks 用于 RHEL 安装。在本例中，它们位于设备地址 `0957` 和 `DAS51`，这些已格式化并标记为 `MD957` 和 `MDA51`。

```
LINUX01 LINX4VM 26G G
INCLUDE LINDFT
OPTION APPLMN
MDISK 0A1 3390 000 001 <MD957> MR LINX4VM LINX4VM
```

- 3. 将新卷添加到 `$ALLOC$` 用户 ID，这样它们就不会在映射中显示为空隙。使用 `FILE` 命令保存更改：

```
== tcp
==== /alloc
USER $ALLOC$ NOLOG
MDISK 0A1 3390 000 001 <MD850> R
MDISK 0A2 3390 000 001 <MD853> R
MDISK 0A3 3390 000 001 <MD854> R
MDISK 0A4 3390 000 001 <MD857> R
MDISK 0A5 3390 000 001 <MD856> R
MDISK 0A6 3390 000 001 <MD952> R
MDISK 0A7 3390 000 001 <MD953> R
MDISK 0A8 3390 000 001 <MD954> R
MDISK 0A9 3390 000 001 <MD955> R
MDISK 0A8 3390 000 001 <MD957> R
MDISK 0AC 3390 000 001 <MMDA51> R
== file
```

- 4. 再次检查间隙和重叠。你可以使用带有逻辑或 `l` 的 `ALL` 子命令来检查这两个字符串。你应该只会看到一个 501 缸间隙。

```
=> diskmap user
=> x user diskmap
==> all /gap//overlap/
--- 4 line(s) not displayed
----------------- 0 500 501 GAP
----------------- 368 line(s) not displayed
```

- 5. 使用 `DIRECTXA` 命令将更改上线：

```
=> directxa user
z/VM USER DIRECTORY CREATION PROGRAM - VERSION 5 RELEASE 3.0
EOJ DIRECTORY UPDATED AND ON
```

Linux 用户 ID 已经定义。

## 9.1.2 将 LINUX01 添加到 AUTOLOG 的 PROFILE EXEC 中

你定义的新的 Linux ID 需要具备访问 `VSWITCH` 的权限。可以在 `AUTOLOG1 PROFILE EXEC` 中添加一个带有 `GRANT` 参数的 `SET VSWITCH` 命令来实现此目的。此外，如果用户 ID 在 z/VM 启动时自动登录，则可以添加 `XAUTOLOG` 语句。

链接并访问 `AUTOLOG1 191` 磁盘的读/写并编辑 `PROFILE EXEC`。在授予 `VSWITCH` 和 `XAUTOLOG` Linux 用户 ID 的部分中添加 `LINUX01`：
