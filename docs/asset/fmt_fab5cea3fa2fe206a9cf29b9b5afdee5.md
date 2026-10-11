
`init` 程序与主要位于 `/etc/rc.d` 目录及其子目录的多个脚本交互。`/etc/rc.d` 目录包含一组子目录和脚本，旨在允许 `init` 程序以不同的配置启动 Linux 系统。目录命名为 `rc0`, `rc1`, `rc2`, `rc3`, `rc4`, `rc5`, `rc6` 和 `init.d`。此外，还有 `rc.sysinit` 和 `rc.local` 等初始化脚本。

`/etc/rc.d/init.d` 目录中的每个文件都是可执行脚本，并且通常接受如 `start`、`stop`、`status`、`restart` 和 `reload` 等简单参数。每个名为 `rcN` 的目录（`N` 取值 0 到 6）代表系统启动到的特定运行级别，并包含指向 `/etc/rc.d/init.d` 目录中部分脚本的链接，以便在该级别执行。在这些目录中建立的链接以 `K` 或 `S` 开头，后跟一个两位整数和脚本名称。

# 面向 Windows 程序员的 Linux 23

该链接建立的脚本。字母 `K` 表示由该链接标识的进程被杀死（或停止），字母 `S` 表示应该启动该进程。两位数字整数表示执行脚本的顺序（无论是启动还是停止），`00` 为优先级最高，`99` 为优先级最低。列表 2.1 显示了 Red Linux 8.0/9.0 系统第 5 层定义的典型链接列表。

## 列表 2.1

```
lrwxrxrwx 1 root 19 Oct 12 16:44 K05saslaauth -> ../init.d/saslauth
lrwxrxrwx 1 root 16 Oct 12 16:44 K12mysqld -> ../init.d/mysql
lrwxrxrwx 1 root 15 Oct 12 16:44 K15htthpd -> ../init.d/httpd
lrwxrxrwx 1 root 20 Oct 12 16:44 K15postgresql -> ../init.d/postgresql
lrwxrxrwx 1 root 13 Oct 12 16:44 K20nfs -> ../init.d/nfs
lrwxrxrwx 1 root 14 Oct 12 16:44 K24irda -> ../init.d/irda
lrwxrxrwx 1 root 15 Oct 12 16:44 K25squid -> ../init.d/squid
lrwxrxrwx 1 root 19 Oct 12 16:44 K34yppassdd -> ../init.d/named
lrwxrxrwx 1 root 17 Oct 12 16:44 K35winbind -> ../init.d/winbind
lrwxrxrwx 1 root 15 Oct 12 16:44 K44named -> ../init.d/named
lrwxrxrwx 1 root 15 Oct 12 16:44 K50snmpd -> ../init.d/snmpd
lrwxrxrwx 1 root 19 Oct 12 16:44 K50snmptrapt -> ../init.d/nmptrad
lrwxrxrwx 1 root 13 Oct 12 16:44 K50ktux -> ../init.d/tux
lrwxrxrwx 1 root 13 Oct 12 16:44 K54pxpe -> ../init.d/pxpe
lrwxrxrwx 1 root 17 Oct 12 16:44 K70aep1000 -> ../init.d/aep1000
lrwxrxrwx 1 root 14 Oct 12 16:44 K70bcm5820 -> ../init.d/bcm5820
lrwxrxrwx 1 root 14 Oct 12 16:44 K74ntptd -> ../init.d/ntptd
lrwxrxrwx 1 root 16 Oct 12 16:44 K74ypserv -> ../init.d/ypserv
lrwxrxrwx 1 root 16 Oct 12 16:44 K74pxypfrd -> ../init.d/ypfrd
lrwxrxrwx 1 root 19 Oct 12 16:44 K95firstboot -> ../init.d/firstboot
lrwxrxrwx 1 root 15 Oct 12 16:44 S05kuddu -> ../init.d/kuddu
lrwxrxrwx 1 root 18 Oct 12 16:44 S08iptables -> ../init.d/iptables
lrwxrxrwx 1 root 14 Oct 12 16:44 S09isdnd -> ../init.d/isdnd
lrwxrxrwx 1 root 17 Oct 12 16:44 S10network -> ../init.d/network
lrwxrxrwx 1 root 16 Oct 12 16:44 S12syslog -> ../init.d/syslog
lrwxrxrwx 1 root 17 Oct 12 16:44 S13portmap -> ../init.d/portmap
lrwxrxrwx 1 root 17 Oct 12 16:44 S14hfslock -> ../init.d/nfslock
lrwxrxrwx 1 root 18 Oct 12 16:44 S17keytable -> ../init.d/keytable
lrwxrxrwx 1 root 16 Oct 12 16:44 S20random -> ../init.d/random
lrwxrxrwx 1 root 16 Oct 12 16:44 S24pcmcmia -> ../init.d/pcmcmia
```

## 24 企业级 Linux 应用开发

```
lrwxrxrwx 1 root root 15 Oct 12 16:44 S25nets -> ../init/netfs
lrwxrxrwx 1 root root 14 Oct 12 16:44 S26apmd -> ../init/apmd
lrwxrxrwx 1 root root 16 Oct 12 16:44 S28autofs -> ../init/autofs
lrwxrxrwx 1 root root 14 Oct 12 16:44 S55sshd -> ../init/sshd
lrwxrxrwx 1 root root 20 Oct 12 16:44 S56rawdevices -> ../init/rawdevices
lrwxrxrwx 1 root root 16 Oct 12 16:44 S56xinetd -> ../init/xinetd
lrwxrxrwx 1 root root 13 Oct 12 16:44 S60lpd -> ../init/lpd
lrwxrxrwx 1 root root 18 Oct 12 16:44 S80sendmail -> ../init/sendmail
lrwxrxrwx 1 root root 15 Oct 12 16:44 S85gpm -> ../init/gpm
lrwxrxrwx 1 root root 13 Oct 12 16:44 S90crond -> ../init/crond
lrwxrxrwx 1 root root 15 Oct 12 16:44 S90xfs -> ../init/xfs
lrwxrxrwx 1 root root 17 Oct 12 16:44 S95anron -> ../init/anron
lrwxrxrwx 1 root root 13 Oct 12 16:44 S95atd -> ../init/atd
lrwxrxrwx 1 root root 15 Oct 12 16:44 S97rhns -> ../init/rhns
lrwxrxrwx 1 root root 11 Oct 12 16:44 S99local -> ../init/local
```

该链接建立的脚本。字母 `K` 表示由该链接标识的进程被杀死（或停止），字母 `S` 表示应该启动该进程。两位数字整数表示执行脚本的顺序（无论是启动还是停止），`00` 为优先级最高，`99` 为优先级最低。列表 2.1 显示了 Red Linux 8.0/9.0 系统第 5 层定义的典型链接列表。
