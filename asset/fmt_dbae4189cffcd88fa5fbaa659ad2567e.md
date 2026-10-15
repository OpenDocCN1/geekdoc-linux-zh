
`export -f trash_file`

在用户启动配置中创建的导出函数充当了功能更强大的别名。

由于函数是用命令声明的，因此可以“动态”地重新定义或使用 `unset -f` 丢弃。在脚本中，这是一种危险的做法，因为删除或重新定义函数会让你的脚本难以调试。当脚本因为错误意外停止时，很难知道在停止时定义了哪个版本的函数。

结构良好的脚本会在脚本顶部创建函数，并使用 `readonly` 命令设置只读属性。

```bash
readonly -f trash_file
```

只读函数无法取消设置或重新定义。

可以使用 `declare` 和 `-F`（函数）开关列出当前函数。你可以使用 `-p` 开关列出完整的函数以及所有变量。

还可以使用旧的 Bourne shell 语法创建，即省略 "function" 关键字并在函数名后添加一对空括号。

## 参考部分

### `exec` 命令开关

- `-c`- 在运行新程序之前，让 `exec` 销毁所有变量
- `-l`- 像用户登录时运行的第一个程序一样运行该程序
- `-a`- 为 `$0` 指定一个不同的程序名称 `n`

### `crontab` 命令开关

- `-u user`- 列出要修改其 `crontab` 的另一个用户的名称
- `-l`- 列出当前的 `crontab`
- `-r`- 删除当前的 `crontab`
- `-e`- 使用默认编辑器编辑当前的 `crontab`

## Shell 安全

文件的所有者有权删除它。

每个文件都有一个权限数字，指示哪些用户可以访问它。

权限的每个位表示可以执行某些操作，如读取文件、写入文件或执行程序。

权限分为三组位。每组代表特定类型用户的访问权限。由于三位组成一个八进制（基8）数字，权限通常写为四个八进制数字。最右边的数字代表不属于任何类别的用户的权限：这些通常是“其他”或“世界”权限。右起第二个数字代表与文件同组的用户的权限。第三个数字代表所有者的权限。例如，`/tmp` 目录的权限数为 `777`，表示任何用户都有完全权限。

对于目录，读取访问表示读取目录内容的能力。写入访问允许用户在目录中创建新文件，实际上“写入”一个新的目录项。由于目录无法执行，执行权限只有在知道名称的情况下才能目录中运行程序。

每组三位中的位含义部分取决于文件类型。左侧位表示读取能力。中间位启用写入。右侧位启用执行文件，或者在目录的情况下，启用将当前目录移动到该目录的能力。常见的用户权限数 `755` 表示任何人都可以读取或执行，但只有文件所有者可以进行更改。

以下是位的拆解。

- `1` (八进制 `1`)—其他执行
- `2` (八进制 `2`)—其他写入
- `4` (八进制 `4`)—其他读取

## 了解你是谁 (`id`)

- `16` (八进制 `20`)—组写入
- `32` (八进制 `40`)—组读读
- `64` (八进制 `100`)—用户执行
- `128` (八进制 `200`)—用户写入
- `256` (八进制 `400`)—用户读取
- `512` (八进制 `1000`)—粘滞位 (Sticky bit)
- `1024` (八进制 `2000`)—设置 gid
- `2048` (八进制 `4000`)—设置 uid

`ls` 命令不显示八进制数字。相反，它显示位列表，当某个字母出现时，对应的比特位即为开启状态。减号表示该访问已关闭。

实际的 Linux 安全模型要复杂得多，有更多类型的 ID 数字，但这些不会影响脚本。第四个也是最左侧的权限数字代表特殊程序和目录的访问权限。这些将在本章稍后的 `chmod` 章节中介绍。通常，该数字为 `0`。

超级用户 `root` 或 `uid` 对所有文件具有完全访问权限。

## 了解你是谁 (`id`)

`id` 命令用于识别你的登录名称、组以及你所属的任何补充组。该命令同时显示名称和对应的数字。

```
$ id uid=503 (kburtch) gid=503 (kburtch) groups=503 (kburtch)
```

在当前会话下创建的任何文件都属于 `uid` 和组 `id`。

```
$ touch temp.txt
$ ls -l temp.txt
-rw-rw-r--
```

`id` 切换可以隐藏部分信息 `-user`（或 `-u`）切换只打印 `uid` 信息 `-group`（或 `-g`）切换只打印组信息 `-groups`（或 `-G`）切换只打印补充组信息 `-real`（或 `-r`）切换显示真实的、有效的 `uids` 或 `gids` `-name`（或 `-n`）切换只显示名称，不显示数值。

```
$ id -user -real -name
kburtch
```

## 转移所有权 (`chown`/`chgrp`)

Linux `chown`（更改所有者）命令更改文件的所有者。要执行 `chown`，你必须是该文件的所有者。只有 `root` 可以使用 `chown` 更改所有权。只要用户也是目标组的成员，普通用户可以使用它来更改组。

所有者可以是数字 `uid` 或是名称。

```
$ chown order_sys orders.txt
```

`--reference` 切换可以从另一个文件复制所有权。

```
$ chown --reference=last_orders.txt orders.txt
```

为了在切换中增加额外的安全性，`--from` 切换可以在更改新所有者之前验证旧所有者。`--reference` 和 `--from` 不能在同一个 `chown` 命令中组合。

```
$ chown --from=kburtch order_sys orders.txt
```

当所有者后面跟着冒号和组名时，`chown` 会同时更改所有者组。如果组部分缺失，组将设置为所有者的组。如果所有者部分缺失，则只更改所有者。也可以在 `--from` 切换中使用冒号指定组。

```
$ chown --recursive (or -R) nogroup orders.txt
```

`--recursive`（或 `-R`）切换递归更改子目录中的文件。`--changes`（或 `-c`）切换会宣布每次更改。`--verbose`（或 `-v`）切换提供更多信息。`--quiet`（或 `--silent` 或 `-f`）切换隐藏错误消息。`--dereference` 切换处理符号链接。

使用 `chown` 来是否可以访问脚本及其相关文件，以尽量减少隐藏脚本可能引起的问题。

避免在超级用户登录下运行脚本。在超级用户登录下运行的脚本可以更改任何文件的所有者。然而，如果你发现执行系统管理之外的任务必须使用超级用户登录，这说明文件的所有权是错误的。更改文件的所有者，甚至创建一个虚拟用户来拥有文件，而不是在超级用户登录下运行。超级用户脚本中的错误影响范围广泛、非常危险且难以追踪。

Linux `chgrp`（更改组）命令是 `group:group` 的简写形式。`chgrp` 仅更改组所有权。

## 更改访问权限 (`chmod`)

与 `chown` 更改文件所有权类似，Linux `chmod`（更改模式）命令更改文件的权限。该名称来自 Linux 术语 `mode`（模式），这是一个由权限位和其他文件信息组成的数字。尽管名称表明该命令可以更改任何模式设置，但此命令仅更改访问权限。

权限可以用两种方式表示。
首先，它们可以用四位八进制权限数表示。

```
$ touch orders.txt
$ ls -l orders.txt
-rw-r--r-- 1 ken      users      May 9 12:48 orders.txt
$ chmod 0755 orders.txt
$ ls -l orders.txt
-rwxr-xr-x 1 ken      users      May 9 12:48 orders.txt
```

对于不使用八进制数字的人，可以使用加号 (`+`) 添加权限，或使用减号 (`-`) 权限。权限按用户 (`u`)、组 (`g`)、其他 (`o`) 或所有 (`a`) 分组，并具有读 (`r`)、写 (`w`) 或执行 (`x`) 权限。因此，为文件和用户添加权限，你可以：

```
$ chmod 0000 orders.txt
$ ls -l orders.txt
       1 ken      users      May 9 12:48 orders.txt
$ chmod +r orders.txt
$ ls -l orders.txt
-r--r--r-- 1 ken      users      May 9 12:48 orders.txt
```

要从不是文件所有者且不在同一组的用户中删除写权限，你可以：

```
$ chmod a+rwx orders.txt
$ ls -l orders.txt
-rw-rwxrwx 1 ken      users      May 9 12:48 orders.txt
$ chmod o-w orders.txt
$ ls -l orders.txt
-rw-r--r-- 1 ken      users      May 9 12:48 orders.txt
```

等号会导致权限被设置而不是添加或减去。字母 `u`、`g` 和 `o` 分别代表用户、组和其他用户。例如，`g=u` 将组分配为与用户相同的组。

```
$ chmod 755 orders.txt
$ ls -l orders.txt
-rwxr-xr-x 1 ken      users      May 9 12:48 orders.txt
```

## 默认权限 (`umask`)

Bash 使用内置的 `umask` 命令来确定文件的默认访问权限。`umask`，即用户文件创建掩码，是一个表示哪些访问权限通常被禁止的数字。单独运行 `umask` 会以八进制数字显示当前的 `umask` 值，而 `-s` 选项则显示 `umask` 允许的哪些位位。

```
$ touch newfile.txt
$ ls -1 newfile.txt
-rw-rw- 1 kburtch kburtch      0 May 22 11:34 newfile.txt
$ umask
0022
$ umask -S
u=rwx,g=rwx,o=rx
```

在这个示例中，`umask` 被设置为 `2`，这意味着第 2 位（其他用户可以写入文件）通常应该是关闭的。`touch` 命令为所有用户提供了读取和写入权限，但不允许写入的其他用户除外。

你可以通过指定八进制数或权限字符串来创建新的 `umask` 值。

```
$ umask 0
$ rm newfile.txt
$ touch newfile.txt
$ ls -1 newfile.txt
-rw-rw-rw 1 kburtch kburtch      0 May 22 11:40 newfile.txt
```

当 `umask` 为 `0`（允许所有操作）时，`touch` 命令创建的文件可以被任何人读取或写入。

严格遵守 `umask` 命令完全取决于单个脚本或命令。Bash 内部没有内置用于程序检查 `umask` 值的程序。在脚本中，应用 `umask` 是麻烦的，因为 `umask` 和权限使用的是八进制表示法，但这是可以实现的，如列表 15.1 所示。

列表 15.1 `calculate_mode.sh`

```bash
#!/bin/bash
# calculate_mode.sh: 显示如何遵守 umask 的代码片段
DESIRED_MODE="$1"
# 从八进制转为十进制
DESIRED_MODE_DECIMAL=$(printf "%d" "$DESIRED_MODE")
# 获取 umask 并转换为十进制
UMASK_DECIMAL=$(printf "%d" "$umask")
# 反转 umask 中的位，使被设置的位成为允许的位
let UMASK_INVERT=$~UMASK_DECIMAL
# 只允许被 umask 允许的位
let "EFFECTIVE_MODE=DESIRED_MODE_DECIMAL & UMASK_INVERT"
# 转回八进制
MODE=`printf "%o" "$EFFECTIVE_MODE"`
printf "Desired mode = %s\n" "$DESIRED_MODE"
printf "Umask is %s\n" "$umask"
printf "Effective mode = %s\n" "$MODE"
```

在 `umask` 为 `2` 的情况下，所有人进行读取和写入的结果为：

```
$ sh calculate_mode.sh 666
Desired mode = 666
Umask is 0002
Effective mode = 664
```

如果使用了 `umask -p` 选项，`umask` 会打印出恢复当前 `umask` 值所需的 `umask` 命令。

## `setuid`/`setgid` 与脚本

有时，程序需要代表许多人执行操作。例如，Linux `cp` 命令代表计算机上的用户打印文件。与其与其在特定用户的所有权下运行程序，该程序可以以自己的权限（即创建者的权限）运行。为了实现这一点，Linux 提供了 `setuid` 和 `setgid` 权限。当设置这些权限时，程序将临时以其创建者的权限运行，而不是运行它的用户的权限。

`setuid` 和 `setgid` 权限在某些情况下是必要的，但它们也引入了安全漏洞。如果程序存在 Bug，它可能允许用户执行绕过正常系统安全的操作。当 `setuid` 或 `setgid` 程序代表超级用户执行操作时，这种情况尤其危险。

在在 Bash 脚本的情况下，Bash 会忽略脚本上的 `setuid` 和 `setgid` 位。脚本始终以运行脚本的用户的所有权运行。毕竟，脚本是数据，而不是以特定所有者身份运行的编译后的程序。

如果脚本必须以 `setuid` 或 `setgid` 运行，你可以创建一个简短的 C 语言“包装器”（wrapper）程序来运行脚本，然后在该 C 程序上设置 `setuid` 或 `setgid`。当包装器程序运行时，它以包装器所有者的身份运行，然后运行 Bash 脚本。

使用包装器有两个缺点。首先，从安全角度来看，除非大量用户需要该脚本，否则 `setuid` 可能会向太多人开放访问权限。在更改权限时，很容易忘记包装器。脚本也比编译后的程序对环境和 PATH 的变化更敏感。作为包装器程序的替代方案，考虑使用 Linux 的 `sudo` 命令。

其次，包装器给机器增加了额外负载，因为必须运行两个程序而不是一个。良好的做法是除非绝对必要，否则避免使用包装器，并尽可能尽可能的安全检查。

## `chroot` 命令

Linux `chroot` 命令仅供超级用户脚本可用。`chroot` 更改根目录 `/` 的显式位置。通过移动根目录，你可以将脚本可以访问的文件隔离到文件系统的特定部分。

`chroot` 可以应用于命令。要运行的命令必须出现在新的目录结构中，且路径应该是相对于新根目录的。

在这个示例中，`umask` 被设置为 `2`，这意味着第 2 位（其他用户可以写入文件）通常应该是关闭的。`touch` 命令为所有用户提供了读取和写入权限，但不允许写入的其他用户除外。

## 资源限制 (`ulimit`)

## 受限 shell (Restricted Shells)

当 Bash 以 `bash` 名称启动或提供 `-r` 选项运行时，会进入限制模式。受限 shell 防止脚本创建或访问当前目录之外的文件。特别是，受限 shell 具有以下限制：

- 使用 `cd` 切换目录
- 不设置或取消 `SHELL`、`PATH`、`ENV` 或 `BASH_ENV` 的值
- 不指定包含 `/` 的命令名
- 不将包含 `/` 的文件名作为 `-p` 选项的参数
- 不在启动时解析 `SHELLOPS` 的值
- 不使用 `>`、`|`、`>>` 重定向输出
- 不使用 `exec` 内置命令替换 shell
- 不使用 `-f` 和 `-d` 选项添加或删除内置命令
- 不指定内置命令的 `-p` 选项
- 使用 `+r` 或 `+o` 关闭限制模式

否则，受限 shell 的操作与普通 shell 相同。唯一的异常是函数定义无法在启动时导入

```
$ bash -r
$ cd
bash: cd: restricted
$ echo $DATE > temp.txt
bash: temp.txt: restricted: cannot redirect output
$ NOW="date"
$ printf "%s\n" "$NOW"
Thu Jul 5 16:59:28 EDT 2001
$ exit
exit
```

## 安全删除文件 (`wipe`)

`rm` 命令通过删除目录项来移除文件，旧信息仍然保留在磁盘上，直到有新文件覆盖它。通常情况下，除非在设备驱动级别，否则无法访问这些信息。然而，对于绝不能读取的关键信息，这可能是不可接受的。

`wipe` 工具首先用随机数据覆盖文件中的所有信息，然后像 `rm` 命令一样删除文件。磁盘上不会留下任何可以被心怀不轨的人读取的内容。

```
$ ls
logins.txt
$ wipe logins.txt
$
```
