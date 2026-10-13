
# Specify holding disks. These are used as a temporary
# staging area for dumps before they are written to tape and
# are recommended for most sites.

`holdingdisk` `hd1` {
    comment "main holding disk"
    directory "/home/amanda"  # where the holding disk is
    use 290 Mb               # how much space can we use on it
    chunksize -1             # size of chunk
}

# Note that, although the keyword below is infofile, it is
# only so for historic reasons, since now it is supposed to
# be a directory (unless you have selected some database
# format other than the `text` default)

`infofile` "/usr/adm/amanda/normal/curinfo"   # database DIRECTORY
`logdir`   "/usr/sdm/amanda/normal"            # log directory
`indexdir` "/usr/adm/amanda/normal/index"      # index directory

# tapetypes
# Define the type of tape you use here, and use it in "tapetype"
# above. Some typical types of tapes are included here. The
# tapetype tells amanda how many MB will fit on the tape, how
# big the filemarks are, and how fast the tape device is.

`define` `tapetype` `HP-DAT` {
    comment "DAT tape drives"
    # data provided by Rob Browning <rlb@cs.utexas.edu>
    length 1930 mbytes
```

```
    filemark 111 kbytes
    speed 468 kbytes
}
```

## 转储类型

# 这些由磁盘列表文件引用。

`define` `dump` `type` `global` {
    comment "Global definitions"
    # 这对于设置全局参数非常有用，这样你
    # 就不必到处输入它们了。
}

`define` `dump` `type` `always-full` {
    global
    comment "Full dump of this filesystem always"
    compress none
    priority high
    dumpcycle 0
}

这个示例 `amanda.conf` 是从我从 `/etc/amanda/DailySet1` 目录复制的较大示例中删减而来的。示例 `amanda.conf` 文件提供了有关可用配置选项的额外信息。此外，Amanda 的在线手册页也应该有所帮助（输入 `man amanda` 以阅读它）。你可以在 `/usr/share/doc/amanda-server*` 目录中找到更多说明。一般来说，你必须执行以下操作：

- 修改报告的组织名称。
- 将为 `tapepdev` 和 `rawtapepdev` 设置的设备名称更改为与你的磁带设备相匹配。
- 选择适合你的磁带驱动器的磁带类型条目。
- 将 `holding disk` 部分中指定的目录名称更改为与你之前创建的目录相匹配。

## 创建磁盘列表文件

你还必须在 `/etc/amanda/normal` 目录中创建一个磁盘列表文件。它只包含要备份的系统和磁盘分区的列表。限定符 `always-full` 包含在每个条目中，以告诉 Amanda 执行何种类型的备份。这意味着使用完全备份，而不是增量备份。

```
# sample Amanda2 disklist file
#
# File format is:
#
#       hostname diskdev dumptype [spindle [interface]]
#
# where the dumptypes are defined by you in amanda.conf.
dexter hda5 always-full
dexter hda6 always-full
dexter hda7 always-full
dexter hda8 always-full
daffy hda5 always-full
daffy hda6 always-full
daffy hda7 always-full
daffy hdb1 always-full
daffy hdb2 always-full
```

此示例文件备份了两个系统，`dexter` 和 `daffy`。系统和分区的顺序被选定，以便最重要的数据首先被备份。这样，如果磁带驱动器已满，你仍然设法备份了最重要的數據。

## 添加 Amanda 网络服务

Amanda 设计用于通过网络执行备份。以下 `amanda` 服务在 `/etc/services` 文件中定义：

| 服务 | 端口 |
| :--- | :--- |
| amanda | 10080/udp |
| amanda | 10080/tcp |
| amandaidx | 10082/tcp |
| amidxtape | 10083/tcp |

## 在 amanda 服务器上

为了在 Red Hat Linux 中向网络提供这些服务，你需要配置 `xinetd` 守护进程以侦听这些服务。你通过以 root 用户身份输入以下内容来启用 `amandaidx` 和 `amidxtape` 服务：

```
# chkconfig amidxtape on
# chkconfig amandaidx on
```

这使 Amanda 能够接受来自客户端系统的请求并在无需用户干预的情况下启动备份过程。你需要在此更改生效前通知 `xinetd` 守护进程重新加载 `/etc/xinetd.d` 文件。你可以通过以 root 用户身份输入以下内容来执行此操作：

```
/etc/init.d/xinetd restart
```

## 在每个 amanda 客户端上

接下来，你需要在 `amanda` 服务器将要备份的每台计算机（客户端）上的 `/var/lib/amanda` 目录中配置 `.amandahosts` 文件。该文件应包含将连接到此客户端的任何备份服务器的完全限定主机和域名。开始时，只有你的 `localhost` 在该文件中被定义为备份服务器。要将另一台计算机添加为备份服务器，你可以输入以下内容（以 `amanda` 用户身份登录时，将 `amandahost` 替换为备份服务器的名称）：

```
$ echo amandahost > /var/lib/amanda/.amandahosts
```

你还需要确保 `amanda` 客户端守护进程已配置为在客户端上运行。你通过以 root 用户身份输入以下内容来启用 `amanda` 服务来执行此操作：

```
# chkconfig amanda on
```

这使 `amanda` 客户端能够与 `amanda` 服务器通信。你需要在此更改生效前通知 `xinetd` 守护进程重新加载 `/etc/xinetd.d` 文件。你可以通过以 root 用户身份输入以下内容来执行此操作：

```
# /etc/init.d/xinetd restart
```

## 执行 Amanda 备份

现在一切都已配置好，你可以执行 Amanda 备份了。以 root 身份登录时，输入以下命令：

```
/usr/sbin/amdump normal
```

这会运行 `amdump` 命令并指示它读取在之前创建的 `/etc/amanda/normal` 目录中找到的配置文件。然后它按顺序遍历磁盘列表文件中的系统和分区列表，按其出现的顺序备份每个分区。`amdump` 的结果写入 `/var/lib/amanda/normal` 目录。阅读你在那里找到的文件以检查备份结果。（参见上一节关于如何创建磁盘列表文件以了解 `amdump` 所经历的过程。）

当然，你可以使用 `cron` 自动执行此过程。要创建与前面章节中讨论的常规 dump 调度类似的 `amdump` 调度，请执行以下操作。以 root 身份登录时，使用 `-e` 选项输入 `crontab` 命令：

```
# crontab -e
```
