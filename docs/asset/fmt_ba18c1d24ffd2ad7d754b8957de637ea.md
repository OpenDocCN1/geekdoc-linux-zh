
下面显示了一个 `inittab` 示例。文件中第一个未注释的行定义了默认运行级别（run control level），即 `5`。

```
# cat /etc/inittab
...
id:5:initdefault:

# 系统初始化
si::sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

# 捕捉 CTRL-ALT-DELETE
ca::ctrlaltdl:/bin/shutdown -t3 -r now

# 当我们的 UPS 告诉我们断电时，假设我们还有几分钟的电。
# 计划在 2 分钟后关机。
# 这当然假设你安装了电源，并且你的
# UPS 连接并正常工作。
pf:powerfail:/bin/shutdown -f -h +2 "Power Failure; System Shutting Down"

# 如果在关机启动之前恢复电源，则取消。
pr:12345:powerok:/bin/shutdown -c "Power Restored; Shutdown Cancelled"

# 在运行级别中运行 getys
1:2345:respawn:/bin/mingty tty1
2:2345:respawn:/bin/mingty tty2
3:2345:respawn:/bin/mingty tty3
4:2345:respawn:/bin/mingty tty4
5:2345:respawn:/bin/mingty tty5
6:2345:respawn:/bin/mingty tty6

# 在运行级别 5 中运行 xdm
x:5:respawn:/etc/X11/predfm -noadaem
```

如你所见，每行条目由冒号分隔的四个字段组成。字段如下：

- 第一字段定义包含 1–4 个字符的唯一标识字符串。
- 第二字段标识执行该条目的运行级别。空字段适用于所有运行级别。
- 第三字段确定要执行的操作。有很多可能的操作，包括：
    - `initdefault` 确定系统的默认运行级别。`init` 命令读取此行并启动到指定的运行级别。
    - `sysinit` 在 `init` 尝试访问系统控制台之前执行此操作。
    - `wait` 当执行此操作的条目时，相同运行级别的其他条目将等待其完成。
    - `respawn` 只要进程一死亡立即重启。如果进程正在运行，则不执行任何操作。
- 第四字段定义要执行的进程或命令的完整路径以及参数。

如果修改了 `inittab`，你必须强制 `init` 进程重新读取文件的更新信息：

```
# init
# kill -UP 1
```

## 理解虚拟控制台

第 9 章“安装”中提到文本模式 RHEL 安装期间有五个虚拟控制台（图形模式为六个），可以通过组合键进行切换。RHEL 安装并运行后，相同的概念适用，现在可以调用 12 个虚拟控制台，其中 7 个是预定义的，其余可以自定义。相同的键组合用于在第 9 章定义的控制台之间切换。第七个控制台专门显示图形。

```
# 在标准运行级别运行 getys
1:2345:respawn:/bin/mingty tty1
2:2345:respawn:/bin/mingty tty2
3:2345:respawn:/bin/mingty tty3
4:2345:respawn:/bin/mingty tty4
5:2345:respawn:/bin/mingty tty5
6:2345:respawn:/bin/mingty tty6
```

## 启动系统和网络服务

接下来，`init` 命令执行 `/etc/rc.sysinit` 脚本，它调用相应的脚本和命令来配置网络、SELinux、键盘映射、硬件时钟和主机名。脚本激活交换、对文件系统运行 `fsck`、挂载磁盘并加载内核模块。

`init` 命令调用 `/etc/rc.rc` 脚本，并将 `inittab` 文件中的 `initdefault` 值作为参数传递给它。该脚本在启动目录 `/etc/rc.d` 中查找服务，从 `/etc/sysconfig` 目录获取配置信息，并在初始化目录 `/etc/rc.d/init.d` 中启动它们。

以下是顺序目录和初始化目录的列表：

```
# /etc/rc.d
drwxr-xr-x 2 root 4096 Dec 19 18:17 /etc/rc.d/init.d
-drwxr-xr-x 1 root root 2255 Sep 21 2006 /etc/rc.d/rc
drwxr-xr-x 2 root root 4096 Dec 19 18:17 /etc/rc.d/rc0.d
-drwxr-xr-x 2 root root 4096 Dec 19 18:17 /etc/rc.d/rc1.d
drwxr-xr-x 2 root root 4096 Dec 20 00:44 /etc/rc.d/rc2.d
drwxr-xr-x 2 root root 4096 Dec 20 00:45 /etc/rc.d/rc3.d
drwxr-xr-x 2 root root 4096 Dec 20 00:44 /etc/rc.d/rc4.d
drwxr-xr-x 2 root root 4096 Dec 20 00:45 /etc/rc.d/rc5.d
drwxr-xr-x 2 root root 4096 Dec 19 18:17 /etc/rc.d/rc6.d
-drwxr-xr-x 1 root root 2255 Sep 21 2006 /etc/rc.d/rc
drwxr-xr-x 2 root root 4096 Dec 19 18:17 /etc/rc.d/init.d
drwxr-xr-x 2 root root 4096 Dec 19 18:17 /etc/rc.d/rc0.d
drwxr-xr-x 2 root root 4096 Dec 19 18:17 /etc/rc.d/rc1.d
drwxr-xr-x 2 root root 4096 Dec 20 00:44 /etc/rc.d/rc2.d
drwxr-xr-x 2 root root 4096 Dec 20 00:45 /etc/rc.d/rc3.d
drwxr-xr-x 2 root root 4096 Dec 20 00:44 /etc/rc.d/rc4.d
drwxr-xr-x 2 root root 4096 Dec 20 00:45 /etc/rc.d/rc5.d
drwxr-xr-x 2 root root 4096 Dec 19 18:17 /etc/rc.d/rc6.d
```

注意，`rc0.d` 中的所有脚本都是指向 `/etc/rc.d/init.d` 目录中实际启动/停止脚本的符号链接。

```
# /etc/rc.d/rc0.d
total
lrwxr-xr-x 1 root root 24 Dec 19 18:17 config -> ../etc/rc.d/init.d/config
lrwxr-xr-x 1 root root 24 Dec 19 18:17 network -> ../etc/rc.d/init.d/network
lrwxr-xr-x 1 root root 24 Dec 19 18:17 keyboard -> ../etc/rc.d/init.d/keyboard
lrwxr-xr-x 1 root root 24 Dec 19 18:17 clock -> ../etc/rc.d/init.d/clock
lrwxr-xr-x 1 root root 24 Dec 19 18:17 hostname -> ../etc/rc.d/init.d/hostname
lrwxr-xr-x 1 root root 24 Dec 19 18:17 selinux -> ../etc/rc.d/init.d/selinux
lrwxr-xr-x 1 root root 24 Dec 19 18:17 local -> ../etc/rc.d/init.d/local
lrwxr-xr-x 1 root root 24 Dec 19 18:17 modules -> ../etc/rc.d/init.d/modules
```

以下是 `rc1.d` 的内容：
