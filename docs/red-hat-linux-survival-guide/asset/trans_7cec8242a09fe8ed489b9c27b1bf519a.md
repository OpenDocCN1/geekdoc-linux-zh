
在完成这些步骤后，你应该以匿名用户身份通过 FTP 连接到服务器，并确保只能在指定的目录中上传文件。因为你对 `~ftp/incoming` 目录没有读取权限，所以你不应该能够使用 `ls` 命令看到你上传的文件。但是，如果你提供正确的文件名，你仍然能够下载已上传的文件。

## 安全性和匿名 FTP

创建匿名 FTP 站点本身就是一种安全风险，而拥有可上传目录则增加了更多风险。然而，许多组织多年来成功运行了匿名 FTP 服务器，因此不要过于气馁：只需谨慎即可。以下是增强匿名 FTP 服务器安全性的一些指导原则：

- 确保 `/etc/passwd` 中的 ftp 账户使用无效密码。例如，你在 passwd 文件中的 ftp 账户条目应如下所示：
  
  ```
  ftp:*::14:50:FTP User:/home/ftp:/bin/true
  ```
- `~ftp/bin` 目录应由 root 所有，而不是 ftp 账户。`~ftp/bin` 目录中你拥有的二进制文件如 `ls`、`compress` 和 `tar` 也必须由 root 用户拥有。`~ftp/bin` 目录及其内容应仅可执行，不应有更多权限。你可以运行以下命令以确保 `~ftp/bin` 目录中的所有文件仅可执行：
  
  ```
  chown -R root.root ~ftp/bin; chmod -R 111 ~ftp/bin
  ```
- `~ftp/etc` 目录应由 root 用户拥有，并且必须仅可执行。你可以使用以下命令来实现：
  
  ```
  chown -R root.root ~ftp/etc; chmod 111 ~ftp/etc
  ```
- `~ftp/etc` 目录的内容必须仅可读且由 root 拥有。运行以下命令以确保权限设置正确：
  
  ```
  chown -R root.root ~ftp/etc; cd ~ftp/etc; chmod 444 *
  ```
- 切勿将你的 `/etc/passwd` 或 `/etc/group` 文件复制到 `~ftp/etc` 目录中。`~ftp/etc/passwd` 和 `~ftp/etc/group` 文件是虚拟文件，由于服务器将 `~ftp` chroot 为根目录，运行在 `~ftp` 下的程序查找它们时需要这些文件。
- 最后，作为一般安全规则，确保 `~ftp` 中的任何文件或目录都不由 `ftp` 用户拥有。

## 创建访客 FTP 账户

访客 FTP 账户是一个具有真实用户名和密码的真实账户。然而，访客与真实 FTP 之间的唯一区别是，当访客用户访问 FTP 服务器时，她看不到自己主目录之外的任何内容。当访客用户登录 FTP 服务器时，服务器会对访客用户的主目录执行 chroot 操作，从而使访客用户的主目录看起来像整个文件系统。最大的优势是用户无法看到其他任何内容，例如系统文件和其他用户目录。这一安全特性值得花费时间来配置访客用户账户。除了配置访客账户所需的额外工作外，另一个牺牲是磁盘空间的冗余使用。就像匿名 FTP 用户一样，每个访客用户都必须拥有自己的二进制文件集，用于 ls、gzip 和 tar 等简单操作。然而，考虑到磁盘空间的成本每天都在降低，也许磁盘空间对大多数人来说并不是真正的问题。

最简单的方法是使用 anonftp 软件包来设置访客账户，即使你不想提供匿名 FTP 服务。只需临时安装该软件包以创建单个访客账户即可。以下各节将向你展示创建访客账户的步骤。

### 步骤 1：创建访客用户账户

以 root 身份登录并像创建真实用户账户一样创建访客用户账户。我假设此访客用户账户名为 mrfrog，并且它已使用通常的 useradd 命令创建如下：

```
useradd mrfrog
```

现在使用以下命令为 mrfrog 设置所需的密码：

```
passwd mrfrog
```

### 步骤 2：停止 Telnet 访问

现在使用以下命令将 mrfrog 的默认 shell 更改为 /bin/true：

```
chsh mrfrog
```

当提示输入新的 shell 路径时，输入 /bin/true。此命令禁止 mrfrog 通过 Telnet 登录系统并浏览其他用户文件或系统文件。毕竟，当此用户通过 FTP 服务器访问系统时，我们禁止所有这些操作。

现在编辑 /etc/passwd 文件并在现有主目录路径后附加 /./。例如，如果 /etc/passwd 文件中有一行如下：

```
mrfrog:1dev33vylewv.:516:519::/home/mrfrog:/bin/true
```

则将其更改为

```
mrfrog:1dev33vylewv.:516:519::/home/mrfrog/./:/bin/true
```

/./ 序列决定了 chroot() 函数执行的位置。

现在编辑 /etc/shells 文件并在文件末尾添加 /bin/true。此更改使 /bin/true 程序成为有效的 shell 选项。请注意，/bin/true 程序不执行任何操作，并在运行后立即退出。此特性使其成为需要验证但拒绝用户任何操作然后退出的 shell 的良好候选者。因为退出 shell 会注销用户，所以在尝试 Telnet 连接时，用户永远没有机会做任何事情。

### 步骤 3：安装 anonftp 软件包

如果你的系统上已安装 anonftp 软件包，请跳过此步骤并进入下一步。如果未安装，请获取最新的 anonftp 软件包并通过运行 rpm 命令进行安装：

```
rpm -ivh anonftp-3.0-6.i386.rpm
```

你的 anonftp 软件包名称根据系统架构和 anonftp 版本而有所不同。另请注意，如果你没有已安装的 FTP 服务器（如 wu-ftpd），则 anonftp 软件包不会安装。

### 步骤 4：将 anonftp 软件包文件复制到访客用户的主目录

将目录更改为 ~ftp 并使用以下命令将所有文件和目录复制到例如 ~mrfrog：

```
tar cvf - * | ( cd ~mrfrog ; tar xvf - )
```

mrfrog 真正需要的只是 ~ftp/bin、~ftp/etc 和 ~ftp/lib 目录。你可以删除 ~ftp/pub 目录或从你的 ~ftp 目录中删除任何其他目录。

### 步骤 5：更新 ~mrfrog/etc/passwd 和 ~mrfrog/etc/group 文件

现在编辑 ~mrfrog/etc/passwd 文件并删除 ftp 用户的行。从 /etc/passwd 文件中附加 mrfrog 的确切密码行。但是，删除 mrfrog 的密码并将其替换为 * 以使其无效。例如：

```
mrfrog:1dev33vylewv.:516:519::/home/mrfrog/./:/bin/true
```

将此行复制到 ~mrfrog/etc/passwd 并替换密码，使该行如下所示：

```
mrfrog:*:516:519::/home/mrfrog/./:/bin/true
```

现在，修改 ~mrfrog/etc/group 文件并添加在 /etc/group 中找到的 mrfrog 行。

![](img/9eb7e89292d2f85707b4d49102c865b7_447_0.png)

我假设你没有以某种方式禁用 Red Hat 的默认功能，即为与新用户同名的用户自动创建私有组。换句话说，当你使用 useradd 程序创建用户时，它会自动为该用户创建同名的私有组。因此，当你
创建 mrfrog 时，你也应该自动创建了一个名为 mrfrog 的组在 /etc/passwd。如果你更改了 useradd 程序的默认行为或手动创建了用户，请确保为该用户创建组并将其添加到 ~mrfrog/etc/group 文件中。此外，从 ~ftp/etc/group 文件中删除 ftp 组。

### 步骤 6：设置目录和文件权限

按如下方式更改目录/文件权限：

```
chown mrfrog.mrfrog ~mrfrog
chmod 750 ~mrfrog
```

chown 命令将用户和组所有权设置为 mrfrog 的用户和组。第二个命令使 ~mrfrog 目录仅对 mrfrog 用户和组可访问。

```
chown -R root.root ~mrfrog/etc ~mrfrog/bin ~mrfrog/lib
```

此命令将 ~mrfrog 下的 etc、bin 和 lib 子目录的所有权更改为 root 用户和组。

```
cd ~mrfrog
chmod -R 111 *
```

第一个命令将目录更改为 ~mrfrog，第二个命令使所有文件和目录仅对所有人可执行。

```
cd etc; chmod 444 *
```

这些命令将目录更改为 ~mrfrog/etc 目录并将文件权限更改为对所有人只读。

### 步骤 7：在 /etc/ftpaccess 中设置 guestgroup

因为我们希望真实用户 mrfrog 成为访客用户，所以我们需要将 mrfrog 的组（也称为 mrfrog）添加到 guestgroup 组
