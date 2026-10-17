
或者，当你使用 `chkconfig`（第 446 页）开启或关闭服务时，它会更改相应 xinetd 配置文件中的 `disable` 参数值并通过发送信号重加载 xinetd。如果你包含 `only_from`，它指定 xinetd 允许使用服务的系统。仅使用 IP 地址是一个好主意——如果 DNS 失败，使用主机会导致服务不可用。IP 地址中的零被视为通配符。例如，`192.168.0.0` 允许来自 `192.168.0.0` 子网的任何系统的访问。

有关 xinetd 配置参数的更多信息，请查看 `inetd.conf` 手页。

# 安全服务器

保护服务器的方法有两种使用 TCP wrappers 和设置 chroot jail。本节介绍了这两种技术。或者，你可以使用 `system-config-firewall`（第 293 页）保护系统。http 等协议不受 libwrap 保护。更多信息请参阅第 458 页的“安全系统”。

## TCP wrappers：安全服务器 (hosts.allow 和 hosts.deny)

当你向从远程访问的系统开放本地系统时，请遵循这些指南：

- 仅对你想访问的系统开放本地系统。
- 允许每个远程系统访问你想访问的数据。
- 允许每个远程系统仅以适当的方式（只读、读写）访问数据。

作为客户端/服务器模型的一部分，TCP wrappers 可以用于任何链接到 `libwrap` 的守护进程，它依赖 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件作为简单访问控制列表 (ACL) 的基础。这种访问控制语言根据客户端地址和客户端尝试访问的守护进程定义了允许客户端访问本地系统守护进程的规则。`ldd` 的输出显示 sshd 的共享库依赖之一是 libwrap：

```
$ ldd /usr/bin/sshd | grep libwrap
libwrap.so.0 => /lib/libwrap.so.0 (0x0e7c00)
```

`hosts.allow` 和 `hosts.deny` 文件中的每行都有以下格式：

`daemon_list : client_list [: command]`

其中 `daemon_list` 是一个或多个服务器守护进程的逗号分隔列表（例如 `rpcbind`, `vsftpd`, `sshd`），`client_list` 是一个或多个客户端的逗号分隔列表（参见第 478 页表 11-5），可选的 `command` 是当 `client_list` 中的客户端尝试访问 `daemon_list` 中的守护进程时执行的命令。

当客户端请求连接服务器时，将按照以下顺序查询服务器系统上的 `hosts.allow` 和 `hosts.deny` 文件，直到找到匹配项：

1. 如果守护进程/客户端对匹配 `hosts.allow` 中的某行，则允许访问。
2. 如果守护进程/客户端对匹配 `hosts.deny` 中的某行，则拒绝访问。
3. 如果在 `hosts.allow` 或 `hosts.deny` 中没有匹配项，则允许访问。

第一个匹配项决定了允许客户端访问服务器。当 `hosts.allow` 和 `hosts.deny` 都不拒绝访问时，就像文件项为空一样。虽然不建议，但可以通过删除两个文件允许所有客户端访问守护进程。

## 设置服务器

示例：为了更安全的系统，请将以下行放入 `hosts.deny` 中以阻止所有访问：

```
$ cat /etc/hosts.deny
```

```
ALL : ALL : echo '%c tried to connect to %d and was blocked' >> /var/log/tcpwrappers.log
```

此行防止任何客户端连接到任何服务，除非在 `hosts.allow` 中显式允许这样做。当此规则匹配成功时，它会在名为 `/var/log/tcpwrappers.log` 的文件中添加一行。`%c` 扩展为客户端信息，`%d` 扩展为尝试连接的客户端守护进程名称。

在配置了上述 `hosts.deny` 文件的情况下，你可以在 `hosts.allow` 中包含行来显式允许访问某些服务。例如，以下 `hosts.allow` 允许任何客户端连接 OpenSSH 守护进程（ssh, scp, sftp），但仅允许来自与本地系统同一网络以及 `192.168.subnet` 用户的 telnet 连接：

```
$ cat /etc/hosts.allow
sshd: ALL
in.telnet: LOCAL
in.telnet: 192.168.* 127.0.0.1
```

第一行允许从任何系统（ALL）连接到 ssh。第二行允许从与服务器同一局域的任何系统（LOCAL）连接。第三行匹配任何 IP 地址以 192.168 开头的系统，以及本地系统。

## 设置 chroot 监狱 (JAIL)

在早期的 UNIX 变体中，根目录是文件系统中的一个固定点。在现代 UNIX 变体（包括 Linux）中，你可以基于进程定义根目录。`chroot` 工具允许你运行具有非 `/` 根目录的进程。

根目录出现在目录层次结构的最顶端且没有父目录。因此，进程无法访问根目录以上的文件，因为这些文件不存在。例如，如果你运行一个程序（process）并指定根目录为 `/home/sam/jail`，该程序将无法感知 `/home/sam` 之上的任何文件：jail 是程序的根目录，并被标记为 `/`（not jail）。

通过创建一个虚拟的根目录（通常称为 chroot jail），你可以防止程序访问、执行或可能恶意地修改从根目录开始的文件。你必须正确设置 chroot jail 以增加安全性：如果你没有正确设置 chroot jail，可能会让恶意用户更容易访问系统。

### 使用 chroot

创建一个 chroot jail 是简单的：使用 root 权限运行命令 `/usr/sbin/chroot`。该目录就变成了根目录，进程尝试运行默认 shell。使用 root 权限运行，以下命令（existing）在 `/home/sam/jail` 目录下设置了 chroot jail：

```
# /usr/bin/chroot /home/sam/jail
/bin/chroot: failed to run '/bin/bash': No such file or directory
```

此示例设置了 chroot jail，但当系统尝试运行 bash shell 时，操作失败了。一旦 jail 设置好，名为 jail 的目录接替根目录 `/`。结果是 chroot 找不到路径为 `/bin/bash` 的文件。在这种情况下，chroot jail 虽然有效但没有用。

让 chroot jail 以你想要的方式工作更为复杂。为了让前面的示例在 chroot jail 中运行 bash，请在 `/home/sam/jail/bin` 创建一个二进制目录并将 `/bin/bash` 拷贝进去。由于二进制文件动态链接到共享库，你还需要将这些库拷贝到 jail 中。库位于 lib 目录。

下一个示例创建了必要的目录，拷贝了 bash，使用 `ldd` 显示 bash 的共享库依赖，并将必要的库拷贝到 lib。`linux-gate.so` 文件是内核提供的动态共享对象（DSO）；你不需要拷贝它。

```
$ pwd
/home/sam/jail
$ mkdir bin lib
$ cp /bin/bash bin
$ ldd bin/bash
linux-gate.so => (0x009800)
libinfo.so.5 => /lib/libinfo.so.5 (0x076b00)
libinfo.so.2 => /lib/libinfo.so.2 (0x076b00)
libc.so.6 => /lib/libc.so.6 (0x011000)
linux-gate.so.2 => /lib/linux-gate.so.2 (0x092300)
```

```
$ cp /lib/{libinfo.so.5,libinfo.so.2,libc.so.6,linux-gate.so.2} lib
```

现在启动 chroot jail。设置工作由普通用户完成，但必须使用 root 权限运行 chroot：

```
$ su
Password:
# /usr/bin/chroot /home/sam/jail /bin/bash
# pwd
/
# ls
bash: command not found
```

这一次 chroot 找到了并启动了 bash，显示了默认的提示符（prompt）。`pwd` 命令有效是因为它是内置命令。然而，bash 无法找到 ls 工具，因为它不在 chroot jail 中。如果你想让 jail 中的用户使用 ls，可以将 `/bin/ls` 及其库拷贝到 jail 中。`exit` 命令允许你退出 jail。

如果你为 chroot 提供第二个参数，它会将该参数作为在 jail 内运行的程序名称。以下命令与前面的一个等效：
