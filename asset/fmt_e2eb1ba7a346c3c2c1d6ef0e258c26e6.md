
第三，如果 `pam_rhosts_auth.so` 验证了用户身份，PAM 会立即向 rlogin 返回成功，而不进行任何密码检查。如果 `pam_rhosts_auth.so` 无法验证用户身份，则该失败的验证将被忽略。

最后（如果 `pam_rhosts_auth.so` 未能验证用户身份），则执行常规的 unix 密码验证。

### 10.4.4 默认条目

当安装包含使用 PAM 的应用程序的软件包时，它们会自动向 `/etc/pam.d` 添加条目。只要可能，它们不指定使用哪些模块——它们只是复制 `/etc/pam.conf` 顶部附近 DEFAULT 条目中放入的内容。通过更改该条目，你可以更改大多数应用程序使用的默认条目。如果你这样做，在添加新的 PAM 感知应用程序后，你需要检查 `/etc/pam.conf`，以确保添加的条目符合你的系统。

### 10.4.5 影子密码

默认的 `pam_unix.*.so` 模块可以支持影子密码。为了将系统转换为影子密码，请使用以下命令：

```
cd /etc
pwconv
chmod 600 passwd- shadow-
```

`pam_unix.*.so` 模块将自动检测你正在使用影子密码并进行所有必要的调整。

### 10.4.6 更多信息

这仅仅是 PAM 的介绍。系统中 `/usr/doc` 包含更多信息，格式包括文本、HTML 和 PostScript，包括*系统管理员指南*、*模块编写者手册*、*应用程序开发人员手册*以及 PAM 标准 DCE-RFC 86.0。此外，文档可从 Red Hat 网站获取，网址为 http://www.redhat.com/linux-info/pam/

## 10.5 启动过程、Init 和关闭

### 10.5.1 System V Init

本节简要描述启动过程的内部机制。它主要详细说明了机器如何使用 SysV Init 启动，以及它与旧版 Linux 发行版中使用的原始 init 之间的区别。

Init 是内核在启动时运行的程序。它负责启动启动时需要运行的所有常规进程。这些包括允许你登录的 gettys、NFS 守护进程、FTP 守护进程，以及你希望在机器启动时运行的任何其他内容。

SysV Init 正在迅速成为 Linux 世界中控制启动时软件启动的标准。这是因为它比传统的 BSD init 更易使用，且更强大、更灵活。

SysV init 还与 BSD init 不同，其配置文件位于 `/etc` 的子目录中，而不是直接位于 `/etc` 中。该目录名为 `rc.d`。在其中你可以找到 `rc.sysinit` 以及以下目录：

- `init.d`
- `rc0.d`
- `rc1.d`
- `rc2.d`
- `rc3.d`
- `rc4.d`
- `rc5.d`
- `rc6.d`

`init.d` 包含大量脚本。基本上，对于你可能需要启动的每个服务（在启动时或进入另一个运行级别时）都需要一个脚本。服务包括网络、nfs、sendmail、httpd 等内容。服务不包括那些只能运行一次然后退出（如 setserial）的内容。这类内容应放在 rc.local 或 rc.serial 中。

如果你想要 rc.local，它应该在 `/etc/rc.d` 中。大多数系统都包含一个，尽管它没做太多事情。如果你需要在启动时执行特定于串行端口的操作，也可以在 `/etc/rc.d` 中包含 rc.serial。

事件链如下：

- 内核在几个位置查找 init 并运行它找到的第一个
- init 运行 `/etc/rc.d/rc.sysinit`
- `rc.sysinit` 执行许多必要操作，然后运行 `rc.serial`（如果存在）
- init 运行默认运行级别的所有脚本。
- init 运行 `rc.local`

默认运行级别在 `/etc/inittab` 中确定。你应该在顶部附近看到类似如下的行：

```
id:3:initdefault:
```

由此，你会查看第二列并看到默认运行级别是 3，这对大多数系统来说应该是正确的。如果你想更改它，可以手动编辑 `/etc/inittab` 并更改 3。在修改 inittab 时要非常小心。如果你搞乱了，你可以通过重新启动并执行以下操作来修复：

```
LILO boot: linux single
```

这应该允许你进入单用户模式，以便你可以修复 inittab。

现在，它是如何运行所有正确的脚本的？如果你在 `rc3.d` 上执行 `ls -l`，可能会看到类似以下内容：

```
lrwxrwxrwx 1 root root 17 13:11 S10network -> ../init.d/network
lrwxrwxrwx 1 root root 16 13:11 S30syslog -> ../init.d/syslog
lrwxrwxrwx 1 root root 14 13:32 S40con -> ../init.d/con
lrwxrwxrwx 1 root root 14 13:11 S50net -> ../init.d/net
lrwxrwxrwx 1 root root 13 13:11 S60nfs -> ../init.d/nfs
lrwxrwxrwx 1 root root 15 13:11 S70lpd -> ../init.d/lpd.init
lrwxrwxrwx 1 root root 11 13:11 S91local -> ../rc.local
```

你会发现该目录中没有实际的“文件”。那里的一切都是指向 init.d 目录中某个脚本的链接。链接的开头还有“S”和一个数字。“S”意味着启动该特定脚本，“K”意味着停止它。数字的存在仅仅是为了排序。Init 将按出现顺序启动所有服务。你可以重复数字，但这只会让你有些困惑。你只需要使用两位数字，加上一个大写的“S”或“K”来启动或停止你需要的服务。

init 如何启动和停止服务？很简单。每个脚本都编写为接受一个参数，可以是“start”和“stop”。你实际上可以用如下命令手动执行这些脚本：

```
/etc/rc.d/init.d/httpd init stop
```

以停止 httpd 服务器。Init 只是读取名称，如果它有“K”，就调用脚本并传入“stop”参数。如果它有“S”，就调用脚本并传入“start”参数。为什么要所有这些运行级别？有些人想要一种简单的方式来设置机器以使其具有多功能性。我可能有一个“server”运行级别，只运行 httpd、sendmail、网络等。然后我可能有一个“user”运行级别，运行 xdm、网络等。

### 10.5.2 Init 运行级别

通常，Red Hat Linux 在运行级别 3 下运行——完整的多用户模式。Red Hat Linux 使用以下运行级别：

- 0 停机。
- 1 单用户模式。
- 2 多用户模式，无 NFS。

### 10.5.2 进入单用户模式引导

- 完全多用户模式。
- 重启。

如果你的机器进入了一种由于 `/etc/inittab` 损坏而无法引导的状态，或者因为 `/etc/passwd` 损坏或你忘记了密码而无法登录，请在 LILO 引导提示符处输入 `linux 1` 以进入单用户模式。此时会启动一个非常精简的系统，并给你一个 shell，你可以通过它来修复问题。

### 10.5.3 关闭系统

要关闭 Red Hat Linux，请执行 `shutdown` 命令。你可以阅读 `shutdown` 的手册页以获取完整细节，但最常见的两种用法是：

```
shutdown -h now
shutdown -r now
```

两者都能干净地关闭系统。在所有服务停止后，第一条命令将停止机器，第二条命令将重启机器。

为了避免对文件系统造成损坏，请直接避免运行 `reboot` 或 `halt` 命令。

## 10.6 救援模式

当系统出现问题时，有几种方法可以进行修复。然而，这要求你充分了解你的系统。本手册无法教你该做什么，但我们将介绍如何使用我们的产品进入救援模式，在那里你可以利用自己的知识来拯救系统。

### 10.6.1 通过 LILO

如果系统能够引导，但在完成引导后不允许你登录，你可以使用 `single` 或 `emergency` 引导选项。在 LILO 引导提示符处，输入 `linux single` 以单用户模式引导。在单用户模式下，你的本地文件系统将被挂载，但你的网络不会被激活。在紧急模式下，几乎没有任何设置。只有根文件系统会被挂载，并且它是只读挂载的。

### 10.6.2 紧急启动软盘

安装软盘集也可以用作救援磁盘集。当你启动引导软盘时，在引导提示符处输入 `rescue`（在非 Intel 平台上，将 `rescue` 作为选项添加到你正在引导的内核中，例如 `linux rescue`），安装过程会问几个问题，要求你插入第二张磁盘，并在 VC 1 和 VC 2 上设置 shell。正在运行的 shell 是 `ash`，一个没有历史记录或命令行编辑功能的最小 bourne shell。
