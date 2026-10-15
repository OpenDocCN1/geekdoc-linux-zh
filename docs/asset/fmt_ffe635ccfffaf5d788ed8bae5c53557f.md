
```
Nov 1 21:51:36 login: setuid() failed from 199.52.34

Nov 1 21:52:17 login.telnetd[14211]: connect from 207.115.57

Nov 1 21:54:49 login: FAILURES from ppp-207.115.57

Nov 1 21:54:51 login: in.telnetd[14214]: connect from 207.115.57

Nov 2 22:02:11 in.telnetd[14228]: connect from 209.124.46.67

Nov 2 05:27:22 in.telnetd[14442]: connect from 207.115.57

Nov 3 08:08:24 in.telnetd[15596]: connect from 206.116.14

Nov 3 08:08:24 in.pop3d[15604]: loop: peer died: Unknown error

Nov 1 15:06:33 in.pop3d[16004]: connect from 207.115.57.80

Nov 3 16:28:11 in.pop3d[16042]: connect from 207.115.57.96

Nov 3 17:58:52 sendmail[16088]: RAA16087:to=root, date=00:00,

Nov 14 13:17 in.telnet[16888]: connect from 206.115.11.14

Nov 14 13:78 in.com: LOGIN FAILURES from ugu.com

Nov 14 14:57 in.telnet[17083]: connect from 206.115.11.14

Nov 14 17:39 in.telnet[17248]: connect from 206.115.11.14
```

wait

当这些程序和脚本运行时，有几点需要考虑。大多数终端带有屏幕保护程序，这些程序永远激活，导致字符被绘制到显示器上。安全问题是其中之一。如果你的环境中对安全性非常敏感，取决于你打算实现此类程序，你可能需要考虑这种安全风险。如果你没有设置安全或受限 `shell` 方法，你可能希望让程序拥有自己的账户。

```
vi /etc/passwd

monsyshdk13J5SBIEz:8888:20:Monitor System:/usr/bin/monsys
```

设置账户，使程序位于 `/etc/passwd` 文件的 `shell` 中。这样，如果退出或按下 `Ctrl+C`，账户将立即注销。

## 原因

并不是所有的 ASCII 终端在电源循环后或新出箱时都能按预期工作。测试和监控它们的功能往往是必要的。

## 实战经验

当系统和终端每天移动时，验证各种 ASCII 终端的功能就会发生。你永远不知道仿真何时会按预期运行。系统移动后，将其放入测试，并让你的监控工具让终端看起来很忙可能。这不仅仅是给管理层和其他人的表演——如果终端位于 NFS 文件服务器上，它将由于有数据传输而显得繁忙。这是防止用户进入服务器并阻止任何登录尝试的有效威慑。

## 其他资源

Man 页：

`clear`, `yes`, `top`

万网：

- http://ftp.groupsys.com/pub/top/

| UNIX 技巧与技巧 | 目录 | 索引 |
|---|---|---|
| 第 7 章：显示与仿真 | | 上一章 下一章 |
| 本章节内容： | | | |
| 7.5 测试 ASCII 终端 | 7.8 刷新 X | 7.11 用键盘控制鼠标 |
| 7.4 终端类型 | 7.6 ASCII 终端故障排除 | 7.12 从远程 X 运行显示 |
| 7.2 设置终端类型 | 7.9 使用 xkill 杀死资源 | 7.13 ASCII |
| 7.3 使用 sty | 7.10 设置 xterm 标签栏 | | |
| 7.4 热键 | | | |

## 第 7 章：显示与仿真：7.6 ASCII 终端的故障排除

变体：AT&T, BSD

Shell：全部

语法：

```
kill PID
```

ASCII 终端的控制台由一个名为 `getty` 的守护进程控制。该 `getty` 会设置新的名称、速度，并将控制台重置为控制台端口或 ASCII 终端。`getty` 会设置终端类型、模式和行设置。在 UNIX 中，该守护进程由 `init` 进程控制。当 `init` 启动时，它引用 `/etc/init` 文件（或较旧的 BSD 系统上的 `/etc/tty`）进行所有配置。一个条目包含字段：ID、运行状态和操作。

```
t21:23:respawn:/sbin/getty ttydl co_9600
```

由于 `getty` 守护进程由 `init` 进程控制，你只需要杀死 `getty` 进程，它就会自动重启。这是由于 `initab` 条目中的第三字段的作用，如果守护进程因某种原因不存在，则将其重新启动（`respawn`）。

> **警告 - 不要杀死 `init` 进程，因为根据配置表的设置，这样做可能会适得其反。**

```bash
rocket 6# ps -ef | grep getty

root 20665    1  0  Dec 05 ttydl    0:00 /sbin/getty ttydl_9600

rocket 7# kill 20665

rocket 8# ps -ef | grep getty

root 3463     1  0 01:31:14 ttydl    0:00 /sbin/getty ttydl_9600
```
