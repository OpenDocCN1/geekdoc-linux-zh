
```
# 我们不希望用户能够向这些区域上传。
upload/home/ftp/* no
upload/home/ftp/* /etc no
upload/home/ftp/* /dev no
```

```
# 我们将阻止从 retrievere 下载。
retrievere/home/ftp/etc
retrievere/home/ftp/dev
```

`log security real,guest`

`guest-root /home/ftp ftppadmin webmaster`

`restricted-uid ftppadmin webmaster`

`restricted-gid ftppadmin webmaster`

`greeting terse`

`keepalive yes`

`norétéve.notar`

## 第 2 步

现在，将其默认权限更改为 600：

```
[root@deep #] chmod 600 /etc/ftppass
```

这告诉 `ftppass` 为此特定的配置设置进行自配置：

`class opener 208.164.186.`

此 "`class`" 指定了那些可以访问您的 FTP 服务器的一类用户。您可以在 "`ftppass`" 文件中定义任意数量的此类类。在我们的示例中，我们定义了类名 `<openarch>`，并且只允许在 FTP 服务器上拥有账户的 `<guest>` 用户在他们来自 `208.164.186..` 时访问 FTP 主目录。需要注意的是，三种不同的用户是：匿名用户（anonymous）、客人（guest）或真实用户（real）。匿名用户是连接到服务器但没有账户的网络用户。客人是系统中的设置与匿名 FTP 完全相同（这是我们在示例中设置的），而真实用户必须拥有服务器的 shell（这可能带来安全风险）才能访问它。

`limit opener 20 MoTuWeTh,Fr0000-1800 /home/ftp/many.msg`

此 "`limit`" 选项指定按类和时间允许登录 FTP 服务器的用户数。在我们的示例中，我们将类名 `<openarch>` 的 FTP 服务器限制为 20 个用户 `<20>`，从周一到周四 `<MoTuWeTh>` 全天，以及周五从午夜到 6:00-1800。此外，如果达到了 20 个用户的限制，将向连接的用户显示文件 `<home/ftp/.many.msg>` 的内容。当您需要控制服务器资源时，这是一个非常有用的参数。

`logintails 3`

此 '`logintails`' 选项指定在断开之前可以进行的失败登录尝试次数。在我们的示例中，我们在用户尝试三次失败后断开其与 FTP 服务器的连接。

`readme README* login`

`readme* cwd=`

这些 '`readme*`' 选项指定在登录时或更改目录时通知客户端其当前目录下的文件已修改。在我们的示例中，我们指定了在登录时通知。

`message_message`

`cwd=*`

这些 '`message`' 选项指定在登录时或更改目录时通知客户端其当前目录下的文件已修改。在我们的示例中，我们指定了在登录时通知。

# "/etc/ftpusers" 文件的配置

`"/etc/ftpusers"` 文件指定了那些**不允许**连接到你的 FTP 服务器的用户。

## 第 1 步

创建 `ftpusers` 文件（`touch /etc/ftpusers`）并出于安全考虑，在该文件中添加以下用户：

- root
- bin
- daemon
- adm
- lp
- sync
- shutdown
- halt
- mail
- news
- uucp
- operator
- games
- nobody

## 第 2 步

现在，将其默认权限更改为 600：

```
[root@deep ~]# chmod 600 /etc/ftpusers
```

# "/etc/ftpconversions" 文件的配置

`"/etc/ftpconversions"` 文件包含指令权限，用于在传输前按需压缩文件。

## 第 1 步

编辑 `ftpconversions` 文件（` /etc/ftpconversions`）并在该文件中添加以下行：

```
::Z: /bin/compress -d -c %sT $REG_ASIIO:UNCOMPRESS:UNCOMPRESS
::Z: /bin/gzip -c %sT $REG_ASIIO:COMPRESS:$REG_ASIIO:UNCOMPRESS:GZIP
::Z: /bin/gzip -z %sT $REG_ASIIO:COMPRESS:GZIP
::Z: /bin/tar -c -f %sT $REG_DIR:TAR:TAR
::Z: /bin/tar -c -z -f %sT $REG_DIR:COMPRESSIO:TAR+COMPRESS
::Z: /bin/tar -z -f %sT $REG_DIR:COMPRESSIO:TAR+GZIP
::crc: /bin/cksum %sT $REG_CRC:CKSUM
::md5: /bin/md5 %sT $REG_MD5:MD5SUM
```

## 第 2 步

现在，将其默认权限更改为 600：

```
[root@deep ~]# chmod 600 /etc/ftpconversions
```

# "/etc/pam.d/fpt" 文件的配置

配置你的 `/etc/pam.d/fpt` 文件以使用 `pam` 认证。

创建 `fpt` 文件（`touch /etc/pam.d/fpt`）并添加以下行：

关于此书的意见和建议请邮件至 `gmourani@videotron.ca`

```
#%PAM-1.0
auth required /lib/security/pam_listfile.so item=user-sense deny=/etc/ftpsusers onerr=succeed
auth required /lib/security/pam_pwd.so nullok
auth required /lib/security/pam_shells
account required /lib/security/pam_pwdb
session required /lib/security/pam_pwdb
```

# "etc/logrotate.d/fptd" 文件的配置

配置你的 "etc/logrotate.d/fptd" 文件，每周自动滚动你的日志文件。

创建 `fptd` 文件（`touch /etc/logrotate.d/fptd`）并添加以下行：

```
/var/log/*
# ftptd 无法正确处理 SIGHUP
nocompress
```

# 配置 fptd 使用 tcp-wrappers inetd 超服务器

`Tcp-wrappers` 负责启动和停止 `fptd` 服务器。在执行时，`inetd` 从配置文件（默认是 `"/etc/inetd.conf"`）中读取配置信息。配置文件中的每个字段必须有一个条目，条目之间用制表符或空格分隔。

## 第 1 步

编辑 `inetd.conf` 文件（`vi /etc/inetd.conf`）并验证以下行是否存在：：

> 注意：在文件中添加该行后，通过发送 `SIGHUP` 信号（`killall -HUP inetd`）来更新 "`inetd.conf`"。

* 要更新你的 "`inetd.conf`" 文件，请使用以下命令：

```
[root@deep ~]# killall -HUP inetd
```

## 第 2 步

编辑 `hosts.allow` 文件（`vi /etc/hosts.allow`）并添加以下示例行：

`in.fptd: 192.168.1.4 win.openarch.com`

这意味着 IP "`192.168.1.4`" 且主机名为 "`win.openarch.com`" 被允许 FTP 到该服务器。

# FTP 管理工具

## ftpwho

`ftpwho` 程序工具显示系统上所有活跃的 ftp 用户及其当前的进程信息。该命令的输出格式类似于 `"/bin/ps"` 命令。该命令的格式为：

* 要显示所有活跃的 ftp 用户及其当前进程，请使用以下命令：

```
[root@deep ~]# ftpwho
```

Service class

5443 ? S 0:00 fpd:win.openarch.com: fptadmin: IDLE

- 1 users (20 maximum)

关于此书的意见和建议请邮件至 `gmourani@videotron.ca`

要显示所有活跃的 ftp 用户及其当前进程，请使用以下命令：

```
[root@deep ~]# ftpwho
```

该命令输出示例如下：

Service class 5443 ? S 0:00 fpd:win.openarch.com: fptadmin: IDLE

- 1 users (20 maximum)

## ftpcount

`ftpcount` 工具显示系统当前活跃的 ftp 用户数量（以及最大限制）。它是 `ftpwho` 的简化版本，仅显示当前活跃的 ftp 用户数：

```
[root@deep ~]# ftpcount
```

- 1 users (20 maximum)

## 安全 ftp
