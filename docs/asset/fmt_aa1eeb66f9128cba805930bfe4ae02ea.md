
# 16.2 文件传输协议 (ftp)

通过 `ftp`，计算机之间可以交换文件。底层协议定义在 `[rfc0959]` 中。在两个计算机之间交换数据时，可以区分两种基本的替代方案：

- 你在远程计算机上有一个用户 ID，既可以通过 `telnet` 登录，也可以通过 `ftp` 传输文件。²
- 你在远程计算机上没有用户 ID，但该计算机被设置为一个匿名 `ftp` 服务器。你可以以匿名或 `ftp` 身份登录，通常指定你的电子邮件地址作为密码。通常，你还可以使用短形式名称 `name@`，这种格式会被 `ftp` 服务器自动识别。

随后，你可以从这台计算机下载文件，或将文件上传到特殊目录（通常称为 `incoming`）。在管理员将这些文件集成到 `ftp` 目录后，其他用户就可以访问这些文件。在互联网上，这种方法被用于交换程序和文档。关于此主题的更多信息可以在 `[rfc1635]` 中找到。匿名 `ftp` 服务器在第 18 章中介绍。

你可以用计算机名称作为参数启动 `ftp` 程序，从而与该计算机建立直接连接；你也可以不带参数的情况下启动 `ftp`，这将让你进入命令模式（带有 `ftp>` 提示符）。`help` 显示可用命令的概览。列表 16.2 显示了一个 `ftp` 会话的示例。

## 列表 16.2 使用 ftp 传输文件

```
(Linux):> ftp corn

Connected to corn.

220 FTP server (version wu-2.4(1)) ready.

name (corn:jochen):jochen

331 Password required for jochen.

Password:

230 User jochen logged in.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp> bin

200 Type set to I.

ftp> hash

Hash mark printing on (1024 bytes/hash mark).

ftp> prompt

Interactive mode off.

ftp> lcd /tmp

Local directory now /tmp

ftp> get .emacs

200 PORT BINARY mode data connection for .emacs.

################

226 Transfer complete.

11557 bytes received in 0.0184 secs (6.1e+02 Kbytes/sec)

ftp> quit

221 Goodbye.
```

在第一步中，建立了与 `corn` 计算机的连接。使用用户名 `jochen` 和密码进行登录，因为远程计算机不允许匿名 `ftp`。数据传输应采用二进制模式（输入 `bin`），否则协议将尝试进行字符集转换。这通常会使归档和其他文件不可用。

`prompt` 命令在后续操作期间抑制对 `ftp` 客户端确认的请求。`cd` 命令更改 `ftp` 服务器上的另一个目录，而通过 `lcd` 更改本地目录。在最后一步，传输了文件 `.emacs` 并关闭了连接。

可以通过文件 `~/.netrc` 来对 `ftp` 程序进行配置。在该文件中，例如你可以为每个主机定义一系列命令，在（可能是自动的）登录后执行。列表 16.3 显示了一个示例。匿名 `ftp` 服务器在第 18 章中描述。

第一列，其后是选项和命令。一个条目可以跨多行，只要后续延续行以空格（空白或制表符）开头。

在列表 16.1 中，为计算机 `localhost` 和 `corn` 设置了二进制传输模式。此外，还更改了计算机 `corn` 上的中断字符。在激活后，所有选项都将通过 `telnet` 程序进行原型化。

请注意，所有信息（甚至是用户名和密码）都是通过网络传输的。如果具有 `tcpdump` 或类似工具的恶意用户在同一网络的一台机器上拥有 `root` 权限，他们可能会记录并滥用这些信息。目前有多种启用的 `telnet` 版本，但这些尚未广泛发布。由于美国现在允许加密技术出口，情况发生了变化。对于日常使用，我推荐使用 `ssh`；参见第 17.4 节。

# 426 网络应用程序

# 427 文件传输协议 (ftp)

# 16.3 r 工具

## 16.3.1 在远程计算机上执行程序

在本地计算机上运行 `rsh`。这是 GNU `getopt` 的一个特性，该工具被用于评估命令行选项和参数。

如果用户具有不同的账户（例如，在一台电脑上是 `hein`，在另一台电脑上是 `jhein`），可以使用 `-l` 在允许登录的计算机名称之前指定任何用户 ID。实用的选项包括 `-8` 用于 8 位容量的序列，`-E` 用于关闭对转义字符（通常是波浪号 `~`）的特殊处理。选项 `-e` 可用于为该字符指定一个替换字符。

```
(Linux):> rsh -- pea -l -d bin

drwxrxr-xr-x 2 hein staff 512 Jul 26 16:22 bin
```

### 列表 16.4 使用 rsh 在远程计算机上执行程序

某些 `rlog` 守护进程允许在 `.rhosts` 文件中指定 `+`。这允许具有相同用户名的用户登录，无论他们从哪台计算机调用登录。出于安全考虑，应该避免此类此类条目；某些守护进程会忽略此类条目。

列表 16.5 显示了文件 `~/.rhosts` 的示例。该文件应仅对个人用户可读。每行描述了一台允许无密码通过 `rsh`、`login` 或 `rcp` 访问的计算机。作为计算机名称，你应该指定 `/etc/hosts` 文件中的第一个条目或完全限定域名名 `FQDN`。如果你在不同的计算机上具有不同的 ID，可以输入一个用户名。

```
corn.example.org hein

pea.example.org jhein
```

### 列表 16.5 文件 ~/.rhosts 的示例

系统管理员可以通过在每台计算机的 `/etc/hosts.equiv` 文件（列表 16.6）中输入所有本地计算机的名称，将计算机（在本地网络中）设置为相等权限。然而，这对于集中管理计算机和用户的网络才有意义。

`/etc/hosts.equiv` 文件不用于用户 ID `root` 的访问，因此在这种情况下需要额外的 `~/.rhosts` 文件。在需要集中管理的本地网络中，这可以极大方便操作，例如，它允许使用 `rdist`（见第 16.6 节）。

# 430 网络应用程序

```
corn.example.org

-carrot.example.org

cabbage.example.org  sven
```
