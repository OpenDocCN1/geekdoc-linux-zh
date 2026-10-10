

2. 通过输入 `ls` 命令验证您是否拥有 `/home` 分区的备份磁带。您应该看到类似以下目录列表，代表在 `/home` 中具有主目录的用户：

```text
restore > ls
:
bob/ jane/ joe/ lost+found/ mary/ thad/
```

3. 是的，这是主分区。现在使用 `cd` 命令将当前目录更改为 Joe 的主目录。再次输入 `ls` 以查看其主目录的内容。

```text
restore > cd joe
restore > ls
./joe/
.mozilla/ Desktop/ report.html
.tcshrc Mail/ letter.txt
.xinitrc News/ www/
```

4. 现在使用 `add` 命令将 Mail 目录标记为提取对象：

```text
restore > add Mail
```

5. 如果您再次使用 `ls` 命令，您会看到 Mail 目录前有一个星号 (*) 字符，这意味着它已被标记为待提取。

```text
restore > ls
./joe/
.mozilla/ Desktop/ report.html
.tcshrc *Mail/ letter.txt
.xinitrc News/ www/
```

6. 现在使用 `extract` 命令开始提取过程。`restore` 将提示您输入起始磁带的编号。这是一个单磁带备份，因此只需输入数字 `1`。当它提示您为 ‘,’, ? 设置 owner/mode 时，通过输入 `y` 并按 Enter 键回答“是”。随后，`restore` 将恢复它正在恢复到的目录的文件权限（如有必要）。在像这样提取单个文件时，这并不是关键步骤，但在进行完整恢复时，您应该始终对此提示回答“是”。无论如何，您的屏幕现在应显示以下内容：

```text
restore > extract
You have not read any tapes yet.
Unless you know which volume your file(s) are on you
should start with the last volume and work toward the first.
Specify next volume #: 1
set owner/mode for ‘,’, ? [yn] y
restore >
```

此时，文件已恢复，您可以通过发出 `quit` 命令退出 `restore` 程序。就这样。您现在已掌握使用 `dump` 和 `restore` 命令的基本知识。

## 配置 Amanda 进行网络备份

使用 Amanda（高级马里兰自动网络磁盘归档器），您可以使用服务器上的单个大容量磁带驱动器通过网络备份来自多台计算机的文件。Amanda 软件包（amanda、amanda-client 和 amanda-server）包含各种命令。Amanda 的在线 man 页面描述的命令如表 12-6 所示。

### 表 12-6：与 Amanda 一起使用的备份命令

| 命令 | 描述 |
| :--- | :--- |
| **amdump** | 执行自动 Amanda 备份。此命令通常由名为磁带服务器主机的计算机上的 cron 运行，并请求对位于备份客户端上的文件系统执行备份。`amdump` 将 disklist 文件中的所有磁盘备份到磁带，或者在出现问题时备份到专用的暂存磁盘。所有备份完成后，`amdump` 会发送邮件报告失败和成功的情况。 |
| **amflush** | 将备份从暂存磁盘刷写到磁带。`amflush` 在 `amdump` 报告无法将备份写入磁带后使用。发生这种情况时，备份保留在暂存磁盘中。修复磁带问题后，运行 `amflush` 将暂存磁盘上的备份写入磁带。 |
| **amcleanup** | 清理被中断的 `amdump`。仅当 `amdump` 因某种原因（通常是因为磁带服务器主机在 `amdump` 运行时崩溃）无法完成时，才需要此命令。 |
| **amrecover** | 提供交互式界面以浏览 Amanda 索引文件并选择要从哪些磁带恢复文件。有时 `amrecover` 还可以运行 `amrestore` 和系统恢复程序（如 `lar`）。 |
| **amrestore** | 读取 Amanda 磁带，搜索请求的备份。`amrestore` 适用于从交互式恢复单个文件到完整恢复故障磁盘上所有分区的所有情况。 |
| **amlabel** | 在磁带上写入 Amanda 格式标签。所有 Amanda 磁带都必须使用 `amlabel` 进行标记。`amflush` 不会将数据写入未标记的磁带。 |
| **amcheck** | 验证磁带驱动器中的磁带是否正确，以及所有备份客户端系统上的所有文件系统是否准备好进行备份。可以选择在 `amdump` 之前通过 cron 运行，这样如果有人需要采取纠正措施以避免备份失败，他们就会收到邮件警告。 |
| **amadmin** | 处理管理任务，例如找出恢复文件系统所需的磁带、强制主机对选定磁盘执行完全备份以及查看计划平衡信息。 |
| **amtape** | 处理磁带更换器控制操作，例如装入特定磁带、弹出磁带以及扫描磁带架。 |
| **amverify** | 检查 Amanda 备份磁带的错误（仅适用于 GNU tar 格式备份）。 |
| **amrmtape** | 从磁带列表和 Amanda 数据库中删除磁带。 |
| **amstatus** | 提供正在运行的 `amdump` 的状态。 |

`amdump` 命令是您使用最频繁的命令，但在开始之前，您需要配置备份服务器（带有磁带驱动器的系统）和备份客户端（被备份的系统）上的几项内容。在 Amanda 客户端上，您需要安装 `amanda` 和 `amanda-client` 软件包。在 Amanda 服务器上，您还需要安装 `amanda-server` 软件包。

### 创建 Amanda 目录

您需要创建一些目录来存放 Amanda 配置文件，并提供写入 Amanda 日志文件的位置。配置文件位于 `/etc/amanda` 目录中，日志和数据库文件位于 `/var/lib/amanda`。在这两种情况下，您都应该以 `amandabackup` 用户身份登录，并在这些目录中创建子目录，每个计划运行的备份计划一个子目录以及一个索引文件，如下面的示例所示。

> **注意：** 出于安全原因以及确保 Amanda 命令可以访问其所需的所有必要文件，您应该以 `amandabackup` 用户身份执行所有 Amanda 管理任务。为此，root 用户可以通过输入 `passwd amandabackup` 并输入新密码来为 `amandabackup` 创建密码。然而，更好的替代方案可能是锁定 `amandabackup` 用户账户，然后简单地输入 `su - amandabackup`（如以下示例所示），以便在不额外使用密码的情况下以 root 用户身份执行 Amanda 任务。本过程的其余部分假设您已以 `amandabackup` 用户身份登录。

```bash
# su - amandabackup
# mkdir -p /var/lib/amanda/normal/index
# mkdir -p /etc/amanda/normal
```

为了本示例的目的，我仅创建了一个 `normal` 备份配置，用于备份几台机器上的数据驱动器。您可能还会决定创建一个 `upgrade` 备份配置来备份操作系统分区。然后，您可以在执行任何操作系统升级之前运行该备份。

您还需要指定一个 Amanda 可以使用的暂存磁盘，以便在将数据写入磁盘前临时暂存备份。该目录应有大量空闲空间。由于我的服务器上有一个大的 `/home` 分区，因此我在那里创建了一个 Amanda 目录用作暂存磁盘：

```bash
# mkdir /home/amanda
# chmod 700 /home/amanda
# chown amandabackup /home/amanda
# chgrp disk /home/amanda
```

### 创建 amanda.conf 文件

接下来，作为 `amandabackup` 用户，您必须为 Amanda 创建两个配置文件并将它们存储在 `/etc/amanda/normal` 目录中：`amanda.conf` 和 `disklist`。您可以通过从 `/etc/amanda/DailySet1` 目录复制这些文件的样本来开始，如下所示：

```bash
$ cd /etc/amanda/DailySet1
$ cp amanda.conf disklist /etc/amanda/normal
```

`amanda.conf` 文件设置各种一般配置值，而 `disklist` 文件定义要备份的机器和分区。`amanda.conf` 文件可能相当复杂，但幸运的是，其大多数值可以保留默认值。下面是一个简化版的 `amanda.conf` 文件，其中嵌入了一些注释以助于解释：

```text
#  
# amanda.conf - sample Amanda configuration file. This started life as  
#  the actual config file in use at CS.UMD.EDU.

org "GLACI"  # your organization name for reports  
mailto "amandabackup"  # space separated list of operators at your  
site  
dumpuser "amandabackup"  # the user to run dumps under

# Specify tape device and/or tape changer. If you don't have a tape  
# changer, and you don't want to use more than one tape per run of  
# amdump, just comment out the definition of tpchanger.

runtapes 1  # number of tapes to be used in a single  
  # run of amdump  
tapedev "/dev/nrft0"  # the no-rewind tape device to be used  
rawtapdev "/dev/rft0"  # the raw tape device to be used (ftape only)

tapetype HP-DAT  # what kind of tape it is  
  # (see tapetypes below)  
labelstr "^normal[0-9][0-9]*$"  # label constraint all  
  # tapes must match

# Specify holding disks. These are used as a temporary  
# staging area for dumps before they are written to tape and  
# are recommended for most sites.

holdingdisk hdl {  
  comment "main holding disk"  
  directory "/dumps/amanda"  # where the holding disk is  
  use -290 Mb  # how much space can we use on it  
  chunksize 1Gb  # size of chunk  
}

# Note that, although the keyword below is inofile, it is  
# only so for historic reasons, since now it is supposed to  
# be a directory (unless you have selected some database  
# format other than the 'text' default)

inofile "/var/lib/amanda/normal/curinfo"  # database DIRECTORY
```

