
## init 脚本

目录 /etc/init.d/ 中包含用于在系统启动时执行特定任务以及在运行系统中启动和停止服务的 shell 脚本。以下展示了 /etc/init.d/ 中的一些文件。

```
halo:~ # ls -al /etc/init.d/
total 635
drwxr-x--- 11 root root   3336 May 24 13:40 .
drwxr-x---  77 root root   6712 May 25 13:19 ..
-rw-r-----  1 root root   1393 May 24 13:40 .depend.boot
-rw-r-----  1 root root   3465 May 24 13:40 .depend.start
-rw-f-----  1 root root   3002 May 24 13:40 .depend.stop
-rw-f-----  1 root root     482 Aug  25  2004 Makefile
-rw-f-----  1 root root    7827 May 10 18:17 README
-rwxr-xr-x  1 root root    1257 May  8 20:09 SuSEfirewall2_init
-rwxr-xr-x  1 root root    1650 May  8 20:09 SuSEfirewall2_setup
-rwxr-xr-x  1 root root    2696 May  8 20:29 aacagentd
-rwxr-x---  1 root root     5729 May  8 20:15 acpid
-rwxr-xr-x  1 root root    5265 May  8 21:01 alsaasound
-rwxr-xr-x  1 root root    3689 May  9 14:49 atd
-rwxr-xr-x  1 root root    6691 May  9 15:03 audtd
-rwxr-xr-x  1 root root    9234 May  9 15:01 autofs
-rwxr-xr-x  1 root root    2967 Mar 14 13:40 autovast
-rwxr-xr-x  1 root root     7072 Apr 20 15:02 boot
-rwxr-xr-x  1 root root    2792 May  8 20:29 boot.apparmor
...
```

文件 `.depend.[boot,start,stop]` 由 insserv 创建，包含用于确定当 /etc/sysconfig/boot 中的 `RUN_PARALLELL` 设置为 yes 时启动服务的正确顺序的依赖关系。

shell 脚本可以通过以下方式调用：

-   系统启动、系统关闭或用户通过 Ctrl+Alt+Del 停止系统时，由 init 直接调用。这些脚本的示例包括 /etc/init.d/boot 或 /etc/init.d/rc。
-   更改运行级别时，由 init 间接调用。在这种情况下，脚本 /etc/init.d/rc 会在运行级别变更期间以正确的顺序和参数调用必要的脚本。
-   通过 /etc/init.d/script parameter 直接调用。

如果 /sbin/ 或 /usr/sbin/ 中设置了相应的链接，你也可以输入 `rcs* script parameter`。

可以使用以下参数：

表 5-2

| 参数 | 描述 |
|-----------|-------------|
| start | 启动未运行的服务。 |
| restart | 停止正在运行的服务并重新启动它。 |
| stop | 停止正在运行的服务。 |
| reload | 重新读取服务的配置，而不停止和重新启动服务本身。 |
| force-reload | 如果服务支持此功能，则重新加载配置。否则，执行与 restart 相同的操作。 |
| status | 显示服务的当前状态。 |

如果在没有参数的情况下调用脚本，一条消息会告知你可能的参数。

存储在 /etc/init.d/ 中的一些重要脚本包括：

-   **boot.** 此脚本在系统启动时由 init 直接启动。它只运行一次且仅一次。它评估目录 /etc/init.d/boot.d/ 并启动所有文件名以“S”开头的脚本（参见第 5-31 页的“运行级别符号链接”）。

这些脚本执行例如以下任务：

-   检查文件系统
-   配置 LVM
-   删除 /var/lock/ 中不必要的文件
-   设置系统时间
-   使用 isapnp 工具配置 PnP 硬件

-   **boot.local.** 此脚本包含在切换到运行级别之前启动时执行的附加命令。你可以向此脚本添加你自己的系统扩展。

-   **halt.** 如果输入运行级别 0 或 6，则运行此脚本。它要么通过 `halt` 命令调用（系统完全关闭），要么通过 `reboot` 命令调用（系统关闭然后重新启动）。

-   **rc.** 此脚本负责从一个运行级别正确切换到另一个运行级别。它运行当前运行级别的停止脚本，然后运行新运行级别的启动脚本。

-   **service.** 每个服务（如 cron、apache2、cups）都附带一个脚本，允许你启动和停止服务、重新加载其配置或查看其状态。要创建自己的脚本，你可以将文件 /etc/init.d/skeleton 用作模板。

### 运行级别符号链接

要进入特定的运行级别，init 调用脚本 /etc/init.d/rc，并将运行级别作为参数。此脚本检查相应的运行级别目录 /etc/init.d/rc*.d/，并根据该目录中的链接启动和停止服务。

对于每个运行级别，/etc/init.d/ 中都有一个对应的子目录。对于运行级别 1，它是 /etc/init.d/rc1.d/；对于运行级别 2，它是 /etc/init.d/rc2.d/，以此类推。

当你查看 /etc/init.d/rc3.d/ 等目录中的文件时，你会看到两种类型的文件——以“K”开头的和以“S”开头的：

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

第一个字母后面总是跟随两位数字和服务的名称。某个服务在特定运行级别中是否被启动，取决于 /etc/init.d/rc*.d/ 目录中是否存在 **S***service 和 **K***service 文件。

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

通常，运行级别目录中的两个链接指向同一个脚本。例如，如果在 `/etc/init.d/rc3.d/` 目录中输入 **ls -l \*network**，你会看到两个网络链接都指向脚本 `/etc/init.d/network`：

```
dallo:~ # ls -l /etc/init.d/rc3.d/\*network
lrwxrwxrwx 1 root root 10 May 15 10:23 /etc/init.d/rc3.d/K17network -> ../network
lrwxrwxrwx 1 root root 10 May 15 10:23 /etc/init.d/rc3.d/S05network -> ../network
```

> 有时 **K/x** 链接被称为 *kill scripts*（终止脚本），而 **S/x** 链接被称为 *start scripts*（启动脚本）。实际上，启动和停止服务有单独的脚本，但脚本是根据参数 `stop` 或参数 `start` 调用的。

### init 如何确定要启动和停止哪些服务

你已经知道服务是通过参数 start 启动的，通过参数 stop 停止的。在从一个运行级别切换到另一个运行级别时，也使用相同的参数。

当运行级别更改时，init 调用带有新运行级别作为参数的脚本 rc，例如 /etc/init.d/rc 3。脚本 /etc/init.d/rc 检查目录 /etc/init.d/currrent rl .d 和 /etc/init.d/rcnewrl.d/，并确定要执行的操作。

假设我们从当前的运行级别 5 更改为新的运行级别 3。有三种可能性：

-   在 /etc/init.d/rc5.d/ 中某服务有 Kxx 链接，而在 /etc/init.d/rc3.d/ 中同一服务有 Sxx 链接。
    -   在这种情况下，服务既不会启动也不会停止；/etc/init.d/ 中相应的脚本根本不会被调用。
-   在 /etc/init.d/rc5.d/ 中某服务有 Kxx 链接，而在 /etc/init.d/rc3.d/ 中没有对应的 Sxx 链接。
    -   在这种情况下，/etc/init.d/service 中的脚本以参数 stop 调用，服务被停止。
-   在 /etc/init.d/rc3.d/ 中有 Sxx 链接，而在 /etc/init.d/rc5.d/ 中该服务没有对应的 Kxx 链接。
    -   在这种情况下，/etc/init.d/service 中的脚本以参数 start 调用，服务被启动。

K 或 S 后面的数字决定了脚本被调用的顺序。

因此，脚本 K10cron 在脚本 K20haldaemon 之前被调用，这意味着 cron 在 haldaemon 之前关闭。

脚本 S05network 在 S11postfix 之前被调用，这意味着服务 network 在 postfix 之前启动。如果 postfix 依赖于正在运行的 network 服务，这一点很重要。

