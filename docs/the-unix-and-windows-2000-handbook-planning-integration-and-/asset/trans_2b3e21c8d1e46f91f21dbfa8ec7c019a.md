
对于 line，第一个配置项（:lp:）指定了该打印机的设备名。由于 line 打印机是远程打印机，因此我们不需要为 lp 赋值。对于 line，第二个配置项指定了远程机器名（server1.sniglets.com），lpd 将连接该机器以传输控制文件和数据文件。第三个配置项（:rp:line:）指定了该打印机在远程机器上的名称。第四个配置项指定了该打印机在本地机器上的假脱机目录。最后一个配置项指定了错误日志文件。

请注意，两台打印机共享同一个错误日志文件（/var/spool/lp/errlog）。错误日志文件中的每个条目都包含生成该错误行的打印机名称。错误日志文件对于排查本地打印机的问题以及判断与远程打印机的通信问题非常重要。错误日志文件随着时间推移可能会变得非常大。为了限制该文件的增长，应每周运行一个简单的 shell 脚本来轮转日志。下面的 shell 脚本应通过 cron 每周运行，并将在 /var/spool/lp 目录中保留四个星期的压缩日志文件。

```
#!/bin/sh
# Rotate printer error logfile
#
SPOOLDIR=/var/spool/lp
if test -d $SPOOLDIR
then
    cd $SPOOLDIR
    if test -s $ERRLOG
    then
        test -f $ERRLOG.1.gz && mv $ERRLOG.1.gz $ERRLOG.2.gz
        test -f $ERRLOG.0.gz && mv $ERRLOG.1.gz
        mv $ERRLOG $ERRLOG.0
        /usr/local/bin/gzip -9 $ERRLOG.0
        cp /dev/null $ERRLOG
        chmod 644 $ERRLOG
    fi
fi
```

打印机可以共享同一个错误日志文件，但不应共享假脱机目录。必须为所有本地连接和远程打印机创建假脱机目录。打印作业的控制文件和数据文件在发送到本地打印机或传输到远程机器之前，会存储在该目录中。系统管理员在添加新打印机时必须创建该目录。创建假脱机目录的步骤将在下一段中介绍。

假设你最近购买了一台新的 Postscript 打印机，并希望将其添加到本地 UNIX 工作站。新打印机将连接到工作站的并行端口（/dev/lp1），并命名为 laser 和 post。这台打印机还将使用一个输入过滤器将文本文件转换为 Postscript。需要将以下行添加到 /etc/printcap 文件中：

```
Laser|post|Postscript printer in Rm 155:\
:lp=/dev/lp1:\
:sd=/var/spool/lp/laserjet:\
:if=/var/spool/lp/errlog:\
:lf=/usr/local/etc/filters/iflaser:
```

下一步是创建假脱机目录 /var/spool/lp/laser。目录权限应为 775，所有者和组设置为 daemon。要创建目录，请输入以下命令：

```
# mkdir /var/spool/lp/laser
```

要设置该目录的所有者，请输入以下命令：

```
# chown daemon /var/spool/lp/laser
```

接下来，将该目录的组设置为 daemon：

```
# chgrp daemon /var/spool/lp/laser
```

最后，更改权限：

```
# chmod 775 /var/spool/lp/laser
```

打印机在网络中非常常见。与通过串行或并行端口连接的打印机相比，它们提供了更容易的访问和更快的连接。网络上的每台打印机都需要分配一个 IP 地址。请查阅打印机附带的文档，以配置合适的 IP 地址。

网络打印机的 printcap 条目与远程打印机的相同。清单 10.1 中的打印机 swat 被视为远程打印机。rm 条目包含分配给该打印机的完全限定域名（FQDN）。指定远程机器时，应始终使用 FQDN。FQDN 确保打印作业将发送到 swat.sniglets.com。如果将 rm 条目指定为 swat，则可能导致作业被发送到 swat.mark.sniglets.com，而不是 swat.sniglets.com。

## 控制命令

lpq 命令提供打印假脱机队列的快照。清单 10.2 包含 lpq 命令的输出。它包括排名、所有者、
