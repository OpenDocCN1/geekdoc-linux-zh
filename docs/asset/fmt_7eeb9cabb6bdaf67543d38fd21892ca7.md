
Adore rootkit 是一组 Linux 内核模块，可让入侵者隐藏进程、文件和网络设备详细信息。它还包含一个 root shell 后门。Adore 可从 http://www.team-teso.net/releases.php 获取。

## Linux Rootkit (LRK)

最流行的 Linux rootkit——LRK 包含许多常见命令的特洛伊化二进制文件，包括但不限于：`chfn`, `chsh`, `crontab`, `du`, `find`, `ifconfig`, `inetd`, `killall`, `login`, `ls`, `netstat`, `passwd`, `pidof`, `ps`, `rshd`, `syslogd`, `tcpd`, `top`, `sshd` 和 `su`。它还包含嗅探器以及 root shell 后门。LRK 可从 http://www.packetstormsecurity.org/ 获取。

## Tornkit

Tornkit 由各种特洛伊二进制文件、嗅探工具以及自动禁用 `syslogd` 和其他关键服务的工具组成。可从 http://www.packetstormsecurity.org/ 下载。

## Knark

Knark 是一种可以隐藏文件和进程的 rootkit，并且还具有重定向命令的能力。它包含一个可用于远程执行命令的后门。Knark 可从 http://www.packetstormsecurity.org/ 获取。

## 检测 Rootkits

可以使用以下工具来检测 rootkits 和特洛伊木马：

- `Chkrootkit` 可用于检查系统上的 rootkits。可从 http://www.chkrootkit.org/ 获取。
- 使用 `Tripwire` 或 `Samhain` 来检测修改后的二进制文件。有关 `Tripwire` 的更多详细信息，请参见 http://www.tripwire.com/。有关 `Samhain` 的信息可在 http://samhain.sourceforge.net/ 获取。

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_181_0.png)

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_181_1.png)

### 总结

从清理日志文件到安装后门和 rootkits，本章描述的众多技术列举了入侵者采用的各种方法，以隐藏其踪迹并确保对受害主机持续的 root 访问权限。正如讨论的主题所示，检测高级黑客的存在通常相当困难。因此，虽然本章结束了攻击方法论的内容，但强烈建议您考虑本书第二部分中的建议，以对主机的策略和配置进行加固。

# 第二部分

## 主机加固

- 第 7 章 默认设置和服务
- 第 8 章 用户和文件系统权限
- 第 9 章 日志记录和补丁管理

此页有意留空

## 第 7 章

### 默认设置和服务

**本章内容：**

- 设置密码策略
- 删除或禁用不必要的账户
- 从 PATH 变量中移除 `~`
- 检查 `/etc/hosts.equiv` 的内容
- 查找 `.rhosts` 文件
- 禁用栈执行
- 使用 TCP Wrappers
- 加固 inetd 和 xinetd 配置
- 加固远程服务
- 总结

大多数 Unix 和 Linux 发行版的默认安装为加固各种策略、应用程序和服务留下了改进空间。本章提供了有关如何加固主机及其常用服务的技巧。

#### 设置密码策略

入侵者经常利用薄弱的密码策略来获取用户账户的访问权限。为了加固密码策略，可以采取以下步骤：

- 确保使用影子密码（shadowed passwords）。检查确保 `/etc/passwd` 文件中没有密码哈希值。密码哈希值应仅存在于 `/etc/shadow` 中，并且该文件必须仅可由 root 读取。
- 编辑 passwd 配置文件（`/etc/default/passwd`）或使用 `chage` 实用程序更改密码过期时间长度。

#### 删除或禁用不必要的账户

检查 `/etc/passwd` 以查看主机上启用的账户。许多服务在运行期间会创建非特权账户，例如：`ftp`, `lp`, `news`, `gopher`, `ntp`。确保通过将它们的 shell 设置为 `/bin/false` 来禁用此类账户。如果这些账户对应的服务未被使用，请卸载它们并删除账户。

#### 从 PATH 变量中移除 ""

当用户执行命令时，命令 shell 会在 PATH 环境变量包含的目录列表中搜索命令的位置。为防止执行恶意用户放置在文件系统上的特洛伊木马，请确保 PATH 环境变量永不包含当前目录（`"./"`）。

检查 `/etc/rc.local`、`/etc/profile`、`/etc/bashrc`、`/etc/csh.cshrc`、`~/.bashrc`、`~/.bash_profile`、`~/.cshrc` 和 `~/login` 等文件，以确保 PATH 变量不包含 `""`。如果您使用的不是 bash shell，请检查相应的资源文件。

使用 `echo` 打印当前用户 PATH 变量的值：

```bash
echo $PATH
```

#### 检查 /etc/hosts.equiv 的内容

`/etc/hosts.equiv` 文件包含一个被认为受信任的主机名和用户列表。`rlogin`、`rsh`、`rcp` 和 `rcpd` 等服务使用此文件来确定受信任的实体。请检查此文件，确保其中仅存在受信任的主机名和用户。如果不需要信任任何远程主机或用户，建议删除此文件。

#### 检查 .rhosts 文件

检查文件系统中是否存在 `.rhosts` 文件。该文件中包含的主机名和用户名允许通过 `rlogin` 等 r-服务登录，而无需指定密码。使用 `find` 命令检查 `.rhosts` 文件：

```bash
find / -name .rhosts -type f -print 2> /dev/null
```

#### 禁用堆栈执行

禁用堆栈执行可以防止某些类型的缓冲区溢出情况。如果使用 Solaris，请编辑 `/etc/system` 并添加以下行：

```
set noexec_user_stack=1
set noexec_usr_stack_log=1
```

对于非 Solaris 发行版，可以使用以下产品：

- `StackGuard`: http://www.immunix.org/stackguard.html
- `Libsafe`: http://www.research.ayavalabs.com/project/libsafe/
- `StackGhost`: http://stackghost.cerias.purdue.edu/
- `Openwall`: http://www.openwall.com/linux

#### 使用 TCP WRAPPERS

TCP Wrappers 允许监控和过滤针对网络服务的传入请求。大多数发行版默认安装 TCP Wrappers，但如果您需要它，可以从 `ftp://ftp.porcupine.org/pub/security/index.html` 获取。

在安装了 TCP Wrappers 的主机上，编辑 `/etc/hosts.allow`，并确保以下行是第一个未注释的语句：

```
ALL::ALL:deny
```

同时，确保默认拒绝来自所有主机的连接。可以通过在 `/etc/hosts.deny` 中放置以下条目来实现：

```
all:all
```

通过在 `/etc/hosts.allow` 中放置适当的条目，仅允许受信任的主机连接到服务。请参阅 `http://www.cert.org/security-improvement/implementations//041.07.html` 获取详细说明。

#### 加固 inetd 和 xinetd 配置

互联网服务守护进程 `inetd` 用于启动提供网络服务的守护进程。它监听所有必需的端口，并在传入网络连接到达时立即启动相应的守护进程。因此，`inetd` 常被称为“超级服务器”。`xinetd` 守护进程与 `inetd` 类似，但它包含更多的功能，因此 `inetd` 用户应强烈考虑升级到 `xinetd`。

##### 禁用不必要的服务

如果使用 `inetd`，请编辑 `inetd.conf` 文件，确保不必要的服务已禁用。例如，考虑 `inetd.conf` 中负责 FTP 守护程序的以下行：

```
ftp stream tcp nowait root /usr/local/etc/tcpd /usr/local/etc/ftpd
```

要从 `inetd` 禁用 FTP，请在该行前添加 #：

```
#ftp stream tcp nowait root /usr/local/etc/tcpd /usr/local/etc/ftpd
```

重新启动 `inetd` 以使更改生效：

```
killall -HUP inetd
```

如果使用 `xinetd`，请编辑 `xinetd.d` 目录中相应的服务文件，并确保存在 `disable=yes` 行。
