

# Amanda 配置示例

```bash
labelstr "-normal[0-9][0-9]*$"      # 标签约束全部
                                      # 磁带必须匹配

# 指定持有磁盘。这些磁盘作为转储写入磁带之前的临时
# 暂存区，推荐大多数站点使用。

holdingdisk hd1 {
    comment "主持有磁盘"
    directory "/home/amanda"       # 持有磁盘的位置
    use 290Mb                    # 可以使用多少空间
    chunksize -1                 # 块大小
}

# 请注意，尽管下面的关键字是 infofile，但
# 它之所以这样命名仅仅是出于历史原因，因为现在它应该
# 是一个目录（除非你选择了除默认 'text' 以外的某种数据库
# 格式）

infofile "/var/lib/amanda/normal/curinfo"   # 数据库目录
logdir "/var/lib/amanda/normal"          # 日志目录
indexdir "/var/lib/amanda/normal/index"   # 索引目录

# 磁带类型

# 在此定义你使用的磁带类型，并在上面的 "tapetype" 中
# 使用它。这里包含了一些典型的磁带类型。
# 磁带类型告诉 amanda 磁带上能容纳多少 MB，
# 文件标记有多大，以及磁带设备有多快。


define tapetype HP-DAT {
    comment "DAT 磁带驱动器"
    # 数据由 Rob Browning <rlb@ccs.utexas.edu> 提供
    length 1930 mbytes
    filemark 111 kbytes
    speed 468 kbytes
}

# dumptypes
#
# 这些在 disklist 文件中被引用。


define dumptype glocal {
    comment "全局定义"
    # 这对于设置全局参数非常有用，这样你
    # 就不必在所有地方重复输入它们。
}

define dumptype always-full {
    global
    comment "此文件系统始终全量转储"
    compress none
    priority high
    dumpcycle 0
}
```

这个示例 amanda.conf 文件是从我在 /etc/amanda/DailySet1 目录中复制的一个较大的示例中精简而来的。该示例 amanda.conf 文件提供了有关可用配置选项的额外信息。此外，Amanda 的在线 man 页应该会有所帮助（输入 `man amanda` 进行阅读）。你可以在 /usr/share/doc/amanda-server* 目录中找到更多说明。通常，你需要执行以下操作：

- 修改组织名称以便用于报告。
- 更改为 tapedev 和 rawtapedev 设置设备名称，使其与你的磁带设备匹配。
- 选择一个适合你磁带驱动器的磁带类型条目。
- 更改持有磁盘部分中指定的目录名称，使其与你之前创建的目录匹配。

## 创建 disklist 文件

你还必须在 /etc/amanda/normal 目录中创建一个 disklist 文件。该文件简单地包含要备份的系统及磁盘分区列表。每个条目中都包含限定符 always-full，以告知 Amanda 要执行什么类型的备份。这意味着使用全量备份而非增量备份。

```bash
# 示例 Amanda2 disklist 文件
#
# 文件格式为：
#
#       主机名 磁盘设备 dumptype [spindle [interface]]
#
# 其中 dumptype 由你在 amanda.conf 中定义。

dexter sda5 always-full
dexter sda6 always-full
dexter sda7 always-full
dexter sda8 always-full

daffy sda5 always-full
daffy sda6 always-full
daffy sda7 always-full
daffy sdb1 always-full
daffy sdb2 always-full
```

这个示例文件备份了两个系统，**dexter** 和 **daffy**。系统和分区的顺序经过选择，以确保最重要的数据首先被备份。这样，如果磁带驱动器已满，你仍然能够成功备份最重要的数据。

## 添加 Amanda 网络服务

Amanda 旨在通过网络执行备份。以下 amanda 服务定义在 /etc/services 文件中：

| 服务 | 端口/协议 |
| :--- | :--- |
| amanda | 10080/udp |
| amanda | 10080/tcp |
| amandaidx | 10082/tcp |
| amidxtape | 10083/tcp |

## 在 Amanda 服务器上

要在 CentOS 中向网络提供这些服务，你需要配置 xinetd 守护程序以监听这些服务。你可以通过输入以下内容来启用 amandaidx 和 amidxtape 服务（作为 root 用户）：

```bash
# chkconfig amidxtape on
# chkconfig amandaidx on
```

这使 Amanda 能够接受来自客户端系统的请求，并在无需用户干预的情况下启动备份过程。你需要告知 xinetd 守护程序重新加载 /etc/xinetd.d 文件，此更改才会生效。你可以作为 root 用户输入以下内容来实现：

```bash
# /etc/init.d/xinetd reload
```

## 在每个 Amanda 客户端上

接下来，你需要配置每个将由 Amanda 服务器进行备份的计算机（客户端）上 /var/lib/amanda 目录中的 .amandahosts 文件。该文件应包含任何将连接到此客户端的备份服务器的完全限定主机名和域名。开始时，此文件中只定义了你的本地主机作为备份服务器。若要添加另一台计算机作为备份服务器，请输入以下内容（将 amandahost 替换为备份服务器的名称，同时你需登录为 amanda 用户）：

```bash
$ echo amandahost >> /var/lib/amanda/.amandahosts
```

你还需要确保 amanda 客户端守护程序已配置为在客户端上运行。你可以通过输入以下内容来启用 amanda 服务（作为 root 用户）：

```bash
# chkconfig amanda on
```

这使 Amanda 客户端能够与 Amanda 服务器通信。你需要告知 xinetd 守护程序重新加载 /etc/xinetd.d 文件，此更改才会生效。请作为 root 用户输入以下内容执行操作：

```bash
# /etc/init.d/xinetd reload
```

## 执行 Amanda 备份

现在一切配置就绪，你可以执行 Amanda 备份了。在实际运行备份之前，你应该运行 amcheck 以检查你的驱动器和配置。当登录为 root 时，输入以下命令：

```bash
# /usr/sbin/amcheck DailySet1
# /usr/sbin/amdump normal
```

这执行了 amdump 命令，并告诉它读取在之前创建的 /etc/amanda/normal 目录中找到的配置文件。然后它按 disklist 文件中列出的系统和分区列表顺序工作，按出现顺序备份每个分区。amdump 的结果写入 /var/lib/amanda/normal 目录。阅读你在那里找到的文件以检查备份结果。（请参阅上一节关于如何创建 disklist 文件的内容，以理解 amdump 经过的过程。）

当然，你可以使用 cron 自动执行此过程。若要创建一个类似于早期部分讨论的常规转储计划的 amdump 计划，请执行以下操作。当登录为 root 时，输入带有 -e 选项的 crontab 命令：

```bash
# crontab -e
```

这将在编辑器中打开 root crontab 文件。将以下行添加到文件末尾：

```bash
0 22 * * 0 /usr/sbin/amdump normal
0 22 * * 1 /usr/sbin/amdump incremental
0 22 * * 2 /usr/sbin/amdump incremental
0 22 * * 3 /usr/sbin/amdump incremental
0 22 * * 4 /usr/sbin/amdump incremental
0 22 * * 5 /usr/sbin/amdump incremental
0 22 * * 6 /usr/sbin/amdump incremental
```

保存并退出文件。cron 守护程序将在每周每天下午 10:00（24 小时制为 22:00）运行 amdump。此示例假设已经创建了第二个增量配置。你可以通过在 /etc/amanda 下创建一个名为 incremental 的子目录，并填充适当修改的 amanda.conf 和 disklist 文件来实现。你还必须在 /var/lib/amanda 下创建一个名为 incremental 的子目录，以便 amanda 有地方为此配置写入日志文件。

将所有内容布置好可能需要一些工作，但一旦完成，Amanda 可以大大简化网络备份的管理。对于小型办公室来说，这可能有点过于复杂，但在大型企业网络环境中，它使 CentOS 能够充当一个强大的备份服务器。

## 使用 pax 归档工具

多年来，出现了各种 UNIX 操作系统，导致出现各种相似但不兼容的文件归档格式。即使名称相同的工具，其使用方式也可能略有

