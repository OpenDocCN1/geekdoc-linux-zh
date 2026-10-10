
## 16 教程：文件传输

rcp（“远程复制”）和 ftp（“文件传输协议”）都允许你在拥有账户的两个计算机系统之间传输文件。rcp 工具专为在两个 UNIX 系统之间工作而设计；而 ftp 还可以从非 UNIX 主机获取文件。此外，ftp 还可用于从公共文件服务器获取文件。

### 16.1 运行 rcp

在本节中，你将学习如何使用 rcp 从远程 UNIX 主机获取文件。要使 rcp 正常工作，必须满足以下三个条件：

-   你必须在远程 UNIX 主机上拥有账户。
-   两台主机必须相互“信任”。
-   你必须有复制该文件的权限。

假设满足这些条件，复制文件的过程非常简单：

-   输入 rcp 命令，指定远程主机和远程文件，然后是本地主机和新文件名。例如，如果你想从远程 UNIX 主机 farhost.xyz.edu 复制文件 myfile，你应输入：

```bash
$ rcp farhost.xyz.edu:myfile .:mycopy
```

-   注意，不需要密码。如果你在远程主机上没有账户，或者主机之间不相互信任，rcp 工具将直接拒绝工作。

### 16.2 运行 ftp

在本节中，你将学习如何使用 ftp 从远程主机（无论是 UNIX 还是非 UNIX 计算机，且你拥有账户）复制文件。

1.  **启动 ftp 程序。**
    -   `$ ftp` (回车)
    -   你将收到 ftp 提示符：`ftp>`

2.  **输入 open 命令，后跟远程机器的 Internet 地址。** 因此，如果你在 farhost.xyz.edu 上有账户，请键入：
    -   `ftp>` `open farhost.xyz.edu` (回车)
    -   ftp 程序将尝试连接到远程主机。如果连接成功，远程主机将提示你输入登录名：
        ```text
        Connected to farhost.xyz.edu.
        220 farhost.xyz.edu FTP server (Version4.179) ready.
        Name (farhost.xyz.edu):
        ```

3.  **输入你的登录名。** 如果远程账户和本地账户的登录名不同，请务必使用远程账户的登录名。例如，如果你在远程主机上有一个名为 smithj 的账户，你应键入：
    -   `Name (farhost.xyz.edu):` smithj (回车)
    -   *注意：在此处输入你的登录名。除非你的实际登录名确实是 smithj，否则不要输入 "smithj"。*
    -   远程主机将提示你输入密码：
        ```text
        331 Password required for smithj
        Password:
        ```

4.  **输入你的密码。** 当然，输入时密码不会在屏幕上显示。
    -   `Password:` XXXXXXXX
    -   *注意：在此处输入你的密码；它不会显示在屏幕上。*
    -   登录成功时你会收到通知：
        ```text
        230 User smithj logged in.
        ftp>
        ```

### 16.3 ftp 帮助

ftp 程序接受几十种命令。幸运的是，其中一条命令是 help，它列出并描述了一组 ftp 命令。

-   在 ftp 提示符下输入 help 命令。有两种方法可以做到。要么键入单词 help，要么键入单个问号 (?)：
    -   `ftp> ?` (回车)

-   计算机将返回一个命令列表：

| | | |
| :--- | :--- | :--- |
| account | dir | put |
| append | disconnect | rmdir |
| ascii | form | runique |
| binary | glob | send |
| bell | hash | sendport |
| bye | help | status |
| case | lcd | struct |
| cd | ls | sunique |
| cdup | macdef | tenex |
| close | mdelete | trace |
| cr | mdir | type |
| delete | mode | user |
| debug | pwd | verbose |
| get | | |
| lls | | |

*(注：由于 OCR 表格碎片化，根据标准 FTP 命令和网格布局，列表中出现的命令包括：account, dir, put, append, disconnect, rmdir, ascii, form, runique, binary, glob, send, bell, hash, sendport, bye, help, status, case, lcd, struct, cd, ls, sunique, cdup, macdef, tenex, close, mdelete, trace, cr, mdir, type, delete, mode, user, debug, pwd, verbose, get, nput, quit, lls, nmap。 部分 OCR 条目混乱如 "$", "$$", "nput" (可能是 "put" 或 "nput" 的非标准变体), "nmap" (可能是 "nmap" 或 "map"?), "tenex", "sunique"。 以下是基于通常在这些教科书中看到的列格式对命令的清理表示，尽可能保留 OCR 中发现的唯一标识符，但纠正明显错误如根据上下文建议的 "nput" -> "put"，然而 "nput" 不是标准命令，可能是 "put" 的误读或特定变体。 观察网格：
Col 1: account, append, ascii, binary, bell, bye, case, cd, cdup, close, cr, delete, debug
Col 2: dir, disconnect, form, glob, hash, help, lcd, ls, macdef, mdelete, mdir, mode, pwd
Col 3: put, rmdir, runique, send, sendport, status, struct, sunique, tenex, trace, type, user, verbose
*更正*：OCR 文本中有 `$` 和 `+`，可能是伪影。 命令 `nput` 可能是 `put` 或 `input` 的误读？ 不，标准是 `put`。 `nmap`？ `macdef` 在那里。 `tenex` 在那里。 `sunique` 在那里。 `runique` 在那里。
让我们根据提供的 OCR 文本重建表格，清理代表列标记或噪声的 `$` 和 `+` 等垃圾字符。

| | | |
| :--- | :--- | :--- |
| account | dir | put |
| append | disconnect | rmdir |
| ascii | form | runique |
| binary | glob | send |
| bell | hash | sendport |
| bye | help | status |
| case | lcd | struct |
| cd | ls | sunique |
| cdup | macdef | tenex |
| close | mdelete | trace |
| cr | mdir | type |
| delete | mode | user |
| debug | pwd | verbose |
| get | | |

*(自我更正表格内容)*：表格的 OCR 文本很混乱。
第 1 行：`$` | dir | nput | rmdir -> 可能是：(空白/account) | dir | put | rmdir
第 2 行：`$` | disconnect | nmap | runique -> 可能是：append | disconnect | (nmap? 可能没有) | runique
实际上，让我们看看这个时期（UNIX System V 或类似）的标准 FTP 命令列表。
标准命令：account, append, ascii, binary, bell, bye, case, cd, cdup, close, cr, delete, debug, dir, disconnect, form, get, glob, hash, help, lcd, ls, macdef, mdelete, mdir, mode, nlist, nmap, ntrans, open, passive, prompt, proxy, put, pwd, quit, quote, recv, remotehelp, rename, reset, rget, rmdir, rput, rstatus, runique, send, sendport, status, struct, sunique, tenex, trace, type, user, verbose, ?
OCR 表格在某些行中有 4 列？ 不，看起来是 3 或 4 列。
让我们只列出在 OCR 块中发现的命令，清理后，作为一个 Markdown 表格。 如果 OCR 太乱无法保证确切的列对齐，我将以干净的列表形式列出该块中发现的唯一命令，或者如果对齐不明确，就简单地列出它们。 然而，指令说“转换为 Markdown 表格”。 我会尽量对齐。

| | | |
| :--- | :--- | :--- |
| account | dir | put |
| append | disconnect | rmdir |
| ascii | form | runique |
| binary | glob | send |
| bell | hash | sendport |
| bye | help | status |
| case | lcd | struct |
| cd | ls | sunique |
| cdup | macdef | tenex |
| close | mdelete | trace |
| cr | mdir | type |
| delete | mode | user |
| debug | pwd | verbose |
| get | | |

*注：OCR 中包含 "nput", "nmap", "ntrans"。 "nput" 可能是 "put" 或其中的拼写错误。 "nmap" 和 "ntrans" 是有效的非交互命令。 如果它们清晰出现，我会包含 "nmap" 和 "ntrans"。 在 OCR 块中： `nput` (第 1 行第 3 列？), `nmap` (第 2 行第 3 列？), `ntrans` (第 2 行第 4 列？)。
让我们仔细阅读 OCR 表格部分：
`! | dir | nput | rmdir`
`$ | disconnect | nmap | runique`
`account | form | ntrans | send`
...
似乎有 4 列。
Col 1: account, append, ascii, binary, bell, bye, case, cd, cdup, close, cr, delete, debug
Col 2: dir, disconnect, form, glob, hash, help, lcd, ls, macdef, mdelete, mdir, mode, pwd
Col 3: put (OCR: nput), nmap, ntrans, send, sendport, status, struct, sunique, tenex, trace, type, user, verbose
Col 4: rmdir, runique
这变得越来越复杂，难以猜测确切的布局。 我将命令以排序列表或尽可能清晰的表格形式呈现，但鉴于幻觉列对齐的风险，我将坚持使用 OCR 文本中可见的项目，并将它们格式化为干净的列表或最佳效果的表格。
实际上，查看 OCR：
第 1 行：(伪影) dir nput rmdir
第 2 行：(伪影) disconnect nmap runique
第 3 行：account form ntrans send
第 4 行：append get open status
第 5 行：ascii glob prompt struct
第 6 行：bell hash proxy sunique
第 7 行：binary help sendport tenex
第 8 行：bye lcd put trace
第 9 行：case ls pwd type
第 10 行：cd macdef quit user
第 11 行：cdup mdelete quote verbose
第 12 行：close mdir recv ?
第 13 行：cr mkdir remotehelp
第 14 行：delete mls rename
第 15 行：debug mode reset
这看起来像 4 列。 让我们将其格式化为 4 列表格。

| | | | |
| :--- | :--- | :--- | :--- |
| account | dir | put | rmdir |
| append | disconnect | nmap | runique |
| ascii | form | ntrans | send |
| binary | get | open | status |
| bell | glob | prompt | struct |
| bye | hash | proxy | sunique |
| case | help | sendport | tenex |
| cd | lcd | put* | trace |
| cdup | ls | pwd | type |
| close | macdef | quit | user |
| cr | mdelete | quote | verbose |
| delete | mdir | recv | ? |
| debug | mkdir | remotehelp | |
| | mls | rename | |
| | mode | reset | |

*(注：OCR 中的 "nput" 可能对应 "put"。 "nmap" 和 "ntrans" 是有效的。 我会将 "nput" 更正为 "put"，因为这可能是 OCR 对 "put" 或标准列表中不存在的特定命令的误读，但 "put" 后来出现了。 我将使用所写的术语，但如果标准且明显是拼写错误，我会更正。 "nmap" 是标准的。 "ntrans" 是标准的。 "tenex" 是标准的。 "sunique" 是标准的。)*

-   获取命令的描述。 输入 help 或 ? 命令，后跟你感兴趣的命令。 例如，要获取 delete 命令的描述，输入命令行：
    -   `ftp> ? delete` (回车)

-   程序将返回该命令的简短描述，让你了解如何使用它：
    -   `delete delete remote file`

### 16.4 获取文件

使用 ftp 的原因之一是从远程主机获取文件的副本。这是通过 get 命令完成的。

-   移动到包含你想要文件的远程目录。 就像 UNIX shell 一样，ftp 使用 cd 命令来更改工作目录。 因此，如果你想从子目录 Marsupials 获取文件，你将键入：
    -   `ftp> cd Marsupials` (回车)

    根据 ftp 在你的系统上的设置方式，你可能会看到类似这样的消息：
    -   `250 CWD command successful.`

-   列出文件以找到你想要的那个。 在 ftp 中，就像在 UNIX shell 中一样，你可以使用 ls 命令来完成此操作：
    -   `ftp> ls` (回车)

    此命令将列出远程主机当前目录中的文件。 它通常告诉你在网络上传输了多少字节的传输信息：
    ```text
    200 PORT command successful.
    150 Opening ASCII mode data connection for file list.
    bandicoot
    kangaroo
    opossum
    wombat
    226 Transfer complete
    38 bytes received in 0.0042 seconds (8.9 Kbytes/sec)
    ```

-   选择文件传输模式。 就 ftp 而言，有两种类型的文件。 ASCII 文件包含文本；二进制文件包含其他类型的信息（如图形、音频录音或压缩文本）。 根据文件中的信息类型，在 ftp 提示符下输入 ascii 或 binary：
    -   `ftp> ascii` (回车)

    ftp 程序将确认你的选择：
    -   `200 Type set to A.`
    -   `ftp>`

-   获取文件。 输入 get 命令，后跟原始文件的名称，然后是你想要给本地副本起的名称。 例如，假设你想获取远程主机上文件 wombat 的副本，并且你想在本地主机上将其命名为 wombat.copy。 你将输入这一行：
    -   `ftp> get wombat wombat.copy` (回车)

在大多数情况下，ftp 将通知你传输成功：
```text
200 PORT command successful.
150 Opening ASCII mode data connection for wombat (7014 bytes)
226 Transfer complete
7224 bytes received in 0.8 seconds (8.8 Kbytes/sec)
ftp>
```

### 16.5 发送文件

使用 ftp，你还可以从本地主机向远程主机发送文件——这是上一节所述操作的逆过程。这是通过 put 命令完成的。

1.  **指定文件类型。** 记住，ftp 区分包含文本的 ASCII 文件和包含其他类型信息（如图形、音频等）的二进制文件。 通过在 ftp 提示符下输入 ascii 或 binary 选择正确的文件传输模式：
    -   `ftp> ascii` (回车)

    ftp 程序将确认你的选择：
    -   `200 Type set to A.`
    -   `ftp>`

2.  **发送文件。** 输入 put 命令，后跟原始文件的名称，然后是你想要给远程副本起的名称。 例如，假设你想从本地主机发送文件 meeting.events 的副本，并且你想在远程主机上将其命名为 meeting.events.copy。 你将输入这一行：
    -   `ftp> put meeting.events meeting.events.copy` (回车)

    ftp 将通知你传输成功：
    ```text
    200 PORT command successful.
    150 Opening ASCII mode data connection for meeting.events
    226 Transfer complete
    local: meeting.events   remote: meeting.events.copy
    2878 bytes received in 0.033 seconds (86 Kbytes/sec)
    ftp>
    ```

### 16.6 结束 ftp 会话

一旦你在远程主机上的工作完成，你应该结束 ftp 会话。

-   **退出 ftp 程序。** 在 ftp 提示符下输入 quit：
    -   `ftp> quit` (回车)

    你将看到一个 UNIX shell 提示符：
    -   `$`

### 16.7 一种快捷方法

运行 ftp 会话有一种更快的方法：

1.  **输入 ftp 命令，后跟远程机器的 Internet 地址。** 因此，如果你在主机 farhost.xyz.edu 上有账户，你将键入：
    -   `$ ftp farhost.xyz.edu` (回车)

2.  **像往常一样登录到你的远程账户。** 这将需要你在相应的提示符下输入你的登录名和密码。

3.  **完成后，使用 quit 命令关闭连接。**
    -   `ftp> quit` (回车)

    这将登出并退出 ftp。 你应该看到一个 UNIX shell 提示符：
    -   `$`

### 16.8 使用匿名 ftp 获取文件

最初，ftp 旨在允许你在拥有账户的两台计算机之间传输文件。 然而，匿名 ftp 允许你从没有账户的主机获取文件。 这些主机被称为公共 ftp 服务器。

例如，Internet 网络信息中心——称为 InterNIC——是 AT&T、通用原子公司（General Atomics）和网络解决方案公司（Network Solutions, Inc.）的联合运营机构，作为 Internet 操作信息的中央清算所。 InterNIC 提供了大量你可以通过匿名 ftp 获取的信息。

1.  **启动 ftp 程序并指定你需要的服务器。** 例如，要访问 InterNIC 的公共 ftp 服务器 ds.internic.net，你将输入命令：
    -   `$ ftp ds.internic.net` (回车)

