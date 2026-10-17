
# 目录

`passwd.compat`、`group_compat` 和 `shadow_compat` 仅由 `glibc` 2.x 支持。如果 `/etc/sswitch.conf` 中某些 `shadow` 规则，`glibc` 将使用 `passwd` 规则进行查找。如前所述，`glibc` 还有一些查找模块。有关更多信息，请参阅 `glibc` 文档。

# 7 设置 NIS+ 需要什么？

## 7.1 软件

Linux NIS+ 客户端代码是为 GNU C 库 2 开发的。还有一个针对 Linux5 的移植版本，因为所有商业应用程序都链接到此库，而你无法重新编译它们以使用 `glibc`。`libc5` + NIS+ 存在问题。你无法与之链接静态程序，且使用此库编译的程序无法与其他 `libc5` 版本配合。

你需要获取并收集最新的 GNU C 库 2 快照。并且你需要一个基于 `glibc` 的系统，如 RedHat 5.0 或 Debian。但请注意：这些都是测试版软件！阅读关于 `glibc` 快照的文档以及发行版的说明！`glibc` 2.0.x 不包含 NIS+ 支持，且永远不会包含。第一个包含 NIS+ 支持的版本将是 2.1。

可以从以下获取 NIS+ 客户端软件：

| 站点 | 目录 |
|---|---|
| `ftp.kernel.org` | `/pub/software/libs libc-*, glibc-crypt*, glibc-linuxthreads-*` |
| `ftp.kernel.org` | `/pub/linux/utils/net/NIS+ nis-threads-1.4.tar.gz` |
| `ftp.kernel.org` | `/pub/linux/utils/net/NIS+ pam_keylogin-1.1.tar.gz` |

基于 `glibc` 的发行版可以从中获取：

| 站点 | 目录 |
|---|---|
| `ftp.redhat.com` | `/pub/redhaft/mustang` |
| `ftp.debian.org` | `/pub/debian/hamm` |

编译 GNU C 库，请遵循软件附带的说明。在这里你可以找到基于 NYS 和 `glibc` 源码的补丁 `libc5`，可直接替换标准 `libc5`：

| 站点 | 目录 | 文件名 |
|---|---|---|
| `ftp-kernel.org` | `/pub/linux/utils/net/NIS+` | `libc-5.4.38-nisnisl-0.4.6.tar.gz` |

你还应该查看 `http://www-vt.uni-paderborn.de/~kukuk/linux/nisplus.html` 获取更多信息和最新源码。

## 7.2 设置 NIS+ 客户端

**重要**：设置 NIS+ 客户端时，请阅读你的 Solaris NIS+ 文档了解服务器端需要的操作！本文档仅描述客户端端需要的操作！

在安装新的 `libc` 和 `nis-tools` 后，在 NIS+ 服务器上为新客户端创建凭据。然后运行

```
hostname nisplus.domain.

nisinit c -H <NIS+ server>
```

以初始化冷启动文件（Cold Start File）。更多选项请阅读 `nisman` 页面。确保主机名在重启后始终能被设置。如果你不知道网络上的 NIS+ 域名，请询问你的系统/网络管理员。

现在你应该更改你的 `/etc/nsswitch.conf` 文件。确保 `pubkey` 之后的服务只有 `nisplus` (`pubkey: nisplus`) 而没有其他！之后，启动 `keysyserv` 并确保它在启动时总是运行。运行

```
keylogin -r
```

在你的系统上存储 root secret。`niscat passwd.dir` 现在应该显示 `passwd` 数据库中的所有条目。

## 7.3 NIS+、keylogin 和 PAM

当用户登录时，他需要将 secret 设置为 `keysys`。这是通过调用 `"keylogin"` 完成的。`shadow` 包将执行此操作。对于 PAM 登录，你必须安装 `keylogin-1.1.tar.gz` 并更改 `/etc/pam.d/login` 文件使用 `pam_unix_auth`，而不是不支持 NIS 的 `pwdb`。

```
#PAM-1.0

auth required /lib/security/securetty.so

auth required /lib/security/pam_keylogin.so

auth required /lib/security/pam_unix_auth.so

auth required /lib/security/pam_unix_nlogin.so

account required /lib/security/pam_unix_acct.so

password required /lib/security/pam_unix_passwd.so

session required /lib/security/pam_unix_session.so
```

## 7.4 nsswitch.conf 文件

网络服务切换文件 `nsswitch.conf` 决定了请求信息时的查找顺序，就像 `host.conf` 决定查找方式一样。例如，行

```
hosts: files nisplus dns
```

指定主机查找首先在本地 `/etc/hosts`，然后是 NIS+ 查找，最后是域名 (`/etc/resol.conf`)，`nsswitch.conf` 的第一个版本可以在 `http://www-vt.uni-paderborn.de/kukuk/linux/misc.html` 找到。适用于 NIS+ 的良好 `nsswitch.conf` 文件如下：

```
# /etc/nsswitch.conf

# 示例服务文件。此文件应该将最常用的服务排在开头。

# 条目意味着如果查找为空则停止。注意如果由于其他原因

#（例如没有 NIS 服务器响应）则继续查找下一个条目。

# 有效条目有：

nisplus                  使用 NIS+ (NIS 版本3)

nis                      使用 NIS (NIS 版本2)，也称为 YP

dns                      使用 DNS (域名服务)

files                    使用本地文件

db                       使用 /var/db 数据库

如果未找到则停止

passwd:                 compat

# 用于 libc5: passwd: nisplus

group:                   compat

# 用于 libc5: group: nisplus

shadow:                  compat

# 用于 libc5: shadow: nisplus

passwd_compat: nisplus

group_compat: nisplus

shadow_compat: nisplus

hosts: nisplus

services: nisplus

networks: nisplus

protocols: nisplus

rpc: nisplus

ethers: nisplus

netmasks: nisplus

netgroup: nisplus

bootstraps: nisplus

publickey: nisplus

automount: files

alias: nisplus
```

# 8 设置 NIS

## 8.1 服务器程序 ypserv

本文档仅描述如何设置 `"ypserv"` 服务器。NIS 服务器软件可以在此处找到：

| 站点 | 目录 | 文件名 |
|---|---|---|
| `ftp.kernel.org` | `/pub/linux/utils/net/NIS` | `ypserv-1.2.8.tar.gz` |
| `waag.eros.com` | `/pub/net/nis` | `ypserv-1.2.8.tar.gz` |

你也可以查看 `http://www-vt.uni-paderborn.de/kukuk/linux/nis.html` 获取更多信息和最新源码。传统 NIS 和 NIS 的服务器设置是相同的。编译软件生成 `"ypserv"` 和 `"makedbm"` 程序。如果你作为主节点运行服务器，确定哪些文件需要通过 NIS 可，并在 `/var/yp/Makefile` 中添加或删除相应的条目。现在编辑 `/var/yp/security` 和 `/etc/ypserv.conf`。有关更多信息，请阅读 `ypserv(8)` 和 `ypserv.conf(5)` 手页。确保 `portmapper` (`portmap(8)`) 正在运行，并启动服务器命令 `"ypserv"`

```
% rpinfo -u localhost ypserv
```
