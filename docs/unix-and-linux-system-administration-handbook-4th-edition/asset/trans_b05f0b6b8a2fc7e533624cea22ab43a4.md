

在开始向新的打印服务器上传打印机驱动程序之前，你必须在系统层面处理好一些细节。确保 printadm 账户存在并且有权限访问 Samba。

```
$ sudo useradd printadm
$ sudo smbpasswd -a printadm
```

只有当适当的目录结构存在并且由 printadm 拥有时，Samba 才能存储打印机驱动程序（由 write list 选项定义）：

```
$ sudo mkdir -p /var/lib/samba/printers
$ sudo cd /var/lib/samba/printers
$ sudo mkdir W32X86 WIN40 x64
$ sudo chown -R printadm .
```

此时有两种选择：你可以走到一台 Windows 机器上从那里上传打印机驱动程序，或者你可以使用 Samba 工具从命令行全部完成。不幸的是，没有简单的方法知道特定驱动程序到底需要安装什么，因此在大多数情况下我们推荐第一种方法。只有当你面临在多台服务器上反复安装驱动程序时，才值得研究安装过程并学习如何使用命令行工具复制它。

## 从 Windows 安装打印机驱动程序

要从 Windows 客户端安装驱动程序，通过在开始 -> 运行对话框中输入 \\sambaserver 打开与 Samba 服务器的连接。Windows 会要求你登录到 Samba 服务器。以用户 printadm 登录。如果一切顺利，会弹出一个窗口，列出服务器提供的共享。

在 Printers 子文件夹中，你应该能看到从服务器共享的所有打印机。右键单击打印机图标周围的空白区域以激活服务器属性对话框，然后利用驱动程序选项卡添加你喜欢的打印机驱动程序。

上传的驱动程序最终会存放在为 [print$] 共享指定的目录中。此时，你可能想快速查看一下刚刚上传的驱动程序的属性。这个文件列表就是如果你想自动化驱动程序的上传，将来需要提供给 Samba 命令行工具的内容。

## 从命令行安装打印机驱动程序

正如你可能已经猜到的，其中一些步骤在没有 Windows 的情况下很难复制，特别是设置打印机默认值。但如果你想在 Samba 服务器上设置数百台打印机，你可能仍想尝试从命令行完成。命令行配置对于 PostScript 打印机特别有效，因为 Windows PostScript 打印机驱动程序在没有默认配置信息的情况下也能正确工作。

如果你记下了特定驱动程序所需的文件，你可以从命令行安装驱动程序。首先，将所需文件复制到 [print$] 共享：

```
$ cd ~/mydriver
$ smbclient -U printadm //samba-server/print$ -c 'mput *.'
```

接下来，将驱动程序分配给特定打印机。假设你有一台简单的 PostScript 打印机，并带有自定义 PPD 文件：

```
$ rpcclient -U printadm -c "
adddriver \"Windows NT x86\" \"Our Custom PS\\
PSCRIPTS.DLL:CUSTOM.PPD:PSSUI.DLL:PSCRIPT.HLP:NULL:NULL:PSCRIPT.NTF\" \
samba-server
```

行尾的反斜杠允许将命令拆分为多行以提高清晰度；如果你愿意，可以省略这些反斜杠并将命令输入在一行中。双引号前的反斜杠区分了嵌套的引号集。

上面的长字符串包含在从 Windows 安装打印机驱动程序时，在打印机驱动程序属性对话框中列出的信息：

- 长打印机名称
- 驱动程序文件名
- 数据文件名
- 配置文件名
- 帮助文件名
- 语言监视器名称（如果没有，请将其设置为 NULL）
- 默认数据类型（如果没有，请将其设置为 NULL）
- 附加文件的逗号分隔列表

要配置打印机使用其中一个已上传的驱动程序，运行

```
$ rpcclient -U printadm -c "
set driver \"myprinter\" \"Our Custom PS\"" samba-server
```

## 30.8 调试 SAMBA

Samba 通常无需太多关注即可运行。但是，如果你遇到问题，可以查阅两个主要的调试信息来源：日志

