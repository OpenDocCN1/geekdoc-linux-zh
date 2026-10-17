
### 安装命令

```
[root]## qmail-1.03] # ln -s /var/qmail/bin/sendmail /usr/sendmail/mailq
[root]## qmail-1.03] # ln -sf /var/qmail/bin/qmail-greadd /usr/bin/mailq
[root]## qmail-1.03] # rm -rf /var/qmail/boot/
[root]## qmail-1.03] # rm -rf /var/qmail/doc/
[root]## qmail-1.03] # mailidrm -rf /etc/skel/Maildir
[root]## qmail-1.03] # cd
[root]## find / -name Qmail2
[root]## qmail-1.03] # diff qmail qmail2 > Qmail-Installed
```

上述命令将配置软件以确保你的系统拥有必要的库来成功编译包，将所有源文件编译为可执行的二进制文件，然后将它们以及任何支持文件安装到适当的位置。

# Qmail 第三章

## 第二步

你必须告诉 Qmail 主机名。要这样做，请使用 Qmail 的配置脚本，它会在 DNS 中查找你的主机。该配置脚本会在 DNS 中查找你的 IP 地址，以决定它应该接受哪些主机的邮件。默认情况下，它只接受你默认主机的入站邮件。这是一个安全功能，用于防止邮件服务器上的垃圾邮件和开放中继。

```
[root@deep root]# cd /var/tmp/qmail-1.03/
[root@deep qmail-1.03]# # ./config
Your hostname is smtp
Your's fully qualified name in DNS is smtp.domain.com.
Putting smtp.domain.com into control/me...
Putting domain.com into control/default.domain...
Putting domain.com into control/plusdomain...
```

检查本地 IP 地址：
`127.0.0.1`: Adding `localhost` to `control/locals`...
`1.2.3.4`: Adding `smtp.domain.com` to `control/locals`...

如果有任何其他指向你的域名，你必须将它们添加到 `/var/qmail/control/locals/`。
你不需要担心别名，即带有 CNAME 记录的域名。

将 `/var/qmail/control/locals` 复制到 `/var/qmail/control/rphosts/`。
现在 Qmail 将拒绝接受除来自这些主机以外的 SMTP 消息。
如果你向 `locals` 或 `virtualdomains` 添加了主机，请确保更改 `rphosts`！

> 注意：如果你收到以下错误消息：
> `Your hostname is smtp`
> `hard error:Sorry, I couldn't find your host name in DNS.`
> `You will have to set up control/me`
> 你需要在相同的目录下运行 `config-fast` 脚本：

```
./config-fast smtp.domain.com
```

假设你的域名是 `domain.com`，计算机的主名是 `smtp`。

## 第三步

现在为 Qmail 在你的系统中正常运行所需的最小别名。你应该为 `Postmaster`、`Mail-Daemon` 和 `root` 设置别名。出于安全考虑，超级用户 "`root`" 从不通过 Qmail 接收邮件，由于我们服务器上的许多程序需要向 "`postmaster`","`mailer-daemon`" 或 "`root`" 发送邮件，我们可以在本地或远程创建别名。
最后，一个重要的点是 Qmail 为每个文件都使用别名。这是 Qmail 与 Exim 的主要区别之一。因此，不要忘记为每个用户在其主目录下创建一个名为 `.qmail` 的别名文件。

- 为账户 "`postmaster`","`mailer-daemon`" 和 "`root`" 创建别名

```bash
[root@qmail-1.03]# touch postmaster
[root@qmail-1.03]# touch mailer-daemon
[root@qmail-1.03]# echo sysadmin > .postmaster
[root@qmail-1.03]# echo sysadmin > .mailer-daemon
[root@qmail-1.03]# echo sysadmin > .root
[root@qmail-1.03]# chmod 644 .qmail-*
[root@qmail-1.03]# chown root:root .qmail-*
```

> 注意：Qmail 没有内置支持 `/etc/aliases`。如果你有 `/etc/aliases` 并想保留它，将在稍后的章节讨论单独提供的 "`fastforward`" 包。作为一种安全措施，Qmail 拒绝向不拥有其主目录的用户投递邮件。结果是 "`postmaster`" 没有 `.postmaster`，那么 `postmaster@domain.com` 就不是有效的邮箱。这就是为什么要设置上述别名。

## 第四步

Qmail 包一旦安装在你的系统中，就会提供一个名为 `qmail-local` 的本地递代理，它提供了用户列表控制、跨主机循环检测以及许多重要的 Qmail 功能，例如用于入站邮件的防崩溃 Maildir 目录。此 Qmail 程序 (`qmail-local`) 旨在替换 Linux 用于将邮件本地投递到目录 `/var/spool/mail` 的默认 `/bin/mail` 程序。

`qmail-local` 和 `binmail` 之间有一个区别：`qmail-local` 默认将邮件投递到 `~user/Mailbox` 或 `~user/Maildir`，而不是 `/var/spool/mail`。

这意味着什么？`/var/spool/mail` 有两个问题：

- 它慢。在有数千用户的系统中，`/var/spool/mail` 有数千条目。少数 UNIX 系统支持大规模快速操作，但大多数不支持。
- 这是不明智的。在全局可写目录中编写代码并不容易。请参见 CERT advisory 95:02。

由于这些原因，为了加强我们配置系统的安全性并优化 Qmail 邮件服务器的性能，我们将更改并配置软件直接查找 Qmail `~user/Maildir`。`Maildir` 是 Qmail 的一个功能，用于替代比它可靠的旧 Unix Mailbox 目录。

通常，Linux 会为系统中未来的用户自动创建 Maildir，因为我们已经在服务器的 `/etc/skel` 目录下添加了所需的 Maildir 骨架。对于系统中所有现有用户，你必须按照如下方法创建此新的 Maildir：

- 为系统中的所有现有用户创建一个新的 Maildir，使用命令：
`[root@deep]# maildirmake $HOME/$Maildir`

其中 `<HOME>` 是你想为所有入站消息创建此新 Qmail Maildir 的用户目录。

## 第五步

处理 Qmail 新 Maildir 功能的最后一步是在 `/etc/qmail` 目录下创建一个名为 `.qmail` 的文件，将其设置为默认递代理。Qmail 脚本初始化文件每次邮件服务器启动时都会读取该文件。

- 创建 `.qmail` 文件 (`touch /etc/qmail/.qmail`) 并添加行：
`./Maildir/`

- 将其默认模式更改为 (`0511/-r-x-x--`) 并由超级用户 '`root`' 所有：
`[root@deep]# chmod 511 /etc/qmail/.qmail`
`[root@deep]# chown root:root /etc/qmail/.qmail`

## 第六步

一旦完成软件的编译、优化和安装，我们可以通过删除不再需要的程序存档和相关的源码目录来释放空间。

- 要删除 Qmail 及其相关的源码目录，使用以下命令：
`[root@deep]# cd /var/tmp/`
`[root@deep]# rm -rf qmail-version/`
`[root@deep]# rm -f qmail-version.tar.gz`

上述使用的 `rm` 命令将删除我们用于编译和安装 Qmail 的所有源文件。它还会删除 `/var/tmp` 目录下的 Qmail 压缩包。

# 配置 Qmail

在 Qmail 成功构建并安装到系统之后，下一步是配置并自定义其文件以满足你的需求。

- `/etc/qmail/control/me`: (Qmail 主机名文件)
- `/etc/qmail/control/locals`: (Qmail locals 文件)
- `/etc/qmail/control/rcphosts`: (Qmail rcphosts 文件)
- `/etc/qmail/control/defaultdomain`: (Qmail默认域名)
- `/etc/qmail/control/plusdomain`: (Qmail 加号域名)
- `/etc/init.d/qmail`: (Qmail 初始化文件)

## /etc/qmail/control/me: Qmail 主机名配置文件

`/etc/qmail/control` 目录下的所有文件都是 Qmail 系统的配置文件。Qmail 仅需一个名为 "`me`" 的控制文件即可运行，该文件包含当前主机的完全限定域名 (FQDN)。此 "`me`" 文件被用作其他主机相关控制文件的默认值。你通常不需要修改此 "`me`" 文件，因为它已经包含了 Qmail 运行所需的完全限定域名；否则，如果该文件不存在，请创建它并在其中添加你的完全限定域名（例如 `smtp.domain.com`）。

- 编辑 `me` 文件 (`vi /etc/qmail/control/me`) 并添加：

```
smtp.domain.com
```

## /etc/qmail/control/locals: Qmail 本地配置文件

Qmail 配置文件 `locals` 可用于处理当前主机接收邮件的域名列表，每行一个域名。Qmail 将通过该文件的内容知道它应该向哪些地址在本地投递邮件。

当你将 Qmail 配置为中央邮件服务器时，这一点变得至关重要。如果你想在该文件中配置默认值，它同样是当前主机的完全限定域名 (FQDN)。有关将 Qmail 作为空客户端邮件服务器运行的更多信息，请参阅本章后续。

- 编辑 `locals` 文件 (`vi /etc/qmail/control/locals`) 并添加：

```
smtp.domain.com
```

## /etc/qmail/control/rcphosts: Qmail RCPhosts 文件

`rcphosts` 文件指定了哪些域名允许使用 Qmail 邮件服务器。如果域名未列在 `rcphosts` 中，`lmqpd` 将拒绝任何信封收件人地址。总结来说，Qmail 将通过该文件的内容知道它应该从远程系统发送哪些消息。

默认情况下，Qmail 关闭中继功能，你必须在 `rcphosts` 文件中填充网络上所有授权主机的完全限定域名。对于 Exim 的 `relaydomains` 配置，使用一个文件的方法可能是声明网络中本地的所有完全限定域名。如果你的完全限定域名是 "`smtp.domain.com`" ，你必须将其添加到此文件中以便 Qmail 正常工作。

你不需要在该文件中列出网络上的所有服务器，只需列出你的完全限定域名。再次强调，没有在该文件中列出例如 "`www.domain.com`"、"`ftp.domain.com`" 或 "`something.domain.com`" 等内容，只需运行 Qmail 的服务器的完全限定域名 "`smtp.domain.com`"。

对于虚拟托管，我们还将使用此列表列出托管在我们邮件服务器上的所有虚拟域名。有关使用 Qmail 托管虚拟域的更多信息，请参阅本章后续。

- 编辑 `rcphosts` 文件 (`vi /etc/qmail/control/rcphosts`) 并添加：

```
smtp.domain.com
```

## /etc/qmail/control/defaultdomain: qmail 默认文件

Qmail 使用 "`defaultdomain`" 文件中列出的域名添加到任何不带点的点的机名中。你通常不需要修改 "`defaultdomain`" 文件中列出的默认信息（即 `domain.com`）。

- 编辑 `defaultdomain` 文件 (`vi /etc/qmail/control/defaultdomain`) 并添加：
`domain.com`

## /etc/qmail/control/plusdomain: Qmail plusdomain 文件

Qmail 使用 "`plusdomain`" 文件中列出的域名添加到任何带有加号的主机名中。你通常不需要修改 "`plusdomain`" 文件中列出的默认信息（即 `domain.com`）。

- 编辑 `plusdomain` 文件 (`vi /etc/qmail/control/plusdomain`) 并添加：
`domain.com`

## /etc/init.d/qmail: Qmail 初始化文件

`/etc/init.d/qmail` 脚本负责自动启动和停止 Qmail 服务器。请注意，以下脚本仅适用于使用 System V 的 Linux 操作系统。如果你的 Linux 系统使用其他方法（如 BSD），你将需要调整下面的脚本使其生效。

### 第 1 步

创建 `qmail` 脚本 (`touch /etc/init.d/qmail`) 并添加以下行：

```bash
#!/bin/bash

# 此脚本负责启动和停止 Qmail。

# chkconfig: 2345 80 30

# description: Qmail 是小型、快速、安全的邮件传输代理，\
#      是将 qmail 从一台机器移动到另一台机器的程序。

# processname: qmail-send

# 导入函数库。
. /etc/init.d/functions

# 网络配置。
. /etc/sysconfig/network

# 检查网络是否已启动。
$[NETWORK] = "no" && exit 0

# 如果 Qmail 不可用，现在退出。
[ -f /usr/bin/qmail-send ] || exit 0

RETVAL=0
prog="Qmail"

start() {
  echo -n "Starting $prog:"
  qmail-start "cat /etc/qmail/dot-qmail" splogger qmail &
  RETVAL=$?
  [ $RETVAL -eq 0 ] && touch /var/lock/subsys/qmail
  return $RETVAL
}

stop() {
  echo -n "Shutting down $prog:"
  kill qmail-send
  RETVAL=$?
  [ $RETVAL -eq 0 ] && rm -f /var/lock/subsys/qmail
  return $RETVAL
}

# 如何调用。
case "$1" in
  start)
    start
    ;;
  stop)
    stop
    ;;
  queue)
    qmail-queue
    ;;
  status)
    status qmail-send
    ;;
  restart)
    stop
    start
    ;;
  condrestart)
    if [ -f /var/lock/subsys/qmail ]; then
      stop
      start
    fi
    ;;
  *)
  echo "Usage: $0 {start|stop|queue|restart|condrestart}"
  exit 1
esac

exit $RETVAL
```
