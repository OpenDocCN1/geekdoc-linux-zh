

```
[root@host ~]# tar -czf /root/etcbackup.tar.gz /etc
tar: Removing leading '/' from member names
```

要在主机上创建一个名为 `/root/logbackup.tar.bz2` 的 bzip2 压缩包，并包含 `/var/log` 目录的内容：

```
[root@host ~]$ tar -cf /root/logbackup.tar.bz2 /var/log
tar: Removing leading '/' from member names
```

要在主机上创建一个名为 `/root/sshconfig.tar.xz` 的 xz 压缩包，并包含 `/etc/ssh` 目录的内容：

```
[root@host ~]$ tar -cJf /root/sshconfig.tar.xz /etc/ssh
tar: Removing leading '/' from member names
```

创建压缩包后，使用 `-tf` 选项验证包的内容。列出内容并不强制要求使用压缩代理选项。例如，使用以下命令列出 `/root/etcbackup.tar.gz` 文件（其使用 gzip 压缩）中存档的内容：

```
[root@host ~]# tar -tf /root/etcbackup.tar.gz /etc
etc/
etc/fstab
etc/crypttab
etc/mtab
...output omitted...
```

# 解压压缩包

解压 tar 档的第一步是确定存档文件应该解压到哪里，即创建并切换到目标目录。`tar` 命令会确定使用了哪种压缩，通常不需要使用与创建压缩包时相同的压缩选项。如果你选择这样做，必须使用正确的解压类型；否则 `tar` 会报错，提示选项中指定的解压类型与文件的解压类型不匹配。

在 `/tmp/etcbackup` 目录中解压 gzip 压缩包 `/root/etcbackup.tar.gz` 内容：

```
[root@host ~]# mkdir /tmp/etcbackup
[root@host ~]# cd /tmp/etcbackup
[root@host etcbackup]# tar -tf /root/etcbackup.tar.gz
etc/
etc/fstab
etc/crypttab
etc/mtab
...output omitted...
[root@host etcbackup]# tar -xzf /root/etcbackup.tar.gz
```

在 `/tmp/logbackup` 目录中解压 bzip2 压缩包 `/root/logbackup.tar.bz2` 内容：

```
[root@#] mkdir /tmp/logbackup
[root@#] cd /tmp/logbackup
[root@logbackup] tar -tf /root/logbackup.tar.bz2
var/log/
var/log/last
var/log/README
var/log/private/
var/log/wtmp
var/log/btmp
...output omitted.
[root@logbackup] tar -xjf /root/logbackup.tar.bz2
```

在 `/tmp/sshbackup` 目录中解压 xz 压缩包 `/root/sshbackup.tar.xz` 内容：

```
[root@#] mkdir /tmp/sshbackup
[root@#] cd /tmp/sshbackup
[root@logbackup] tar -tf /root/sshbackup.tar.xz
etc/ssh/
etc/ssh/moduli
etc/ssh/ssh_config
etc/ssh/config_d/
etc/ssh/config_d/05-redhat.conf
etc/ssh/sshd_config
...output omitted.
[root@sshbackup] tar -xjf /root/sshbackup.tar.xz
```

列出压缩包的方法与列出未压缩的 tar 档相同。xz 可以用于：

> 注意
> 此外，gzip、bzip2 和 xz 可以独立压缩单个文件。例如，`gzip` 命令生成 `etc.tar.gz` 压缩文件，`bzip2` 命令生成 `abc.tar.bz2` 压缩文件，而 `xz` 命令生成 `myarchive.tar.xz`。
> 对应的解压命令是 gzip、bzip2 和 unxz。例如，`gzip /tmp/etc.tar.gz` 命令生成 `etc.tar` 未压缩 tar 档，`bzip2 abc.tar.bz2` 命令生成 `abc.tar` 未压缩 tar 档，而 `xz myarchive.tar.xz` 命令生成 `myarchive.tar` 未压缩 tar 档。

参考文献
tar(1), gzip(1), bzip2(1), bunzip2(1), xz(1), unxz(1) 手册

# 引导式练习

# 管理压缩 tar 档

在此练习中，你将使用 `tar` 命令创建存档并解压其内容。

# 结果

你应该能够存档一个目录树并将存档内容解压到另一个位置。

# 开始之前

在工作站上以 student 用户身份登录。

在工作站运行 `lab-manage start` 命令。该命令运行一个脚本，判断主机 `servera` 是否可访问。该脚本还会确保练习中创建的文件和目录在 `servera` 上不存在。

```
[student@workstation ~$] lab-manage start
```

1. 使用 `ssh` 命令以 student 用户登录服务器。

```
[student@workstation ~$] ssh@servera
[student@servera ~$]
```

2. 切换到 root 用户，因为只有 root 用户才能访问 `/etc` 目录的所有内容。

```
[student@servera ~$] su -
Password: redhat
[root@servera #]
```

3. 使用带有 `-czf` 选项的 `tar` 命令使用 gzip 压缩创建 `/etc` 目录的存档。将存档文件保存为 `/tmp/etc.tar.gz`。

```
[root@servera #] tar -czf /tmp/etc.tar.gz /etc
Removing leading '/' from member names
[root@servera #]
```

4. 使用带有 `-tzf` 选项的 `tar` 命令验证 `etc.tar.gz` 存档包含 `/etc` 目录的文件。

```
[root@servera #] tar -tzf /tmp/etc.tar.gz
etc/
etc/mtab
```

```
etc/fstab
etc/crypttab
etc/resolv.conf
...output omitted...
```

5. 在 servera 上创建一个名为 `/backuptest` 的目录。通过将文件解压到 `/backuptest` 来验证 `etc.tar.gz` 存档是有效的。

5.1. 创建 `backuptest` 目录。

```
[root@servera #] mkdir /backuptest
```

5.2. 切换到 `backuptest` 目录。

```
[root@servera #] cd /backuptest
```

5.3. 在解压前列出 `etc.tar.gz` 存档的内容。

```
[root@servera #] tar -tf /tmp/etc.tar.gz
etc/
etc/mtab
etc/fstab
etc/crypttab
etc/resolv.conf
...output omitted...
```

5.4. 将 `/etc.tar.gz` 存档解压到 `backuptest` 目录。

```
[root@servera #] tar -xzf /tmp/etc.tar.gz
```

5.5. 列出 `backuptest` 目录的内容。

```
[root@servera #] ls -l
total 1204
drwxr-xr-x 2 root root 4096 Jan 16 23:31 etc
-rw-r-- 1 root root 8198 Sep 10 21:52 aliases
drwxr-xr-x 2 root root 4096 Feb 4 21:58 alternatives
-rw-r-- 1 root root 541 Oct 2 21:01 anacontab
drwxr-xr-x 2 root root 4096 Jan 16 23:31
...
```

6. 退出 servera。

```
[root@servera #] exit
```

```
[student@servera ~$] exit
Connection to servera closed.
[student@workstation ~$]
```

在工作站上运行 `lab-manage finish` 完成此练习。

```
[student@workstation ~$] lab-manage finish
```

本引导式练习结束。

# 安全地在系统间传输文件

# 目标

完成本节后，你应该能够使用 SSH 在系统间传输文件。

# 使用安全拷贝传输文件

OpenSSH 适用于在远程系统运行 shell 命令。安全拷贝 `scp` 是 OpenSSH 软件包的一部分，可以将文件从远程系统复制到本地系统，或从本地系统复制到远程系统。该命令使用 SSH 服务器进行验证并在传输时加密数据。

你可以为复制的文件指定远程源或目标。远程位置的格式应该是 `[user@host:path]`。用户部分是可选的。如果提供了，将使用你的当前用户名来验证远程服务器，就像基于密钥的认证一样。会提示输入密码。

以下示例演示了如何将 `/etc/yum.conf` 和 `/etc/hosts` 文件复制到远程主机上 `remoteuser` 的家目录：

```bash
$user@host ~$ scp /etc/yum.conf /etc/hosts remoteuser@remotehost:/home/remoteuser
remoteuser@remotehost's password: password
yum.conf             100%  813      0.8KB/s    00:00
hosts                100%  227      0.2KB/s    00:00
```

你也可以反向复制文件，从远程系统到本地文件系统。在此示例中，远程主机上的 `/etc/hostname` 文件被复制到本地目录 `/home/user`。`scp` 命令以用户 `remoteuser` 的身份验证远程主机。

```
$user@host ~$ scp remoteuser@remotehost:/etc/hostname /home/user
remoteuser@remotehost's password: password
hostname             100%  22      0.0KB/s    00:00
```

要递归复制目录，请使用 `-r` 选项。在以下示例中，远程主机上的 `/var/log` 目录被递归复制到主机的 `/tmp/` 目录。你必须以 root 身份连接到远程系统，以确保读取远程 `/var/log` 目录中的所有文件。

```
$user@host ~$ scp -r root@remotehost:/var/log /tmp
root@remotehost's password: password
...output omitted...
```

