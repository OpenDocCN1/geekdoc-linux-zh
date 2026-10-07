
```
smb: > more.txt
getting file /tmp/smbmore.15986 size of 21 as /tmp/smbmore.15986 (6.83571 kb/s)
(average 6.83594 kb/s)
This is a file test.
smb: > quit $
```

在上一个会话中，通过“放入”文件 `test.txt` 证明了可写性，通过目录列表和使用 `more` 命令显示 `test.txt` 的内容证明了可读性。由于 Windows 9x 共享不需要工作，因此没有使用用户名。相反，你应该在用户密码的通常位置输入共享的密码（而不是用户的密码）。

类似的命令可用于 Mainserv 共享。通过以下命令和会话显示 NTdata 共享项以及特殊共享项 `ADMIN$`、`IPC$` 和 `CS`。在 NT 目录显示：

```
$smclient //mainserv/temp -Username%password
added interface ip=192.168.100.1 bcast=192.168.100.255 nmask=255.255.255.0
added interface ip=192.168.200.1 bcast=192.168.200.255 nmask=255.255.255.0
```

创建即插即用的 Samba 系统

第二部分

```
added interface ip=192.168.100.1 bcast=192.168.100.255 nmask=255.255.255.0
Domain[MYGROUP] OS=[Windows NT 4.0] Server=[NT Lan Manager 4.0]
smb: > put test.txt (10.2534 kb/s) (average 10.259 kb/s)
| 共享名 | 类型 | 注释 |
| :--- | :--- | :--- |
| ADMIN$ | 磁盘 | 远程管理 |
| IPC$ | IPC | 远程 IPC |
| CS | 磁盘 | 默认共享 |
| NTdata | 磁盘 | NT 数据目录 |
| Server | 注释 | |
| Workgroup | 主节点 | |
```

上文显示了 NTdata 共享项以及特殊共享项 `ADMIN$`、`IPC$` 和 `CS`。

`-L` 选项目的是显示所有可见的共享项。因此，此 `smclient` 执行了测试可可见性的价值功能。它是对可可见性最准确的测试。

## 使用 smclient 测试访问性

`//servername/sharename`

可可见性和可访问性之间是相互独立的。一个共享项可以是可可见且可访问、可可见但不可访问、不可可见但可访问，或不可可见且不可访问。

## Samba 客户端工具

第 12 章

Mainserv 上共享项的访问性通过以下命令和会话显示：

```
$ smbclient //mainserv/temp -Username%password
added interface ip=192.168.100.1 bcast=192.168.100.255 nmask=255.255.255.0
added interface ip=192.168.200.1 bcast=192.168.200.255 nmask=255.255.255.0
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.6]
smb: ls > *
orbit-myuid D 0 Fri Sep 24 14:30:19 1999
orbit-root D 0 Sun Oct 17 19:28:54 1999
```

61906 个大小为 32768 的块。可用 8509 个块。

```
smb: > quit
```

一旦进入 `smclient` 会话，可以使用 `smclient` 的 `put` 命令测试可写性。

`smclient` 也非常适合测试对 Windows 98 共享项的访问，如下会话所示：

```
$ smbclient //wincli/menudata -Usharepassword
added interface ip=192.168.100.1 bcast=192.168.100.255 nmask=255.255.255.0
added interface ip=192.168.200.1 bcast=192.168.200.255 nmask=255.255.255.0
smb: > put test.txt
putting file test.txt as \test.txt (10.2534 kb/s) (average 10.259 kb/s)
smb: > ls
```

+ D 0 Thu Dec 17 08:50:28 1998

D 0 Thu Dec 17 08:58:28 1998

A 149 Thu Dec 17 00:49:38 1998

A 21 Sun Nov 21 17:05:42 1999

+ .a.mnu

test.txt

36189 个大小为 32768 的块。可用 20688 个块。

```
smb: > more.txt
getting file /tmp/smbmore.15986 size of 21 as /tmp/smbmore.15986 (6.83571 kb/s)
(average 6.83594 kb/s)
This is a file test.
smb: > quit $
```

在上一个会话中，通过“放入”文件 `test.txt` 证明了可写性，通过目录列表和使用 `more` 命令显示 `test.txt` 的内容证明了可读性。由于 Windows 9x 共享不需要工作，因此没有使用用户名。相反，你应该在用户密码的通常位置输入共享的密码（而不是用户的密码）。

类似的命令可用于 Mainserv 共享。通过以下命令和会话显示 NTdata 共享项以及特殊共享项 `ADMIN$`、`IPC$` 和 `CS`。在 NT 目录显示：

```
$smclient //mainserv/temp -Username%password
added interface ip=192.168.100.1 bcast=192.168.100.255 nmask=255.255.255.0
added interface ip=192.168.200.1 bcast=192.168.200.255 nmask=255.255.255.0
```

创建即插即用的 Samba 系统

第二部分

```
added interface ip=192.168.100.1 bcast=192.168.100.255 nmask=255.255.255.0
Domain[MYGROUP] OS=[Windows NT 4.0] Server=[NT Lan Manager 4.0]
smb: > put test.txt (10.2534 kb/s) (average 10.259 kb/s)
| 共享名 | 类型 | 注释 |
| :--- | :--- | :--- |
| ADMIN$ | 磁盘 | 远程管理 |
| IPC$ | IPC | 远程 IPC |
| CS | 磁盘 | 默认共享 |
| NTdata | 磁盘 | NT 数据目录 |
| Server | 注释 | |
| Workgroup | 主节点 | |
```

上文显示了 NTdata 共享项以及特殊共享项 `ADMIN$`、`IPC$` 和 `CS`。

`-L` 选项目的是显示所有可见的共享项。因此，此 `smclient` 执行了测试可可见性的价值功能。它是对可可见性最准确的测试。

可可见性和可访问性之间是相互独立的。一个共享项可以是可可见且可访问、可可见但不可访问、不可可见但可访问，或不可可见且不可访问。

## Samba 客户端工具

第12 章

Mainserv 上共享项的访问性通过以下命令和会话显示：

```
$ smbclient //mainserv/temp -Username%password
added interface ip=192.168.100.1 bcast=192.168.100.255 nmask=255.255.255.0
added interface ip=192.168.200.1 bcast=192.168.200.255 nmask=255.255.255.0
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.6]
smb: ls > *
orbit-myuid D 0 Fri Sep 24 14:30:19 1999
orbit-root D 0 Sun Oct 17 19:28:54 1999
```

61906 个大小为 32768 的块。可用 8509 个块。

```
smb: > quit
```

一旦进入 `smclient` 会话，可以使用 `smclient` 的 `put` 命令测试可写性。

`smclient` 也非常适合测试对 Windows 98 共享项的访问，如下会话所示：

```
$ smbclient //wincli/menudata -Usharepassword
added interface ip=192.168.100.1 bcast=192.168.100.255 nmask=255.255.255.0
added interface ip=192.168.200.1 bcast=192.168.200.255 nmask=255.255.255.0
smb: > put test.txt
putting file test.txt as \test.txt (10.2534 kb/s) (average 10.259 kb/s)
smb: > ls
```

+ D 0 Thu Dec 17 08:50:28 1998
D 0 Thu Dec 17 08:58:28 1998
A 149 Thu Dec 17 00:49:38 1998
A 21 Sun Nov 21 17:05:42 1999

+ .a.mnu
test.txt

36189 个大小为 32768 的块。可用 20688 个块。

```
smb: > more.txt
getting file /tmp/smbmore.15986 size of 21 as /tmp/smbmore.15986 (6.83571 kb/s)
(average 6.83594 kb/s)
This is a file test.
smb: > quit $
```

在上一个会话中，通过“放入”文件 `test.txt` 证明了可写性，通过目录列表和使用 `more` 命令显示 `test.txt` 的内容证明了可读性。由于 Windows 9x 共享不需要工作，因此没有使用用户名。相反，你应该在用户密码的通常位置输入共享的密码（而不是用户的密码）。

类似的命令可用于 Mainserv 共享。通过以下命令和会话显示 NTdata 共享项以及特殊共享项 `ADMIN$`、`IPC$` 和 `CS`。在 NT 目录显示：

```
$smclient //mainserv/temp -Username%password
added interface ip=192.168.100.1 bcast=192.168.100.255 nmask=255.255.255.0
added interface ip=192.168.200.1 bcast=192.168.200.255 nmask=255.255.255.0
```

> 注意
> 使用 tar 备份共享的常规方法是使用 `smbtar` 实用程序，它将在本书稍后的“使用 nmblookup 进行诊断测试”部分进行介绍。

`history` 命令显示 `smclient` 会话的命令历史。`setmode` 命令可用于设置共享中文件的 DOS 只读、系统、隐藏和存档属性。

## 使用 smclient 打印到远程打印机

可以使用 `smclient` 将字节流打印到远程打印机。如下例所示可以打印文本文件：

```
$ smclient '//wincli/localiii' -c "print test.txt"
```

在前面的示例中，除非 `test.txt` 以换页符结尾，否则必须手动进纸。此外，打印内容会出现阶梯状错位，即每行新行都从上一行结束位置的右侧开始。这可以通过 CRLF<->CR 翻译来解决，如接下来的命令所示：

```
$ smclient '//wincli/localiii' -c "translate; print test.txt"
```

以下是向打印机馈送内容的快速方法：

```
$ echo -L | smclient '//wincli/localiii' -c "print -"
```

> 注意
> 前述命令中的 ^L 是换页符（Ctrl+L），在 UNIX 中通过 Ctrl+V Ctrl+L 组合键产生。

以下命令将你输入的任何内容打印到远程打印机：

```
$ cat | smclient '//wincli/localiii' -c "translate; print -"
```

注意要结束输入会话，需要按下 Ctrl+D 文件结束组合键。

## 创建开箱 Samba 系统

> 注意
> 前述打印方法打印纯文本。虽然可以将打印过滤器的输入管道到 `smbclient`，但向打印机打印图形或格式化材料的常规方法是使用打印队列中的打印过滤器。

## smbclient 自动化

`smbclient` 打印命令是 `smbclient` 自动化的一种形式。`-T` 命令行选项支持自动化，`-c` 允许运行上一节讨论的任何 `smbclient` 会话命令。示例如下，它将 Windows 9x 客户端上的文件标记为只读、隐藏、存档：

```
$ smbclient //wincli/menudata -Usharepass -c "setmod test.txt rash"
```

以下命令将文件经过 CRLF 翻译复制到 Windows 客户端：

```
$ smbclient //wincli/menudata -Usharepass -c "translate; put menu.dat"
```

上述操作对于运行 UNIX 进程输出 UNIX 文本文件的服务器端自动化过程来说可能特别有用。如果过程的最后一步是上述命令，用户就可以在其本地磁盘上找到已相应转换为 DOS 文本风格的报告。自然，这需要对客户端名称进行一些变量替换。

## 故障排除 smbclient

- 共享是在 `smb.conf` 中定义的还是在 Windows 共享中定义的？
- 如果是服务器模式而非用户模式共享，请确保输入 `smbclient` 的密码是共享密码，而不是用户密码。
- 如果问题涉及 `smbclient -NL computername`，如果计算机是 Windows NT 或 2000 计算机，请确保使用以下命令：
  `smbclient -L -Username%password`。

这里有三个快速采取的初步步骤：

- 使用 `ping` 测试连接性。
- 使用 `testpart` 测试 `smb.conf` 是否合法。
- 使用 `ps ax | grep -i mbd` 测试正在运行的守护进程。

下一步涉及以下额外的 `smclient` 参数：

- 使用 `-I` `IP 地址`。
- 使用 `-u` 配合不同的可用用户。
- 使用 `-w` 配合不同的工作组。
- 在双斜杠使用 IP 地址作为服务器名。

如果你能让命令运行起来，请利用有效的命令格式与无效的命令格式之间的差异。

## 使用 smbmount 将 SMB 共享挂载为 UNIX 目录

`smbmount` 命令将 SMB 或 CIFS 共享挂载为 Linux 目录。它仅适用于 Linux。

> 注意
> `smbmount` 的语法在 Samba 2.0.6 中发生了完全变化。预计新语法将继续生效一段时间。本章仅讨论 2.0.6 的语法。如果你运行的是旧版本的 `smbmount`，请咨询你的 man 页面和不带参数的 `smbmount` 命令。

> 警告
> Samba 的默认构建不产生 `smbmount`。要获得 `smbmount` 命令，必须在 `./configure` 命令中包含 `--with-smbmount` 参数。

`smbmount` 命令有一段长而有趣的历史。它最初是一个尚未被集成到 Samba 中的贡献。`mbsh` 命令的设计旨在取代它，但在 Linux 开始使用 glib-2.1 编译后，`mbsh` 命令遇到了麻烦。此后，Samba 项目接纳了 `smbmount` 并对产品进行了快速更改。这些更改非常迅速，以至于文档滞后。因此，你应该不带参数运行 `smbmount` 并遵循其其中描述的语法。

`smbmount` 最简单的用法如下：

```
# smbmount //wincli/menudata /mnt/temp
```

上述命令仅限 root 运行。它将来自 Windows 98 机器 `wincli` 的 `menudata` 共享到挂载点 `/mnt/temp`。当询问密码时，如果主机是共享模式，你应该回答共享密码。一旦通过用户名挂载，该共享中的任何文件都可以由该用户名写入，并且任何访问此挂载点的用户都可以编辑。

换句话说，如果 root 之前运行了上述命令，`myuid` 就可以编辑 `/mnt/temp` 中 `username` 的文件。这与 `smbclient` 非常相似。

# 创建即用型 Samba 系统
第二部分

由于之前的挂载是共享模式，它只需要密码，因此没有用户名。与其重启，您应该按照如下测试此共享：

```
$ mount /mnt/menu
$ ls -ldf /mnt/menu/*
$ mount /mnt/menu
```

以下 `fstab` 条目将 Windows NT 共享 `ntdata` 挂载到 `/mnt/ntdata`：

```
//desk1/ntdata /mnt/ntdata smbfs username=username%whatever 0 0
```

以下 `fstab` 条目将 Linux 共享 `//mainserv/music` 挂载：

```
