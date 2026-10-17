
（注：由于原文后续存在大量重复和逻辑跳跃，翻译已在保持原文原意的基础上进行了最小化对齐。）

通过共享，你可以限制打印机供某些用户使用，拒绝公共访问。以下示例设置了一个仅允许 `larisa` 和 `aleina` 用户访问的打印机（如果你需要可以添加其他用户）。用户需要对打印机的池目录具有写权限。

```
[larisaslaser]
path = /var/spool/samba
writeable = yes
valid users = larisa aleina
guest ok = no
printable = yes
printing = cups
printer = myhp
oplocks = no
share modes = no
```

# 变量替换

对于分配给参数的字符串值，可以使用替换运算符。这为指定可能取决于上下文的值（例如用户名）提供了更大的灵活性。例如，假设一个服务需要为每个登录的用户使用单独的目录。此类目录的路径可以使用 `%u` 变量指定，该变量替换为当前用户名。字符串 `path = /tmp/%u` 对于 Justin 用户将变为 `path = /tmp/just`，对于 dylan 用户将变为 `path = /tmp/dylan`。表 33-3 列出了几个较常见的替换变量。

| 变量 | 描述 |
| :--- | :--- |
| `%S` | 当前服务的名称 |
| `%P` | 当前服务的根目录 |
| `%u` | 当前服务的用户名 |

表 33-3. Samba 替换变量

## 测试 Samba 配置

| 变量 | 描述 |
| :--- | :--- |
| `%H` | 用户的家目录 |
| `%h` | 运行 Samba 的互联网主机名 |
| `%m` | 客户端机器的 NetBIOS 名称 |
| `%L` | 服务器的 NetBIOS 名称 |
| `%M` | 客户端机器的互联网名称 |
| `%I` | 客户端机器的 IP 地址 |

表 33-3. Samba 替换变量（续）

在你对 `smb.conf` 文件进行更改后，可以使用 `testpar` 程序来查看条目是否输入正确。`testpar` 检查 Samba 条目的语法和有效性。默认情况下，`testpar` 检查 `/etc/samba/smb.conf` 文件。如果你使用不同的文件作为配置文件，可以将其作为参数传递给 `testpar`。你也可以让 `testpar` 检查特定主机是否有误。`Printing` 选项可以从通用打印机继承。

（注：用户提供的文本后半部分存在大量内容重复，翻译时已遵循“不要重复输出原文”的原则，仅对核心逻辑部分进行了翻译。）

# 第 33 章：Samba

如果你正在访问 Samba 服务器上特定账户的主目录，可以直接指定 homes 服务器。在下一个示例中，用户在提示输入该账户密码后，访问了 Samba 服务器上 aleina 账户的主目录：

```
smbclient //turtle.mytrek.com/homes -U aleina
```

你也可以使用 `smbclient` 访问位于 Windows 客户端上的共享资源。指定 Windows 客户端的计算机名称及其共享文件夹。在下一个示例中，用户访问了 Windows 客户端 lizard 上的 windata 文件夹。该文件夹配置为允许任何人访问，因此用户只需在密码提示处按回 ENTER 键即可。

```
$ smbclient //lizard/windata
added interface ip=192.168.0.2 bcast=192.168.0.255 nmask=255.255.255.0
Got a positive name response from 192.168.0.3 ( 192.168.0.3 )
Password:
Domain=[WORKGROUP] OS=[Windows 5.1] Server=[Windows 2000 LAN Manager]
smb: > ls
D 0 Sat Sep 7 17:29:19 2002
D 0 Sat Sep 7 17:29:19 2002
hi A10 Sat Sep 7 17:27:27 2002
mynewdoc.doc A0 Sat Sep 7 16:59:13 2002
39997 blocks of size 104856. 39930 blocks available
smb: > mget hi
Get file hi? y
getting file hi of size 10 as hi (1.22069 kb/s) (average 1.2207 kb/s)
smb: > quit
```

![](img/0160c5015efa6b5e7fe8c8f2b89e33c1_828_0.png)

登录后，你可以执行 `smbclient` 来管理文件和切换目录。可以使用 `/` 操作符执行 Shell 命令。要传输文件，可以使用 `mget` 和 `put` 命令，这与它们在 FTP 程序中的用法相同。`recurse` 命令允许你开启递归模式，一次性复制整个子目录。你可以使用文件匹配操作符（称为掩码）来选择一组文件。文件匹配（掩码）运算符有 `*`、`[]` 等（参见第 9 章）。默认掩码为 `*`，可匹配所有内容。接下来的示例使用 `mget` 复制所有以 .c 结尾的文件，如 myproc 中的文件：

```
smb> mget *.c
```

在传输过程中，你可以让 `smbclient` 对每个单独的文件进行提示，也可以直接传输所有选中的文件。提示命令可以切换此文件提示的开启。

要访问远程系统上的特定打印机，可以将打印机名称作为 `smbclient` 命令的参数，后跟跟任何选项。在下一个示例中，`smbclient` 使用 dylan 登录名访问了 `turtle.mytrek.com` 系统上的 `myepson` 打印机：

```
smbclient //turtle.mytrek.com/myepson -U dylan
```

连接后，会显示 SMB 提示符，你可以使用 `smbclient` 命令如 `print` 来打印文件，并使用 `printmode` 指定图形或文本。在下一个示例中，用户在访问 `turtle.mytrek.com` 上的 `myepson` 打印机后，打印了一个名为 myfile 的文件：

```
smb> print myfile
```

## smbmount

使用 `smbmount` 命令，Linux 或 Unix 客户端可以将共享目录挂载到其本地系统。`smbmount` 命令的语法与 `smbclient` 命令类似，具有许多相应的选项。`smbmount` 命令的参数是 Samba 服务器和共享目录，随后是你想要挂载该目录的本地目录。接下来的示例将 `myreports` 目录挂载到本地系统的 `/mnt/myreps` 目录：

```
smbmount //turtle.mytrek.com/myreports /mnt/myreps -U dylan
```

要挂载目录，请如下所示，使用本地目录名称使用 `smbmount` 命令：

```
smbmount /mnt/myreps
```

要挂载服务器上特定用户的主目录，请指定 homes 服务和该用户的登录名。接下来的示例将用户 larisa 的主目录挂载到本地系统的 `/home/chris/larisastuff` 目录：

```
smbmount //turtle.mytrek.com/homes /home/chris/larisastuff -U larisa
```

你也可以使用 `smbmount` 挂载 Windows 客户端上的共享文件夹。只需指定 Windows 客户端的计算机名称及其文件夹。如果文件夹名称包含空格，请用单引号括起来。在下一个示例中，用户将 lizard 上的 windata 文件夹挂载为 `/mylinux` 目录。对于任何人都可以访问的文件夹，只需在密码提示处按 ENTER 键。

```
$ smbmount //lizard/windata /mylinux
Password:
$ ls /mylinux
_hi_mynydewdoc.doc_myreport.txt
```

（注：原文后续部分存在大量重复内容，已根据指令要求完成核心逻辑翻译）

这将显示输入此 NIC 适配器 IP 地址的窗口。点击“高级”按钮，然后点击 WINS 选项卡。此外，确保勾选“启用 LMHOSTS 查找”和“在 TCP/IP 上启用 NetBIOS”项。

接下来，确保计算机名称和工作组与你在 Samba `smb.conf` 文件使用的相同。点击“控制面板”，点击“网络标识”选项卡。将显示 Windows 系统的计算机名称和工作组。如果没有提供，或者你想更改它，请点击“属性”打开一个窗口，你可以在其中输入计算机名称和工作组。
