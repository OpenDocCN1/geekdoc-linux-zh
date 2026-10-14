

## 31.2.2 接收传真

要接收传真，请使用带 -w 选项的 efax。你可能还必须使用 -iS0=1 向调制解调器发送 S0=1 命令以将其设置为自动应答，并在 efax 退出后使用 -kZ 向调制解调器发送 'ATZ' 复位请求。

与发送传真一样，使用 -d 选项指定要使用的设备文件的完整路径名。

默认情况下，efax 会将“会话日志”输出到标准错误，其中包含接收到的传真消息的状态信息；使用重定向将其重定向到文件（参见 Recipe 3.2.3 [Redirecting Error Messages to a File]，第 68 页）。

- ⇒ 要设置 efax 以接收传入传真并将会话日志保存到文件 faxlog 中，输入：

```
$ efax -d /dev/modem -kZ -w -iS0=1 2>&1 >> faxlog RET
```

此命令启动 efax 并设置调制解调器等待传入传真。传真接收后，efax 退出。你可以在它接收传真之前通过键入 CTRL-C 或杀死 efax 作业来停止 efax（参见 Recipe 3.3.5 [Stopping a Job]，第 73 页）。

当传真被接收时，它会被写入当前目录中的一个文件，其基本名称由当前数字日期和 efax 生成的会话号组成；每一页都会写入到一个单独的文件中，其三位数字文件扩展名为页码。接收到的传真文件采用 TIFF Group 3 传真格式；使用 display 查看它们（参见 Recipe 17.1 [Viewing an Image in X]，第 407 页），或将其转换为 PostScript 或其他格式以便打印（参见 Recipe 31.2.4 [Converting to and from Fax Format]，第 604 页）。

## 31.2.3 自动接收传真

上一节中描述的命令只能接收一个传真；一旦传真被接收，efax 就会退出。要运行 efax 以便自动接收所有传入传真消息，请使用 Bash while 循环，以便在传真接收后，efax 重新启动并继续，直到你中断它（有关此内置功能的更多信息，请参阅 Bash Info 文档）。

⇒ 要自动接收任何传入传真消息，输入：

```
$ while true ; do efax answer ; done [RET]
efax: Wed Feb 24 08:38:52 1999 efax v 0.8a (Debian release 08a-6)
Copyright 1996 Ed Casas
efax: 38:52 opened /dev/modem
efax: 38:53 waiting for activity
```

此命令使用 efax 包的所有默认设置，你可以对其进行配置。旧的 spool 文件将被删除，任何接收到的传真都会被邮件发送给你。

如果你需要为 efax 设置更多开关，并且不想每次想要设置传真机时都输入这些内容，你可以编写一个 shell 脚本来执行更多操作并将其保存到名为 faxon 的文件中，如图 31-4 所示。将其放在你的个人 bin 目录中（参见 Recipe C.1 [Using a Directory for Personal Binaries]，第 727 页）。每次接收到传真并保存后，efax 会重新启动，等待另一个传真。会话日志会写入你主目录中的文件 faxlog。

```
#!/bin/sh
while :
    do
        trap break 2;
        efax -d /dev/modem -kZ -u -iS0=1 2>&1 >> ~/faxlog;
    done
```

图 31-4. faxon 文件。

如果有传入的传真消息到达，efax 将接收它并以文件形式将消息写入当前目录中，文件名约定如前所述；然后 efax 重新启动，准备接收另一份传真。键入 CTRL-C 以停止脚本并退出 efax。

## 31.2.4 在传真格式之间转换

为了查看或打印接收到的传真，或传真你拥有的文件，你必须先将文件转换为或从 TIFF Group 3（TIFFG3）传真格式，这是在发送传真文件时的标准格式。 （不过，你可以使用 GIMP 或 display 查看 TIFFG3 文件——参见 Recipe 17.1 [Viewing an Image in X]，第 407 页）。因此，通过传真接收到的文件将采用此格式，你可能希望将其转换为其他格式。

有几种方法可以做到这一点。

### 方法 #1

使用 efix 来转换（或“修复”）用于传真的文件；它会将你想要传真的文件转换为 TIFFG3 格式。你也可以使用它将接收到的传真文件转换为你可以查看或打印的另一种格式。efix 工具写入标准输出，但你可以重定向其输出以保存到文件。

要转换用于传真的文件，输入 efix 后跟要转换的文件名，并将标准输出重定向到你希望包含传真图像的文件。efix 可以读取纯文本、PBM 和 TIFF 文件。

⇒ 要将文件 chart.pbm 转换为传真格式，输入：

```
$ efix -i pbm chart.pbm > chart.fax [RET]
```

此命令将文件 chart.pbm 的副本转换为 TIFFG3 传真格式，并将其写入名为 chart.fax 的文件。原始 PBM 文件不会被更改。

### 方法 #2

要将接收到的传真文件转换为你可以预览（参见 Recipe 17.4.2 [Previewing a PostScript File]，第 414 页）或打印（参见 Recipe 25.1.1 [Sending a Print Job to the Printer]，第 510 页）的 PostScript 文件，请使用带 -o ps 选项的 efix。

⇒ 要将接收到的传真文件 19990325.001 转换为 PostScript 文件，输入：

```
$ efix -o ps 19990325.001 > received.ps [RET]
```

此命令将传真文件转换为 PostScript，并将输出写入名为 received.ps 的文件。原始传真文件不会被更改。

### 方法 #3

Ghostscript
DEB: gs-common gs
RPM: ghostscript
WWW: http://www.cs.wisc.edu/~ghost/

要将 PostScript 文件转换为传真格式，请使用 gs 并指定“tiffg3”作为输出设备进行写入。

