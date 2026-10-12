
如果用户打开了新的 bash shell，则过程是：`~/.bashrc -> /etc/bashrc`。如果用户登录到非 Bash 会话，则执行 `/etc/profile` 和 `~/.profile`，然后要么都不执行脚本，要么执行特定于该 shell 的脚本（例如 `~/.cshrc`、`/etc/csh.cshrc`）。

## 9.6.2 初始用户设置与默认值

`/etc/profile` 执行的步骤之一是建立 `umask` 值。`umask` 指令设置了默认文件权限。每当创建一个文件或目录时，其初始权限由 `umask` 值决定。每个用户都有自己的 `umask` 指令设置。在 `/etc/profile` 中，我们希望建立一个取决于用户是 `root` 还是其他人的 `umask` 值。`umask` 的格式为 `umask value`，其中 `value` 是三位数 777 或 666。

作为 `root`，我们希望为创建的所有文件建立 644，为所有目录建立 755。我们通过从 666 减去 644 以及从 777 减去 755 来获得 `umask` 值。即 777-755=002 且 666-664=022，因此 `root` 的 `umask` 为 022。对于普通用户，我们可能使用文件 664 和目录 775 的默认权限。看 777-775=002 和 666-664=002，我们为用户的 `umask` 使用 002。对于软件，我们也使用 002。

检查 `/etc/profile` 文件显示了设置 `umask` 的以下指令：

```
if [ $UID -gt 199 ] && [ "$(id -gn)" = "$(id -un)" ]; then
    umask 022
else
    umask 022
fi
```

该指令测试用户的 `UID` 以检查其是否大于 199，并检查用户的 ID 和组名是否匹配。操作 `-gn` 提供用户的组名，操作 `id -un` 提供用户的用户名。我们预期任何普通用户的这两个值都相等。如果 `UID` 大于 199 且用户名与组名相等，我们极可能是在处理一个普通用户，而不是 `root` 或软件账户。普通用户被赋予 002 的 `umask` 值（创建 775 和 664 的权限）。`root` 和软件被赋予 022 的 `umask` 值（创建 755 和 644 的权限）。

## 9.7 SUDO 命令

`sudo` 命令允许用户以其他身份执行命令。假设 `zappaf` 创建了一个可执行程序，可以读取其家目录下的数据文件。由于这些数据文件包含敏感信息，`zappaf` 设置了权限使得只有他可以访问。然而，该程序是他希望 `duke` 能够使用的。与其创建一个 `zappaf` 和 `duke` 都是成员的用户，`zappaf` 决定通过 `sudo` 命令赋予 `duke` 权限。现在，`duke` 可以通过 `sudo` 运行它。

`sudo` 命令的格式为：

```
sudo [-u username|uid] [-g groupname|gid] command
```

用户名/UID 或组 GID 是执行程序的所有者，而不是运行程序的用户。因此，例如，`duke` 可以执行 `sudo -u zappaf program`；`program` 是 `zappaf` 想要与他共享的程序。我们会注意到用户和组是可选的。

# 378 操作系统概念中的 Linux

作为建立系统管理程序访问权限的示例，让我们考虑 `groupadd` 指令。`groupadd` 指令的权限为 `rwx---`，因此其他人无法访问。`groupadd` 的用户和组所有者都是 `root`。因此，`root` 是唯一具有访问权限的用户。然而，`groupadd` 是一个相对无害的指令。也就是说，它不会干扰用户账户或组。因此，我们可以允许用户使用此指令。

该过程分为两个步骤。首先，系统管理员必须编辑 `/etc/sudoers` 文件。该文件的条目格式如下：

```
username(s) host=command
```

`username` 是允许访问 `sudo` 的用户的用户名。如果你没有列在 `username` 下，任何尝试通过 `sudo` 使用命令的尝试都将导致错误消息并记录该事件。若要指定多个用户，请用逗号分隔它们，但不要留空格。或者，你可以指定 `%users` 来指示系统的所有用户，或使用 `%group` 指定其他用户组。

`host` 是允许此 `sudo` 执行的主机值。你可以使用 `ALL` 来表示此 `sudo` 命令在网络系统的所有计算机上都有效，或者对于当前计算机使用 `localhost`。或者，你可以使用这台计算机的 `HOSTNAME`。

最后，命令应包含完整路径以及根据需要的选项和参数。如果你有多个命令，请用空格分隔它们。我们为 `groupadd` 的条目可以是：

```
%users localhost=/usr/bin/groupadd
```

编辑完成后，保存 `sudoers` 文件。

第二步是让用户发布命令。该命令是简单命令，前面带有 `sudo` 符号，例如 `sudo groupadd my_new_group`。`sudo` 程序要求用户提交其密码以确保获得授权执行该命令。此密码带有时间戳，因此以后使用 `sudo` 时将不再需要密码。后文会提到该时间戳可以重置。

既然用户可以创建自己的组了，他们就可以开始向这些组中添加用户了吗？`groupadd` 命令不允许将用户插入到组中。为此，我们需要提供对 `usermod` 的访问。我们只想提供对 `usermod -G` 的访问。

所以，现在我们再次修改 `sudoers` 文件。我们在 `sudoers` 文件中的条目可以是：

```
%users localhost=/usr/bin/usermod -G
```

用户现在可以执行命令：

```
sudo /usr/bin/usermod -G group1,group2 newuser
```

将 `newuser` 添加到 `group1` 和 `group2` 中。由于 `sudoers` 文件指定了 `-G` 选项，用户将无法执行带有其他选项的 `sudo` 命令。

# 用户账户 ■ 379

我们并不真的想为这两个命令中的任何一个提供 `sudo` 访问，因为它们构成了安全漏洞。假设我们让 `zappaf` 使用这两条指令。用户 `zappaf` 可以使用命令创建一个名为 `hackers` 的新组：

```
sudo /usr/sbin/groupadd -g 0 -o hackers
```

接着执行：

```
sudo /usr/sbin/usermod -G hackers zappaf
```
