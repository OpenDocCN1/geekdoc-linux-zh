
首先，我们将包含 `RSA PRIVATE KEY` 和 `CERTIFICATE` 部分的 `privkey` 文件移动到 `certs` 目录，并将其重命名为 `smtp.pem` 以供 Qmail 用于 SMTP 协议。之后，我们从系统中删除 `tmp.pem` 文件，因为它不再需要了。

## 在 qmail 初始化文件中添加所需的 SSL 参数：

一旦创建了 Qmail 证书并移动到适当的位置，我们就更改默认的 `/etc/init.d/qmail` 初始化文件，以配置 Qmail 在服务器上运行 SSL。这是必要的，因为 Qmail 应该使用 stunnel 启动，我们必须用 stunnel 定义一些新参数以使 Qmail 在 SSL 下运行。

为了让 Qmail 以 SSL 运行，我们需要在 `/etc/init.d/qmail` 初始化文件中添加以下内容。

## 最后一步
最后，我们必须重启 Qmail 以使更改生效。

- 若要重启 Qmail，请使用以下命令：
```bash
[root@deep]# /etc/init.d/qmail restart
```
关闭 Qmail:
启动 Qmail:

# 允许虚拟主机进行中继：

请记住，Qmail 默认不允许在没有妥妥身份验证的情况下进行中继，对于虚拟域名也是如此。你必须确保相关的虚拟域名已添加到 Qmail 的 `rpchosts` 文件中，以便允许其中继。这非常重要，否则中继将被拒绝。

## 第 1 步

将所有希望 Qmail 中继的域名添加到用于中继的 `rpchosts` 文件中。

- 编辑 `rpchosts` 文件 (`vi /etc/qmail/control/rpchosts`) 并添加以下内容：
```
# 此文件处理所有允许中继的域名。

# 默认情况下，我们包含了服务器的 localhost，否则任何功能都无法工作。

# 添加到此列表的虚拟域名将不会拒绝中继请求。

# 注意：修改此文件后必须重启 Qmail。

#nssmtp.domain.com

virtual1.com

virtual2.com
```

> 警告：如果虚拟域名被列在 `/etc/qmail/control/locals` 文件中，则 `virtualdomains` 配置将不会生效且无法工作。这意味着你只需要将相关的虚拟域名添加到 `virtualdomains` 和 `rpchosts` 文件中。

### 第 2 步

现在，必须重启 Qmail 守护进程使更改生效。

- 重启 Qmail 请使用以下命令：
```
[root@deep #] /etc/init.d/qmail restart
Shutting down Qmail: [OK]
Starting Qmail: [OK]
```

# 安装 fastforward 软件：

通过上述操作，虚拟主机可以正常工作，但如果你想将某个虚拟用户账户转发到外部邮件帐户（如 "..."），你将需要更多工作。为了解决这个问题，我们可以安装名为 fastforward 的 Qmail 软件。fastforward 根据 `cdb` 数据库处理 Qmail 转发。它可以从 sendmail 风格的 `/etc/aliases` 或面向用户-域名的类型创建转发域名。

## 第 1 步

首先，我们需要获取 "fastforward" 程序 (`http://cr.yp/fastforward.html`) 并将其复制到系统的 `/var/tmp` 目录，然后在解压存档之前切换到该位置。之后，将其移动到新创建的 fastforward 目录，并执行以下步骤进行编译和优化。
```
[root@deep #] cp fastforward-version.tar.gz /var/tmp/
[root@deep #] cd /var/tmp/
[root@deep tmp]#] tar xpf fastforward-version.tar.gz
[root@deep tmp]#] cd fastforward-0.51
```

### 第 2 步

在编译程序之前，我们将编辑 `conf-cc` 文件并将默认编译器更改为适应我们自己的 CPU 架构以获得更好的性能。

- 编辑 `conf-cc` (`vi conf-cc`) 并更改该行：
```
cc -02
```
修改为：
```
gcc -02 -march=i686 -funroll-loops
```

### 第 3 步

现在，我们将在你所属的系统中创建一个文件列表并安装软件，然后使用 `diff` 工具对它们进行比较，找出哪些文件被放置在什么位置，最后在系统中安装 `fastforward`。
```
[root@deep] fastforward-0.51]# make
[root@deep] fastforward-0.51]# cd
[root@deep] find / > Fast1
[root@deep] cd /var/tmp/fastforward-0.51]# make setup check
[root@deep] fastforward-0.51]# rm -rf /var/qmail/doc/
[root@deep] fastforward-0.51]# cd
[root@deep] find / -name Fast2
[root@deep] fastforward-0.51]# diff Fast1 Fast2 > Fast-Installed
```

### 第 4 步

一旦安装了 fastforward 软件，我们需要创建 `aliases` 文件并填充一些别名以便程序与 Qmail 工作。

- 创建 aliases 文件 (`touch /etc/aliases`) 并添加以下行。以下是我们建议你使用的内容。
```
# 下列别名是邮件 RFC 2821 和 2822 的。
# 至少，你应该将 "postmaster" 设置为处理该系统邮件问题的人员地址。
#
```
```
postmaster: sysadmin@localhost
mailer-daemon: postmaster
root: postmaster
```
```
# 重定向发送到系统账户的任何消息是一个好主意，
#这样它们就不会被直接忽略。
#
```
```
bin: root
daemon: root
decode: root
dumper: root
sync: root
mail: root
pop: root
uucp: root
ftp: root
body: root
www: root
manager: root
```
# Qmail 3
第 1 章
```
named:      root
postgres:   root
mysql:      root
squid:      root
amavis:     root
operator:   root
abuse:      root
hostmaster: root
webmaster: root
```
**注意：** 请不要忘记将 "postmaster" 更改为你网络系统管理员的电子邮件。你的别名 "sysadmin@localhost" 是一个示例，因此请更改它。你的别名可能会复杂，，尽管如此，请注意示例展示了别名的最小形式。

### 第 5 步

现在，将 aliases 文件的权限设置为 644，所有者设置为 root。

- 将 aliases 文件的权限设置为 644，所有者设置为 root。
- 更改文件的模式和所有权请使用：
```
[root@deep #] chmod 644 /etc/aliases
```

### 第 6 步

最后，我们要在 qmail 下创建一个新文件 qmail-default。

- 创建 qmail-default 文件 (`touch /etc/qmail/qmail-default`) 并添加以下行。以下是我们建议你使用的内容。
```
# 下列别名是邮件 RFC 2821 和 2822 的。
...
```

### 第 7 步

现在，将 qmail-default 文件的权限设置为 644，所有者设置为 root。

- 将 qmail-default 文件的权限设置为 644，所有者设置为 root。
- 更改文件的模式和所有权请使用：
```
[root@deep #] chmod 644 /etc/qmail/qmail-default
```

在此阶段，我们可以使用 qmail-default。

> **注意：** 请不要忘记将 "postmaster" 更改为你网络系统管理员的电子邮件。你的别名 "sysadmin@localhost" 是一个示例，因此请更改它。你的别名可能会复杂，，尽管如此，请注意示例展示了别名的最小形式。

# 作为空客户端的 Qmail

现在我们已经解释了如何配置 qmail 进行发送/接收。这种配置也称为邮件枢纽服务器，当你需要一个功能完整的邮件服务器时非常有用。在某些情况下，我们根本不需要运行 qmail，因为我们要运行的服务器并不是邮件服务器，而是运行其他服务，如 web、ftp、dns 等。在这些服务器上，我们不需要运行功能完整的邮件服务器。

空客户端服务器是不监听入站连接的服务器，垃圾邮件发送者无法利用它转发邮件。这意味着空客户端只能将生成的邮件递送到中央邮件枢纽服务器。

以下是可能配置的概述：

# 中央邮件服务器配置：

与其让每台服务器或工作站处理自己的邮件，不如让处理所有邮件的强大中央服务器更有优势。这样的服务器被称为邮件枢纽服务器。中央邮件服务器的优势是：

- 可以接收和发送任何邮件。
- 允许用户连接到邮件帐户发送或获取邮件。
- 能够接收并管理来自空客户端的邮件。

# 空邮件服务器配置：

邮件服务对于所有类型的服务器都是不可或缺的，即使相关服务器的任务不是处理邮件，我们至少应该能够获取本地生成并发送给本地系统账户（postmaster）的消息。

空邮件服务器直接从外部世界接收邮件，并将所有的邮件通过中央邮件枢纽服务器中继（发送）。这样，发送给本地系统账户的重要邮件可以远程递送到中央邮件枢纽服务器进行验证。空客户端邮件服务器的优势是：

- 邮件不会直接发送到系统的本地用户帐户。
- 所有邮件都发送（转发）到中央邮件枢纽服务器。
- 外部世界不需要客户端名称。
- Qmail 守护进程不需要监听入站邮件连接。

# 创建必要的 smtproutes 文件：

`/etc/qmail/control/smtproutes` 文件用于定义中央邮件枢纽服务器的全限定域名（FQDN），该服务器将处理来自我们空客户端邮件服务器（Null Client Mail Server）的所有邮件。每当你需要在系统上设置空客户端邮件服务器时，都应该创建此文件。

### 步骤 1
默认情况下，`smtproutes` 文件不存在，因此我们必须手动创建它。

- 创建 smtproutes 文件（执行 `touch /etc/qmail/control/smtproutes`）并在其中添加中央邮件枢纽服务器的全限定域名（FQDN），该服务器将处理我们空客户端邮件服务器的所有邮件：
`:mail.domain.com`

在上面的示例中，`<mail.domain.com>` 是我们想要发送所有出站邮件的中央邮件枢纽名称。`-* ` 表示将所有出站邮件通过 "domain.com" 域名传输。

### 步骤 2
现在，出于安全考虑，将 smtproutes 文件的权限模式设置为 `(0644/-rw-r--)` 并所有者为超级用户 `root`。

- 更改 smtproutes 文件的权限模式和所有者，请使用：
`root@deep ]# chmod 644 /etc/qmail/control/smtproutes`
`root@deep ]# chown root.root /etc/qmail/control/smtproutes`

### 步骤 3
最后，我们必须禁用本地投递。这很重要，因为我们希望将所有本地邮件转发到中央邮件枢纽服务器。为了这一结果，我们必须删除空客户端邮件服务器上的 Qmail `locals` 文件。

- 删除 Qmail 的 `locals` 文件，请使用以下命令：
`root@deep ]# rm -f /etc/qmail/control/locals`

> 警告：在安装 uspi-tcp、fastforward 和 checkpoint 软件包之前，务必确保在 DNS（域名服务器）中已正确设置 MX 记录。Qmail 空客户端邮件服务器不需要在你的服务器上安装这些软件。

# 更新所有 .qmail-* 别名文件：

一旦设置了 smtproutes 文件，我们就必须编辑所有的 `.qmail-*` 文件，并更改文件内部列出的用户，指向远程用户，该用户将接收由空客户端邮件服务器发送到中央邮件枢纽的系统消息。

- 可以通过以下命令完成：
```
[root@deepalias] [qmail-1.03] # cd -alias
[root@deepalias] # echo noc@domain.com > .qmail-postmaster
[root@deepalias] # echo noc@domain.com > .qmail-mailer-daemon
[root@deepalias] # echo noc@domain.com > .qmail-root
```

在这里，我们使用 qmail 将所有属于 "postmaster" 或超级用户 "root" 的消息发送到 domain.com 的远程非特权用户 noc。

# 使 qmail 不监听入站的连接：

当 qmail 被配置为作为空客户端邮件服务器运行时，它不应该在你的服务器上监听入站的连接。出于安全考虑，这非常重要，我们必须编辑默认的 `/etc/init.d/qmail` 文件并进行修改。

为了让 qmail 作为完全运行的中央邮件枢纽服务器，它应该被配置为启动 `qmail-smtp`、`qmail-local` 和 `pop3d`。这是我们在安装软件时默认的操作。当 qmail 作为空客户端邮件服务器运行时，我们必须更改此项。

下面显示了你需要添加到或修改默认 qmail 初始化文件的行。**粗体文本**是我们添加到默认 qmail 初始化文件内容。

### 步骤 1
编辑 qmail 脚本（`vi /etc/init.d/qmail`）并添加/修改以下行：
```bash
#!/bin/bash

# 此 shell 脚本负责启动和停止 qmail。

# config: 2345 80 30

# description: qmail 是一个小型快速邮件传输代理，
# 将邮件从一台机器移动到另一台机器。

# processname: qmail-send

# 引入库。
# /etc/init.d/functions

# 引入网络配置。
# /etc/config

# 检查网络是否启动。
# [ ${NETWORK} = "no" ] && exit 0

# 如果 qmail 不可用。
[ -f /usr/bin/qmail-send ] || exit 0

RETVAL=0

prog="qmail"

start() {
echo -n "$Starting prog: "
qmail-start "/var/etc/qmail/dot-qmail" &
RETVAL=$?
  [ $RETVAL -eq 0 ] && touch /var/lock/subsys/qmail
  return $RETVAL
}

stop() {
  echo -n "$Shutting down prog:"
  kill qmail-send
  RETVAL=$?
  [ $RETVAL -eq 0 ] && rm -f /var/lock/subsys/qmail
  return $RETVAL
}

# 查看如何调用它。
case "$1" in
- start)
  ;
stop)
  ;
queue)
qmail-qstat
  ;
status)
status qmail-send
RETVAL=$?
  ;
restart)
stop
start
RETVAL=$?
  ;
condrestart)
if [ -f /var/lock/subsys/qmail ]; then
  stop
start
RETVAL=$?
fi
  ;
*) echo "Usage: {start|stop|queue|restart|condrestart}"
exit 1
esac

exit $RETVAL
```
