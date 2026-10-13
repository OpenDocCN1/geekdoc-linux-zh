
## 步骤 1
在终端上输入命令删除下面列出的用户：

```
[root]@deep /# userdel shutdown
[root]@deep /# userdel halt
[root]@deep /# userdel news
[root]@deep /# userdel uucp
[root]@deep /# userdel operator
[root]@deep /# userdel games
```
如果不使用 X Server，请删除此用户。

```
[root]@deep /# userdel gopher
[root]@deep /# userdel ftp
```
如果不使用 ftp 匿名服务器，请删除此用户。

## 步骤 2
在终端上输入命令删除下面列出的组：

```
[root]@deep /# groupdel adm
[root]@deep /# groupdel ip
[root]@deep /# groupdel news
[root]@deep /# groupdel uucp
[root]@deep /# groupdel games
```
如果不使用 X Server，请删除此组。

```
[root]@deep /# groupdel dip
[root]@deep /# groupdel ppupers
[root]@deep /# groupdel popusers
```
如果不使用 pop 服务器发送邮件，请删除此组。

```
[root]@deep /# groupdel slipipers
```

### 步骤 3
向系统添加新用户：

- 在你的系统中添加新用户，使用命令：
```
[root]@deep /# useradd username
```

## 22. 禁止任何人进入 root

`su`（切换用户）命令允许你变成系统上的其他用户。例如，你可以临时变成“root”并以超级用户“root”的身份执行命令。如果你不想让任何人进入 root 或想限制某些用户使用“su”命令，可以在 `/etc/pam.d/su` 文件中设置以下两行。我们建议限制人员使用“su”账户。

### 步骤 1
编辑 `su` 文件（`/etc/pam.d/su`）并在顶部添加以下行：

```
auth sufficient /lib/security/pam_rootok.debug
auth required /lib/security/pam_wheel.so group=wheel
```

添加上述两行后，`/etc/pam.d/su` 文件应该如下：

```
#PAM-1.0
auth sufficient /lib/security/pam_rootok.debug
auth required /lib/security/pam_wheel.so group=wheel
auth required /lib/security/pampwdb.shadow nullok
account required /lib/security/pampwdb.so
password required /lib/security/cracklib.so
password required /lib/security/pampwdb.shadow nullok authtok
session required /lib/security/pampwdb.so
session optional /lib/security/pamxauth.so
```

这意味着只有 `wheel` 组的用户才能 `su` 到 `root`，这也包括登录。注意，“wheel” 组是你系统上可用于此目的的特殊账户。你不能使用任何组名来实现此技巧。此技巧与允许 `root` 登录的 TTY 设备相结合，将提高你系统的安全性。

### 步骤 2
既然我们在 `/etc/pam.d/su` 配置中定义了“wheel”组，现在是时候将某些用户添加到“su”到“root”账户了。如果你想让用户 `admin` 成为“wheel”组的成员并能够 `su root`，执行以下命令：

```
root@deep# usermod -G wheel admin
```

其中“G”意味着用户所属的摘要组列表。“10”是用户 ID “wheel”的数值值，“admin”是我们想要添加到“wheel”组的用户。对上述命令适用于你系统上的所有用户，使其能够 `su` “root”账户。

## 23. 资源限制

位于 `/etc/security/` 目录下的 `limits.conf` 文件可用于控制和限制系统的资源。为所有用户设置资源限制是非常重要的，这样他们无法无法拒绝服务攻击（进程数、内存量等）。这些限制将在他们登录时生效。例如，你系统中所有用户的限制可能如下所示：

### 步骤 1
编辑 `limits.conf` 文件（`/etc/security/limits.conf`）并添加或更改行：

- `* hard core 0`
- `* hard rss 5000`
- `* hard nproc 20`

这表示关于核心文件的创建“core 0”，将进程数限制为 20 “nproc 20”，并将除超级用户“root”以外的所有人的内存使用限制为 5M “5000”。以上仅通过系统登录提示的用户。通过此配额，你对用户的进程、核心文件和内存使用有了更多控制。星号 `*` 表示：登录服务器的用户。

### 步骤 2
你必须编辑“etc/pam.d/login” 文件并在底部添加以下行：

`required`。在添加上述行后，`/etc/pam.d/login` 文件应该如下：

```
%PAM-1.0
auth required /lib/pam.d/security.so
auth required /lib/pam.d/pwdb.so shadow nullok
auth required /lib/pam.d/login.so
account required /lib/pam.d/pwdb.so
password required /lib/pam.d/cracklib.so
password required /lib/pam.d/pwdb.so nullok authtok md5 shadow
session required /lib/pam.d/pwdb.so
```

```
session required /lib/security/pam_limits.so
#session optional /lib/security/pam_console.so
```

关于此书的意见和建议请邮件至 `gmourani@videotron.ca`

## 24. 挂载文件系统的控制

你可以通过一些实用的选项如 `noexec`、`nodev` 和 `nousid` 来控制如“home”和“tmp”等分区的文件系统挂载。这些可以在 "/etc/fstab" 文本文件中设置。`fstab` 文件描述了关于各种文件系统选项的信息；每行对应一个文件系统。

`fstab` 文件中与安全选项相关的信息有：

- `defaults` 允许在这些分区上编辑（配额 `quota`、读写权限 `rw` 和 `suid`）。
- `noquota` 不在此分区上设置磁盘配额。
- `nousid` 不在此分区上设置 SUID/GID 访问权限。
- `nodev` 不在此分区上设置字符设备或特种设备访问权限。
- `noexec` 不允许在该分区上执行任何二进制文件。
- `quota` 允许在该分区上的用户使用磁盘配额。
- `ro` 允许在此分区上只读。
- `rw` 允许在此分区上读写。
- `suid` 允许在此分区上设置 SUID/GID 访问权限。

注意：有关可以在文件 (`fstab`) 中设置的选项的更多信息，请参阅关于 (8) 的 `man`页。

编辑 `fstab` 文件 (`/etc/fstab`) 并更改你的依赖：

```
/dev/sda1 /tmp ext2 defaults,nodev,noexec 1 2
/dev/home /home ext2 defaults/nousid 1 2
```

修改为：

```
/dev/sda1 /tmp ext2 rw,nodev,noexec 1 2
/dev/sda6 /home ext2 rw,nousid,1 2
```

这意味着对于 `<nodev>` 不解释字符设备或用户 ID 或组 ID 位以使其生效，对于 `<noexec>` 不允许在挂载的文件系统上执行任何二进制文件。请注意，如果我们在上述修改行中添加了 "rw" 选项，是因为这些行的默认选项是 "defaults"，这意味着设置了配额、读写和 suid，因此我们必须添加 "rw" 选项以继续对这些修改的文件系统拥有读写权限。

## 25. 将 RPM 二进制文件移动到安全位置或更改其默认权限

一旦你在 Linux 服务器上使用 `RPM` 命令安装了系统，为了获得更好的安全性，将其移动到安全的地方（如软盘或其他你选择的安全位置）是一个好主意。通过这种方法，如果有人访问你的服务器并意图使用 `RPM` 命令安装软件，他将无法做到。当然，如果你将来想通过 `RPM` 安装或升级新软件，你只需要将 `RPM` 二进制文件替换回原始目录即可。

- 要将 `RPM` 二进制文件移动到软盘，使用命令：
```
