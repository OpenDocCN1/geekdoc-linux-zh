
客户端仅通过 `telnet` 连接到集群。为了从集群中移除一个节点，集群管理员将仅使用以下命令：

```
#ipvsadm -e -t 209.100.100.100:23 -r 10.11.11.11:23 -g -w 0
```

在此命令中，`209.100.100.100` 是 VIP，`10.11.11.11` 是要移除的集群节点，`:23` 是 `telnet` 端口。在权重设置为大于 0 的数字之前，连接到 VIP 的新用户将无法访问 `10.11.11.11` 集群节点。案例研究中的假设组织每天下午 5 点换班。当所有用户在下午 5 点退出且新班上班时，系统管理员可以安全地重启集群。Idirect 重启后看到集群节点恢复在线，将自动将其重新加入 IPVS 表并供用户使用。

# 在集群环境中发送和接收电子邮件

在案例研究中，我们希望在集群节点上使用向客户发送外部电子邮件的应用程序。因此，每个集群节点将伪装外部电子邮件使其看起来来自同一个域名，使用每个集群节点 `/etc/mail/sendmail.mc` 文件中的条目：

```
MASQUERADE_AS('yourdomain.com').dnl
FEATURE('always_add_domain').dnl
FEATURE('masquerade_envelope').dnl
FEATURE('allmasquerade').dnl
```

我们还将电子邮件发送到集群（中继）电子邮件服务器，以便在电子邮件无法正常送达时更容易排除故障，在每个集群节点的 `/etc/mail/sendmail.mc` 文件中添加以下行：

```
define('SMART_HOST','mailserver.yourdomain.com').dnl
```

当 Joseph 和 Sam 在集群节点上拥有账户时，邮件将发送给 Joseph 或 Sam。为了强制这些邮件消息发送到中央邮件服务器，你还需要添加：

```
define(` LOCAL_RELAY`,`mailserver.yourdomain.com``)dnl
```

如果你需要设置例外，并强制某些邮件在集群节点上本地投递（例如，发送到 overprocessing 的邮件，它实际上是一个将邮件发送到某个程序进行自动处理的邮件别名），你可以使用如下条目：

```
LOCAL_USER(` `orderprocessing``)dnl
```

**注意**：`root` 用户始终在 `LOCAL_USER` 异常列表中。一旦对每个集群节点上的 `sendmail.mc` 文件进行了更改，你就需要使用以下命令创建一个新的 `sendmail.cf` 文件：

```
# m4 /etc/sendmail.mc > /etc/sendmail.cf
```

然后，在所有集群节点上停止并重启 `sendmail` 守护进程。

### 从命令行测试邮件

你可以使用命令 `mail -v tester@wherever.com` 来测试此更改是否会影响出站邮件的发件人（From）地址。此命令将提示你输入主题（Subject），然后提供输入邮件正文文本的机会。在新的一行按回车表示消息结束，并在提示输入 `Cc:` 邮件地址时按回车。你将看到在集群节点上运行的邮件会话记录尝试连接远程邮件服务器（如果你使用了上述的 `SMART_HOST` 选项，则为中央中继服务器）以及集群节点正在使用的发件地址。

# 创建无单点的批量作业调度系统

在最后一个案例研究中，我们想要构建一个没有单点的批量作业调度器。在这种情况下，我们再次假设集群受防火墙保护，集群节点之间不需要安全屏障。（与旧的单体服务器一样，`root` 权限被破解意味着破解者将访问所有内容）

我们将使用 `ssh` 构建一种从单台机器访问任何集群节点上的 shell 或运行命令的方法。

## 运行 ssh-keygen

回想第 4 章，`ssh-keygen` 命令可以在无密码的情况下使用因此因此在使用 `ssh` 命令时就不需要每次都输入密钥密码。在集群节点管理器上运行以下命令：

```
# ssh-keygen -t rsa
```

在提示时不要输入密码。现在，将集群节点管理器上 `/.ssh/id_rsa.pub` 文件的内容复制到每个集群节点的 `/root/.ssh/authorized_keys` 文件中。

## 修改每个集群节点上的 sshd_config 文件

我们信任 ssh 密钥来保护集群免受 root 用户攻击（你必须知道用于从集群节点管理器作为 root 用户连接到集群节点的 RSA 密钥的私半部分）。集群节点管理器上的 `root` 用户账户和 RSA 密钥的保护将像保护 root 密码一样重要。你可以使用 [LIDS](http://www. lids.org) 来隐藏此文件以增加安全性，或者创建一个没有 `root` 权限的独立集群管理账户。

修改每个集群节点 `/etc/ssh/sshd_config` 文件中的 `PermitRootLogin` 行，使其看起来如下：

```
PermitRootLogin without-password
```

然后，在每个集群节点上启动或重启 `sshd` 守护进程。

**注意**：确保每次集群节点启动时都启动 `sshd` 守护进程（参见第 1 章）。

## 在集群节点管理器上创建 (RSA) known_hosts 条目

在集群节点管理器上输入类似下面的命令：

```
# ssh cnode1 hostname
```

为每个集群节点运行一次命令，将示例中的 `cnode1` 替换为每个集群节点的名称。你应该看到类似下面的消息，这将允许为每个集群节点管理器保存主机密钥。

> 6 参见第 4 章中关于 `sudo` 命令的讨论，了解如何赋予特殊管理账户仅访问某些 root 级命令或权限。

主机 'node1' 的真实性无法确认。

RSA 密钥指纹为 04:54:c1:f3:33:ff:89:1a:08d:67:f5:43:21。

你确定要继续连接吗？(yes/no) yes

警告：已将 'node1' (RSA) 添加到已知 hosts 列表中。

**注意**：如果在每个集群节点上提示输入密码，请查阅第 4 章如何排查你的 `ssh` 配置。

## 批量作业调度器

我们将启动批量作业的系统称为批量作业调度器。在这种情况下，批量作业调度器是集群节点管理器（现在它已拥有访问所有集群节点的 ssh 权限）。批量作业调度器是一个高可用服务器，它将 `cron` 守护进程置于 Heartbeat 控制下，并使用 `crontab`⁷ 使用位于第 5 章目录下的 CD 刻光中的 cron 脚本提交批量作业。批量作业调度器上的示例 cron 表目如下：

```
30 14 *** clustersh /clusterdata/scripts/myscript
```

批量作业调度器上的此 cron 表目表示每天 14:30 运行集群脚本 `/clusterdata/scripts/myscript`。

**注意**：`crontab` 文件是 `cron` 守护进程用于存储作业列表的文件。为了在主作业调度器上备份该作业调度器，使用 `cron -e`。

`clustersh` 脚本包含了节点的主机名（见详细文档）。如果某个集群节点宕机，`clustersh` 将尝试执行 `/clusterdata/scripts/myscript`。如果你想在所有集群节点上每天 15:30 运行该脚本，crontab 条目将如下所示：

```
30 14 *** clustersh /clusterdata/scripts/myscript
```

使用此配置的一个危险是，你可能在主作业调度器上更改 `crontab` 但忘记在备份作业调度器上做相同更改。⁷ `crontab` 文件是 `cron` 守护进程用于存储作业列表的文件。为了在主作业调度器上备份该作业调度器，使用 `rsync` 来自以下脚本，它复制 `/var/spool/cron` 目录的内容：

```
#!/bin/bash
OPTS="--force --delete --ignore-errors -a -e ssh -z"
rsync $OPTS /etc/ha.d/          backup:/etc/ha.d/
rsync $OPTS /etc/hosts         backup:/etc/hosts
rsync $OPTS /etc/printcap      backup:/etc/printcap
rsync $OPTS /var/spool/lpd/    backup:/var/spool/lpd/
rsync $OPTS /etc/mon           backup:/etc/mon
rsync $OPTS /var/spool/cron/   backup:/var/spool/cron/
```

该配置的最后一行告诉 `rsync` 将 `/var/spool/cron` 的内容复制到主机名为 backup 的备份作业调度器。

# 结语
