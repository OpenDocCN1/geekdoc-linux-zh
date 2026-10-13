
init 进程执行 `/sbin/rc<n>` 脚本，这些脚本反过来执行位于 `/etc` 目录中的一系列其他脚本。对于 `/sbin` 目录中的每个 rc 脚本，相应的目录名为 `/etc/rc<n>.d`，其中包含用于该运行级别执行各种操作的脚本。例如，`/etc/rc2.d` 包含用于启动和停止运行级别 2 进程的文件。在启动时，rc 脚本按数字顺序运行，直到达到默认运行级别；例如，要达到运行级别 3，将运行 `/sbin/rc1`、`/sbin/rc2` 和 `/sbin/rc3`。

所有运行控制脚本也位于 `/etc/init.d` 目录中。这些文件链接到 `/etc/rc<n>.d` 目录中的相应运行控制脚本。

以下是安装操作系统时放置在 `/etc/rc2.d` 中的默认脚本列表。如后所述，系统管理员将向此目录添加自定义脚本：

```
ls /etc/rc2.d
K06mipagent
K07dmi
K07snmpdx
K16apache
K28nfs.server
README
S01MOUNTFSYS
S05RMTTMPFILES
S10lu
S20syssetup
S21perf
S30sysid.net
S40llc2
S47asppp
S69inet
S70uucp
S71ldap.client
S71rpc
S71sysid.sys
S72autoinstall
S72inetsvc
S72slpd
S73cachefs.daemon
S73nfs.client
S74autofs
S74syslog
```

尽管脚本在每个目录中显示为文件，但 `rc<n>.d` 目录包含指向 `/etc/init.d` 目录的硬链接。在其他 UNIX 系统上，启动脚本有时可以在 `/sbin/rc<n>.d` 和 `/etc/rc<n>.d` 目录中找到。Solaris 中放置了链接，以便习惯于其他类型的 UNIX（HP-UX、SunOS 等）的用户可以轻松找到启动文件。此外，他们可能移植的引用这些启动文件的任何脚本都可以在不修改的情况下兼容。此外，通过将所有脚本放在一个位置 `/etc/init.d`，可以方便地找到启动或停止特定功能所需的脚本，而无需搜索所有 `/etc/rc<n>.d` 目录。

- `S74xntpd`
- `S75cron`
- `S75savecore`
- `S76nscd`
- `S80lp`
- `S80PRESERVE`
- `S80spc`
- `S85power`
- `S88sendmail`
- `S88utmpd`
- `S89bdconfig`
- `S90wbem`
- `S92volmgt`
- `S93cacheos.finish`
- `S94ncalogd`
- `S95lvm.sync`
- `S96ab2mgr`
- `S99audit`
- `S99dtlogin`

`/etc/rc<n>.d` 脚本始终按 ASCII 排序顺序运行。第一个字母（S 或 K）后面的数字指定脚本运行的顺序，可以是任何数值。数字后面的名称与运行顺序无关。脚本的名称形式如下：

```
[K,S][#][A-Z]
```

以 K 开头的文件用于终止系统进程。以 S 开头的文件用于启动系统进程。每个运行控制级别脚本的操作总结如下：

### `/sbin/rc0`
脚本运行 `/etc/rc0.d` 脚本，执行以下操作：
- 停止系统服务和守护进程
- 终止所有正在运行的进程
- 卸载所有文件系统

### `/sbin/rcS`
脚本运行 `/etc/rcS.d` 脚本以将系统提升到单用户模式并执行以下操作：
- 建立最小网络
- 如有必要，挂载 `/usr`
- 设置系统名称
- 检查 `/` 和 `/usr` 文件系统
- 挂载伪文件系统（`/proc` 和 `/dev/fd`）
- 重建设备条目（用于重新配置启动）
- 检查并挂载在单用户模式下需要挂载的其他文件系统

运行级别 init S 与运行级别 1 相似，只是所有文件系统都会被挂载并且可访问。

### `/sbin/rc1`
脚本运行 `/etc/rc1.d` 脚本并执行以下操作：
- 停止系统服务和守护进程，除了最基本的 OS 服务
- 使所有文件系统可用，并允许已登录的任何用户保持登录状态
- 将系统以单用户模式启动

> TIP
> 使用 init S 运行级别执行系统管理任务，以确保其他用户无法登录并访问系统。

### `/sbin/rc2`
脚本设置 `TIMEZONE` 变量，运行 `/etc/rc2.d` 脚本，并执行以下操作：
- 挂载所有文件系统
- 如果至少有一个文件系统使用 quota 选项挂载，则启用磁盘配额
- 将编辑器临时文件保存到 `/usr/preserve`
- 删除 `/tmp` 目录中的任何文件
- 配置系统记账
- 配置默认路由器
- 设置 NIS 域
- 设置 ifconfig 网络掩码
- 如果 `/.PREINSTALL` 或 `/AUTOINSTALL` 存在，则从安装介质或启动服务器重新启动系统
- 如适用，启动 `inetd`、`rpcbind` 和 `named`
- 启动 Kerberos 客户端守护进程（`kerbd`）
- 如适用，启动 NIS 守护进程（`ypbind`）和 NIS+ 守护进程（`rpc.nisd`）
- 启动 `keyserv`
- 启动 `statd`、`lockd`、`xntpd`、`vold` 和 `utmpd`
- 挂载所有 NFS 条目
- 启动 `automount`
- 启动 `cron`
- 启动 `lp` 守护进程
- 启动 `sendmail` 守护进程

### `/sbin/rc3`
脚本运行 `/etc/rc3.d` 脚本并执行以下操作：
- 清理 `sharetab`
- 启动 `nfsd`
- 启动 `mountd`
- 如果是启动服务器，则启动 `rarpd`、`rpld` 和 `rpc.bootparamd`

### `/sbin/rc5` 和 `/sbin/rc6`
脚本运行 `/etc/rc0.d` 脚本并执行以下操作：
- 终止所有活动进程
- 卸载所有文件系统

## 使用运行控制脚本停止或启动服务

每个运行级别都有单独脚本的优点是，您可以在不重新启动或更改 init 状态的情况下单独运行这些脚本来关闭 Solaris 中的进程。

例如，您可以通过键入 `/etc/init.d/nfs.server stop` 并按 Enter 来关闭 NFS 服务器功能。在更改系统配置后，您可以通过键入 `/etc/init.d/nfs.server start` 并按 Enter 来重新启动该功能。

使用 `pgrep` 命令验证服务是否已停止或启动：

```
pgrep -f <service>
```

`pgrep` 实用程序检查系统上的活动进程并报告进程的进程 ID。有关此命令的详细信息，请参阅第 9 章“进程控制”。

## 向运行控制目录添加脚本

如果添加脚本，请将其放入 `/etc/init.d` 目录，并创建指向适当的 `rc<n>.d` 目录的链接。为新脚本分配适当的编号和名称，以便按正确顺序运行。

### 1.2 添加运行控制脚本

1. 成为超级用户。
2. 将脚本添加到 `/etc/init.d` 目录：

   ```
   # cp <filename> /etc/init.d
   # chmod 0744 /etc/init.d/<filename>
   # chown root:sys /etc/init.d/<filename>
   ```
3. 创建指向适当的 `rc<n>.d` 目录的链接：

   ```
   # cd /etc/init.d
   # ln <filename> /etc/rc2.d/S<nn>filename
   # ln <filename> /etc/rc<n>.d/K<nn>filename
   ```
4. 使用 `ls` 命令验证脚本是否在指定目录中具有链接：

   ```
   # ls -l /etc/init.d/ /etc/rc2.d/ /etc/rc<n>.d/
   ```

以下示例创建一个名为“program”的 rc 脚本，该脚本将在运行级别 2 启动，并在运行级别 0 停止：

```
# cp program /etc/init.d
# cd /etc/init.d
# ln /etc/init.d/program /etc/rc2.d/S100program
# ln /etc/init.d/program /etc/rc0.d/K100program
# ls -l /etc/init.d /etc/rc2.d /etc/rc0.d
```

continued

系统将显示以下内容：

```
/etc/init.d:
total 250
-rwxr--r-- 3 root sys 171 Jan 5 2000 ANNOUNCE
-rwxr--r-- 3 root sys 1881 Jan 5 2000 MOUNTFSYS
-rwxr--r-- 2 root sys 256 Jan 5 2000 PRESERVE
-rw-r--r-- 1 root sys 681 Jan 5 2000 README
-rwxr--r-- 2 root sys 2004 Jan 5 2000 RMTMPFILES
-rwxr--r-- 1 root sys 833 Jan 5 2000 acct
-rwxr--r-- 1 root sys 392 Mar 16 2000 acctadm
```
