
```
$ ls -l /etc/xinetd.d
total 76
-rw-r--r-- 1 root root 560 Jul 8 2003 charger
-rw-r--r-- 1 root root 580 Jul 8 2003 charger-udp
-rw-r--r-- 1 root root 417 Jul 8 2003 daytime
-rw-r--r-- 1 root root 437 Jul 8 2003 echo
-rw-r--r-- 1 root root 339 Jul 8 2003 echo
-rw-r--r-- 1 root root 358 Jul 8 2003 echo-udp
-rw-r--r-- 1 root root 317 Jul 8 2003 finger
-rw-r--r-- 1 root root 257 Jul 8 2003 ntalk
-rw-r--r-- 1 root root 359 Jul 8 2003 resec
-rw-r--r-- 1 root root 376 Jul 8 2003 login
-rw-r--r-- 1 root root 429 Jul 8 2003 rsh
-rw-r--r-- 1 root root 317 Jul 8 2003 rsync
-rw-r--r-- 1 root root 310 Jul 8 2003 servers
-rw-r--r-- 1 root root 312 Jul 8 2003 services
-rw-r--r-- 1 root root 245 Jul 8 2003 talk
-rw-r--r-- 1 root root 303 Jul 8 2003 telnet
-rw-r--r-- 1 root root 495 Jul 8 2003 time
-rw-r--r-- 1 root root 515 Jul 8 2003 time-udp
-rw-r--r-- 1 root root 328 Apr 25 13:48 wu-ftpd
```

每个文件都对服务的执行方式提供了细粒度的控制，包括它应该以的用户运行以及日志选项：

```
$ cat /etc/xinetd.d/finger
# default: on
# description: The finger server answers finger requests.
# finger 是一种允许远程用户查看本地用户
# 登录名和最后登录时间的协议。
service finger
{
    disable = yes
    socket_type = stream
    wait = no
    user = nobody
    server = /usr/sbin/in.fingerd
}
```

启用或禁用服务只需用编辑器打开文件并更改 `disable` 值即可。

在谈到内联属性时，可以为单个服务或通过 `/etc/xinetd.conf` 文件全局地定义许多其他属性。特别值得注意的是：

- `no_access`: 不允许访问服务的客户端列表。
- `only_from`: 允许访问服务的客户端列表。
- `cps`: 每秒最大连接数。达到此阈值后，新的连接尝试将被临时拒绝。
- `instances`: 允许运行的最大并发实例数。
- `max_load`: 服务停止接受连接的系统负载百分比。
- `per_source`: 允许同一源的连接数。
- `bind`: 将服务绑定到特定的接口。

`bind` 在防火墙机器上特别有用，因为你可能希望从局域网内部 `ssh` 到该机器，但不想让从互联网访问该服务。`cps`、`instances`、`max_load` 和 `per_source` 都是对抗 DoS 攻击的有用工具，但要小心（特别是 `per_source`）不要将这些值设置得太低。

对 `xinetd` 服务进行任何必要的更改后，使用以下命令重启守护进程：

```
killall -HUP xinetd
```

此更改在重启后依然有效。

## inetd

在使用 `inetd` 而非 `xinetd` 的发行版中，禁用服务只需用文本编辑器打开 `/etc/inetd.conf` 并注释掉相关行即可：

- `# 文件传输协议 (FTP) 服务器：`
  `ftp-server stream nowait root /usr/sbin/tcpd proftpd`
- `# Telnet 服务器：`
  `#telnet stream nowait root /usr/sbin/tcpd in.telnetd`
- `# 当 biff 设置为 y 时，comsat 守护进程会通知用户有新邮件：`
  `comsat dgram udp wait root /usr/sbin/tcpd in.comsat`
- `# Shell, login, exec 和 talk 是 BSD 协议：`
  `#shell stream tcp nowait root /usr/sbin/tcpd in.rshd -L`
  `#login stream tcp nowait root /usr/sbin/tcpd in.rlogindd`

保存更改后，使用以下命令重启 `inetd`：

```
killall -HUP inetd
```

## 其他服务

并非所有服务都从 `inetd/xinetd` 启动；然而，要找到其余服务，你需要深入系统的初始化脚本。在采用 System V 初始化方法的发行版中，每个服务都由自己的 shell 脚本控制。以下是来自 SuSE 机器的随机脚本，用于控制随机数生成器（为了简洁略微编辑）：

```bash
#! /bin/sh
# /etc/init.d/random
#
# 用于在启动时快照随机状态并重新加载的脚本。
#
# 保存并恢复系统熵池以更高质量的
# 随机数生成。

random_seed=/var/lib/misc/random-seed

rc_reset
case "$1" in
start)
  echo -n "Initializing random number generator"
  if test ! -f $random_seed ; then
    cat $random_seed > /dev/urandom
    rc_status
  else
    > $random_seed
    rc_status
  fi
  chmod 600 $random_seed
  dd if=/dev/urandom of=$random_seed count=1 bs=512 \
  2>/dev/null
  rc_status -v
  ;
stop)
  echo -n "Saving random seed"
  if test ! -f $random_seed ; then
    > $random_seed
    rc_status
  fi
  chmod 600 $random_seed
  dd if=/dev/urandom of=$random_seed count=1 bs=512 \
  2>/dev/null
  rc_status -v
  ;
status)
  echo -n "Checking for random generator (always true)"
  rc_status -v
  ;
*)
  echo "Usage: $0 {start|stop|status}"
  exit 1
esac
rc_exit
```

有了脚本处理所有这些性性工作，启动或停止随机数生成器只需带有相应的参数调用脚本：

`# 基础系统安全措施 237`

```bash
# /etc/init.d/random stop
saving random seed
done
```

```bash
# /etc/init.d/random start
Initializing random number generator
done
```

```bash
# /etc/init.d/random status (always true)
Checking for random generator
running
```

类似的脚本通常用于控制其他服务，包括 `SSH`、`gpm`（控制台守护进程）、`xdm`（X 显示管理器）、`nfslock` 和 `hotspot`。你可以看到，`init`（初始化）脚本是启动——更重要的是停止服务的关键。在 Redhat 系统上，`init` 脚本可以在 `/etc/rc.d/` 中找到；在 SuSE 上，它们位于 `/etc/init.d`（技术上，这是两者中更正确的位置）。为了避免你输入完整路径，Redhat 还提供了 `service` 命令。因此：

```bash
# service nfslock stop
```

等同于

```bash
# /etc/rc.d/init.d/nfslock stop
```

### 运行级别（Runlevels）和初始化脚本
