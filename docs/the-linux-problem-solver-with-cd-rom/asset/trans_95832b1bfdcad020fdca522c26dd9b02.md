
# 问题 97

症状：磁带容量超出限制。磁带容量未被充分利用。

问题：磁带几何规格不正确。

修复：几何设置正确非常重要，因为如果 Amanda 误以为磁带比实际更长，就可能向磁带写入过多数据。你应该可以在手册中找到这些信息，但如果你无法找到（无论在你的磁带驱动器手册中还是在默认的 amanda.conf 文件中），请查看 Amanda 主页上的 tapetypes 列表链接。

接下来，更改 holding disk（用于在将备份数据写入磁带之前存储备份数据的大型磁盘分区）的定义。默认设置如下：

```
holdingdisk hdi {
  comment "main holding disk"
  directory "/dumps/amanda"
  use 290 Mb
  chunksize -1
}
```

将 /dumps/amanda 改为你有足够磁盘空间的某个目录；你应该将其命名为 amanda（或其他有辨识度的名称），因为你将在这个目录中创建许多内容。暂时不用理会 chunksize 参数，因为你将从一个 holding disk 开始。

现在更改索引和日志的位置：

```
infofile "/usr/adm/amanda/DailySet1/curinfo"   # database DIRECTORY
logdir  "/usr/adm/amanda/DailySet1"            # log directory
indexdir "/usr/adm/amanda/DailySet1/index"     # index directory
```

在 Linux 下，/usr/adm 不是放置这类内容的常规位置，所以请使用其他位置，例如 /var/log/amanda。但请确保你有足够的磁盘空间。如果你要备份大量的机器和文件，索引文件可能会增长到几十兆字节。

在运行任何 Amanda 程序之前，请确保你为数据库、索引和日志位置设置的目录存在。

在 tapetype 定义之后，你会看到一些具有以下结构的 dump type 定义：

```
define dumptype global {
}
define dumptype root-tar {
    global
    program "GNUTAR"
    comment "root partitions dumped with tar"
    compress none
    index
    exclude list "/usr/local/lib/amanda/exclude.gtar"
    priority low
}

define dumptype user-tar {
    root-tar
    comment "user partitions dumped with tar"
    priority medium
}
```

注意每个 define 通常都建立在前一个 define 之上。global define（你应该将其包含在所有定义中）默认为空。root-tar 包含一组针对 / 分区的设置（GNU tar 格式、索引、无压缩和一个要排除的文件列表）。user-tar 的结构几乎相同，所以它的定义只是包含了 root-tar。（我们将在下面的“高级配置”一节中更详细地讨论这些定义。）

## disklist

disklist 文件的格式如下：

```
atlantic   /home      user-tar
mikado     /etc       root-tar
pacific    /usr/local root-tar
```

第一个字段指定要备份的机器（这里我们备份的是名为 atlantic、mikado 和 pacific 的机器），第二个字段标识目标目录，第三个字段指定转储类型（amanda.conf 中 dumptype 定义之一；参见上一节）。刚开始时，你应当在这个文件中只放置一行——选择一台不太忙的机器上的一个小目录。从小处着手，因为在大量机器和目录上调试 Amanda 需要更长时间。

## 安装客户端软件

在配置好 amanda.conf 和 disklist 文件并将其放在服务器上之后，将 Amanda 客户端软件安装到你要备份的机器上。这是一个相当标准的 inetd 服务，在 /etc/inetd.conf 中有如下行：

```
amanda dgram udp wait root /usr/local/libexec/amandad
amandaidx stream tcp nowait root /usr/sbin/tcpd /usr/local/amanda/libexec/amindexd
amidxtape stream tcp nowait root /usr/sbin/tcpd /usr/local/amanda/libexec/amidxtaped
```

/etc/services 文件包含：

| amanda | 10080/udp | # amanda 备份服务 |
| kamanda | 10081/tcp | # amanda 备份服务（Kerberos） |
| kamanda | 10081/udp | # amanda 备份服务（Kerberos） |
| amandaidx | 10082/tcp | # amanda 备份服务 |
| amidxtape | 10083/tcp | # amanda 备份服务 |

## 测试你的配置

在驱动器中放入空白磁带，并查看 amanda.conf 中的 labelstr。示例 amanda.conf（在 example 目录中）中的 labelstr 是

```
labelstr "DailySet[0-9][0-9]*"
```

这是一个正则表达式；它匹配任何以 DailySet 开头且后跟至少一个数字的字符串。要让 Amanda 接受用于备份的磁带，你需要在磁带上创建一个新标签。假设你坚持使用默认值。要写入一个与 labelstr 匹配的磁带标签，请运行以下命令（假设 01 是该系列磁带中的第一个磁带编号）：

```
# amlabel servers DailySet101
```

现在，你可以运行 amcheck 来查看备份是否能正常进行（仍然假设我们的配置目录是 servers）：

```
# amcheck servers
```

输出如下：

```
Amanda Tape Server Host Check

/var/spool/amanda: 1331470 KB disk space available, that's plenty.
NOTE: skipping tape-writable test.
Tape dailytap e01 label ok.
Server check took 31.260 seconds.
```

