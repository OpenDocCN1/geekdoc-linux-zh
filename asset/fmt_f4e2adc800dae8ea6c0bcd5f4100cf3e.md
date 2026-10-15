
你可以使用“打印设置”窗口为每个打印机定义所需的过滤器，以便文本能够正确格式化。`lp`命令的选项可以添加过滤器来正确处理文本。管理文档的其他命令包括`lpq`（查看打印队列内容）、`lprm`（从队列中删除打印作业）和`lpstat -t`（控制打印机）。

## 第 16 章：配置打印服务器

### 使用 lp 打印

你可以使用`lp`命令将文档打印到本地和远程打印机（前提是打印机已本地配置）。文档文件可以添加到`lp`命令行的末尾，或者通过管道（`|`）重定向到`lp`命令。这是一个简单的`lp`命令示例：

```
$ lp doc1.ps
```

当你仅用`lp`指定文档文件时，输出将重定向到默认打印机。作为个人用户，你可以通过设置`PRINTER`变量的值来更改默认打印机。通常，你会将`PRINTER`变量添加到你的启动文件之一，例如`$HOME/.bashrc`。例如，在`.bashrc`文件中添加以下行可以将你的默认打印机设置为`lp3`：

```
export PRINTER=lp3
```

要覆盖默认设置，请在`lp`命令上指定特定的打印机。以下示例使用`-P`选项来选择不同的打印机：

```
$ lp -P anypons doc1.ps
```

`lp`命令有多种选项，允许`lp`解释并格式化不同类型的文档。`-# num`，其中`num`替换为打印的副本数（1 到 100），以及`-1`（这会导致文档以原始模式发送，假设文档已经格式化）。要了解更多选项，请输入`man lp`。

### 使用 lpstat -t 列出状态

使用`lpstat -t`命令列出打印机的状态。这是一个示例：

```
$ /usr/sbin/lpstat -t
printer hp disabled Wed 10 Jul 2019 10:53:34 AM EDT
printer deskjet-555 is idle. enabled Wed 10 Jul 2019
10:53:44 AM EDT
```

此输出显示了两个活动状态打印机。`hp`打印机目前处于禁用状态（离线）。`deskjet-555`已启用。

### 使用 lprm 删除作业

用户可以使用`lprm`命令从队列中删除自己的作业。在命令行上单独使用`lprm`会从默认打印机中删除该用户的所有作业。要从特定打印机删除删除作业，请使用`-P`选项，如下：

```
$ lprm -P lp0
```

要删除当前用户的所有作业，请输入以下：

root用户可以通过在`lprm`命令行上指定用户来删除该用户的所有打印作业。例如，要删除名为`mike`的用户所有打印作业，root用户输入：

```
# lprm -U mike
```

要从队列中删除单个打印作业，请在`lprm`命令行上指定其作业号。要查找作业号，请输入`lpq`命令。该命令的输出可能如下：

```
# lpq
```

| Rank | Owner | Job | Files | Total Size |
| :--- | :--- | :--- | :--- | :--- |
| active | root | 133 | /home/jake/pr1 | 467 |
| 2 | root | 197 | /home/jake/mydoc | 23948 |

输出显示有两个可打印作业在等待-

## 第四部分：成为 Linux 服务器管理员

使用地址而不是主机名。（如果这样做有效，则说明存在 DNS 解析问题。）运行如`tcpdump`等工具可以让你看到事务何处失败。

检查`cupsd`正在监听哪些地址。为了让远程系统能够打印，`cupsd`进程必须在`localhost`之外监听。按照如下方式（作为 root 用户）使用`netstat`命令进行此检查。第一个示例显示`cupsd`仅监听在本地主机（`127.0.0.1:631`）；第二个示例显示`cupsd`监听在所有网络接口（`0.0.0.0:631`）；

```
# netstat -tupl | grep 631
tcp       0 127.0.0.1:631         0.0.0.0:*      LISTEN
6492/cupsd
# netstat -tupl | grep 631
tcp       0 0.0.0.0:631             0.0.0.0:*      LISTEN
6492/cupsd
```

对共享打印机的更改可以在`/etc/cups/`目录下的`cupsd.conf`和`printers.conf`文件中进行。

## 配置共享 Samba 打印机

你的 Linux 打印机可以配置为 SMB 打印机，以便在 Windows 系统上显示可用。要像 Samba (SMB) 打印机一样共享你的打印机，只需按照第 19 章“配置 Windows 文件共享服务器”中的描述配置基本的 Samba 服务器设置。你所有的打印机默认都应该在本地网络上共享。下一节将展示生成的设置外观，以及你可能想要更改它们。

### 理解用于打印的 sm.conf

当你配置 Samba 时，系统会构建`/etc/smb.conf`文件以启用你所有配置的打印机进行共享。以下是`smb.conf`文件中与打印机共享相关的几行：

```
[global]
..
load printers = yes
cups options = raw
printcap name = /etc/printcap
printing = cups
...
```

```
[printers]
comment = All Printers
path = /var/spool/samba
browseable = yes
writeable = no
printable = yes
```

你可以阅读注释行来了解更多关于文件内容的信息。以分号（`;`）开头的行表示该选项在注释行上的默认设置。删除分号即可更改设置。

所选行显示了来自`/etc/printcap`的打印机已加载，并且正在使用 CUPS 服务。当`cups`设置为`raw`时，Samba 假设打印文件在到达你的打印机之前已经过格式化。这允许 Linux 或 Windows 客户端提供它们自己的打印机。

最后几行是打印机的实际定义。通过将`browseable`选项从`no`改为`yes`，你赋予了用户打印所有打印机（`printable = yes`）的能力。你还可以为 Samba 服务器存储 Windows 打印驱动程序。当 Windows 客户端使用你的打印机时，驱动会自动可用。你不需要从供应商网站下载驱动程序。要启用打印机程序，请添加如下 Samba 共享`print$`：

```
comment = Printer Drivers
path = /var/lib/samba/drivers
browse = yes
guest ok = no
read only = yes
write list = chris, dduffey
```

在共享可用后，你可以开始将 Windows 打印驱动程序拷贝到`/var/lib/samba/drivers`目录。

## 设置 SMB 客户端

如果你在 Linux 计算机上配置 Samba 打印机，很有可能你想要将其与 Windows 客户端共享。如果 Samba 在你的电脑上配置正确，且客户端计算机可以通过网络访问你，用户在使用你的打印机时应该不会遇到问题。

对于许多 Windows 10 系统，点击开始 -> 打印机和扫描仪并从列表中选择打印机进行配置。

在 Windows Vista 中，你打开网络图标。你的主机计算机名称（NetBIOS 名称）将显示在这里。下一节将展示生成的设置外观，以及你可能想要更改它们。提示：如果你在 Windows 操作系统上要配置 SMB 打印机，请前往开始 -> 打印机。共享打印机。在打印机窗口中，点击你的打印机。CUPS 服务（`cupsd`进程）窗口显示了你的打印机。

使用地址而不是主机名。（如果这样做有效，则说明存在 DNS 解析问题。）运行如`tcpdump`等工具可以让你看到事务何处失败。
