
# 默认运行级别

默认运行级别（在此情况下为 `2`）

`id2:init:default:` 系统启动时运行的脚本（在进入默认运行级别之前）

`si:sysinit:wait/sbin/etc/init.d/rc` # 进入运行级别 # 时调用的程序（如果发生这种情况）

`si`（用户操作表示启动了 # 进程且没有其他）`--=S:wait/sbin/config`

# 系统中可用的不同运行级别

`10:wait:/etc/init.d/rc 0`
`11:wait:/etc/init.d/rc 1`
`12:wait:/etc/init.d/rc 2`
`13:wait:/etc/init.d/rc 3`
`14:wait:/etc/init.d/rc 4`
`15:5:wait:/init.d/rc 5`
`15:6:wait:/init.d/rc 6`

# 按 Ctrl+Alt+Del 时运行的命令

`ca=12345:ctrlaltld:-t1 -a r`

# 每个运行时打开的控制台

`respawn` 动作表示进程完成后 `getty` 将再次启动

`1:2345:respawn:/bin/getty 3840 tty1`
`2:2345:respawn:/bin/getty 3840 tty2`
`3:2345:respawn:/bin/getty 3840 tty3`
`4:2345:respawn:/bin/getty 3840 tty4`
`5:2345:respawn:/bin/getty 3840 tty5`
`6:2345:respawn:/bin/getty 3840 tty6`

## 运行级别组织

这些守护进程在每个运行级别中的组织方式非常简单。每个运行级别在 `/etc/rc/X/` 下有一个目录，其中 `X` 是级别的数字。在这些目录中，我们将找到指向守护进程脚本的符号链接，通过这些脚本我们可以告诉系统我们是想启动还是停止它们指向的守护进程。

链接的名字标识了我们将执行的操作：如果链接以 `s`（start，启动）开头，我们告诉系统我们想要启动该守护进程；如果它以 `k`（kill，杀死）开头，我们告诉系统我们想要停止或杀死它。如果名字不以这两个字母中的任何开头，系统将什么都不做。在该字母之后，必须输入一个 `00` 到 `99` 之间的两位数字，以指示它们必须启动或停止的顺序。这个顺序非常重要，因为某些守护进程需要在其他守护进程运行之前才能启动。

在更改运行级别时，系统将检查对应目录下的守护进程，并首先停止指定的守护进程，然后启动它们。我们所做的仅仅是带有启动或停止参数的调用守护进程，因此如果我们停止了任何当前没有运行的守护进程，也不会有问题，因为脚本会考虑到这一点。这可以用于不考虑我们之前所处级别的情况下更改运行级别。

### 表 7.2

| 运行级别 2 | 正在运行的守护进程 | | |
|---|---|---|---|
| K50shd | S10sysklog | syslogd | |
| K1apache-ssl | S12nermeld | kerneld | |
| K2tftpd | S20dhcpd | dhcpd | |
| K3telnet | S50proftpd | proftpd | |
| 运行级别 3 | | | |
| K0dhcpd | S10sysklog | syslogd | |
| K1proftpd | S12nermeld | kerneld | |
| K2apache | S20shd | sshd | |
| K3tftpd | S50apache-ssl | apache-ssl | |
| K3telnet | | apache | |
| 运行级别 4 | | | |
| K0dhcpd | S10sysklog | syslogd | |
| K1proftpd | S12nermeld | kerneld | |
| K2apache | S20tftpd | tftpd | |
| K3tftpd | S50telnet | telnet | |

## `/etc/init` 文件配置

`/etc/init` 文件包含了所有运行级别的配置：默认运行级别、每个运行级别可用的控制台数量。文件的每一行都是一个指令，语法为：`<id>runlevel:<action>`。

第一个字段是指令的标识符；下一个显示该指令中有效的运行级别、我们将执行的操作以及将启动的进程。

下面的示例显示了如何配置这些指令：

```
# 默认运行级别（在此情况下为 2） id2:init:default: 系统启动时运行的脚本（在进入默认运行级别之前） si:sysinit:wait/sbin/etc/init.d/rc # 进入运行级别 # 时调用的程序（如果发生这种情况） si（用户操作表示启动了 # 进程且没有其他）--=S:wait/sbin/config # 系统中可用的不同运行级别 10:wait:/etc/init.d/rc 0 11:wait:/etc/init.d/rc 1 12:wait:/etc/init.d/rc 2 13:wait:/etc/init.d/rc 3 14:wait:/etc/init.d/rc 4 15:5:wait:/init.d/rc 5 15:6:wait:/init.d/rc 6 # 按 Ctrl+Alt+Del 时运行的命令:ca=12345:ctrlaltld:-t1 -a r # 每个运行时打开的控制台（respawn 动作表示进程完成后 getty 将再次启动） 1:2345:respawn:/bin/getty 3840 tty1 2:2345:respawn:/bin/getty 3840 tty2 3:2345:respawn:/bin/getty 3840 tty3 4:2345:respawn:/bin/getty 3840 tty4 5:2345:respawn:/bin/getty 3840 tty5 6:2345:respawn:/bin/getty 3840 tty6
```
