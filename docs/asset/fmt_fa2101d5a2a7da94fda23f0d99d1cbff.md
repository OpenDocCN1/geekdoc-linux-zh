
|---|---|---|---|

| 域管理员 | 500 | 用户 | 否 |
| 域来宾 | 501 | 用户 | 否 |
| 域 KRBTGT | 502 | 用户 | 否 |
| 域管理员 | 512 | 组 | 否 |
| 域用户 | 513 | 组 | 是 |
| 域来宾 | 514 | 组 | 是 |
| 域计算机 | 515 | 组 | 否 |
| 域控制器 | 516 | 组 | 否 |
| 域证书管理员 | 517 | 组 | 否 |
| 域架构管理员 | 518 | 组 | 否 |
| 域企业管理员 | 519 | 组 | 否 |
| 域策略管理员 | 520 | 组 | 否 |
| 内置管理员 | 544 | 别名 | 否 |
| 内置用户 | 545 | 别名 | 否 |
| 内置来宾 | 546 | 别名 | 否 |
| 内置高级用户 | 547 | 别名 | 否 |
| 内置账户操作员 | 548 | 别名 | 否 |
| 内置系统操作员 | 549 | 别名 | 否 |
| 内置打印操作员 | 550 | 别名 | 否 |
| 内置备份操作员 | 551 | 别名 | 否 |
| 内置复制器 | 552 | 别名 | 否 |
| 内置 RAS 服务器 | 553 | 别名 | 否 |

## 11.2.5 配置示例

通过执行 `net groupmap list` 可以列出映射数据库中的各个组。这里是一个示例：

```
root# net groupmap list
Domain Admins (S-1-5-21-2547222302-1596225915-2414751004-512) -> domainadmin
Domain Users (S-1-5-21-2547222302-1596225915-2414751004-513) -> domuser
Domain Guests (S-1-5-21-2547222302-1596225915-2414751004-514) -> domguest
```

有关 `net groupmap` 的完整详细信息，请参见 `net(8)` 手册页。

## 11.3 配置脚本

每个人都需要工具。有些人喜欢创建自己的工具，其他人则更喜欢使用现成的工具（即由他人预制供通用使用的工具）。

### 11.3.1 示例 smb.conf 添加组脚本

示例 11.3.1 提供了一个用于创建编译后的组名称以供 Samba 组接口使用的脚本。该脚本在 `/etc/group` 文件中添加一个临时条目，然后将其重命名为所需的名称。这是一个用于规避操作系统维护工具限制的方法示例，例如某些版本的 `groupadd` 工具中存在的限制。

```
#!/bin/bash

# Add the group using normal system groupadd tool.
groupadd smbtmpgrp00

thegid=`cat /etc/group | grep ^smbtmpgrp00 | cut -d":" -f3`

# Now change the name to what we want for the MS Windows networking end
cp /etc/group /etc/group.bak
cat /etc/group.bak | sed "s/^smbtmpgrp00/$1/g" > /etc/group
rm /etc/group.bak

# Now return the GID as would normally happen.
echo $thegid
exit 0
```

上述脚本的 `smb.conf` 条目如示例 11.3.2 所示，演示了如何使用它。

```
[global]
add group script = /path/to/tool/smbgrpadd.sh "%g"
```

### 11.3.2 配置组映射的脚本

在我们的示例中，我们创建了一个名为 ntdamin 的 UNIX/Linux 组。我们的脚本将创建额外的组 Orks、Elves 和 Gnomes。保存此 shell 脚本是个好主意以备后用，以防你需要重建映射数据库。为方便起见，我们选择将此脚本保存为名为 `initGroups.sh` 的文件。该脚本见示例 11.3.3。

## 示例 11.3.3 设置组映射的脚本

```bash
#!/bin/bash

net groupmap modify ntgroup="Domain Admins" unixxgroup=ntadmin
net groupmap modify ntgroup="Domain Users" unixxgroup=users
net groupmap modify ntgroup="Domain Guests" unixxgroup=nobody

groupadd Orks
groupadd Elves
groupadd Gnomes

net groupmap add ntgroup="Orks"    unixxgroup=Orks    type=d
net groupmap add ntgroup="Elves"   unixxgroup=Elves   type=d
net groupmap add ntgroup="Gnomes"  unixxgroup=Gnomes   type=d
```

当然，预期管理员会根据本地需求对此进行修改。有关使用 `net groupmap` 工具的信息，请参阅手册页。

## 11.4 常见错误

此时，对于疏忽的大侠管理员来说，有许多小的意外。从实际意义上说，至关重要的一点是，自动化控制脚本的每个步骤在投入使用前都必须仔细进行手动测试。

### 11.4.1 添加组失败

这是 `groupadd` 被 Samba 接口脚本直接调用时常见的一个问题，该脚本位于 `smb.conf` 文件中，对应于*添加组脚本*。

失败的最常见原因是试图添加一个包含大写字母和/或空格字符的 MS Windows 组账户。

有三种可能的解决方案。首先，仅使用符合 UNIX/Linux `groupadd` 系统工具限制的组名。其次，使用本章前面提到的脚本。第三，手动创建一个 UNIX/Linux 组账户以替代 MS Windows 组名，然后使用上述步骤将该组映射到 MS Windows 组。

### 11.4.2 将域用户添加到工作站 Power Users 组

“我需要做什么才能将域用户添加到 Power Users 组？”

Power Users 组是本地于每个 Windows 200x/XP 专业版工作站的组。你不能自动将域用户组添加到 Power Users 组；必须在每个工作站上以本地工作站的*管理员*身份登录，然后使用以下步骤完成：

1. 单击 **开始 -> 控制面板 -> 用户和密码**。
2. 单击 **高级** 选项卡。
3. 单击 **高级** 按钮。
4. 单击 **组**。
5. 双击 **Power Users**。这将启动面板，用于向本地机器的 **Power Users** 组添加用户或组。
6. 单击 **添加** 按钮。
7. 选择要从其添加 **域用户** 组的域。
8. 双击 **域用户** 组。
9. 单击 **确定** 按钮。如果在此过程中出现登录框，请记住输入连接身份为 `DOMAIN\UserName`，即，对于域 `MIDEARTH` 和用户 `root`，输入 `MIDEARTH\root`。

## 远程和本地管理：NET 命令

`net` 命令是 Samba-3 的新功能之一，旨在为大多数常见的远程管理操作提供有用的工具。`net` 工具在设计上是灵活的，既适用于命令行使用，也适用于脚本控制应用。

最初引入时，`net` 命令旨在模拟 Microsoft Windows 中同名命令，如今已演变成为一种非常强大的工具，成为 Samba 网络管理员工具箱中不可或缺的一部分。Samba 团队引入了诸如 `smbgroupedit` 和 `rpcclient` 等工具，其中真正有用的功能已集成到 `net` 中。`smbgroupedit` 命令已完全并入 `net`，而只有 `rpcclient` 命令的一些功能被移植过来。任何发现这些实用程序及其所提供功能的旧引用的人，在搜索其他地方之前，应查看 `net` 命令。

Samba-3 管理员不能略过本章，因为这样做几乎肯定会带来自我伤害、痛苦和绝望的代价。请警告：这是一个重要的章节。

## 12.1 概述

安装 Samba-3 服务器（无论是独立服务器还是域成员）或域控制器（PDC 或 BDC）后的任务，始于创建管理权限的需要。当然，用户和组账户的创建对于独立服务器和 PDC 都是必不可少的。对于 BDC 或域成员服务器（DMS），域用户和组账户是从中央域身份验证后端获取的。
