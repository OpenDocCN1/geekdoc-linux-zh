
```
gal0:~ # ls /etc/init.d/rc3.d/
K10cron K1network S07auditd
K10smbfs K2haldaemon S07portmap
K1nscd K21acpid S07splash_early
K1postfix K21dbus S08 nfs
K12alsasound K21fbset S08nfsboot
K12boot.apparmor K21irq_balancer S10alsasound
K12 cups K21random S10boot.apparmor
K12microcode K21resmgr S10cups
K12powersaved S01acpid S10kbd
K12splash S01dbus S10microcode
K12shd S01fbset S10powersaved
K14 nfs S01irq_balancer S10splash
K14nfsboot S01random S10sshd
K15auditd S01resmgr S11ncsd
K15portmap S02haldaemon S11postfix
K15splash_early S05network S12cron
K6novell-zmd S06novell-zmd S12smbfs
K16s1pd S06s1pd
K16syslog S06syslog
```

第一个字母后面总是跟随两位数字和服务的名称。某个服务在特定运行级别中是否被启动，取决于 `/etc/init.d/rc*.d/` 目录中是否存在 `S*service` 和 `K*service` 文件。

在 `/etc/init.d/rcX.d/` 目录中输入 `ls -l` 表明这些文件实际上是指向 `/etc/init.d/` 中服务脚本的符号链接（如下所示）：

```
dallo:~ # ls -l /etc/init.d/rc3.d/
total 0
lrwxrwxrwx 1 root root  7 May 15 10:32 K10cron   -> ../cron
lrwxrwxrwx 1 root root  8 May 15 10:48 K10mbfs -> ../mbfs
lrwxrwxrwx 1 root root  7 May 15 10:32 K1nscd  -> ../nscd
lrwxrwxrwx 1 root root 10 May 15 10:32 K1postfix -> ../postfix
lrwxrwxrwx 1 root root 12 May 15 10:26 K12alsaasound -> ../alsaasound
...
lrwxrwxrwx 1 root root  7 May 15 10:31 S10sshd -> ../sshd
lrwxrwxrwx 1 root root  7 May 15 10:32 S1nscd  -> ../nscd
lrwxrwxrwx 1 root root 10 May 15 10:32 S11postfix -> ../postfix
lrwxrwxrwx 1 root root  7 May 15 10:32 S12cron -> ../cron
lrwxrwxrwx 1 root root  8 May 15 10:48 S12mbfs -> ../mbfs
```

通过仅在子目录中使用符号链接，如果脚本需要必要的更改，则只需修改 `/etc/init.d/` 中的版本即可。

通常，运行级别目录中的两个链接指向同一个脚本。例如，如果在 `/etc/init.d/rc3.d/` 目录中输入 `ls -l *network`，你会看到两个网络链接都指向脚本 `/etc/init.d/network`：

```
dallo:~ # ls -l /etc/init.d/rc3.d/*network
lrwxrwxrwx 1 root root 10 May 15 10:23 /etc/init.d/rc3.d/K17network -> ../network
lrwxrwxrwx 1 root root 10 May 15 10:23 /etc/init.d/rc3.d/S05network -> ../network
```

> 有时 `K/x` 链接被称为 *kill scripts*（终止脚本），而 `S/x` 链接被称为 *start scripts*（启动脚本）。实际上，启动和停止服务有单独的脚本，但脚本是根据参数 `stop` 或参数 `start` 调用的。

## init 如何确定要启动和停止哪些服务

你已经知道服务是通过参数 `start` 启动的，通过参数 `stop` 停止的。在从一个运行级别切换到另一个运行级别时，也使用相同的参数。

当运行级别更改时，`init` 调用带有新运行级别作为参数的脚本 `rc`，例如 `/etc/init.d/rc 3`。脚本 `/etc/init.d/rc` 检查目录 `/etc/init.d/currrent rl .d` 和 `/etc/init.d/rcnewrl.d/`，并确定要执行的操作。

假设我们从当前的运行级别 5 更改为新的运行级别 3。有三种可能性：

- 在 `/etc/init.d/rc5.d/` 中某服务有 `Kxx` 链接，而在 `/etc/init.d/rc3.d/` 中同一服务有 `Sxx` 链接。
  - 在这种情况下，服务既不会启动也不会停止；`/etc/init.d/` 中相应的脚本根本不会被调用。
- 在 `/etc/init.d/rc5.d/` 中某服务有 `Kxx` 链接，而在 `/etc/init.d/rc3.d/` 中没有对应的 `Sxx` 链接。
  - 在这种情况下，`/etc/init.d/service` 中的脚本以参数 `stop` 调用，服务被停止。
- 在 `/etc/init.d/rc3.d/` 中有 `Sxx` 链接，而在 `/etc/init.d/rc5.d/` 中该服务没有对应的 `Kxx` 链接。
  - 在这种情况下，`/etc/init.d/service` 中的脚本以参数 `start` 调用，服务被启动。

`K` 或 `S` 后面的数字决定了脚本被调用的顺序。

因此，脚本 `K10cron` 在脚本 `K20haldaemon` 之前被调用，这意味着 `cron` 在 `haldaemon` 之前关闭。

脚本 `S05network` 在 `S11postfix` 之前被调用，这意味着服务 `network` 在 `postfix` 之前启动。如果 `postfix` 依赖于正在运行的 `network` 服务，这一点很重要。

例如，当你从运行级别 3 切换到运行级别 5 时，会发生以下情况：

1. 你通过输入 `init 5`（以 root 身份）告知 `init` 切换到另一个运行级别。
2. `init` 检查其配置文件（`/etc/inittab`）并确定应使用新的运行级别（`5`）作为参数启动 `/etc/init.d/rc`。
3. `rc` 调用当前运行级别中那些在新运行级别中没有启动脚本（`Sxx`）的服务的停止脚本（`Kxx`）。
4. 新运行级别中那些在旧运行级别中没有终止脚本的服务的启动脚本将被启动。

当切换到与当前运行级别相同的运行级别时，`init` 仅检查 `/etc/inittab` 中的更改，并启动相应的步骤（例如在另一个接口上启动 `getty`）。

## 激活和停用运行级别的服务

通过添加或删除运行级别目录 `/etc/init.d`/`rc.d` 中相应的 `K*`/`*service` 和 `S*`/`*service` 链接，可以在运行级别中激活或停用服务。

虽然你可以自己在运行级别子目录中创建符号链接来修改服务，但更简单的方法是编辑脚本的头部，然后调用 `inserv`。

服务脚本开头的 `INIT INFO` 块描述了该服务应在哪个运行级别启动或停止，以及哪些服务应作为先决条件运行：

```
### BEGIN INIT INFO
# Provides:     syslog
# Required-Start: network
# Should-Start:   earlysyslog
# Required-Stop:  network
# Default-Start:  2 3 5
# Default-Stop:
# Description:    Start the system logging daemons
### END INIT INFO
```

`INIT INFO` 块由 `insserv` 程序使用，以确定需要在哪些运行级别子目录中放置链接，以及需要在 `K` 和 `S` 后面放置哪些数字。

> 有关 `insserv` 程序的详细信息，请输入 `man 8 insserv`。

`Default-Start` 条目决定了链接应放置在哪个运行级别目录中。`Required-Start` 条目决定了哪些服务必须在当前考虑的服务之前启动。

编辑 `INIT INFO` 块后，输入 `insserv -d service`（默认值）以创建所需的链接，并根据需要重新编号现有的链接。
