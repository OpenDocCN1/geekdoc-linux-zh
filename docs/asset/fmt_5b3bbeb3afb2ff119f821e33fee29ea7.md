
## 15.8.7. 更多 systemd

还有其他工具……

| `systemd-analyze` | `systemd-logctl` |
| `systemd-ask-password` | `systemd-machine-id-setup` |
| `systemd-cat` | `systemd-nspawn` |
| `systemd-cgls` | `systemd-run` |
| `systemd-ctop` | `systemd-stdio-bridge` |
| `systemd-coredumpctl` | `systemd-sysv-convert` |
| `systemd-delta` | `systemd-tmpfiles` |
| `systemd-detect-virt` | `systemd-tty-ask-password-agent` |

例如，`systemd-analyze blame` 将给出每个服务启动所需时间的概述。

```
[root@rhel7 ~]# systemd-analyze blame | head

1.977s firewalld.service

1.096s tuned.service

993ms postfix.service

939ms iptables.service

925ms vboxadd-xll.service

880ms firstboot-graphical.service

839ms accounts-daemon.service

829ms network.service

822ms ipupdate.service

795ms boot.mount

[root@rhel7 ~]#
```

## 15.9. 练习：init

1. 修改 `/etc/inittab`，使得只有两个进程会重启（`respawn`）。杀死其他进程并验证它们不会恢复。
2. 使用 Red Hat Linux 虚拟机。进入运行级别 5，显示当前和之前的运行级别，然后返回运行级别 3。
3. 你的电脑上是否更改了环境变量？
4. 列出在运行级别 2 下启动的所有 `init.d` 脚本。
5. 编写一个位于 `/etc/init.d/` 的守护进程脚本。它应该有一个 `case` 语句来处理启动/重启和状态。测试该脚本！
6. 使用 `chconfig` 设置你的脚本在运行级别 3、4 和 5 下启动，在其他运行级别下停止。

## 15.10. 答案：init

1. 修改 `/etc/inittab`，使得只有两个会重启。杀死其他进程验证它们不会恢复。你可以编辑 `/etc/inittab` 使其看起来如下所示。不要忘记运行 `-1`。

```
[root@RHEL5 ~]# grep /etc/inittab

# Run in runlevels

1:234:respawn:/sbin/tty1

2:234:respawn:/sbin/tty2

3:234:respawn:/sbin/tty3

4:234:respawn:/sbin/tty4

5:234:respawn:/sbin/tty5

6:234:respawn:/sbin/tty6

[root@RHEL5 ~]#
```

2. 使用 Red Hat Linux 虚拟机。进入运行级别 5，显示当前和之前的运行级别，然后返回运行级别 3。

```
init 5 (观察控制台的变化)

level 3 (再次在控制台观察)
```

3. 你的电脑上更改了环境变量？在 Red Hat 中是 `/etc/rc`，在 Debian/Ubuntu 中是 `/etc/local`。答案可能是否，但在 RHEL5 中脚本设置了变量。

```
[root@RHEL5 etc]# grep HOSTNAME
```

4. 列出在运行级别 2 下启动的所有 `init.d` 脚本。

```
root@RHEL5 ~ chkconfig --list | grep '2:'
```

5. 编写一个位于 `/etc/init.d/` 的守护进程脚本。它应该有一个 `case` 语句处理启动/重启和状态。测试该脚本！脚本可能像这样：

```
#!/bin/bash

#
# chkconfig: 345 99 01
# description: pold script
# /etc/init.d/pold

case "$1" in
    start)
        echo -n "Starting pold..."
        sleep 1
        touch /var/lock/subsys/pold
        echo "done."
        echo pold started >> /var/log/messages
        ;;
    stop)
        echo -n "Stopping pold..."
        sleep 1
        rm -rf /var/lock/subsys/pold
        echo "done."
        echo pold stopped >> /var/log/messages
        ;;
    *)
        echo "Usage: /etc/init.d/pold {start|stop}"
        exit 1
        ;;
esac

exit 0
```
