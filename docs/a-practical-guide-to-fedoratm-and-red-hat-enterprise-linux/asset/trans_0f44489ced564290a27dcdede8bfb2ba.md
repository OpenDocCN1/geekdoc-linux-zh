
(page 732) 设为 YES。当服务器设置为允许 ASCII 传输时，客户端通过使用 ascii、binary 或 cr 命令（第 722 页）来控制是否映射换行符。

## FTP 特定事项

本节介绍了使用 ftp 的详细信息。

## 格式

ftp 命令行的格式如下：

```
ftp [options] [ftp-server]
```

其中 options 是下一节列表中的一项或多项选项，ftp-server 是你想要交换文件的 FTP 服务器的名称或 IP 地址。如果你未指定 ftp-server，则在 ftp 运行后，你需要使用 ftp open 命令连接到一个服务器。

## 命令行选项

-   -g (globbing) 关闭通配符展开。参见 glob（第 723 页）。
-   -i (interactive) 关闭使用 mget（第 722 页）和 mput（第 722 页）进行文件传输时的提示。另请参见 prompt（第 723 页）。
-   -n (no automatic login) 禁用自动登录（第 720 页）。
-   -v (verbose) 提供更多关于 ftp 工作原理的信息。显示来自服务器的响应，并报告文件传输的速度。另请参见 verbose（第 724 页）。

## FTP 命令

ftp 实用程序是交互式的：启动 ftp 后，它会提示你输入命令以设置参数或传输文件。只要缩写是唯一的，你就可以使用命令的缩写形式。可以通过 help 命令（第 724 页）获取程序帮助。

## 外壳命令
!command

如果没有指定 command，则会在本地系统上启动（生成）一个外壳（shell）。完成使用本地外壳后，使用 CONTROL-D 或 exit 返回到 ftp。在感叹号后跟 command 仅执行该命令；当命令执行完毕时，ftp 将显示 ftp> 提示符。由于 ftp 由此命令启动的外壳是正在运行 ftp 的外壳的子进程，因此你在此外壳中做的任何更改在返回 ftp 时都不会被保留。具体来说，当你要将文件复制到除了启动 ftp 所在的目录之外的本地目录时，你需要使用 ftp lcd 命令来更改本地工作目录；在启动的外壳中发出 cd 命令将不会实现你期望的更改。请参阅第 718 页的“Local cd (lcd)”示例。

### 传输文件

在以下描述中，*remote-file* 和 *local-file* 可以是路径名。

-   **append *local-file* [*remote-file*]**
  
  将 *local-file* 追加到远程系统上同名文件中，如果指定了 *remote-file*，则追加到 *remote-file*。

-   **get *remote-file* [*local-file*]**
  
  将 *remote-file* 复制到本地系统，命名为 *local-file*。如果没有指定 *local-file*，ftp 将在本地系统使用 *remote-file* 作为文件名。

-   **mget *remote-file-list***
  
  （多文件获取）将多个文件复制到本地系统，每个文件保留其原始文件名。你可以直接命名远程文件或使用通配符（参见 **glob**）。使用 **prompt**（第 723 页）在传输期间关闭提示。

-   **mput *local-file-list***
  
  （多文件上传）将多个文件复制到服务器，每个文件保留其原始文件名。你可以直接命名单个本地文件或使用通配符（参见 **glob**）。使用 **prompt**（第 723 页）在传输期间关闭提示。

-   **newer *remote-file* [*local-file*]**
  
  如果 *remote-file* 的修改时间比 *local-file* 更新，或者 *local-file* 不存在，则将 *remote-file* 复制到本地系统，命名为 *local-file*。如果没有指定 *local-file*，ftp 将在本地系统使用 *remote-file* 作为文件名。此命令类似于 **get**，但不会用旧文件覆盖较新的文件。

-   **put *local-file* [*remote-file*]**
  
  将 *local-file* 复制到远程系统，命名为 *remote-file*。如果没有指定 *remote-file*，ftp 将在远程系统使用 *local-file* 作为文件名。

-   **reget *remote-file* [*local-file*]**
  
  如果 *local-file* 存在且小于 *remote-file*，则假设之前对 *local-file* 的 **get** 操作被中断，并继续从之前 **get** 停止的地方开始。如果没有指定 *local-file*，ftp 将在本地系统使用 *remote-file* 作为文件名。当大文件的 **get** 在传输中途失败时，此命令可以节省时间。

### 状态

-   **ascii**
  
  将文件传输类型设置为 ASCII。**ascii** 要起作用，**cr** 命令必须处于 ON 状态（第 720 页）。

-   **binary**
  
  将文件传输类型设置为二进制（第 720 页）。

-   **bye**
  
  关闭与服务器的连接并终止 ftp。与 **quit** 相同。

-   **case**
  
  切换并显示大小写映射状态。默认值为 OFF。当为 ON 时，对于 **get** 和 **mget** 命令，此命令将服务器上全大写的文件名映射为本地系统上的全小写。

-   **close**
  
  关闭与服务器的连接，但不退出 ftp。

-   **cr (carriage RETURN)**
  
  切换并显示（回车）RETURN 去除状态。仅在文件传输类型为 ascii 时有效。将 cr 设为 ON（默认值）以去除 Windows 使用的 RETURN/LINEFEED 行终止序列中的 RETURN 字符，从而生成标准的 Linux 行终止 LINEFEED。将 cr 设为 OFF 以保留换行符不变（第 720 页）。

-   **debug [n]**
  
  切换/设置并显示调试状态/级别，其中 n 为调试级别。OFF 或 0（零）为默认值。当 n > 0 时，ftp 显示其发送给服务器的每个命令。

-   **glob**
  
  切换并显示 mdelete（第 724 页）、mget（第 722 页）和 mput（第 722 页）命令的文件名展开（第 165 页）状态。

-   **hash**
  
  切换并显示井号（#）显示状态。当为 ON 时，ftp 每传输 1024 字节的数据块就显示一个井号。

-   **open [hostname]**
  
  指定 hostname 作为要连接的服务器名称。如果没有 hostname，则提示输入服务器名称。此命令在连接超时或其他失败时很有用。请参阅第 718 页的示例。

-   **passive**
  
  在被动（PASV——默认）和主动（PORT）传输模式之间切换，并显示传输模式。更多详情请参阅第 715 页的“被动与主动连接”。

-   **prompt**
  
  切换并显示提示状态。当为 ON（默认值）时，mdelete（第 724 页）、mget（第 722 页）和 mput（第 722 页）在传输每个文件之前都会要求确认。将 prompt 设为 OFF 以关闭这些提示。

-   **quit**
  
  关闭与服务器的连接并终止 ftp。与 bye 相同。

-   **umask [nnn]**
  
  将应用于服务器上创建文件的 umask（第 469 页）更改为 nnn。如果没有 nnn，则显示 umask。

-   **user [username] [password]**
  
  提示或接受允许你在服务器上登录的用户名和密码。当使用 -n 选项调用时，ftp 会自动提示输入用户名和密码。更多详情请参阅第 720 页的“自动登录”。

### 目录

-   **cd remote-directory**
  
  将服务器上的工作目录更改为 remote-directory。

-   **cdup**
  
  将服务器上的工作目录更改为工作目录的父目录。

-   **lcd [local_directory]**
  
  [local change directory] 将本地系统上的工作目录更改为 local_directory。如果没有参数，此命令将本地系统上的工作目录更改为你的主目录（正如不带参数的 cd 外壳内置命令一样）。请参阅第 718 页的“Local cd (lcd)”示例。

### 文件

-   `chmod` *mode* *remote-file*
  
  将服务器上 *remote-file* 的访问权限更改为 *mode*。有关如何指定 *mode* 的更多信息，请参见第 193 页的 `chmod`。

-   `delete` *remote-file*
  
  从服务器上删除 *remote-file*。

-   `mdelete` *remote-file-list*
  
  （多文件 *delete*）从服务器上删除 *remote-file-list* 指定的文件。

### 显示信息

-   `?` (question mark)
  
  与 `help` 相同。

-   `dir` [*remote-directory* \| *file*]
  
  显示服务器上 *remote-directory* 的列表。如果未指定 *remote-directory*，则显示工作目录。如果指定了 *file*，列表将保存在本地系统中名为 *file* 的文件中。

-   `help` [*command*]
  
  显示关于 *command* 的信息。如果没有 *command*，则显示本地 `ftp` 命令列表。也即 `?`。

-   `ls` [*remote-directory* \| *file*]
  
  类似于 `dir`，但对于某些服务器会产生更简洁的列表。如果指定了 *file*，列表将保存在本地系统中名为 *file* 的文件中。

-   `pwd`
  
  显示服务器上工作目录的路径名。使用 `!pwd` 显示本地工作目录的路径名。

-   `rstatus`
  
  显示本地系统（客户端）的 `ftp` 连接和状态信息。

-   `status`
  
  显示远程系统（服务器）的 `ftp` 连接和状态信息。

-   `verbose`
  
  切换并显示详细模式，该模式显示来自服务器的响应并报告文件传输的速度。此命令的效果与在命令行上指定 `-v` 选项相同。

## 配置 FTP 服务器 (vsftpd)

本节介绍如何配置由 Fedora/RHEL 提供的 `vsftpd` 守护进程实现的 FTP 服务器。

### 先决条件

安装以下软件包：

-   `vsftpd`

运行 `systemctl` 使 `vsftpd` 服务（`vsftpd` 守护进程）在每次系统进入多用户模式时启动，然后启动 `vsftpd` 服务。使用 `systemctl` status 命令确保服务正在运行。

