
因为您对 ~/ftp/incoming 目录没有读取权限，所以您不应该能够使用 ls 命令查看您上传的文件。但是，如果您提供正确的文件名，仍然可以下载已上传的文件。

## 增强匿名 FTP 安全

创建匿名 FTP 站点本身就是一种安全风险，而拥有可上传目录会增加这种风险。然而，许多组织多年来一直成功运行匿名 FTP 服务器，因此不要过于气馁——只需谨慎即可。以下是增强匿名 FTP 服务器安全性的一些指南：

- 确保 /etc/passwd 中的 ftp 账户使用无效密码。例如，您在 passwd 文件中的 ftp 账户条目应如下所示：
  `ftp:*::14:50:FTP User:/home/ftp:/bin/true`
- ~/ftp/bin 目录应由 root 所有，而不是 ftp 账户。您在 ~/ftp/bin 目录中的二进制文件，如 ls、compress 和 tar，也必须由 root 用户拥有。~/ftp/bin 目录及其内容应仅可执行。运行以下命令以确保 ~/ftp/bin 目录中的所有文件仅可执行：
  `chown -R root.root ~/ftp/bin; chmod -R 111 ~/ftp/bin`
- ~/ftp/etc 目录应由 root 用户拥有，并且必须仅可执行。您可以使用以下命令使其如此：
  `chown -R root.root ~/ftp/etc; chmod 111 ~/ftp/etc`
- ~/ftp/etc 目录的内容必须只读并且必须由 root 拥有。运行以下命令以确保权限设置正确：
  `chown -R root.root ~/ftp/etc; cd ~/ftp/etc; chmod 444 *`
- 切勿将您的 /etc/passwd 或 /etc/group 文件复制到 ~/ftp/etc 目录中。~/ftp/etc/passwd 和 ~/ftp/etc/group 文件是虚拟文件，因为服务器 chroot 到 ~ftp，所以在 ~ftp 作为根目录运行时，需要这些文件来满足查找它们的程序。
- 作为一般安全规则，请确保 ~ftp 中的任何文件或目录都不是由 ftp 用户拥有的。

## 创建访客 FTP 账户

访客 FTP 账户是一个具有真实用户名和密码的真实账户。当访客用户登录到 FTP 服务器时，服务器会对访客用户的 home 目录执行 chroot 操作，从而使访客用户的 home 目录看起来像整个文件系统。

设置访客账户最简单的方法是使用 anonftp 包，即使您不想提供匿名 FTP 服务。只需暂时安装该包以创建单个访客账户即可。以下是创建访客账户所需的步骤：

### 1. 创建访客用户账户。
以 root 身份登录并以创建真实用户账户相同的方式创建访客用户账户。此示例假设该访客用户账户名为 mrfrog，并且它是通过通常的 useradd 命令创建的，如下所示：

```
useradd mrfrog
```

为 mrfrog 设置所需的密码，使用以下命令：

```
passwd mrfrog
```

### 2. 停止 Telnet 访问。
使用以下命令将 mrfrog 的默认 shell 更改为 /bin/true：

```
chsh mrfrog
```

系统提示输入新的 shell 路径时，输入 `/bin/true`。这禁止 mrfrog 通过 telnet 登录系统，以确保 mrfrog 不能使用 telnet 访问服务器并浏览其他用户或系统文件。

编辑 /etc/passwd 文件并在现有 home 目录路径后附加 /./。例如，如果 /etc/passwd 文件中有类似以下的行：

```
mrfrog:$1$dev33vylewv.:516:519:/home/mrfrog:/bin/true
```

则将其更改为：

```
mrfrog:$1$dev33vylewv.:516:519:/home/mrfrog/./:/bin/true
```

./ 序列用于告诉 FTP 服务器对 /home/mrfrog 目录执行 chroot 操作。

编辑 /etc/shells 文件并在文件末尾添加 /bin/true。这使 /bin/true 程序成为有效的 shell 选项。请注意，/bin/true 程序不执行任何操作，并在运行后立即退出。这使其成为需要验证但拒绝用户任何操作然后退出的 shell 的良好候选者。因为退出 shell 会注销用户，所以在尝试 Telnet 连接时，用户永远没有机会做任何事情。

### 3. 安装 anonftp 包。
如果您系统上已安装 anonftp 包，请跳过此步骤并转到第 4 步。否则，获取最新的 anonftp 包并通过运行 rpm 命令安装它：

```
rpm -ivh anonftp-2.6.1-1386.rpm
```

您的 anonftp 包名称将根据系统架构和 anonftp 版本而有所不同。此外，如果您还没有 FTP 服务器，例如 wu-ftpd，anonftp 包将无法安装。

### 4. 将 anonftp 包文件复制到访客用户的 home 目录。
将目录更改为 ~ftp 并使用以下命令将所有文件和目录复制到 ~mrfrog：

```
tar cvf - * | ( cd ~mrfrog ; tar xvf - )
```

您真正需要的只是 ~ftp/bin、~ftp/etc 和 ~ftp/lib 目录。您可以删除 ~ftp/pub 目录或您在 ~ftp 目录中可能已有的任何其他目录。

### 5. 更新 ~mrfrog/etc/passwd 和 ~mrfrog/etc/group 文件。
编辑 ~mrfrog/etc/passwd 文件并删除 FTP 用户的行。附加来自 /etc/passwd 文件的 mrfrog 的确切密码行。但是，删除 mrfrog 的密码并将其替换为 * 以使其无效。例如：

```
mrfrog:$1$dev33vylewv.:516:519::/home/mrfrog/./:/bin/true
```

此行需要复制到 ~mrfrog/etc/passwd，并且密码需要替换，使该行看起来如下：

```
mrfrog:*:516:519::/home/mrfrog/./:/bin/true
```

修改 ~/mrfrog/etc/group 文件并添加在 /etc/group 中找到的 mrfrog 行。这假设您没有以某种方式禁用 Red Hat 的默认功能，即为与新用户同名的用户自动创建私有组。换句话说，当您使用 useradd 程序创建用户时，它会自动为该用户创建具有相同名称的私有组。因此，当您创建 mrfrog 时，您也应该自动在 /etc/group 中创建了一个名为 mrfrog 的组。如果您更改了 useradd 程序的默认行为或手动创建了用户，请为该用户创建组并将其添加到 ~/mrfrog/etc/group 文件中。此外，从 ~/ftp/etc/group 文件中删除 ftp 组。

### 6. 设置目录和文件权限。
按如下方式更改目录/文件权限：

```
chown mrfrog.mrfrog ~/mrfrog
chmod 750 ~/mrfrog
```

chown 命令将用户和组所有权设置为 mrfrog 的用户和组。chmod 命令使 ~/mrfrog 目录仅对 mrfrog 用户和组可访问。

```
chown -R root.root ~/mrfrog/etc ~/mrfrog/bin ~/mrfrog/lib
```

此命令将 ~/mrfrog 下的 etc、bin 和 lib 子目录的所有权更改为 root 用户和组。

```
cd ~/mrfrog
chmod -R 111 *
```

第一个命令将目录更改为 ~/mrfrog，第二个命令使所有文件和目录对每个人仅可执行。

```
cd etc; chmod 444 *
```

这些命令将目录更改为 ~/mrfrog/etc 目录并将文件权限更改为对每个人只读。

### 7. 在 /etc/ftpaccess 中设置 guestgroup。
因为您希望真实用户 mrfrog 成为访客用户，所以您需要将 mrfrog 的组（也称为 mrfrog）添加到 guestgroup 组列表中。例如，

```
guestgroup mrfrog
```

允许 /etc/group 中找到的 mrfrog 组的任何成员成为访客用户。换句话说，FTP 服务器将执行 chroot 操作。对于 mrfrog 用户，FTP 服务器将 chroot 到 /home/mrfrog。

### 8. 测试账户。
FTP 到服务器并以 mrfrog 身份登录。如果一切设置正确，您将只看到该用户的 home 目录。尝试上传文件或创建目录。您应该被允许执行这些操作。然而，mrfrog 是否被允许删除、覆盖或重命名文件取决于您在 /etc/ftpaccess 中为这些操作设置的权限。例如，默认的 /etc/ftpaccess 包含以下行：

```
chmod  no  guest,anonymous
delete  no  guest,anonymous
overwrite  no  guest,anonymous
rename  no  guest,anonymous
```

这些行禁止访客账户执行 chmod、delete、overwrite 或 rename 操作。如果您希望允许访客账户执行这些操作，请从这些行中的默认类型列表中删除 "guest"，并将它们更改为以下行：

```
chmod  no  anonymous
delete  no  anonymous
overwrite  no  anonymous
rename  no  anonymous
```

如果您不想保留 anonftp 包或不想在 FTP 服务器上拥有 anonftp 功能，请从适当的 (~ftp) 目录中删除包文件，或简单地运行以下命令：

```
rpm -e anonftp-2.6-1.i386.rpm
```

请不要忘记使用适当的文件名，因为您的版本或架构可能与刚才描述的不同。

## 创建虚拟 FTP 站点
如果您有多个域并且需要支持单独的 FTP 服务器（ftp.domain-1.com、ftp.domain-2.com 等），您可以使用虚拟 FTP 服务，该服务允许您共享单个服务器系统以
