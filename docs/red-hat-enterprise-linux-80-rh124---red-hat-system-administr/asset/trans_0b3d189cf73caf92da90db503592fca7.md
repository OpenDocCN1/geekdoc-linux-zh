

anaconda
dnf.rpm-log-20190318 private
audit
dnf.rpm-log-20190324 qemu-ga
boot.log
dnf.rpm-log-20190331 README
...输出已省略...

> 重要
> 在输入 rsync 命令的源目录时，务必记住目录名称末尾是否有斜杠至关重要。它决定了是将目录本身还是仅目录的内容同步到目标位置。

Bash Tab 补全会在目录名末尾自动添加斜杠。

与 sc 和 sftp 命令一样，对于 rsync，你使用 `[user]@host:/path` 格式指定远程位置。远程位置可以是源系统也可以是目标系统，但两台机器中有一台必须是本地。

为了保留文件所有权，最好位于目标系统上。如果目标是远程的，请以 root 身份验证。如果目标是本地的，你必须以 root 运行 rsync。

在此示例中，将本地的 /var/log 目录同步到 remotehost 上的 /tmp 目录：

```
[root@remotehost]# rsync -av /var/log remotehost:/tmp
root@remotehost's password: password
正在增量文件列表
log/
log/README
log/boot.log
...输出已省略...
sent 9,783 bytes received 290,576 bytes 85,816.86 bytes/sec
total size is 11,585,690 speedup is 38.57
```

同样，remotehost 上的 /var/log 远程目录可以同步到本地的 /tmp 目录：

```
[root@remotehost]# rsync -av remotehost:/var/log
root@remotehost's password: password
正在增量文件列表
log/boot.log
log/dnf.librepo.log
log/dnf.log
...输出已省略...
sent 9,783 bytes received 290,576 bytes 85,816.86 bytes/sec
total size is 11,585,690 speedup is 38.57
```

## 参考文献

rsync(1) 手页

## 引导练习

## 安全地在系统之间同步文件

在此练习中，你将通过通过 SSH 使用 rsync，将本地目录的内容与远程服务器上的副本进行同步。

## 结果

你应当能够使用 rsync 命令将本地目录的内容与远程服务器上的副本进行同步。

## 开始之前

在工作站上使用 student 密码登录 student 用户。

从工作站运行 `lab archive-sync start` 命令。该命令运行一个启动脚本，用于判断主机 servera 和 serverb 是否在网络上可达。脚本还会确保练习中要创建的文件和目录不存在于 servera 上。

```
[student@workstation ~$] lab archive-sync start
```

- 1. 使用 ssh 命令以 student 用户身份登录 servera。

```
[student@workstation ~$] ssh student@servera
[student@servera ~$]$
```

- 2. 在 servera 上创建一个名为 /home/student/serverlogs 的目录。使用 rsync 命令在 serverb 上创建 /var/log 目录树的初始拷贝到 servera 的 /home/student/serverlogs 目录中。

2.1. 在 servera 上，创建目标目录 /home/student/serverlogs 以存储从 rsync 同步的日志文件。

```
[student@servera ~$] mkdir -p ~/serverlogs
```

2.2. 使用 rsync 命令将 serverb 上的 /var/log 目录树同步到 servera 的 /home/student/serverlogs 目录。注意，只有 root 用户可以读取 serverb 上 /var/log 目录的所有内容。所有文件将在初始同步中传输。

```
[student@servera ~$] rsync -av root@serverb:/var/log ~/serverlogs
root@serverb's password: redhat
正在增量文件列表
log/
```

```
log/README
log/boot.log
...输出已省略...
tuned/tuned.log
```

sent 992 bytes received 13,775,064 bytes 2,119,393.23 bytes/sec
total size is 13,768,109 speedup 1.0
```

- 3. 在 serverb 上以 root 身份执行 `logger "Log files synchronized"` 命令，在 /var/log/messages 日志文件中创建一个新条目，以反映上次同步的时间。

```
[student@servera ~]$ ssh root@serverb 'logger 'Log files synchronized'
Password: redhat
[student@servera ~]
```

- 4. 使用 rsync 命令从 server 上的 /home/student/serverlogs 目录树安全地同步到 server。注意这次只有已传输的日志文件。

```
[student@servera ~]$ rsync -av root@serverb:/var/log ~/serverlogs
root@serverb's password: redhat
正在增量文件列表
log/messages
log/secure
log/audit/audit.log
```

sent 3,496 bytes received 27,243 bytes 782.57 bytes/sec
total size is 11,502,695 speedup 374.21
```

- 5. 退出 servera。

```
[student@servera ~] exit
Connection to servera.
[student@workstation]$
```

## 完成

在工作站上运行 `lab archive-sync finish` 完成此练习。

```
[student@workstation ~]$ lab archive-sync finish
```

此引导练习结束。

## 归档并传输文件

## 检查列表

在实验中，你将使用 tar、rsync 和 scp 对目录内容进行归档和备份。

## 结果

你应该能够：

- 将远程目录同步到本地目录。
- 创建同步目录内容的归档。
- 安全地将归档拷贝到远程主机。
- 提取归档。

## 开始之前

在工作站上使用密码登录 student 用户。

从工作站运行 `lab archive-review start` 命令。该命令运行一个启动脚本，判断 servera 和 serverb 是否在网络上可达。脚本确保实验中创建的文件和目录不存在于 serverb 或工作站上。

```
[student@workstation ~]$ archive-review start
```

- 1. 在 serverb 上，将 servera 的 /etc 目录树同步到 /configsync 目录。
    1.1. 使用 ssh 命令以 student 身份登录 serverb。
    1.2. 在创建 /configsync 目录之前使用 su 命令切换到 root 用户，这需要超级权限。在后续步骤中，你将归档 /etc 目录树中的文件，这些文件由 root 用户所有，这也需要超级权限。
    1.3. 创建 /configsync 目录以存储来自 servera 的同步配置文件。

## 第12 章 文件系统审计

```
[root@server ~]# mkdir /configsync
```

1.4. 使用 rsync 命令将 servera 的 /etc 目录树同步到 serverb 上的 /configsync 目录。注意 root 用户可以读取 servera 上 /etc 目录的所有内容。

```
[root@server ~]# rsync -av root@servera:/etc /configsync
root@server's password: redhat
正在增量文件列表
etc/
etc/.passwd.lock
...输出已省略...
etc/yum/protected.d -> .../dnf/protected.d
etc/yum/vars -> .../dnf/vars

sent 10,958 bytes received 21,665,987 bytes 3,334,914.62 bytes/sec
total size is 21,615,767 speedup is 1.0
```

2. 使用 gzip 压缩创建一个名为 configfile-backup-server.tar 的归档，包含 /configsync 目录的内容。

2.1. 使用 `tar -czf` 命令创建 gzip 压缩归档。

```
[root@server ~]# tar -czf configfile-backup-server.tar.gz /configsync
tar: Removing leading '/' from members
[root@server ~]
```

2.2. 使用 `tar -tzf` 列出 configfile-backup-server.tar.gz 归档的内容。

```
[root@server ~]# tar tzf configfile-backup-server.tar.gz
...输出省略...
configsync/etc/wgetrc
configsync/etc/xattr.conf
```

3. 以 student 身份使用 student 密码将 /root/configfile-backup-server.tar.gz 归档文件从 server 安全拷贝到工作站的 /home/student 目录。

```
[root@server ~]# scp configfile-backup-server.tar.gz \
> student@workstation:/home/student
...输出已省略...
student@workstation's password: student
configfile-backup-server.tar.gz      100% 510KB  64.5MB/s    00:00
```

## 评估

在工作站上运行 `lab archive-review grade` 确认实验成功。

```
[student@workstation ~]$ archive-review grade
```

## 完成

在工作站上运行 `lab archive-review finish` 脚本完成此练习。

```
[student@workstation ~]$ archive-review finish
```

此实验结束。

## 归档并传输文件

## 检查列表

在实验中，你将使用 tar、rsync 和 scp 对目录内容进行归档和备份。

## 结果

你应该能够：

- 将远程目录同步到本地目录。
- 创建同步目录内容的归档。
- 安全地将归档拷贝到远程主机。
- 提取归档。

## 开始之前

在工作站上使用 student 密码登录 student。

从工作站运行 `lab archive-review start` 命令。该命令运行一个启动脚本，判断 servera 和 serverb 是否在网络上可达。脚本确保实验中创建的文件和目录不存在于 serverb 或工作站上。

```
[student@workstation ~$] archive-review start
```

- 1. 在 serverb 上，将 servera 的 /etc 目录树同步到 /configsync 目录。
    1.1. 使用 ssh 命令以 student 身份登录 serverb。
    1.2. 在创建 /configsync 目录之前使用 su 命令切换到 root 用户，这需要超级权限。在后续步骤中，你将归档 /etc 目录树中的文件，这些文件由 root 用户所有，这也需要超级权限。
    1.3. 创建 /configsync 目录以存储来自 servera 的同步配置文件。

## 第12 章 文件系统审计

```
[root@server ~]# mkdir /configsync
```

