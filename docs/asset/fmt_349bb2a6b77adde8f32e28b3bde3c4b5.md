
Thu Mar 11 14:24:00 PST 2010

接下来 Sam 使用 `sudo` 卸载一个文件系统。由于他在上一个 `sudo` 命令后的 15 分钟内执行了此命令，他不需要提供密码：

```
$ sudo umount /
```

现在 Sam 使用 `-l` 选项检查哪些命令允许他运行。因为他是系统上注册的第一个用户（因此是 `admin` 组的成员），他被允许作为用户运行任何命令。

```
$ sudo -l
User may run the following commands on this host:
(ALL) ALL
```

### 启动 root shell

当你有多个命令需要以 root 权限运行时时，启动一个 root shell 可能会更容易，直接给出命令而无必在每个命令前输入 `sudo`，并退出 shell。这种技术绕过了 `sudo` 的某些安全措施，请谨慎使用，并尽快返回 shell（参见第 420 页）。使用 `-i` 选项启动 root shell：

```
$pwd
/home/sam
$ sudo -l
$ id
uid=0(root) gid=0(root) groups=0(root)
$pwd
/root
$ exit
```

在此示例中，`sudo` 启动了一个 root shell，提示你正在以 root 权限运行。该工具显示运行它的用户身份。`exit` 命令返回你的普通 shell。`-i` 选项启动用于 root（或通过 `-u` 指定的用户）的 `/etc/passwd` 中的 shell，运行 root 的（或该用户的）启动文件，存在某些例外（例如，`TERM` 不是命令）。它不带参数。

另一种处理 `sudo` 运行命令输出重定向的方法是使用 `tee`（第 254 页）：

```
$ ls tee /root/sam
```

此命令将 `ls` 的输出写入文件但同时也显示出来。如果你不想显示输出，可以让特权 shell 将输出重定向到 `/dev/null`（第 489 页）。下一个示例使用这种技术消除屏幕，并使用 `-a` 选项追加到文件而不是覆盖：

```
$ ls tee -a /root/sam > /dev/null
```

# 选项

你可以使用命令行选项来控制 `sudo` 如何运行命令。以下是 `sudo` 命令的语法：

`sudo [options] [command]`

其中 `options` 是一个或多个选项，`command` 是你想执行的命令。在没有 `-u` 选项的情况下，`sudo` 以 root 权限运行命令。下面是一些常用选项；完整列表见 `sudo` 手册。

- `-b` (background)：在后台运行命令。
- `-e` (edit)：使用此选项时，`command` 是文件名而非命令。此选项允许 `sudo` 使用通过通过 `SUDO_EDITOR`、`VISUAL` 或 `EDITOR` 环境变量指定的编辑器编辑命名的文件。（它默认使用 `nano`）。或者你可以使用 `sudoedit` 工具并带有任何选项。
- `-i` (initial login environment)：启动用于 root（或通过 `-u` 指定的用户）的 `/etc/passwd` 中的 shell，运行 root 的（或该用户的）启动文件，存在某些例外（例如，`TERM` 不是命令）。它不带参数。
- `-k` (kill)：重置运行命令的时间戳，这意味着用户下次运行 `sudo` 时必须输入密码。
- `-L` (list defaults)：列出可以在 `sudoers` 文件的 `Defaults` 行中设置的参数。它不带参数。
- `-l` (list commands)：列出运行 `sudo` 的用户允许在本地系统运行的命令。它不带参数。

- (shell) 根据 `/etc/passwd` 文件的指定启动一个新的 root（或通过 `-u` 指定的其他用户）shell。与 `-i` 类似，但不会改变环境。它不接受命令。
- `-user` 以指定用户的权限运行命令。如果不使用此选项，`sudo` 将以 root 权限运行命令。

## sudoers: 配置 sudo

在默认安装状态下，如果不进行完全配置，`sudo` 并不像完全配置后那样安全和健壮。`sudo` 配置文件为 `/etc/sudoers`。编辑 `sudoers` 的最佳方法是使用执行以下命令：`sudo visudo`。`visudo` 工具会仔细地锁定、编辑并检查 `sudoers` 文件的语法。默认情况下，`visudo` 会调用 `nano` 编辑器。你可以设置环境变量 `SUDO_VISUAL`、`VISUAL` 或 `EDITOR` 来让 `visudo` 调用以下命令：

```bash
export VISUAL=vi
```

将其替换为你选择的文本编辑器。将此命令放入启动文件（第 293 页）中，以便每次登录时都设置该变量。

## 始终使用 visudo 编辑 sudoers 文件

`sudoers` 文件中的语法错误可能会导致你无法使用 `sudo` 获取 root 权限。如果你直接编辑此文件（不使用 `visudo`），你将在发现无法使用 `sudo` 之前并不知道自己引入了语法错误。`visudo` 工具在允许你退出之前会检查 `sudoers` 的语法。如果它发现错误，会为你提供三种选择：修复错误、在不保存更改的情况下退出，或者保存更改并退出。最后一种选择通常是不明智的，因此 `visudo` 将其标记为 `(DAN!)`。

在 `sudoers` 文件中，以井号（`#`）开头的注释可以出现在行的任何位置。除了注释，该文件还包含两种类型的条目：别名（aliases）和用户权限规范（user privilege specifications）。每个条目都占据一行，可以通过以反斜杠（`\`）结尾来实现换行。

## 用户权限规范

指定用户权限的行格式如下（等号周围的空格可选可选）：

```
user_list host_list = (runas list) | command_list
```

- `user_list` 指定该规范适用于的用户。此列表可以包含用户名、组（以 `%` 前缀）和用户别名（见下一节）。
- `host_list` 指定该规范行适用于主机。此列表可以包含一个或多个主机名、IP 地址或主机别名（在下一节中讨论）。你可以使用内置的 `ALL` 别名使该行适用于除此 `sudoers` 文件之外的所有系统。

## 带有权限运行命令

- `runas_list` 指定了在带 `-u` 选项调用 `sudo`（第 426 页）时，哪些用户（s）可以运行 `command_list` 中的命令。此列表可以包含用户名、组（以 `%` 前缀）和 `runas` 别名（在下一节中讨论）。它必须包含在括号内。如果没有 `runas_list`，`sudo` 假设为 root。
- `command_list` 指定了该规范适用的内容。此列表可以包含用户名称。

如果你在名称后紧跟两个相邻的双引号（`""`），则该用户将无法指定任何命令行参数（包括选项）。或者，你可以指定参数（包括通配符），以限制用户允许使用的参数。

示例：该用户权限规范允许 Sam 使用 `sudo` 在由 `ALL` 指定的所有系统上挂载和卸载文件系统（以 root 权限运行 `mount` 和 `unmount`），包含此规范的 `sudoers` 文件如下：

```
ALL-(root)/bin/mount, /bin/unmount
```

`(runas)list` 是可选的。如果你省略了它，`sudo` 将允许用户以 root 权限运行 `command_list` 中的命令。在下面的示例中，Sam 利用了这些权限。他不能直接运行 `mount`；相反，他必须调用 `sudo` 来运行。

```bash
$ whoami
sam
$ mount /music
unmount: only root can mount /dev/sdb7 from /music
$ sudo mount /music
[sudo] password for Sam:
$
```

如果你将上述 `sudoers` 中的行替换为下行，Sam 将不被允许卸载 `/p03`，尽管他仍然可以挂载任何其他文件系统并可以使用任何文件系统：

```
sam ALL-(root)/bin/mount, /bin/unmount, /bin/unmount /p03
```

`sudoers` 中前一行的结果如下所示。`sudo` 工具没有提示密码，因为 Sam 在过去的 15 分钟内输入过密码。

```bash
$ sudo mount /p03
Sorry, user sam is not allowed to execute '/bin/unmount /p03' as root on localhost.
```

以下行限制 Sam 只能挂载和卸载挂载在 `/p01`、`/p02`、p03 和 `/p04` 的文件系统：

```
sam ALL-/bin/mount /p0[1-4], /bin/unmount /p0[1-4]
```

以下命令显示了结果：

```bash
$ sudo umount /music
```
