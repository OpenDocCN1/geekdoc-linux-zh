

该命令应为一个程序或脚本，它接受打印机的名称作为唯一参数，并输出打印机状态信息。

当前支持九种打印机状态信息样式：BSD、AIX、LPRNG、PLP、SYSV、HPUX、QNX、CUPS 和 SOFTQ。这涵盖了大多数 UNIX 系统。你使用 `printing` = *option* 来控制预期的类型。

某些客户端（特别是 Windows for Workgroups）可能无法正确发送它们正在请求状态信息的打印机的连接号。为了绕过这个问题，服务器将报告客户端连接的第一个打印机服务。这仅发生在发送的连接号无效时。

如果给定了 `%p`，则打印机名称将放在其位置。否则，它将被放置在命令的末尾。

请注意，在 `lpq` *command* 中包含绝对路径是一个良好的做法，因为 `$PATH` 可能对服务器不可用。当使用 CUPS 库编译时，不需要 `lpq` *command*，因为 smbd 将执行库调用来获取打印队列列表。

## lpr resume command (S)
默认值：`lpr` `resume` *command* = `lpr` *command* = `/usr/bin/lpq` `%p`

此参数指定在服务器主机上执行的命令，以重启或继续打印或暂存特定的打印作业。

该命令应为一个程序或脚本，接受打印机名称和要恢复打印作业的作业号。另请参阅 `lppause` *command* 参数。

如果给定了 `%p`，则打印机名称将放在其位置。`%j` 将被替换为作业号（一个整数）。

请注意，在 `lpr` *resume* *command* 中包含绝对路径是一个良好的做法，因为 `PATH` 可能对服务器不可用。

另请参阅 `printing` 参数。

默认值：当前未给此字符串指定默认值，除非 `printing` 参数的值为 SYSV，在这种情况下默认值为：

`lp` *-i* `%%p-%%j` *-H* *resume*

或者如果 `printing` 参数的值为 SOFTQ，则默认值为：

`qstat` *-s* *-j* `%%j` *-r*

## lprm command (S)
默认值：`lpr` *m* *command* = *由* *printing* *参数决定*

此参数指定在服务器主机上执行的命令，以删除打印作业。

该命令应为一个程序或脚本，接受打印机名称和作业号，并删除该打印作业。

如果给定了 `%p`，则打印机名称将放在其位置。`%j` 将被替换为作业号（一个整数）。

请注意，在 `lprm` *command* 中包含绝对路径是一个良好的做法，因为 `PATH` 可能对服务器不可用。

使用示例如下：

```text
lprm command = /usr/bin/lprm -P%p %j
or
lprm command = /usr/bin/cancel %p-%j
```

## machine password timeout (G)
默认值：`machine password timeout = 604800`

如果 Samba 服务器是 Windows NT 域的成员（参见 `security = domain` 参数），则正在运行的 smbd 进程会定期尝试更改存储在名为 `private/secrets.tdb` 的 TDB 中的 `MACHINE ACCOUNT PASSWORD`。此参数指定更改此密码的频率，以秒为单位。默认值是一周重新以秒表示，与 Windows NT 域成员服务器相同。

另请参阅 smbpasswd(8)，以及 `security = domain` 参数。

## magic output (S)
默认值：`magic output = <magic script name>-outfile.txt`

示例：`magic output = myfile.txt`

此参数指定包含由 magic 脚本生成的输出的文件名（见下文 `magic script` 参数）。

> **警告**
>
> 如果两个客户端在同一目录中使用相同的 *magic script*，输出文件的内容是未定义的。

## magic script (S)
默认值：无默认值

示例：`magic script = user.csh`

此参数指定一个文件的名称，如果该文件被打开，当文件关闭时将由服务器执行。这允许将 UNIX 脚本发送到 Samba 主机并以连接用户的身份执行。

以这种方式执行的脚本在完成时可以被删除，假设用户具有适当的权限级别且文件权限允许删除。

如果脚本生成输出，输出将发送到由 *magic output* 参数指定的文件（见上文）。

请注意，某些 shell 无法解释包含 CR/LF 而不是 LF 作为换行符的脚本。Magic 脚本必须能在主机上原样 *执行*，对于某些主机和某些 shell，这需要 DOS 端的过滤。

Magic 脚本是 *实验性* 的，不应 *依赖* 它们。

## mangled map (S)
默认值：*mangled map = no*

示例：*mangled map = (*.html *.htm)*

这是针对那些想要直接映射无法在 Windows/DOS 上表示的 UNIX 文件名的用户。名称的变形并不总是我们所需的。特别是，你可能拥有文件扩展名在 DOS 和 UNIX 之间不同的文档。例如，在 UNIX 下，通常使用 *.html* 作为 HTML 文件，而在 Windows/DOS 下，*.htm* 更常用。

因此，要将 *html* 映射到 *htm*，你可以使用：

```text
mangled map = (*.html *.htm)
```

一个非常实用的用例是去除某些 CDROM 上文件名末尾烦人的 *;1*（仅在某些 UNIX 下可见）。为此，请使用映射 `(;;1;)`。

## mangled names (S)
默认值：*mangled names = yes*

这控制 UNIX 下的非 DOS 名称是否应映射为 DOS 兼容的名称（“变形”）并使其可见，或者是否应简单忽略非 DOS 名称。

有关如何控制变形过程的详细信息，请参阅 *name mangling* 章节。

如果使用变形，则变形算法如下：

-   文件名最右边点号前的（最多）五个字母数字字符被保留，强制转换为大写，并作为变形名称的开头（最多）五个字符出现。
-   在变形名称的第一部分后追加一个波浪号 `~`，后跟基于原始根名称（即原始文件名减去其最终扩展名）的两个字符唯一序列。最终扩展名仅在包含任何大写字母或长度超过三个字符时才包含在哈希计算中。
-   UNIX 名称以点号开头的文件将作为 DOS 隐藏文件呈现。变形名称将像其他文件名一样创建，但去掉前导点号，并使用 `___` 作为其扩展名（那是三个下划线），无论实际原始扩展名是什么。

请注意，可以使用 *mangling char* 选项来指定要使用的字符，如果你不喜欢 `~`。

两位数哈希值由大写字母数字字符组成。

此算法仅当目录中的文件共享相同的前五个字母数字字符时才会导致名称冲突。发生此类冲突的概率为 1/1300。

名称变形（如果启用）允许在保留长 UNIX 文件名的同时，从 Windows/DOS 在 UNIX 目录之间复制文件。UNIX 文件可以从 Windows/DOS 重命名为新的扩展名，并将保留相同的基名。变形名称在会话之间不会改变。

## mangle prefix (G)
默认值：mangle prefix = 14

示例：mangle prefix = 4

控制生成变形名称时使用的原始名称前缀字符数。较大的值会给出较弱的哈希，因此会导致更多的名称冲突。最小值为 1，最大值为 6。

mangle prefix 仅在变形方法为 hash2 时有效。

## mangling char (S)
默认值：mangling char = `~`

示例：mangling char = `^`

这控制名称变形中用作魔术字符的字符。默认值是 `~`，但这可能与某些软件冲突。使用此选项将其设置为你喜欢的任何字符。这仅在变形方法为 hash 时有效。

## mangling method (G)
默认值：mangling method = hash2

示例：mangling method = hash

控制用于生成变形名称的算法。可以取两个不同的值，"hash" 和 "hash2"。"hash" 是 Samba 多年来使用的算法，并且在 Samba 2.2.x 中是默认值。"hash2" 现在是默认值，它是较新的，被认为是更好的算法（在名称中产生较少冲突）。许多 Win32 应用程序存储变形名称，因此更改算法必须谨慎，除非重新安装，否则这些应用程序可能会损坏。

## map acl inherit (S)
默认值：map acl inherit = no

此布尔参数控制 smbd(8) 是否尝试将 Windows ACL 中存储的 'inherit' 和 'protected' 访问控制项标志映射到名为 user.SAMBA:PAI 的扩展属性。此参数仅在 Samba 在支持扩展属性的平台上运行时才有效（目前是 Linux 和 IRIX）

