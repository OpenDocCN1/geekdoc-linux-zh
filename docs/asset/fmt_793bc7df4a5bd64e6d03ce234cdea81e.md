
接下来你必须为 Amanda 创建两个配置文件并将它们存储在 `/etc/amanda/normal` 目录。`amanda.conf` 文件设置各种通用配置值，而 `disklist` 文件定义了备份哪些机器和分区。`amanda.conf` 文件可能相当复杂，但幸运的是，它的大部分值可以使用默认值。这是一个简化的 `amanda.conf` 文件，其中嵌入了一些注释以帮助解释：

```
# amanda.conf    示例 Amanda 配置文件。该文件是从
#               CS.UM.EDU 使用的实际配置文件开始的。

org "GLACI"      # 报告中的你的组织名称
mailto "root"    # 你站点的操作员分隔列表

dumpser "root"  # 运行 dump 的用户
```

# 指定带设备和/或带库。如果你没有带

# 更改器，如果你不想在每次 amdump 运行中使用多于一盘磁带，请注释掉 tpchanger 的定义。

`runtapes` `l` # 单次 `amdump` 运行中要使用的磁带数量

`tapedev` `/dev/nrtf0` # 将使用的不回带磁带设备

`trawtapev` `/dev/rft0` # 将使用的原始设备磁带设备（仅限 ftape）

`tapype` `HP-DAT` # 磁带的类型

#（详阅下文的 tapypes）

`labelstr` #DailySet[0-9][0-9]* # 所有磁带都必须匹配的标签限制

# 指定暂留磁盘（holding disks）。这些磁盘被用作备份在写入磁带之前的临时

# 阶段区域，这里是大多数站点的推荐配置。

```
holdingdisk hdl {
  "main holding disk"
  directory "/home/amanda" #暂留磁盘的位置
  use 290 MB # 在上面可以使用多少空间
  chunksize -1 # 块大小
}
```

# 注意，虽然下面的关键字是 infofile，但它

# 仅用于历史记录，因为现在它被认为是一个

# 目录（除非你选择了默认“text”以外的数据库格式）

```
infofile "/usr/sdm/amanda/normal/curinfo" # 数据库目录
logdir "/usr/sdm/amanda/normal" # 日志目录
indexdir "/usr/sdm/amanda/normal/index" # 索引目录
```

# tapypes

 在此处定义你使用的磁带类型，并在上面的

# "tapype" 中引用。这里包含了一些典型的磁带类型。

# tapype 告诉 amanda 磁带能容纳多少 MB，文件名

# 有大，以及磁带设备有多快。

```
define tapype HP-DAT {
  comment "DAT 磁带驱动"
  # 数据由 Rob Browning <rlb@cs.utexas.edu> 提供
  length 1930 mbytes
  filemark 111 kbytes
  speed 468 kbytes
}
```

# dumpypes

#

# 这些类型由 disklist 文件引用。

# 第 13 章 ♦ 备份和恢复文件 479

```
define dumptype global (
comment "全局定义"
# 这对于设置全局参数非常有用，这样你就不
# 需要在处处输入它们。
)
```

```
define dumptype always-full (
global
comment "始终对此文件系统进行全备"
compress none
priority high
dumpcycle 0
)
```

这个 `amanda.conf` 示例是从 `/etc/amanda/DailySet1` 中一个较大的示例中精简而来的。与其从零开始编写配置文件，我建议你从示例 `amanda.conf` 开始，并根据需要进行修改。示例 `amanda.conf` 提供了有关可用配置选项的额外信息。此外，Amanda 的在线页面应该很有帮助（输入 `man amanda` 读取它）。你可以在 `/usr/share/doc/amanda-server/` 目录中找到更多指令。通常，你必须执行以下操作：

- 修改报告名称。
- 更改为 `tapedv` 和 `rawtapedev` 指定的设备名称，使其与你的磁带设备匹配。
- 选择适用于你的驱动器的磁带类型条目。
- 修改暂留磁盘部分指定的目录名称，以匹配你之前创建的目录。

# 创建 disklist 文件

你还必须在 `/etc/amanda/normal` 目录下创建一个 `disklist` 文件。它仅包含一个要备份的系统和备份列表。每个条目都包含了 `always-full` 限定符，用于告诉 Amanda 执行什么种类型的备份。这意味着使用全量备份，而不是增量备份。

```
# Amanda2 磁盘list 文件示例
# 文件格式为：
# hostname diskdev dumptype [spindle [interface]]
# 其中 dumptypes 是你在 amanda.conf 中定义的。
```

```
dexter hda5 always-full
dexter hda6 always-full
```

访问 www.unlted.com 获取更多额外内容

# 480 第三部分 + 管理 Red Hat Linux

```
dexter hda7 always-full
dexter hda8 always-full
ndaffy hda5 always-full
daffy hda6 always-full
daaffy hda7 always-full
daffy hdb1 always-full
daffy hdb2 always-full
```

此示例备份了两个系统：`dexter` 和 `daffy`。系统和分区的顺序经过选择，确保最重要的数据首先备份。这样，如果磁带驱动满了，你仍然成功备份了最重要的数据。

# 添加 Amanda 网络服务

Amanda 设计设计用于在网络上执行备份。在 `/etc/services` 文件中定义了以下 amanda 服务：

```
amanda      10080/udp
amandaix    10082/tcp
amidtape   10083/tcp
```

要在 Red Hat Linux 向网络提供这些服务，你需要配置 `xinetd` 守护进程来监听这些服务。你通过启用 `/etc/xinetd.d` 目录下的 `amandaix` 和 `amidtape` 文件中的服务来实现这一点。在这些文件的每个文件中，你需要将 `disable` 行更改为 `no`，如下：

```
disable      = no
```

这使得 Amanda 能够接受来自客户端系统的请求并在无需用户干预的情况下启动备份过程。你需要通过让 `xinetd` 守护进程重新加载来实现这一点，以 root 用户：

```
/etc/init.d/xinetd restart
```

你需要在 `/root` 目录下创建一个 `disklist` 文件。这仅仅包含一个要备份的系统和备份列表。每个条目都包含了 `always-full` 限定符，用于告诉 Amanda 执行什么种类型的备份。这意味着使用全量备份，而不是增量备份。

你可以通过 root 用户执行以下操作，在 `/root` 目录下创建 `amosts` 文件：

```
# echo "always-full" > /root/amosts
```

为了确保只有 root 可以访问，对该文件进行修改：

```
# chmod 600 /root/amosts
```

这使得 Amanda 能够接受来自客户端系统的请求并在无需用户干预的情况下启动备份过程。你需要通过让 `xinetd` 守护进程重新加载来实现这一点，以 root 用户：

```
/etc/init.d/xinetd restart
```

你需要在 root 用户 用户执行以下操作，创建一个 `amosts` 文件：

```
# echo "always-full" > /root/amosts
```

## 第13 章 备份与恢复文件 483

| Pax 命令 | 描述 |
|---|---|
| `pax -w -f myfiles *.txt` | 归档当前目录下所有以 .txt 结尾的文件。 |
| `pax -r -w /olddir /newdir` | 将 `/olddir` 目录的所有内容复制到新目录 `/newdir` 中。 |
| `pax -w -B 1440000 -f /dev/fd0 *` | 将当前目录的内容归档到多块软盘上。 |
| `pax -w -x cpio -f myfiles *` | 使用 `cpio` 格式将当前目录的内容归档为名为 `myfiles` 的归文件。 |
| `pax -r -U mary -f backups` | 从名为 `backups` 的归文件中提取所有用户 `mary` 拥有的文件。 |
