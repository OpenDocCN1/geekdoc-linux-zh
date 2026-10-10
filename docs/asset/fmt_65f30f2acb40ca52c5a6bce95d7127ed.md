
| `amflush` | 将保留磁盘中的备份刷新磁带。当 `amdump` 报告无法写入磁带时使用 `amflush`。此时备份留在保留磁盘。修复磁带问题后，运行 `amflush` 将保留磁盘的写入写入带。 |
| `amcleanup` | 对中断的 amanda 进行清理。只有当 amanda 因某种原因无法完成时（通常是磁带服务器在运行时运行时崩溃），才需要此命令。 |
| `amrecover` | 提供交互式界面以浏览 Amanda 索引文件并选择从哪些磁带进行恢复。`amrecover` 还可以运行 `amrestore` 和系统恢复程序（如 `tar`）。 |
| `amrestore` | 读取 Amanda 磁带并搜索请求的备份。`amrestore` 适用于从单个文件的交互恢复到故障磁盘所有分区的完整恢复。 |
| `amlabel` | 在磁带上写入 Amanda 格式标签。所有 Amanda 磁带都必须使用 `amlabel`。`amdump` 和 `amflush` 不写入未标记的磁带。 |
| `amcheck` | 验证正确的磁带在磁带机中，并确保备份系统上的所有文件已准备好备份。可选在 `amdump` 之前由 cron 运行，这样人们就会收到邮件警告，如果不采取正确行动备份将失败。 |
| `admin` | 处理管理任务，例如查找恢复文件系统所需的磁带、强制对选定磁盘进行全备以及查看调度平衡信息。 |
| `amtape` | 处理磁带库控制操作，如加载特定磁带、卸出磁带和扫描磁带架。 |
| `amverify` | 检查 Amanda 备份磁带是否有错误（仅限 GNU tar 格式备份）。 |
| `amrmtape` | 从磁带列表和 Amanda 数据库中删除磁带。 |
| `amstatus` | 提供运行中的 `amdump` 的状态信息。 |

# 第 13 章：备份与恢复文件 567

`amdump` 命令是你使用最频繁的命令，但在开始之前，你需要在备份服务器（带有磁带驱动器的系统）和备份客户端（被备份的系统）上进行一些配置。在 Amanda 客户端上，你需要安装 `amanda` 包。在 Amanda 服务器上，你也需要安装 `amanda-server` 包。

## 创建 Amanda 目录

你需要创建一些目录来存放 Amanda 配置文件，并为写入 Amanda 日志文件提供位置。配置文件放在 `/etc/amanda` 目录，日志文件放在 `/var/lib/amanda`。在这两种情况下，你都应该以 `amanda` 用户身份登录并在这些目录中创建子目录，为你打算运行的每个备份计划创建一个子目录和一个索引文件，如下例所示。

> 注意：出于安全考虑，你应该以 `amanda` 用户身份执行所有管理操作。要做到这一点，root 用户可以通过传递 `amanda` 并输入新密码为 `amanda` 创建密码。然而，更好的替代方案是锁定 `amanda` 用户账户，然后简单地输入 `su - amanda`（在下例中）以 root 用户身份执行 `amanda` 任务而无需额外密码。此过程的其余部分确保了你是以 `amanda` 用户登录的。

```
# su amanda
$ mkdir -p /var/lib/amanda/normal/index
$ mkdir -p /etc/amanda/normal
```

为了本示例，我只创建了一个备份几台服务器数据的普通备份配置。你也可以决定创建一个备份操作系统分区的升级备份配置。然后你可以在执行任何操作系统升级之前运行该备份。

你还需要指定一个 Amanda 可以使用的暂留磁盘（holding disk），在将备份写入磁盘之前临时将其缓存在。此目录应该有大量的空闲空间。我的服务器上有一个较大的 `/home` 分区，所以我创建了一个 Amanda 目录作为暂留磁盘：

```
# mkdir /home/amanda
# chmod 700 /home/amanda
# chown amanda /home/amanda
# chgrp disk /home/amanda
```

## 创建 amanda.conf 文件

接下来，作为 `amanda` 用户，你必须为 Amanda 创建两个配置文件并将它们存储在 `/etc/amanda/normal` 目录中：`amanda.conf` 和 `disklist`。你可以先从 `/etc/amanda/DailySet1` 目录复制这些文件的样本如下：

```
$ cd /etc/amanda/DailySet1
$ cp amanda.conf disklist /etc/amanda/normal
```

`amanda.conf` 文件设置了各种通用配置值，而 `disklist` 文件定义了要备份哪些机器和分区。`amanda.conf` 文件可能相当复杂，但幸运的是，大部分值可以保持默认值。这里有一个简化的 `amanda.conf` 文件，其中嵌入了一些注释以帮助解释：

```
#
# amanda.conf - amanda 示例配置文件。这最初是
# 在 CS.UMD.EDU 使用的实际配置文件。

org "GLACI" ## 报告中的你的组织名称
mailto "amanda" # 站点操作员的空格分隔的列表
dumperuser "amanda" # 运行备份的用户

# 指定磁带设备/或磁带库。如果你没有磁带
# 库，且你不想希望在每次 amdump 运行中使用超过一块磁带，
# 请直接注释掉 tpchanger 的定义。

tuntapes 1 # 单次 amdump
# # 运行中使用的磁带数量
tapedev "/dev/nrft0" # 将使用的不回绕磁带设备
rawtapedev "/dev/rft0" # 将使用的原始设备（仅限 ftape）

tatype HP-DAT # 磁带的类型
# #（在下文中设置 tapypes）
labelstr "*normal[0-9][0-9]*" # 标签约束所有
# # 磁带必须匹配

# 指定暂留磁盘。这些用作 dump 写入磁带
# 之前的临时阶段区域，并 # 建议大多数站点使用。

holdingdisk hdl1 {
    comment "主暂留磁盘"
    directory "/home/amanda" # 暂留磁盘的位置
    use 290 Mb # 在上面可以使用多大空间
    chunksize -1 # 块大小
}

# 注意，尽管下面的关键字是 infofile，但由于
# 历史原因，它现在应该被认为是一个
# 目录（除非你选择了除默认 'text' 以外的
# 数据库格式）

infile "/var/lib/amanda/curinfo" # 数据库目录
logdir "/var/lib/amanda/normal/" # 日志目录
indexdir "/var/lib/amanda/normal/index" # 索引目录

# tapypes
```

# 在此处定义你使用的磁带类型，并在上面的 "tapype"

# 中它。这里包含了一些典型的磁带类型。

# tapype 告诉 amanda 磁带可以容纳多少 MB，

# 文件标记有多大，以及磁带设备有多快。

```
define tapype HP-DAT {
  comment "DAT 磁带驱动器"
  # 由 Rob Browning <rlb@cs.utex.edu> 提供的数据
  length 1930 mbytes
  filemark 111 kbytes
  speed 468 kbytes
}
```

```
# dumptypes
# 这些由 disklist 文件引用。
```

```
define dumpype always-full {
  global
  comment "此文件系统的全备份"
  # 对于设置全局参数非常有用，
  # 无需处处输入。
}
```

这个示例 `amanda.conf` 文件是从 `/etc/amanda/DailySet1` 复制并裁剪而来的。示例 `amanda.conf` 提供了可用选项的额外信息。此外，Amanda 的在线页面（输入 `amanda` 读取）将会有帮助。通常情况下，你需要执行以下操作：

- 修改报告的 `org` 名称。
- 修改 `tapedev` 和 `rawdev` 名称以匹配你的磁带设备。
- 选择适用于你的磁带驱动器的 `tape` 类型。
- 修改 `holding` 部分的设备名称以匹配你创建的目录。

## 创建 disklist 文件

你还必须在 `/etc/amanda/normal` 目录中创建一个 `disklist` 文件。它包含要备份的系统和分区列表。每个条目上的 `always-full` 限定符告诉 Amanda 执行何种类型的备份。
