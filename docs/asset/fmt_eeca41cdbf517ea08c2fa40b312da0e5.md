
## 确定机器主机名

- 2. 你需要确定机器的主机名。只需输入 `hostname` 命令即可。输出显示你机器的主机名。如果你想临时更改，只需输入 `hostname new_name`，其中 `new_name` 是你机器的主机名。如果主机名未正确设置，你需要运行 `hostname` 命令并编辑 `/etc/hosts` 和 `/etc/network` 文件中的相关行。如果你不编辑这些文件，下次重启时主机名可能无法正确设置。

- 3. 输入以下内容配置编译文件：
`./config-fast`
将 `host_name` 替换为你的完全域名（`foo.yourdomain.com`）。

## 编译并安装 ucspi-tcp

此过程有两个步骤：

- 1. 进入解压的 `/ucspi-tcp` 目录：
`cd /usr/local/src/mailserver/ucspi-tcp`

- 2. 执行编译：
`patch < /usr/local/src/mailserver/netqmail-1.05/other-patches/ucspi-tcp-0.88.errno.patch`
`make`
`make setup check`

## 编译并安装 daemontools

你再次有两个步骤需要遵循：

- 1. 进入你移动 `/daemontools` 目录所在的位置：
`cd /package/admin/daemontools/src`

- 2. 执行编译：
`patch < /usr/local/src/mailserver/netqmail-1.05/other-patches/daemontools-0.76.errno.patch`
`cd package/install`

## 配置 qmail 启动脚本

`qmail` 应用程序需要一些启动脚本来运行。你现在创建它们：

- 1. 创建名为 `/var/qmail/bin/rc` 的文件，内容如下：

```bash
#!/bin/sh

exec env PATH="/var/qmail/bin:$PATH" \
qmail-start /var/qmail/control/defaultdelivery
```

前面的脚本使用了反引号（`` ` ``）而不是引号。

- 2. 更改启动脚本的权限：

`chmod 755 /var/qmail/rc`

## 执行邮箱配置

`qmail` 接受多种类型的邮箱投递。对于此配置，使用 Maildir 配置方法。要启用此项，运行以下命令：

`echo ~/Maildir >/var/qmail/control/defaultdelivery`

## 创建 qmail 系统启动脚本

你将创建的文件是 qmail 系统启动脚本。这个脚本手动输入太长，因此你可以从 Life with qmail 网站（`www.lifewithqmail.org`）下载。要下载脚本，运行以下命令：

```bash
cd /var/qmail/bin

wget http://lifewithqmail.org/qmailctl-script-dt70

mv qmailctl-script-dt70 qmailctl

chmod 755 /var/qmail/bin/qmailctl

ln -s /var/qmail/bin/qmailctl /usr/bin
```

运行上述命令后，你的 `/usr/bin` 路径中就有 `qmailctl` 脚本。这允许你在系统的任何位置运行 `qmailctl`。

供参考，列表 7.1 显示了你刚刚下载的脚本。

## 列表 7.1 qmail 系统启动脚本

```bash
#!/bin/sh

# description: the qmail MTA

PATH=/var/qmail/bin:/usr/bin:/usr/local/bin:/usr/local/sbin

export PATH
```

```bash
QMAILDUID='id -u qmail'

NOFILESGID='id -g qmail'
```

```bash
case "$1" in
start)
  echo "Starting qmail"
  if svok /service/qmail-send ; then
    svc -u /service/qmail-send/service/qmail-send/log
  else
    echo "qmail-send supervise not running"
  fi
  if svok /service/qmail-smtpd ; then
    svc -u /service/qmail-smtpd/service/qmail-smtpd/log
  else
    echo "qmail-smtpd supervise not running"
  fi
  if [ -d /var/lock/subsys ]; then
    touch /var/lock/subsys/qmail
  fi
  ;;
stop)
  echo "Stopping qmail..."
  echo "qmail-smtpd"
  svc -d /service/qmail-smtpd/service/qmail-smtpd/log
  echo "qmail-send"
  svc -d /var/lock/qmail-send/service/qmail-send/log
  if [ -f /var/lock/subsys/qmail ]; then
    rm /var/lock/subsys/qmail
  fi
  ;;
stat)
  svstat /service/qmail-send
  svstat /service/qmail-send/log
  svstat /service/qmail-smtpd
  svstat /service/qmail-smtpd/log
  qmail-qstat
  ;;
dqueue|alrm|flush)
  echo "Flushing timeout table and sending ALRM signal to qmail-send."
  /var/qmail/bin/qmail-tcpok
  svc -a /service/qmail-send
  ;;
queue)
  qmail-qstat
  qmail-gread
  ;;
reload|hup)
  echo "Sending HUP signal to qmail-send."
  svc -h /service/qmail-send
  ;;
pause)
  echo "Pausing qmail-send"
  svc -p /service/qmail-send
  echo "Pausing qmail-smtpd"
  svc -p /service/qmail-smtpd
  ;;
cont)
  echo "Continuing qmail-send"
  svc -c /service/qmail-send
  echo "Continuing qmail-smtpd"
  svc -c /service/qmail-smtpd
  ;;
restart)
  echo "Restarting qmail"
  echo " Stopping qmail-smtpd."
  svc -d /service/qmail-smtpd /service/qmail-smtpd/log
  echo " Sending qmail-send SIGTERM and restarting."
  svc -t /service/qmail-send /service/qmail-send/log
  echo " Restarting qmail-smtpd."
  svc -u /service/qmail-smtpd /service/qmail-smtpd/log
  ;;
cdb)
  tctrules /etc/tcp.smtp.cdb /etc/tcp.smtp.tmp < /etc/tcp.smtp
  chmod 644 /etc/tcp.smtp.cdb
  echo " Reloaded" /etc/tcp.smtp.
  ;;
help?)
  cat <<HELP
+stop -- stops mail service connections refused, nothing goes out
start -- starts mail service connection accepted, mail can go out
pause -- temporarily stops mail service (Connections accepted, nothing leaves)
cont -- continues paused service
stat -- displays status of mail service
