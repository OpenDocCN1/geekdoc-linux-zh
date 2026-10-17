
# 安装 WU-FTPD

`# cd /usr/local/src/`

`# tar zxvf /tmp/wu-ftpd-2.6.tar.gz`

3. 这将创建一个名为 `/usr/local/src/wu-ftpd-2.6` 的目录。使用以下命令将当前目录切换到该新目录：

`# cd wu-ftpd-2.6`

4. 阅读 `INSTALL` 文件以确认安装所需的步骤。此处列出的步骤适用于 2.6 版本，但对于更新版本可能有所更改。您可以使用以下命令阅读该文件：

`# less INSTALL`

5. 使用 `configure` 工具配置源代码以进行编译：

`# ./configure`

如果 `configure` 运行无误，它将生成一个为您的系统量身定制的名为 `Makefile` 的文件。

6. 使用以下命令编译软件：

`# make >& make.out`

命令中的 `>& make.out` 部分会将所有输出重定向到 `make.out` 文件。您可以使用 `tail -f make.out` 命令监视该文件中不断新增的数据，编译完成后该文件仍会保留。这样，如果编译失败，您可以稍后查阅该文件。

7. 如果编译成功，请使用以下命令安装编译后的软件：

`# make install`

8. 此命令将安装以下二进制文件，并将 WU-FTPD 的手册页安装到 `/usr/man/` 目录中：

- `/usr/sbin/in.ftpd`
- `/usr/sbin/ftpshut`
- `/usr/bin/ftpcount`
- `/usr/bin/ftpwho`
- `/usr/sbin/ckconfig`
- `/usr/sbin/ftprestart`

9. 如果这是您首次安装 WU-FTPD，还会创建默认的 `/etc/ftpaccess` 和 `/etc/ftpconversions` 文件。

10. 按照本章后面“使用 ftpaccess 文件”一节中的说明自定义 `/etc/ftpaccess` 文件。

11. 默认的 `/etc/ftpconversions` 文件可以直接使用，无需任何自定义。要完全理解该文件，请参阅本章后面的“使用 ftpconversions 文件”一节。

12. 检查 `/etc/inetd.conf` 中是否有类似以下内容的一行：

`ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd -l -a`

13. 如果 `inetd.conf` 中缺少此行，请添加该行，保存文件，然后按照第 8 章“Linux 进程管理与守护进程”中的说明，向 `inetd` 发送 `SIGHUP` 信号以重启它。

按照这些步骤安装后，您将拥有一个标准的受密码保护的 FTP 服务器。

### 测试新的 WU-FTPD 安装

安装 WU-FTPD 后，您应再次确认它是否正常运行。为此，请使用 Linux 发行版附带的 FTP 客户端连接到新的 FTP 服务器，并以已在 `/etc/ftpaccess` 中被授予 FTP 服务器访问权限的现有用户身份登录：

```
# ftp localhost

Connected to localhost.

220 linux.juxta.com FTP server (Version wu-2.6.0 (1) \
    Mon Apr 19 09:21:53 EDT 1999) ready.

Name (localhost:root):

331 Password required for username.

Password:

230 User username logged in.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp> pwd

257 "/home/username" is the current directory.

ftp> bye
```

如果您能够成功连接到服务器、登录并像示例中那样显示当前目录，则说明您已成功安装 WU-FTPD。

### 匿名 FTP 设置

当您拥有一个可正常运行的 FTP 服务器（无论是随发行版安装，还是从源代码编译而来）时，可以使用以下步骤将其配置为接受匿名访问：

> **注意：** 许多以二进制软件包形式安装 WU-FTPD 的 Linux 发行版会预先配置该软件以接受匿名连接。您可以通过以匿名用户身份连接到 FTP 服务器来确认这一点。

1. 创建一个用于匿名访问的用户。通常，该用户名为 `ftp`。您创建的账户应具有一个唯一的家目录。在大多数 Linux 系统上，这个家目录将是 `/home/ftp/`。您可以按照第 3 章“用户和组管理”中介绍的过程创建该用户和家目录。

2. 将您创建的用户的默认 shell 设置为 `/bin/false`。您可以通过编辑 `/etc/passwd` 文件来完成此操作，使用 `useradd` 或 `/sbin/vipw` 命令，并将 ftp 账户条目中的最后一个字段改为 `/bin/false`，如下面的 `/etc/passwd` 文件示例条目所示：

`ftp:x:14:50:Anonymous FTP User:/home/ftp:/bin/false`

3. 当有人以匿名用户或 ftp 用户身份登录时，服务器会执行 `chroot()`（更改根目录）系统调用，并将 ftp 用户的主目录更改为服务器的根目录。因此，ftp 用户主目录之外的任何内容对服务器和匿名用户都不可见。

4. 为了允许匿名用户执行有用的操作，请在 `/home/ftp/` 目录中创建一个受限环境，该环境包含支持一个可用 FTP 环境所需的最少工具。为此，首先创建以下目录：

- `/home/ftp/bin/`
- `/home/ftp/etc/`
- `/home/ftp/lib/`
- `/home/ftp/pub/`

5. 您可以使用以下命令创建这些目录：

```
mkdir /home/ftp/bin/
mkdir /home/ftp/etc/
mkdir /home/ftp/lib/
mkdir /home/ftp/pub/
```

> **注意**
>
> 您可以自由创建额外的目录。例如，许多 FTP 服务器会有一个 incoming 目录，匿名用户可以在其中上传文件。为此，您可以创建 `/home/ftp/incoming/` 目录。

> **警告**
>
> 仅在绝对必要时才创建 incoming 目录。incoming 目录可能很快就会成为第三方在互联网上进行可疑材料不道德传输的中转站。

6. 任何您希望允许匿名用户使用的命令（例如 `ls` 或 `cp`）都需要复制到 `/home/ftp/bin/`。要创建一个高度受限的环境，请将 `ls` 程序复制到此目录。如果希望支持即时压缩和解压缩，也请将必要的程序（如 `tar`、`compress` 或 `gzip`）复制到 `/home/ftp/bin/`。

> **警告**
>
> 请记住，匿名用户需要一个受限环境，因为他们相当于可以访问您系统一部分的未认证用户。只将必要的工具放在 `/home/ftp/bin/` 中。

7. `/home/ftp/etc/` 目录需要包含一个 `passwd` 文件和一个 `group` 文件。不要在这些文件中添加任何真实用户。`passwd` 文件应包含最少的条目，例如以下内容：

```
root:*:0:0::/
bin:*:1:1:::
ftp:*:14:50:::
```

8. 同样，一个最小的 `group` 文件应包含以下条目：

```
root::0:
bin::1:
daemon::2:
wheel::10:
ftp::50:
```
