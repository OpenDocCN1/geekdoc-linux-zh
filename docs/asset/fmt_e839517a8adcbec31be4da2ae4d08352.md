
以 `.pub` 扩展结尾的文件存储 OpenSSH 服务器的公钥。以 `.key` 扩展的文件存储私钥。私钥不应被 `root` 用户以外的任何人读取。最后一个文件 `ssh_config` 是配置文件。列表 12-1 显示了该文件的默认版本（为了简洁进行了略微修改）。

#### 列表 12-1: `/etc/ssh/ssh_config`

```
# /etc/ssh/ssh_config 文件

# 这是服务器系统范围的配置文件。

Port 22

ListenAddress 0.0.0.0

HostKey /etc/ssh/ssh_host_key

ServerKeyBits 768

LoginGraceTime 600

KeyRegenerationInterval 3600

PermitRootLogin yes

IgnoreHosts yes

StrictModes yes

X11Forwarding no

X11DisplayOffset 10

PrintMotd yes

KeepAlive yes

SyslogFacility AUTH AUTH

LogLevel INFO

RhostsAuthentication no

RhostsRSAAuthentication no

RSAAuthentication yes

PasswordAuthentication yes

PermitEmptyPasswords no

CheckMail no
```

这些指令可能需要更改：

- `Port` 指定 `ssh` 绑定并监听连接的端口号。
- `ListenAddress` 指定 IP 地址。
- `HostKey` 指定主机密钥的路径。
- `ServerKeyBits` 指定密钥的位数。
- `LoginGraceTime` 指定登录的宽限时间。
- `KeyRegenerationInterval` 指定密钥生成的间隔。
- `PermitRootLogin` 指定是否允许 `root` 登录。
- `IgnoreHosts` 指定是否忽略 `rhosts`。
- `StrictModes` 指定严格模式操作。
- `X11Forwarding` 指定是否允许 X11 转发。
- `X11DisplayOffset` 指定 X11 的偏移量。
- `PrintMotd` 指定是否打印当日消息（Motd）。
- `KeepAlive` 指定连接超时时间。
- `SyslogFacility` 指定日志设施。
- `LogLevel` 指定日志级别。
- `RhostsAuthentication` 指定是否允许 `rhosts` 验证。
- `RhostsRSAAuthentication` 指定是否允许 RSA-rhosts 验证。
- `RSAAuthentication` 指定是否允许 RSA 验证。
- `PasswordAuthentication` 指定是否允许密码验证。
- `PermitEmptyPasswords` 指定是否允许空密码。
- `CheckMail` 指定是否检查用户是否有电子邮件。

# 列表 12-2 (续)

```
# config: /etc/ssh/ssh_random_seed

# config: /etc/ssh/sshd_config

# pidfile: /var/run/sshd.pid

# 源函数库

  /etc/rc.d/init.d/functions

RETVAL=0

# 为了提高可读性的某些函数

KEYGEN=/usr/bin/ssh-keygen

RSA_KEY=/etc/ssh/ssh_host_key

DSA_KEY=/etc/ssh/ssh_host_dsa_key

PID_FILE=/var/run/sshd.pid

do_rsa_keygen() {

    if $KEYGEN -R && test -f $RSA_KEY ; then

        echo -n "Generating SSH RSA host key: "

        if $KEYGEN -q -b 1024 -f $RSA_KEY -C '' -N '' >/dev/null; then

            success "RSA key generation"

            echo

    else

        failure "RSA key generation"

        echo

        exit 1

    fi

}

do_dsa_keygen() {

    if test -f $DSA_KEY ; then

        echo -n "Generating SSH DSA host key: "

        if $KEYGEN -q -b 1024 -f $DSA_KEY -C '' -N '' >/dev/null;

        then

            success "DSA key generation"

            echo

    else

        failure "DSA key generation"

        echo

        exit 1

    fi

}

case "$1" in

  start)

    # 如果必要则创建密钥

    do_rsa_keygen;

    do_dsa_keygen;

    echo -n "Starting sshd: *"

    if [ ! -f $PID_FILE ]; then

      sshd

      RETVAL=$?

      if [ "$RETVAL" = "0" ]; then

        success "sshd startup"

        touch /var/lock/subsystem/sshd

      else

        failure "sshd startup"

      fi

    fi

    echo

  ;;

stop)

    echo -n "Shutting down sshd: *"

    if [ -f $PID_FILE ]; then

      killproc sshd

      [ $RETVAL -eq 0 ] && rm -f /var/lock/subsystem/sshd

    fi

    echo

  ;;

restart)

    $0 stop

    $0 start

    RETVAL=$?

  ;;

condrestart)

    if [ -f /var/lock/subsystem/sshd ]; then

      $0 stop

      $0 start

      RETVAL=$?

    fi

  ;;

status)

    status sshd

    RETVAL=$?

  ;;

*)

    echo "Usage: sshd {start|stop|restart|status|condrestart}*"

    exit 1

  ;;

esac

exit $RETVAL
```

# 第三部分：系统安全

2. 使用以下命令将此脚本链接到你的运行级别目录：
   `ln -s /etc/rc.d/init.d/sshd /etc/rc.d/rc3/S55sshd`

这种形式的命令假设你的运行级别是 3，这是很典型的。

`openssh-server-version.rpm` 软件包包含了上述脚本以及其他文件，使得管理 SSH 守护进程变得简单。如果你之前安装过此软件包，可以通过这种方式启动守护进程：

```
/etc/rc.d/init.d/sshd start
```

当你第一次运行上述命令时，你会看到如下输出：

```
Generating SSH RSA host key: [ OK ]
Generating SSH DSA host key: [ OK ]
Starting sshd: [ OK ]
```
