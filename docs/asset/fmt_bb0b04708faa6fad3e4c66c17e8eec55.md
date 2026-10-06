
## 注意事项

你应该避免在没有按照此处描述先关机的情况下直接重启 Linux 系统。与 UNIX 不同，Linux 通过在内存中保留一个磁盘缓冲区集合来加速磁盘访问，这些缓冲区会定期写入磁盘（或在系统临时空闲时写入）。如果你在不将这些磁盘缓冲区写入磁盘的情况下关闭电源或重置系统，你将丢失这些缓冲区中的任何信息。运行 `shutdown` 会强制写入这些缓冲区。你可以在任何时候通过执行 `sync` 命令执行相同的操作；你应该连续执行两个 `sync` 命令，第二个命令可以保证第一个命令已将缓冲区写入磁盘。

`halt` 命令是 `shutdown -h now` 的同义词。`reboot` 命令是 `shutdown -r now` 的同义词。只有当你是系统上唯一的用户时，才使用这些命令。

## 第 15 章：系统管理

如果你在基于 Intel 的计算机上运行 Linux，任何用户都可以通过控制台使用 `CONTROL-ALT-DEL` 组合键强制重置硬件。你可以通过捕获此操作并向 `/etc/inittab` 中添加以下行来发出 `shutdown` 命令以安全重启电脑（你的发行版可能已经是这样配置的）：

```
ca::ctrlaltdel:/etc/shutdown -t3 -rf now
```

由于任何坐在控制台的人都可以使用 `CONTROL-ALT-DEL` 重启电脑，你可以通过在 `/etc/inittab` 中放置如下行来禁用此命令。

```
ca::ctrlaltdel:/bin/true
```

（`/bin/true` 命令会静默成功且不执行其他操作。）

## 可选项

作为超级用户（Superuser），你可以手动执行与 `shutdown` 相同的操作：

- 1. 使用 `cd` 将根目录 (`/`) 设置为工作目录。
- 2. 使用 `wall` (write all) 命令警告所有使用系统的用户注销。
- 3. 创建 `/etc/nologin` 文件并带有某些警告消息，以防止进一步的非根登录尝试。
- 4. 使用 `ps` 工具找到系统上运行的所有其他进程，并使用 `kill -TERM pid` 命令将其终止。如果之后还有剩余进程，使用 `kill -9 pid` 命令杀死剩余进程。
- 5. 执行命令 `sync`；执行 `sync` 并等待几秒。`sync` 工具在所有磁盘缓冲区写入磁盘之前就会返回。第二次 `sync` 并等待几秒可以让系统完成所有缓冲区的写入。
- 6. 执行命令 `unmount -a` 卸载所有挂载的设备。
- 7. 执行命令 `telinit -s` 将系统带入单用户模式，或仅重置或停止电脑。

## 崩溃

崩溃（Crash）是指系统在你不希望的情况下停止。崩溃后，你必须小心地启动操作系统，以尽可能地减少对文件系统可能的损坏。通常情况下，没有损坏或只有极小的损坏。

通常，文件系统在崩溃后会自动检查，因为它们在计算机启动之前没有被干净地挂载。这是通过 `rc.S` 脚本使用如下命令完成的

```
READWRITE=no

if echo -n >> "Testing filesystem status"; then

rm -f "Testing filesystem status"

READWRITE=yes
```

## 系统操作详细说明 595

```
# 检查所有文件系统的完整性

if [ ! $READWRITE = yes ]; then

/sbin/fsck -a

# 如果发生失败，进入单用户模式。

if [ $? -gt 1 ]; then

echo

echo "********************************************************************"

echo "fsck returned error code - REBOOT NOW!"

echo "********************************************************************"

echo

echo

/bin/login

fi

else

# 打印根文件系统不是只读的警告

fi
```

## 重要文件和目录 597

`/etc/group`
组允许用户共享文件或程序，而无需允许其获得整个系统的访问权限。如果多个用户正在处理非公开信息的文件，这种方案将非常有用。`/etc/group` 中的条目包含下面所示的四个字段。如果一个条目过长无法在一行内显示，请在行尾使用反斜杠 (`\`) 结束行，这将转义换行符，并在下一行继续该条目。

`group-name:password group-ID:login-name-list`

`group-name` 应该是八个字符或更少，可以是字母、数字和下划线的任意组合。`password` 是可选的加密密码。由于没有较好的方法向组文件中输入密码，组密码并不 Practical用，应避免使用。`group-ID` 是一个 0 到 65,535 之间的数字，其中 0–99 被预留。`login-name-list` 是属于该组的用户用逗号分隔的列表。这里显示了组文件一个示例条目。名为 `pubs` 的组没有密码，组 ID 为 101。

```
passwd::101:alex,jenny,scott,hlib,barbara
```

`/etc/passwd` 文件并不创建组。当用户在 `/etc/passwd` 文件中分配了一个组号时，组就会产生。`/etc/passwd` 文件将名称与每个组关联起来。

每个用户都有一个在 `/etc/passwd` 文件中分配的登录组。取决于你包含在 `/etc/group` 文件中的哪些 `login-name-lists`，你可能属于其他组。实际上，你同时属于你的登录组以及被分配给 `/etc/group` 的任何组。当你尝试访问一个你不拥有的文件时，操作系统会检查你的访问权限是否由该文件的组访问权限控制。如果你不是拥有该文件访问组的成员，你将受该文件公共访问权限的限制。

当你创建一个新文件时，它会被分配给你的登录组所属的组。如果你想创建或访问分配给另一个组的文件，请使用 `newgrp` 命令。`newgrp` 命令接受一个参数，该参数是你想要设置为当前组的组名。如果你没有提供参数，`newgrp` 将你的当前组重置为 `/etc/passwd` 中指定的组（你的登录组）。一旦你更改了组，你创建的任何新文件都属于新组。你可以随时使用 `id` 命令来确定当前当前是哪个组：

```bash
bash$
id=505(hls) gid=500(bravo) groups=500(bravo),9(sysop)
bash$newgrp sysop
bash$
id=505(hls) gid=9(sysop) groups=500(bravo),9(sysop)
```

## 598 第 15 章：系统管理

列在 `gid=` 之后的组是你当前的、或称为主组。你创建的任何文件都与此组关联。

**注意**
`newgrp` 命令的工作原理是每次运行时都会创建一个新的 shell。退出该新 shell 将带你回到你之前使用的 shell（和组）。如果你登录时间很长并频繁使用 `newgrp`，你可能会发现自己深陷在 shell 中，并在注销之前逐个退出每个 shell。

如果你在目录权限中设置了组 ID 位（第 80 页），那么在该目录中创建的所有文件将获得与目录相同的组。这是避免必须使用 `newgrp` 的方法，并可以设置为某些类型文件系统的默认行为。

- `/etc/mtab`
挂载表文件包含所有当前挂载设备的列表，命名为 `/etc/mtab`。当你不带任何参数调用 `mount` 时，`mount` 会查询此表并显示挂载设备列表。`mount` 和 `umount` 工具保持 `/etc/mtab` 的更新。

- `/etc/motd`
`/etc/motd` 文件包含当日消息（message of the day），每次有人登录时都会显示。该文件应该保持简短，因为用户往往会多次看到消息。通常 `/etc/motd` 由 `rc.m` 脚本自动创建。

- `/etc/pam.conf` 或 `/etc/pam.d/*`
`/etc/pam.conf` 文件指定了系统可能使用的 PAM（可插拔模块）应用程序的验证方法。或者，在 `/etc/pam.d` 目录下可能独立的配置文件。如果 `/etc/pam.d` 存在，则忽略 `/etc/pam.conf`。除非你了解如何配置 PAM，否则更改 `/etc/pam.conf` 或 `/etc/pam.d/*` 的内容可能会导致你的系统无法使用。目前只有少数 Linux 使用 PAM。

- `/etc/passwd`
`/etc/passwd` 中的每个条目占一行，有七个字段，描述系统的一个用户。冒号分隔每个字段与相邻字段。

```
login-name:password:user-ID:group-ID:comment:directory:program
```

`login-name` 是用户的登录名——用户在响应登录提示时输入的名称。`password` 是用户密码的加密副本，或者如果使用了影子密码（第 600 页），则为字符 `x`。虽然允许空密码字段，但为了更好的安全，请确保每个账户都有密码。

## 重要文件和目录 599

`user-ID` 是一个从 0 到 65,535 的数字，00 表示超级用户（Superuser），0-99 按惯例预留。`group-ID` 标识用户为组的成员；一个 0 到 65,535 之间的数字，其中 0–99 被预留。`comment` 是各种程序（如 `finger` 和计费程序）用于识别用户的信息。通常它包含用户的全名。`directory` 是用户主目录的绝对路径。如果 `program` 不存在，则假设为 `/bin/sh`（通常链接到 `/bin/bash`）。你可以使用你选择的任何 shell 的绝对路径，包括 `/bin/bash`、`/bin/tcsh` 和 `/bin/zsh`。为 root 密码文件留出 shell 是个主意。`content` 字段存储了：

| login-name | password | user-ID | group-ID | comment | directory | program |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Root | | 0 | 0 | | / | /bin/sh |
| jenny | | 101 | 50 | Jenkins | /home/jenkins | /bin/zsh |
| alex | | 102 | 50 | Alex | /home/alex | /bin/bash |
| scott | | 104 | 500 | Scott | /home/scott | /bin/tcsh |
| helen | | 105 | 500 | Helen | /home/helen | /bin/bash |
| who | | 1000 | | | /home/who | /who |

`/etc/passwd` 中的条目并不创建组。当用户在 `/etc/passwd` 文件中分配了一个组号时，组就会产生。`/etc/passwd` 文件将名称与每个组关联起来。

每个用户都有一个在 `/etc/passwd` 文件中分配的登录组。取决于你包含在 `/etc/group` 文件中的哪些 `login-name-lists`，你可能属于其他组。实际上，你同时属于你的登录组以及被分配给 `/etc/group` 的任何组。当你尝试访问一个你不拥有的文件时，操作系统会检查你的访问权限是否由该文件的组访问权限控制。如果你不是拥有该文件访问组的成员，你将受该文件公共访问权限的限制。

当你创建一个新文件时，它会被分配给你的登录组所属的组。如果你想创建或访问分配给另一个组的文件，请使用 `newgrp` 命令。`newgrp` 命令接受一个参数，该参数是你想要设置为当前组的组名。如果你没有提供参数，`newgrp` 将你的当前组重置为 `/etc/passwd` 中指定的组（你的登录组）。一旦你更改了组，你创建的任何新文件都属于新组。你可以随时使用 `id` 命令来确定当前当前是哪个组：

```bash
bash$
id=505(hls) gid=500(bravo) groups=500(bravo),9(sysop)
bash$newgrp sysop
bash$
id=505(hls) gid=9(sysop) groups=500(bravo),9(sysop)
```

## 598 第 15 章：系统管理

列在 `gid=` 之后的组是你当前的、或称为主组。你创建的任何文件都与此组关联。

**注意**
`newgrp` 命令的工作原理是每次运行时都会创建一个新的 shell。退出该新 shell 将带你回到你之前使用的 shell（和组）。如果你登录时间很长并频繁使用 `newgrp`，你可能会发现自己深陷在 shell 中，并在注销之前逐个退出每个 shell。

如果你在目录权限中设置了组 ID 位（第 80 页），那么在该目录中创建的所有文件将获得与目录相同的组。这是避免必须使用 `newgrp` 的方法，并可以设置为某些类型文件系统的默认行为。

- `/etc/mtab`
挂载表文件包含所有当前挂载设备的列表，命名为 `/etc/mtab`。当你不带任何参数调用 `mount` 时，`mount` 会查询此表并显示挂载设备列表。`mount` 和 `umount` 工具保持 `/etc/mtab` 的更新。

- `/etc/motd`
`/etc/motd` 文件包含当日消息（message of the day），每次有人登录时都会显示。该文件应该保持简短，因为用户往往会多次看到消息。通常 `/etc/motd` 由 `rc.m` 脚本自动创建。

- `/etc/pam.conf` 或 `/etc/pam.d/*`
`/etc/pam.conf` 文件指定了系统可能使用的 PAM（可插拔模块）应用程序的验证方法。或者，在 `/etc/pam.d` 目录下可能存在独立的配置文件。如果 `/etc/pam.d` 存在，则忽略 `/etc/pam.conf`。除非你了解如何配置 PAM，否则更改 `/etc/pam.conf` 或 `/etc/pam.d/*` 的内容可能会导致你的系统无法使用。目前只有少数 Linux 使用 PAM。

- `/etc/passwd`
`/etc/passwd` 中的每个条目占一行，有七个字段，描述系统的一个用户。冒号分隔每个字段与相邻字段。

```
login-name:password:user-ID:group-ID:comment:directory:program
```

`login-name` 是用户的登录名——用户在响应登录提示时输入的名称。`password` 是用户密码的加密副本，或者如果使用了影子密码（第 600 页），则为字符 `x`。虽然允许空密码字段，但为了更好的安全，请确保每个账户都有密码。

## 重要文件和目录 599

`user-ID` 是一个从 0 到 65,535 的数字，0 表示超级用户（Superuser），0-99 按惯例预留。`group-ID` 标识用户为组的成员；一个 0 到 65,535 之间的数字，其中 0–99 被预留。`comment` 是各种程序（如 `finger` 和计费程序）用于识别用户的信息。通常它包含用户的全名。`directory` 是用户主目录的绝对路径。如果 `program` 不存在，则假设为 `/bin/sh`（通常链接到 `/bin/bash`）。你可以使用你选择的任何 shell 的绝对路径，包括 `/bin/bash`、`/bin/tcsh` 和 `/bin/zsh`。为 root 密码文件留出 shell 是个主意。`content` 字段存储了：

| login-name | password | user-ID | group-ID | comment | directory | program |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Root | | 0 | 0 | | / | /bin/sh |
| jenny | | 101 | 50 | Jenkins | /home/jenkins | /bin/zsh |
| alex | | 102 | 50 | Alex | /home/alex | /bin/bash |
| scott | | 104 | 500 | Scott | /home/scott | /bin/tcsh |
| helen | | 105 | 500 | Helen | /home/helen | /bin/bash |
| who | | 1000 | | | /home/who | /who |
