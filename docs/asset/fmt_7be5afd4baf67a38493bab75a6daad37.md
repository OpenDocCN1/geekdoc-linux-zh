
当然，久而之可能会很烦人 :-)

### postscript (S)
此参数强制打印机将打印文件解释为 postscript。这是通过在输出开头添加 `!` 实现的。
当你有很多 PC 固执在打印作业开头放置控制-D 时，这在混淆你的打印机时非常有用。
默认：`postscript = False`
示例：`postscript = False`

### preferred master (S)
此布尔参数控制 `nmbd` 是否为其工作组的优选主浏览器。

# smb.conf (5) 289

如果此项设置为 true，启动时，`nmbd` 将强制进行选举，并且在选举中具有微弱优势。建议将此参数与 `domain master = yes` 配合使用，以便 `nmbd` 能够保证成为域主大师。默认值 `auto` 在 Samba 被配置为域主浏览器时会启用 `preferred master`。

请谨慎使用此选项，因为如果同一子网内有多个主机（无论是 Samba 服务器、Windows 95 还是 NT）都是首选主浏览器，它们将都会定期且持续地尝试成为本地主浏览器。这将导致不必要的广播流量并降低浏览能力。另请参阅 `os level`。

默认：`preferred master = auto`
示例：`preferred master = yes`

### preferred master (G)
对于不会拼写的人来说，`preferred master` 的同义词。

### preload
`auto services` 的同义词。

### preserve case (S)
这控制新文件名是使用客户端传递的大小写创建，还是强制使用 `默认` 大小写。

默认：`preserve case = yes`
更详细的讨论请参阅 `NAME MANGLING` 章节。

### print command (S)
在打印作业完成到服务的池化后，此命令将通过 `system()` 调用处理打印池文件。通常情况下，指定的命令会将打印池文件提交给主机的打印子系统，但并不要求这样做。服务器不会删除打印池文件，因此你指定的任何内容都应该在处理后删除打印池文件，否则你需要手动删除打印池文件。

`print command` 是文本字符串。它将原样使用，但有两个例外：所有的 `"%s"` 出现将被替换为相应的打印池文件名，`"%f"` 的出现将被替换为相应的打印机名称。打印池文件由服务器自动生成，打印机名称见下文讨论。

如果 `"%s"` 前没有 `'/'`，则将使用完整路径作为文件名。如果你不喜欢（这会弄乱 `lpq` 输出），请使用 `"%f"` 代替。`"%f"` 的出现将被替换为不带前面完整路径的打印池文件名。

`print command` 必须包含至少一次 `"%s"` 或 `"%f"`——`"%p"` 是可选的。在提交作业时，如果没有通过 `"%p"` 提供打印机名称，

如果在 `[global]` 部分指定，则给定的 `print command` 将用于任何没有指定单独 `print command` 的打印服务。

如果可打印服务既没有指定的 `print command`，也没有全局 `print command`，将创建打印池文件但不会进行处理（最重要的是）不会被删除。

注意，在某些 UNIX 上，打印可能会通过 `nobody` 账户失败。如果发生这种情况，请创建一个可以打印的备用访客账户，并在 `global` 部分设置 `guest account`。

通过意识到这些命令只是传递给 shell，你可以形成相当复杂的命令。例如，以下命令将记录打印作业、打印文件，然后删除它。注意 `;` 是 shell 脚本中命令的常用分隔符。

```
print command = echo Printing %s >> /tmp/print.log; lpr -P %p %s; rm %s
```

你可能需要根据你通常在系统中打印文件的方式大幅更改此命令。该参数的默认值取决于 `printing` 设置。

默认：`printing=` BSD, AIX, QNX, LPRNG 或 PLP : `print command = lpr -r -Pp %s`

对于 `printing=` SYS 或 HPUX ： `print command = lp -c -dp %s; rm %s`

对于 `printing=` SOFTQ ： `print command = lp -dp %s; rm %s`
示例：`print command = /usr/local/samba/bin/myprint-script %p %s`

### print ok (S)
`printable` 的同义词。

### printable (S)
如果为 `yes`，则客户端可以对服务的目录打开、写入并提交打印池文件。

注意，可打印服务将始终允许（在用户权限允许的情况下）写入服务路径以进行打印数据的池化。`read only` 参数只控制对资源的非打印访问。

默认：`printable = no`
示例：`printable = yes`

### printcap (G)
`printcapname` 的同义词。

### printcap name (G)
此参数可用于覆盖服务器编译的默认 `printcap`（通常为 `/etc/printcap`）。查看 `[printers]` 章节的讨论以了解你可能想这样做的原因。

在使用 `lpstat` 列出可用打印机的 System V 系统上，你可以使用 `printcap` 列出可用打印机，可以使用 `printcap name = lpstat` 自动获取可用打印机列表。这是

一个最小的 `printcap` 文件看起来如下：

```
print1|My Printer 1
print2|My Printer 2
print3|My Printer 3
print4|My Printer 4
print5|My Printer 5
```

其中 `|` 分隔打印机的别名。第二个别名包含空格，提示 Samba 这是一个注释。

> 注意：AIX 默认 `printcap name` 为 `"/etc/qconfig"`。如果 `printcap` 中出现 `"/etc/qconfig"` 字符串，Samba 将假设文件为 AIX `qconfig` 格式。

默认：`printcap name = /etc/qconfig`
示例：`printcap name = /etc/qconfig`

### print ok (S)
`printable` 的同义词。

### printer (S)
如果为 `yes`，则客户端可以对服务的目录打开、写入并提交打印池文件。注意，可打印服务将始终允许（在用户权限允许的情况下）写入服务路径以进行打印数据的池化。`read only` 参数只控制对资源的非打印访问。

默认：`printable = no`
示例：`printable = yes`

### printcap (G)
`printcapname` 的同义词。

### printcap name (G)
此参数可用于覆盖服务器编译的默认 `printcap`（通常为 `/etc/printcap`）。查看 `[printers]` 章节的讨论以了解你可能想这样做的原因。

在使用 `lpstat` 列出可用打印机的 System V 系统上，你可以使用 `printcap` 列出可用打印机，可以使用 `printcap name = lpstat` 自动获取可用打印机列表。这是

一个最小的 `printcap` 文件看起来如下：

```
print1|My Printer 1
print2|My Printer 2
print3|My Printer 3
print4|My Printer 4
print5|My Printer 5
```
