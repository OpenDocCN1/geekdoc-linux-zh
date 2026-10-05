

# 第 18 章 OpenSSH：安全网络通信

如果远程系统的公钥存储在已知的 `known-hosts` 文件中，而当系统连接时，远程系统提供了不同的指纹，OpenSSH 将显示以下消息 且不完成连接：

```
@ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
@ IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
```

现在可能有人正在窃听你的通信（中间人攻击）！也可能是远程主机发送的 RSA 密钥发生了变化。
远程主机发送的 RSA 密钥指纹为：

```
f1:6f:ea:87:bb:1d:dc:e3:24:60:d3:25:b1:0a.
```

请联系您的系统管理员。
将主机密钥添加到 `/home/sam/.ssh/known_hosts` 以消除此消息。
`/home/sam/.ssh/known_hosts:1` 中的错误密钥：
针对 plum 的 RSA 密钥已更改，且您请求了严格检查。
主机密钥验证失败。

如果你看到此消息，你可能是中间人攻击的目标。然而，更有可能是远程系统上的某些内容发生了变化，导致你提供了新的指纹。请咨询系统管理员。如果无异常，请从指定文件中删除错误密钥（从倒数第三行开始删除）并尝试重新连接。你可以使用带有 `-R` 选项的 `ssh-keygen` 删除哈希后的条目。由于 OpenSSH 会验证你正在连接到正确的系统，你将需要首次身份验证（第 668 页）。按照最初连接到远程主机时的相同步骤操作。

# ssh：连接到远程系统或在其上执行命令

`[options]|user@host [command]:` 的格式为：

其中 `host`（你想要连接的 OpenSSH 服务器/远程系统的名称）是唯一必需的参数。`host` 可以是本地名称、互联网上系统的完全域名（FDN，第 1149 页）或 IP 地址。使用命令 `ssh host` 可以以与本地系统相同的用户名登录远程主机。当你想要使用与本地系统不同的用户名登录时，请包含 `user@`。根据服务器的设置情况，你可能需要提供密码。

**打开远程 shell**：如果不带命令，`ssh` 将你登录到主机。远程系统会显示 shell 提示符，你可以在主机上运行命令。输入命令 `exit` 关闭与主机的连接并返回本地系统的提示符。

在接下来的示例中，登录在 `dog` 上的 Sam 使用 `ssh` 登录到 `plum`，执行 `who am i` 命令显示他所登录的系统 IP 地址，并使用 `exit` 关闭到 `plum` 的连接并返回本地系统的提示符：

```
sam@dog:~ $ ssh plum
sam@plum's password:
Linux plum 6.2.27-generic #1 SMP Aug 23 23:20:09 UTC 2008 i686
...
Last login: Mon Jan 18 22:00:13 2010 from 192.168.0.12
sam@plum:~ $ who am i
sam@plum:~ $ exit
2010-01-23 14:19 (192.168.0.12)
logout
Connection to plum closed.
sam@dog:~$
```

**运行命令**：当你包含 `command` 时，`ssh` 会登录主机、执行命令、关闭到主机的远程连接并将控制权交回本地系统。远程系统永远不会显示 shell 提示符。

下面的示例在远程系统 `plum` 的 `memos` 目录下运行 `ls`。该示例假设运行命令的用户（Sam）在 `plum` 上有登录，且 `memos` 目录是 Sam 在 `plum` 上的目录：

```
sam@dog:~ $ ssh plum ls memos
sam@plum's password:
memo.0921
memo.draft
sam@dog:~$
```

在下一个示例中，假设本地系统（`dog`）上的工作目录下有一个名为 `memos.new` 的文件。你不记得该文件是否包含更改，或者你是否在本地系统上做了这些更改，并在 `plum` 上运行了 `diff memo.draft`。你可以将 `memo.draft` 复制到本地系统并对两个文件运行 `diff`（第 168 页），但这样你就会在两个系统中散布三个文件的副本。如果你在完成后没有不小心删除旧副本，几天后你可能再次感到困惑。与其复制文件，你可以使用 `ssh`：

```
sam@dog:~ $ ssh plum cat memos/memo.draft | diff memos.new
```

当你运行 `ssh` 时，远程系统上命令的标准输出将传递给本地 shell，就像该命令在本地系统上运行一样。对于所有 shell 命令，你必须对不想让本地系统解释的特殊字符加引号。在前面的示例中，`plum` 上命令的输出通过管道发送到 `diff`（运行在 `dog` 上），它比较本地文件 `memos.new` 和标准输入（`-`）。下面的命令行具有相同效用，但会导致 `diff` 在远程系统上运行：

```
sam@dog:~ $ cat memos.new | ssh plum diff - memos/memo.draft
```

远程系统上 `diff` 的标准输出传到本地 shell，由其在屏幕上显示（因为它没有被重定向）。

# 选项

本节描述了与 `ssh` 使用的一些选项。

-   `-C`：启用压缩。（在 `ssh` 的版本中，`-C` 禁用压缩，`+C` 启用压缩。）
-   `-f`：在前台运行。（在 `ssh` 的版本中，`-f` 在后台运行，`-n` 在前台。）
-   `-L`：端口转发。（更多信息请参见第 681 页“隧道/端口转发”。）
-   `-l`：以指定用户登录。
-   `-n`：重定向标准输入到 `/dev/null`。（在后台运行 `ssh` 时，`-n` 是必需的。）
-   `-N`：不执行远程命令。（当需要在后台运行 `ssh` 时配合 `-f` 选项使用。）
-   `-o`：指定选项（在配置文件中的格式，第 674 页）。
-   `-p`：指定端口。
-   `-t`：分配伪终端。
-   `-v`：详细模式。显示关于连接的调试信息。
-   `-x`：关闭代理转发。
-   `-Y`：开启代理转发。

# scp：从远程系统复制文件

`scp`（安全拷贝）工具通过网络从一个系统向另一个系统复制文件或目录。它使用与 `ssh` 相同的验证机制；因此在需要时会请求密码。`scp` 命令的格式为：

```
scp [[user@]from-host:]source-file [[user@]to-host:][destination-file]
```

其中 `from-host` 是复制的源系统，`to-host` 是复制的目标系统。如果没有指定主机，`scp` 假设为本地。你可以通过 `user@` 指定不同的用户。`source-file` 是要复制的文件，`destination-file` 是生成的副本。确保你对写入的文件有写权限，对拷贝的目标目录有权限。你可以指定绝对路径（相对路径相对于指定的或隐式的用户目录）。当 `source-file` 是目录时，你必须使用 `-r` 选项复制其内容。当 `destination-file` 是目录时，每个源文件将保持其文件名。如果目标文件缺失，`scp` 假设为用户主目录。

在下面的示例中，Sam 使用 `scp` 将 `plum` 上 `sls` 账户的 `memo.txt` 复制到本地工作目录下的 `alemos`。如果 `alemos` 不是目录名，`memo.txt` 将被复制并重命名为 `alemos`。

```
sam@dom:$ scp sls@plum:memo.txt alemos
sls@plum's password:
memo.txt 100 4084KB 4.0MB/s 00:01
```

随着传输进行，百分比和字节数增加，剩余时间减少。

在下一个示例中，Sam 在 `peach` 上工作时，将上一个示例中的文件复制到 `speedy` 上的 `old` 目录。为了使此示例生效，Sam 必须能够无密码通过 `ssh` 登录 `speedy`。更多信息请参见第 667 页“授权密钥：自动登录”。

```
sam@peach:$ scp sls@plum:memo.txt speedy-old
sls@plum's password:
```

