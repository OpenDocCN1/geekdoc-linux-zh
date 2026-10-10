

2. 在命令提示符处，输入 `ls -1 /dev/log` 并按下 **Enter** 键。该文件的类型是什么？Ubuntu Server Linux 中哪个守护进程使用此文件？其用途是什么？

3. 在命令提示符处，输入 `less /etc/rsyslog.conf` 并按下 **Enter** 键，查看系统日志守护进程（System Log Daemon）的配置文件。是否有任何条目指定了设施（facilities）、优先级（priorities）或日志文件位置？文件的最后一行指定了什么？完成后，按 **q** 键退出 less 实用程序。

4. 在命令提示符处，输入 `less /etc/rsyslog.d/50-default.conf` 并按下 **Enter** 键。默认情况下，任何优先级的内核消息会被记录到哪里？文件名旁边的 `–` 字符表示什么？完成后，按 **q** 键退出 less 实用程序。

5. 在命令提示符处，输入 `tail /var/log/kern.log` 并按下 **Enter** 键。观察这些条目。

6. 在命令提示符处，输入 `ls /var/log/cups` 并按下 **Enter** 键。哪个守护进程在 /var/log/cups 目录中创建了日志文件？

7. 在命令提示符处，输入 `cat /etc/cron.daily/logrotate` 并按下 **Enter** 键，观察每天运行的 `logrotate` 命令。

8. 在命令提示符处，输入 `less /etc/logrotate.conf` 并按下 **Enter** 键，查看 `logrotate` 命令的配置文件。默认情况下保留多少份旧日志文件的副本？完成后，按 **q** 键退出 less 实用程序。

9. 在命令提示符处，输入 `ls /etc/logrotate.d` 并按下 **Enter** 键。此目录中有多少个文件？这些文件中的条目是否会覆盖 `/etc/logrotate.conf` 中相同的条目？

10. 在命令提示符处，输入 `cat /etc/logrotate.d/cups-daemon` 并按下 **Enter** 键。对于 /var/log/cups 目录中的日志文件，保留多少份旧日志文件的副本？如果日志文件没有内容，它们会被轮换吗？

11. 输入 `exit` 并按下 **Enter** 键以注销你的 shell。

## 项目 10-4

在这个实践项目中，你将查看由 Systemd 日志守护进程（Systemd Journal Daemon）创建的配置和日志条目，以及 Fedora Linux 上 logrotate 实用程序的配置。

- 1. 在你的 Fedora Linux 虚拟机上，通过按下 **Ctrl+Alt+F2** 切换到命令行终端 (tty2)，并使用用户名 `root` 和密码 `LNXRocks!` 登录终端。
- 2. 在命令提示符处，输入 `ls -1 /dev/log` 并按下 **Enter** 键。该文件的类型是什么？Fedora Linux 中哪个守护进程使用此文件？其用途是什么？
- 3. 在命令提示符处，输入 `cat /etc/systemd/journald.conf` 并按下 **Enter** 键，查看 Systemd 日志守护进程的配置文件。哪一行代码可以取消注释并配置，以设置日志数据库的最大大小？
- 4. 在命令提示符处，输入 `journalctl _COMM=` 并按两次 Tab 键。你可以使用哪个关键字来查看来自 GNOME 显示管理器的日志条目？按 **Ctrl+c** 返回命令提示符。接下来，输入 `journalctl _COMM=gnome` 并按下 **Enter** 键，查看来自 GNOME 显示管理器的日志条目。是否显示了多天的条目？
- 5. 在命令提示符处，输入 `journalctl - -COMMEs=xd - -since "5:00"` 并按下 **Enter** 键，查看自上午 5:00 以来来自 GNOME 显示管理器的日志条目。
- 6. 在命令提示符处，输入 `which crond` 并按下 **Enter** 键。cron 守护进程可执行文件的路径是什么？接下来，输入 `journalctl /sbin/crond - -since "5:00"` 并按下 **Enter** 键。显示了哪些条目？
- 7. 在命令提示符处，输入 `ls /var/log` 并按下 **Enter** 键。观察这些条目。`/var/log` 中是否有哪些由未通过 `journald` 记录条目的守护进程创建的日志文件？
- 8. 在命令提示符处，输入 `ls /var/log/cups` 并按下 **Enter** 键。内容是否与项目 10-3 第 6 步中的内容相似？
- 9. 在命令提示符处，输入 `cat /etc/cron.daily/logrotate` 并按下 **Enter** 键，观察每天运行的 `logrotate` 命令。
- 10. 在命令提示符处，输入 `less /etc/logrotate.conf` 并按下 **Enter** 键，查看 `logrotate` 命令的配置文件。默认情况下保留多少份旧日志文件的副本？完成后，按 **q** 键退出 `less` 实用程序。
- 11. 在命令提示符处，输入 `ls /etc/logrotate.d` 并按下 **Enter** 键。此目录中有多少个文件？这些文件中的条目是否会覆盖 `/etc/logrotate.conf` 中相同的条目？
- 12. 在命令提示符处，输入 `cat /etc/logrotate.d/cups` 并按下 **Enter** 键。对于 `/var/log/cups` 目录中的日志文件，保留多少份旧日志文件的副本？如果日志文件没有内容，它们会被轮换吗？
- 13. 输入 `exit` 并按下 **Enter** 键以注销你的 shell。

## 项目 10-5

在这个实践项目中，你将观察 Fedora Linux 上的用户账户数据库，并使用命令行实用程序创建用户账户。

- 1. 在你的 Fedora Linux 虚拟机上，通过按下 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并使用用户名 **root** 和密码 `LNxrocksl` 登录终端。
- 2. 在命令提示符处，输入 `less /etc/passwd` 并按下 **Enter** 键。描述 root 用户的行在这个文件的什么位置？描述 user1 用户的行在这个文件的什么位置？存在多少个守护进程账户？所有账户的密码字段中是什么？完成后，按 **q** 键退出 `less` 实用程序。
- 3. 在命令提示符处，输入 `ls -1 /etc/passwd` 并按下 **Enter** 键。该文件的所有者和组所有者是谁？谁有权读取此文件？
- 4. 在命令提示符处，输入 `less /etc/shadow` 并按下 **Enter** 键。root 用户和 user1 用户账户的密码字段中是什么？大多数守护进程账户的密码字段中是什么？按 **q** 键退出 `less` 实用程序。
- 5. 在命令提示符处，输入 `ls -1 /etc/shadow` 并按下 **Enter** 键。该文件的所有者和组所有者是谁？谁有权读取此文件？将 `/etc/shadow` 的权限与第 3 步中获取的 `/etc/passwd` 的权限进行比较，并解释其区别。
- 6. 在命令提示符处，输入 **pwconv** 并按下 **Enter** 键。接下来，在命令提示符处输入 `less /etc/shadow` 并按下 **Enter** 键。你收到什么错误消息？为什么？
- 7. 在命令提示符处，输入 `less /etc/passwd` 并按下 **Enter** 键。所有账户的密码字段中是什么？为什么？完成后，按 **q** 键退出 less 实用程序。
- 8. 在命令提示符处，输入 **pwconv** 并按下 **Enter** 键。pwconv 命令做什么？
- 9. 接下来，在命令提示符处输入 `less /etc/shadow` 并按下 **Enter** 键。验证文件是否有内容，完成后按 **q**。接下来，在命令提示符处输入 `less /etc/passwd` 并按下 **Enter** 键。验证文件是否有内容，完成后按 **q**。
- 10. 在命令提示符处，输入 `cat /etc/default/useradd` 并按下 **Enter** 键。创建用户时默认使用什么 shell？创建用户时默认的 skel 目录位置在哪里？默认情况下主目录创建在哪里？
- 11. 在命令提示符处，输入 `ls -a /etc/skel` 并按下 **Enter** 键。此目录中存储了哪些文件？创建用户时此目录的用途是什么？
- 12. 在命令提示符处，输入 `cp /etc/initab /etc/skel` 并按下 **Enter** 键，在 /etc/skel 目录中创建 inittab 文件的副本。
- 13. 在命令提示符处，输入 `useradd -m bozo` 并按下 **Enter** 键。-m 选项指定了什么？默认 shell 和主目录信息是从哪里获取的？
- 14. 在命令提示符处，输入 `less /etc/login.defs` 并按下 **Enter** 键。观察条目和描述性注释。在第 13 步中向 useradd 命令指定 -m 选项是否是必需的？请解释。按 **q** 键退出 less 实用程序。
- 15. 在命令提示符处，输入 `cat /etc/passwd` 并按下 **Enter** 键。bozo 的 shell 和主目录是什么？bozo 的 UID 是多少？
- 16. 在命令提示符处，输入 `cat /etc/shadow` 并按下 **Enter** 键。bozo 有密码吗？bozo 可以登录系统吗？
- 17. 在命令提示符处，输入 `passwd bozo` 并按下 **Enter** 键。输入密码 LNXrocks! 并按下 **Enter** 键。再次输入密码 LNXrocks! 进行确认，然后按下 **Enter** 键。
- 18. 在命令提示符处，输入 `ls -a /home/bozo` 并按下 **Enter** 键。此目录中有多少个文件？将此列表与第 11 步中获取的列表进行比较。inittab 文件是否存在？
- 19. 输入 **exit** 并按下 **Enter** 键以注销你的 shell。

## 项目 10-6

在这个实践项目中，你将使用命令行实用程序修改 Fedora Linux 上的用户账户。

- 1. 在你的 Fedora Linux 虚拟机上，通过按下 Ctrl+Alt+F2 切换到命令行终端 (tty2)，并使用用户名 root 和密码 LNXrocks! 登录终端。

