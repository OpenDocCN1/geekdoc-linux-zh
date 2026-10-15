
```bash
# cd /usr/src
# wget \
http://www.lids.org/download/v2.6/2.6.7/lids-2.2.0rc3-2.6.7.tar.gz
# tar -zxvf lids-2.2.0rc3-2.6.7.tar.gz
# cd linux-2.6.7
# patch -p1 < \
/src/lids-2.2.0rc3-2.6.7/2.2.0rc3-2.6.7.patch
```

接下来配置内核。LIDS 要求启用 `SHA256` 摘要算法：你可以在“密码学选项”（`Cryptography Options`）菜单下的“密码学 API”（`Cryptography API`）中找到此选项。LIDS 配置选项位于“安全选项”（`Security Options`）菜单下。在本书期间，LIDS 与其他 `LSM` 模块兼容，因此确保没有选择其他模块（如 `SELinux` 和 `Capabilities`）。可用的 LIDS 配置选项有：

- **尝试防止日志泛滥 (`CONFIG_LIDS_NO_FLOOD_LOG`)：** 这限制了相同消息记录的速率。
- **允许切换 LFS 和状态 (`CONFIG_LIDS_ALLOW_SWITCH`)：** LFS（LIDS 自由会话，我们稍后会讨论）允许管理员执行不受 LIDS 限制的命令；这非常有用，但也是一个可能的攻击点。我们建议在实验 LIDS 时启用此选项，但在生产服务器上可能需要考虑禁用它。请忽略此选项的帮助菜单，它说明必须通过 `lidsam` 命令设置密码——这些信息已经过时。
- **允许关闭 Linux 自由会话 (`CONFIG_LIDS_ALLOW_LFS`)：** 这允许在系统运行时关闭 LIDS。同样这是一个潜在的安全弱点，但在开始使用 LIDS 时很有用。
- **将模式切换限制到指定的终端 (`CONFIG_LIDS_RESTRICT_MODE_SWITCH`)：** 此选项限制了可以启动 LFS 的终端。可以选择的三类终端是控制台（`console`）、串口控制台（`serial console`）和 `PTY`。第三种最危险，因为它可能允许远程攻击者进入 LFS。我们建议只启用第一种，将 LFS 限制为物理坐在机器前的用户。

## Lidools

编译内核后，可以安装 `lidtools` 包。除非你的启用了 LIDS 的内核位于 `/usr/src/linux`，否则你需要在 `configure` 时指定其位置，如下：

```bash
$ tar -zvxf lidtools-2.2.5rc1.tar.gz
$ cd lidtools-2.2.5rc1.tar.gz
$ ./configure KERNEL_DIR=/usr/src/linux-2.6.7
$ su
$ make install
```

安装结束时，系统将提示你输入 LIDS 管理员密码：此密码不应与你的 `root` 密码相同。你现在可以重启系统到新内核。如果你在任何时候想在关闭 LIDS 的情况下启动启用了 LIDS 的内核，可以在启动时传递 `security=0` 参数。

## LIDS 管理

现在我们已经查看了如何在内核中配置 LIDS，让我们转向用户态的配置。通过 `Grsecurity`，LIDS 使用 `ACL` 来控制文件和进程与系统的交互，但它还提供了其他有用功能，如内核密封（`kernel sealing`）和 `LFS`。

## 密封内核

内核模块非常有用，允许根据需要将代码加载到内核中，但正如你在第 2 章中看到的，恶意内核模块是入侵者维持访问权限的一种流行且极难检测的方法。在内核中禁用模块支持是一种解决方案，但这相当不利；遗憾的是，它可以被绕过。LIDS 使用“密封”的概念来保护内核免受此类攻击。当使用 `lidsadm -I` 命令密封内核时，不能再从内核中加载或卸载模块。通过将此命令放在系统启动脚本的末尾（通常是 `rc.local`），你可以确保在内核密封之前所有所需的模块已加载。请注意，密封并不能完全消除恶意内核的威胁：拥有 `root` 权限的入侵者可以轻易修改启动脚本，在内核密封之前加载他的模块，然后重启系统。密封内核还强制执行能力边界集（`capabilities bounding set`），我们稍后会查看。

## LIDS 自由会话

LIDS 自由会话（`LFS`）仅仅在一个不强制执行 LIDS 的 `shell` 中，允许用户执行在 LIDS 下通常不允许的任务。这具有潜在的危险性，因为获得 LFS 的攻击者可以绕过 LIDS 提供的整个保护；然而，这是必要的代价。对 LFS 的访问由之前设置的 `lidsadm` 密码控制。此外，内核配置可以将此类会话仅限于控制台用户 `/etc/lids`（通常这是一个好主意）。

`LFS` 的主要用途之一是为维护任务解除系统限制。例如，如果你需要更新内核或加载模块，可以使用 LFS 执行这些操作，而无需禁用整个系统的 LIDS。

## 370 Linux 网络安全

不要手动编辑此文件——而是使用我们接下来要介绍的特殊 `lidsconf` 工具：

```
0:0:1:0:1114128:834:/sbin:0-0
0:0:1:0:1933326:834:/bin:0-0
0:0:1:0:2:833:/boot:0-0
0:0:1:0:573456:834:/lib:0-0
```

如果你好奇这些神秘的数字意味着什么，LIDS 实际上是在 `inode` 上维护 `ACL`（访问控制列表），而不是文件名——例如，如果我们对 `/var/log/messages` 设置了 `APPEND` 模式，LIDS 将其在内部存储为对 `/var/log/messages` 文件所在 `inode` 的访问控制。这意味着，如果一个文件被删除并随后被重新创建（可能是因为该文件所属的软件包已升级），它的 `inode` 将发生变化，导致 `lids` 的信息将变得不同步。因此，在完成升级应用程序等管理任务后，你必须要求 LIDS 同步其 `ACL` 配置。接下来我们将看到如何实现这一点。

## lidsconf

从 2.0 版本开始，LIDS 将配置和管理分为两个独立的命令。第一个命令 `lidsadm`，我们已经讨论过了；第二个命令叫做 `lidsconf`。`lidsconf` 提供的最重要的命令有：

- `-A,--add`: 添加条目。
- `-C,--check`: 检查现有条目。
- `-D,--delete`: 删除条目。
- `-Z,--zero`: 删除所有条目。
- `-U,--update`: 更新 `/dev` 和 `inode` 编号。
- `-L,--list`: 列出所有条目。

下面的示例显示了 `lidtools` 2.2.5rcl 提供的默认 `ACL`。为了清晰起见已添加行号：

```
# lidsconf -L
Subject ACCESS inherit Object
------------------------------------------------------
1) Any file READONLY: 0           /sbin
2) Any file READONLY: 0           /bin
```

## 访问控制 371

```
3) Any file READONLY: 0 /boot
4) Any file READONLY: 0 /lib
5) Any file READONLY: 0 /usr
6) Any file READONLY: 0 /etc
7) Any file DENY: 0 /etc/lids
8) Any file DENY: 0 /etc/shadow
9) Any file APPEND: 0 /var/log
10) Any file WRITE: 0 /var/log/tmp
11) /bin/login READONLY: 0 /etc/shadow
12) /bin/login GRANT: 0 CAP_SETUID
13) /usr/sbin/sshd GRANT: 0 CAP_NET_ADMIN
14) /bin/login GRANT: 0 CAP_SETGID
```

如果多个规则适用于一个对象，则以最具体的规则胜出。这从第 6、7、8 和第 11 行中看出：第一个 `/etc` 目录被设置为 `READONLY`（只读），然而 `/etc/lids` 和 `/etc/shadow` 随后被设置为不可见（`DENY`）。由于主体是 `Any file`（任何文件），这些规则将适用于任何尝试访问的文件。在第 11 行中，`/etc/shadow` 对 `/bin/login` 设置为 `READONLY`。

在添加条目时，`-A` 选项接受以下参数：

```
lsconf -A [acl-type] [-s subject] -o object [-t from-to] \
[-i level] ACTION
```

如你所见，大多数参数都是可选的；在许多情况下，添加 `ACL` 可以简单如于：

```
lsconf -A -o /etc/hosts.conf -j READ
```
