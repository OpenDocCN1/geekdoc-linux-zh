
请注意，每个文件中行的顺序非常重要。虽然 `required` 模块的调用顺序实际上并不重要，但还有其他控制标志可用。虽然 `optional`（可选）很少使用，在 Red Hat Linux 系统上默认从不使用，但 `sufficient`（足够）和 `requisite`（必要）会导致顺序变得重要。

在登录的认证配置中：

```
auth required      /lib/security/pam_security.so
auth sufficient    /lib/security/pam_rhosts.auth.so
auth required      /lib/security/pam_pwdb.so shadow nullok
auth required      /lib/security/pam_login.so
```

看起来几乎和登录条一样，但多了一行指定额外模块的行，且模块指定的顺序不同。

首先，`pam_security.so` 防止了在不安全的终端上进行 root 登录。这实际上禁止了所有 root 登录尝试。如果你希望允许它们（在这种情况下，我们建议不要连接互联网或使用良好的防火墙），你可以简单地删除该行。

其次，`pam_nologin.so` 检查上述指定的 `/etc/nologin`。

第三，如果 `pam_rhosts.auth.so` 验证了用户，PAM 将立即返回允许登录，无需进行任何密码检查。如果 `pam_rhosts.auth.so` 未能验证用户，则该失败的认证将被忽略。

最后（如果 `pam_hosts.auth.so` 未能验证用户），`pam_pwdb.so` 模块执行正常的密码认证。

请注意，如果你不想在安全检查失败时提示密码，可以将 `pam_security.so` 模块从 `required` 改为 `requisite`。

### 11.4.4 影子密码

影子密码支持在 Red Hat Linux 5.0 中发生了巨大变化。请参考第 7 页的第 1.3.2 节获取最新信息。

`pam_pwdb.so` 模块会自动检测你正在使用影子密码并进行所有必要的调整。

### 11.4.5 更多信息

这只是对 PAM 的介绍。系统 `/usr/doc/pam*` 中包含了更多信息，包括《系统管理员指南》、《模块编写手册》、《应用程序开发者手册》以及 PAM 标准 DCE-RFC 860。此外，还可以从 Red Hat 网站获取文档，地址为 `http://www.redhat.com/linux-info/pam/`。

## 11.5 启动过程、Init 和关机

本节是对启动过程内部的简要描述。它基本上详细涵盖了使用 SysV Init 启动机器的方法，以及与旧版 Linux 版本使用的原始 init 之间的区别。

`Init` 是内核在启动时运行的程序。它负责启动所有启动时需要运行的标准进程。这些包括允许你登录的 `getty`、NFS 守护进程、FTP 守护进程以及你希望在机器启动时运行的任何程序。

SysV Init 正迅速成为 Linux 世界中控制软件启动启动的标准。这是因为比传统的 BSD init 更容易使用，且更强大、更灵活。

`init` 同样与 `BSD init` 的不同之处在于，配置文件位于 `/etc` 的子目录中，而不是直接位于 `/etc` 中。该目录被称为 `rc.d`。在里面你会找到 `rc.sysinit` 和以下目录：

```
init.d
rc0.d
rc1.d
rc2.d
rc3.d
rc4.d
rc5.d
rc6.d
```

`init.d` 包含一组脚本。基本上，对于每个可能需要在启动时或进入另一个运行级别（runlevel）时启动的服务，你都需要脚本。服务包括网络、`sendmail`、nfs、http 等。服务不包括像 `setserial` 这样必须运行一次后退出的程序。这类程序应该放在 `rc.local` 或 `rc.serial` 中。

如果你想要 `rc.local`，它应该位于 `/etc/rc.d`。大多数系统都包含一个，尽管它没做什么工作。如果你需要在启动时执行特定的串口特定操作，也可以在 `/etc/rc.d` 中包含一个 `rc.serial`。

事件链如下：

* 内核在几个地方查找 `init` 并运行找到的第一个。

* `init` 运行 `/etc/rc.d/rc.sysinit`。

* `rc.sysinit` 执行一系列必要操作，然后运行 `rc.serial`（如果存在）。

* `init` 运行默认运行级别的所有脚本。

* `init` 运行 `rc.local`。

默认运行级别在 `/etc/inittab` 中决定。你应该在顶部有类似这样的一行：

```
id:3:initdefault:
```

通过此，你可以查看第二列并看到默认运行级别为 3，这应该是大多数系统的情况。如果你想更改它，可以手动编辑 `/etc/inittab` 并更改 3。在处理 `inittab` 时要非常小心。如果你搞砸了，可以通过重启并执行来修复：

```
LILO boot:    linux single
```

这将允许进入单用户模式以修复 `inittab`。

现在，它是如何运行所有脚本的？如果你在 `rc3.d` 上输入 `ls -1`，你可能会看到类似输出：

```
lrwxrwxr-x root root 17 Jan 3:11 .../init.d/network
lrwxr-xr-x root root 17 Jan 3:11 .../init.d/syslog
lrwxrwxr-x root root 17 Jan 3:11 .../init.d/cron
lrwxrwxr-x root root 17 Jan 3:11 .../init.d/inet
lrwxrwxr-x root root 17 Jan 3:11 .../init.d/nfs
lrwxrwxr-x root root 17 Jan 3:11 .../init.d/nfs
lrwxrwxr-x root root 17 Jan 3:11 .../init.d/lpd
lrwxrwxr-x root root 17 Jan 3:11 .../init.d/local
```

## 11.6.1 通过 LILO

如果你的系统可以启动，但在完成启动后没有允许你登录，可以使用单用户或紧急启动选项。在 LILO 启动提示符处，输入 `linux single` 以单用户模式启动。在单用户模式下，本地文件系统将被挂载，且网络将不会激活。在紧急模式下，几乎没有东西会被设置。只有根文件系统会被挂载，并且为只读模式。

## 11.6.2 紧急启动软盘

安装盘也可以作为救援盘集使用。当你启动软盘时，在启动提示符处输入 `rescue`（在非 Intel 平台上，为你正在启动的内核添加 `rescue` 选项，例如 `linux rescue`），安装过程将询问你几个问题，要求你插入第二块磁盘，并在 VC 1 和 VC 2 上设置 shell。正在运行的 shell 是 `ash`，这是一种极简的 bourne shell，没有历史记录或命令行编辑功能。

`PATH` 环境变量已设置好，使得一旦你挂载了根分区 `/mnt`，如果根分区上不存在某些二进制文件，则将运行根分区中的文件。此外，如果需要，将使用 `/mnt/lib` 和 `/mnt/usr/lib` 中的库。在修复系统期间，你可能希望更改 `PATH` 以不包含 `/bin` 和 `/usr/bin`，而是保留 `/mnt/bin`、`/mnt/usr/bin` 等。如果你这样做了，你需要使用 `/bin/mount` 来卸载 `/mnt`。

在挂载 `/mnt` 之前，可用重要工具的版本：

- `mount`: `mount` 命令不要求挂载的设备节点已存在，也不要求设备的全名。除非另有说明，否则它假设为 ext2 文件系统。

```
mount /dev/sda1 /mnt -t ext2
```

功能上等同于

```
mount sda1 /mnt
```

- `ash`: 完整版本
- `cat`: 不接受任何选项

## 6 救援模式

- `mod`: `chmod` 命令不接受符号模式名称，只接受八进制模式。
- `io`: 完整版本
- `fsck`: 完整版本
- `disk`: 完整版本
- `ip`: 完整版本
- `nzip`: 完整版本
- `smod`: 完整版本
- 完整版本
- `mod`: 不接受任何选项
- `dir`: 无 GNU 长格式选项
- `e2fs`: 完整版本
- `mod`: `mod` 命令不接受符号模式名称，只接受八进制模式。
- `en`: 完整版本
- 无 GNU 长格式选项
- `mod`: 完整版本
- 到 `ash` 的软链接
