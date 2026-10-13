
如果 `WU-FTPD` 已安装，你可以直接跳到“配置服务器”部分。或者，你可能考虑按照后文节“安装和构建源码 RPM”中的说明，为你的系统定制 `WU-FTPD`。更好的方法是通过下载、编译并从源码发行版安装 `WU-FTPD` 的最新版本，该版本包含了最新的安全补丁和错误修复，具体方法见后文“安装和构建源码发行版”章节。

第 23 章提供了有关安装 RPM、编译源码 RPM 以及从原始源代码构建并安装程序的详细信息和步骤说明。

另一方面，如果你收到的消息是 `package wu-ftpd is not installed`，在继续本章内容之前，你至少安装二进制 RPM。

## 安装二进制 RPM

要从 Red Hat 安装 CD-ROM 安装 `WU-FTPD` 二进制 RPM，请按照以下步骤操作：

- 1. 以 root 用户身份登录或使用 `su` 变为 root。
- 2. 挂载 Red Hat Linux 安装 CD-ROM（磁盘 1）。
- 3. 输入以下命令安装 `WU-FTPD`（如果你的 CD-ROM 驱动器挂载点不同，请将 `/mnt/cdrom` 替换为实际挂载点）：
```
# rpm-ivh /mnt/cdrom/RedHat/RPMS/wu-ftpd*rpm
```
- 4. 继续“安装 anonftp 包”章节。

## 安装并构建源码 RPM

如果你选择安装并构建源码 RPM，请按照以下步骤操作：

- 1. 以 root 用户身份登录或使用 `su` 变为 root。
- 2. 挂载 Red Hat Linux 安装 CD-ROM（磁盘 2）。
- 3. 输入以下命令安装 `WU-FTPD`（如果你的 CD-ROM 驱动器挂载点不同，请将 `/mnt/cdrom` 替换为实际挂载点）：
```
# rpm -rebuild /mnt/cdrom/RPMS/wu-ftpd*src.rpm
# rpm -ivh /usr/src/redhat/RPMS/i386/wu-ftpd*rpm
```
- 4. 继续“安装 anonftp 包”章节。

## 安装并构建源码发行

从原始源代码安装和构建任何软件包是系统定制的最终步骤，因为你可以对配置和构建过程进行几乎完全控制。由于第 23 章详细讨论了从源码构建，本节仅向你展示执行构建和安装的命令。然而，它详细介绍软件配置。

## 第 13 章：配置 FTP 服务

你可以从 `http://ftp.wu-ftpd.org/pub/wu-ftpd` 下载源码发行版。在你下载源码 tar 包或从附带的 CD-ROM 中的本章源码目录复制 tar 包后，过程包括解压源码、根据你的需求进行配置、构建并安装。以下步骤将引导你完成该过程（你必须是 root 用户）：

- 1. 使用以下命令解压存档：
```
# cd /usr/local/src
# tar xzf /tmp/wu*ftpd*tar.gz
# cd wu-ftpd
```
- 2. 使用以下命令为你的系统配置软件：
```
# ./configure --prefix=/usr/local --enable-quota --enable-pam --disable-newlines --enable-restart-logging
```
尽管此命令在文中显示为两行，但应将其作为单行输入（在输入时它可能会换到下一行）。`--prefix=/usr/local` 将 `/usr/local` 设置为此版本的根目录：所有二进制文件和支持文件都安装在 `/usr/local` 的子目录下。`--enable-quota` 启用配额支持，当用户上传文件时强制执行磁盘使用限制。`--enable-pam` 启用对 PAM（可插身份模块）的支持，这可以增强系统安全性。`--disable-newlines` 抑制 `ftppd` 输出不必要的空行。`--enable-restart-logging` 让 `ftppd` 能更准确地记录客户端请求。

> 第 21 章提供了更多关于磁盘配额的信息。第 25 章详细解释了可插身份模块（Pluggable Authentication Modules）。

- 3. 输入以下命令开始编译：
```
# make
```
- 4. 构建完成后，使用以下命令安装软件：
```
# make install
```

安装完成后，继续下一节。

![](img/d1fb1ff3244ecb66d002a5e633e6f729_336_0.png)

## 安装 anonftp 包

如前所述，`anonftp` 包为匿名 FTP 创建了一个安全环境。特别是，它在 `/var/ftp` 中为匿名 FTP 创建了一个 `chroot` 环境，并将关键文件复制到 `/var/ftp/lib`、`/var/ftp/bin` 和 `/var/ftp/etc` 子目录。`chroot`（更改根目录）目录是一种类似于“监狱”的目录，它严重限制了用户对系统的视图。当远程用户以匿名或 `ftp` 身份登录 FTP 服务器时，FTP 守护进程 `ftpd` 会将用户放置在特殊目录 `/var/ftp` 中，该目录被更改为用户的根（/）目录 `/var/ftp` 及其子目录构成了用户对系统的整个视图，因为用户无法 `cd` 出该目录，因此无法看到真实文件系统的布局。然而，由于这些限制，必须将二进制文件、库和配置文件复制到 `chroot` 监狱中，用户才能执行某些命令。这种复制操作正是 `anonftp` 包所做的。

> FTP 服务器二进制文件的名称为 `/usr/sbin/ftpd`。为了方便起见，我在整个章节中称其为 `ftpd`。

如果命令 `rpm -q anonftp` 返回消息 `package anonftp not installed`，请按照以下步骤安装它：

- 1. 以 root 用户身份登录或使用 `su` 变为 root。
- 2. 挂载 Red Hat 安装 CD-ROM。
- 3. 输入以下命令安装 `WU-FTPD`（如果你的 CD-ROM 驱动器挂载点不同，请将 `/mnt/cdrom` 替换为实际挂载点）：
```
# rpm -ivh /mnt/cdrom/RedHat/RPMS/wu-ftpd*rpm
```

## 第13 章：配置 FTP 服务

`daemon`
`adm`
`lp`
`sync`
`shutdown`
`halt`
`mail`
`news`
`uucp`
`operator`
`games`
`body`

因此，为了防止用户 `bubba` 使用 FTP 登录，或者准确地说，防止用户 `bubba` 通过 FTP 登录到系统，请在 `/etc/ftpusers` 的末尾添加 `bubba`。列表 13-1 所示的默认条目应该足够，但如果您安装了某个软件包（例如数据库软件包），它需要一个或多个特殊用户账户，请考虑将这些账户添加到 `/etc/ftpusers` 中，以便对 FTP 服务器的访问保持严格的限制。

`/etc/fhosts` 文件的作用与 `/etc/ftpusers` 类似，用于限制 FTP 访问，但它更加灵活。`/etc/fhosts` 定义了每行一条访问规则，允许从登录源的主机访问 FTP 服务器。每条访问规则由 `allow`（允许）或 `deny`（拒绝）关键字、用户名以及或多个 IP 地址组成。访问规则的通用格式为：

```
allow username ipaddr [...]

deny username ipaddr [...]
```

`username` 标识规则适用的用户名，`ipaddr` 标识规则适用的 IP 地址。以 `#` 开头的行是注释，会被忽略。`allow` 规则仅允许 IP 地址与 `ipaddr` 匹配的主机以 `username` 登录 FTP 服务器。`deny` 规则则防止任何源主机 IP 地址与 `ipaddr` 匹配的连接使用 `username` 进行 FTP 登录。正如您预期的，如果 `username` 是 `anonymous`（匿名），则相应的规则适用于匿名 FTP 用户。可以通过空格分隔来指定多个 IP 地址。

例如，`allow bubba 192.168.0.1` 允许当连接来自 IP 地址 `192.168.0.1` 时，名为 `bubba` 的用户登录 FTP 服务器。相反，`deny` 规则防止当源连接为 `127.0.0.1` 时，名为 `kwall` 的用户登录。

需要注意的是 `/etc/fhosts` 中访问规则规范的一个特性。您可以使用 CIDR（无类域间路由路由）表示法或通过在 `ipaddr` 后附加冒号和子网掩码来指定 IP 地址范围。例如，要允许 `bubba` 从子网 `166.70.186.8` 中的任何 IP 地址登录，您可以将 `ipaddr` 指定为 `166.70.186.8:255.255.248` 或 `166.70.186.8/29`。因此，完整的规则将是以下之一：

```
allow bubba 166.70.186.8:255.255.248

allow bubba 166.70.186.8/29
```
