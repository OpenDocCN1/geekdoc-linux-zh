
```bash
# local-host-names - 在此处包含你机器的所有别名。
opencena.com
deep.opencena.com
www.opencena.com
win.opencena.com
mail.opencena.com
```

使用这种配置，任何发送的邮件看起来都像是从 "opencena.com" 发出的，而任何发送到 "www.opencena.com" 或其他主机的邮件将投递到 "mail.opencena.com" 或我们的邮件枢纽。

请注意，如果你配置系统伪装成另一台机器，那么从你的系统发送到你所伪装机器的任何电子邮件都会受到影响。例如，在上面的插图中，Linux 的 cron 进程定期发送到 root@www.opencena.com 的日志文件将被发送到 root@mail.opencena.com 我们的邮件枢纽。

Copyright 1999 - 2000 Gerhard Maurani, Open Network Architecture & and OpenDocs Publishing

272

## 适用于所有配置的 `/etc/sysconfig/sendmail` 文件配置

`/etc/sysconfig/sendmail` 文件用于 `SENDMAIL` 配置信息，例如 sendmail 是否应该作为守护进程运行、它是否应该监听邮件，以及在队列目录中的消息未投递时，应等待多久后发送警告。

创建 sendmail 文件（`touch /etc/sysconfig/sendmail`）并在此文件中添加：

```bash
DAEMON=yes
QUEUE=1h
```

"`DAEMON=yes`" 选项指示 Sendmail 作为守护进程运行。当 Sendmail 客户端配置为不直接从外部接收邮件，而是为了将本地邮件转发到中央枢纽时，此行非常有用；不运行守护进程还可以提高安全性。如果你这样配置了你的服务器或客户端机器，你只需要将 "`DAEMON=yes`" 替换为 "`no`"。

通常被放入队列是因为邮件无法立即传输。"`QUEUE=1h`" 设置了在消息未投递之前向发送者发送的时间间隔。

## 适用于所有配置的 `/etc/rc.d/init.sendmail` 脚本配置

配置你的 `/etc/rc.d/init.sendmail` 脚本文件以启动和停止 Sendmail 守护进程。

创建 sendmail 脚本文件（`touch /etc/rc.d/init.sendmail`）并添加：

```bash
#!/bin/sh
# sendmail      此脚本负责启动和停止
#               sendmail.
#
# chkconfig 2345 80 30
# description: Sendmail 是一个邮件传输代理，它是将邮件
#       从一台机器移动到另一台机器的程序。
# process_name:sendmail
# config=/etc/sysconfig.cf
# pidfile:/var/run/sendmail.pid

# 引入函数库。
./etc/rc.d/init/functions

# 引入网络配置。
./etc/sysconfig/network

# 引入 sendmail 配置。
if [ -f /etc/sysconfig/sendmail ]; then
  ./etc/sysconfig/sendmail
else
  DAEMON=yes
  QUEUE=1h
fi

# 检查网络是否启动。
if [ $NETWORKING = "no" ]; then
  exit 0
fi

# 检查 sendmail 是否存在。
if [ -x /usr/sbin/sendmail ]; then
  exit 0
fi

RETVAL=0

# 根据参数操作。
case "$1" in
  start)
    echo -n "Starting sendmail: "
    for i in virtertable domainable mailertable; do
      if [ -f /etc/mail/$i ]; then
        makemap $i
      fi
    done
    if [ $DAEMON = "yes" ]; then
      /usr/sbin/sendmail &
    else
      /usr/sbin/sendmail
    fi
    if [ $? -eq 0 ]; then
      echo "OK"
    else
      echo "FAILED"
      RETVAL=1
    fi
    ;;
  stop)
    echo -n "Shutting down sendmail: "
    /usr/sbin/sendmail stop 2>/dev/null
    if [ -f /var/run/sendmail.pid ]; then
      kill `cat /var/run/sendmail.pid`
      rm -f /var/run/sendmail.pid
    fi
    echo "OK"
    ;;
  reload)
    if [ -f /etc/sysconfig/sendmail ]; then
      ./etc/sysconfig/sendmail
    else
      DAEMON=yes
      QUEUE=1h
    fi
    echo -n "Reloading sendmail: "
    /usr/sbin/sendmail restart
    echo "OK"
    ;;
  status)
    if ps -C sendmail >/dev/null 2>&1; then
      echo "sendmail is running"
    else
      echo "sendmail is not running"
    fi
    ;;
  *)
    echo "Usage: $0 {start|stop|reload|status}"
    exit 1
    ;;
esac

exit $RETVAL
```

## 服务器软件（邮件网络服务）

第5章

例如：

`Mprog, P=/bin/sh, F=lsDFMoequ9, S=10, R=20/40, D=$z/, T=X-Unix, A-sh-c Su`

其应更改为：

`Mprog, P=/usr/bin/smirch, F=lsDFMoequ9, S=10, R=20/40, D=$z/, T=X-Unix, A-sh-c Su`

现在使用以下命令手动重启 sendmail 进程：

`[root@]# /etc/init.d/sendmail start`

在我们上面的邮件枢纽服务器 "`sendmail.mc`" 文件中，我们已经使用“宏”配置了此行，将 "`usr/bin/smirch`" 替换为 m4 宏 "`FEATURE`"; smirch；因此，如果邮件枢纽中继的 "`/etc/mail.mc`" 文件已经设置了 "`usr/bin/smirch`" 指定，请不要惊讶。相反，请使用上述方法为网络中的其他 "`/etc/mail.mc`" 文件创建一个用于 nullclient（本地或相邻客户端和服务器）的文件，使用 "`null.mc`" 配置来生成 "`/etc/mail.mc`" 文件。

## `/etc/mail/aliases`

管理不当的 "`aliases`" 文件很容易被用来获取特权状态。例如，许多厂商的系统在 "`/etc/aliases`" 文件中有一个 "`decode`" 别名。其意图是为用户提供一种使用 mail 翻译二进制文件的简单方法。发送端使用 "`uencode`" 将二进制转换为 ASCII，然后将结果邮寄到接收端的 "`decode`" 别名。该别名将消息通过 "`usr/bin/uencode`" 程序处理，该程序将 ASCII 转换回原始二进制文件。

从你的 `/etc/mail/aliases` 文件中删除 "`decode`" 别名行。同样，每一个执行你未亲自放置并检查的程序的别名都应该受到质疑并可能被删除。

编辑别名文件（`vi /etc/mail/aliases`）并删除以下行：

```
# 基础系统别名 -- 这些必须保留。
MAIL-DAEMON: postmaster
postmaster: root

# 伪账户的通用重定向。
bin: root
daemon: root
games: root ← 删除此行。
Ingres: root ← 删除此行。
nobody: root
system: root ← 删除此行。
toor: root ← 删除此行。
uuccp: root ← 删除此行。
```

```
# 拦截 decode 以捕获安全攻击
decode: root ← 删除此行。
```

```
# 应该接收邮件的人员
#root: marc
```

- 为了使更改生效，你需要运行：

  `[root@]# /usr/bin/newaliases`
