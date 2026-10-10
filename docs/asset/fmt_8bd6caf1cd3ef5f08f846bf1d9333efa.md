
`setfattr` `[-h]` `-n` `name` `[-v` `value]` `pathname...` `setfattr` `[-h]` `-x` `name` `pathname...`

`setfattr` `[-h]` `--restore=file`

### 描述

`setattr` 命令为每个指定文件将新的 *value* 与扩展属性 *name* 关联起来。

### 选项

- `-n` `name`, `--name=name`：指定要设置的扩展属性的 `name`。
- `-v` `value`, `--value=value`：指定扩展属性的新值。有三种方法可用于编码 `value`。如果给定的字符串用双引号括起来，则内部字符串被视为文本。在这种情况下，反斜杠和双引号具有特殊含义，需要通过前导反斜杠进行转义。任何控制字符都可以编码为反斜杠后跟三个八进制 ASCII 码数字。如果给定的字符串以 `0x` 或 `0X` 开头，则表示十六进制 `number`。如果给定的字符串以 `0s` 或 `0S` 开头，则期望 base64 编码。另请参阅 `(1)` 中的 `--encoding` 选项。
- `-x` `name`, `--remove=name`：完全移除 `named` 扩展属性。
- `-h`, `--no-dereference`：不跟随符号链接。如果 `pathname` 是符号链接，则不跟随它，而是该符号链接本身是被修改的 inode。
- `--restore=file`：从 `file` 恢复扩展属性。文件必须处于由 `getfattr` 命令使用 `--dump` 选项生成的格式。如果给定的文件 `name` 是破折号 `(-)`，`setfattr` 将从标准输入读取。
- `--version`：打印 `setfattr` 的版本并退出。
- `--help`：打印帮助，解释命令行选项。
- `--`：命令行选项结束。其余所有参数都被解释为文件 `names`，即使它们以破折号字符开头。

### 作者

Andreas Gruenbacher, ‹› 和 SGI XFS 开发团队, ‹›。

请将这些地址用于发送您的错误报告或评论。

### 参见

`(1)`，和 `(5)`。

### SETLEDS

### 名称

`setleds` - 设置键盘指示灯

### 概要

`setleds` `[-v]` `[-L]` `[-D]` `[-F]` `[{+|-}num]` `[{+|-}caps]` `[{+|-}scroll]`

### 描述

`Setleds` 报告并更改 VT 的 led 标志设置（通常指 NumLock、CapsLock 和 ScrollLock）。如果没有参数，`setleds` 将打印当前设置。如果带有参数，它将设置或清除指定的标志（并保留其他标志不变）。如果提供了 `-v` 标志，则会报告更改前后的设置。

Led 标志设置对于每个 VT 是特定的（使用的是对应于标准输入的 VT）。

默认情况下（或使用选项 `-F`），`setleds` 仅更改 VT 标志（其设置可能通过键盘指示灯反映出来）。

使用选项 `-D` 时，`setleds` 将更改 VT 标志及其默认设置（因此随后的重置不会撤销更改）。对于始终希望开启 numlock 的人来说，这可能很有用。

使用选项 `-L` 时，`setleds` 不会触及 VT 标志，而只更改指示灯。从此刻起，指示灯将不再反映 VT 标志（而是显示放入其中的任何内容）。命令 `setleds -L`（无其他参数）将恢复指示灯反映 VT 标志的状态。

可以在 `/etc/rc` 中使用 `setleds` 来定义 NumLock 的初始和默认状态，例如：

```
INITTY=/dev/tty[1-8]
for tty in $INITTY; do setleds -D +num < $tty; done
```

### 选项

- `-num` `+num`

  清除或设置 NumLock。（目前，NumLock 设置影响小键盘按键的解释。按下 NumLock 键会反转 NumLock 设置。）

- `-caps` `+caps`

  清除或设置 CapsLock。（目前，CapsLock 设置在应用于字母时会反转 Shift 键。按下 CapsLock 键会反转 CapsLock 设置。）

- `-scroll` `+scroll`

  清除或设置 ScrollLock。（目前，按下 ScrollLock 键（或 ^S/^Q）会停止/启动控制台输出。）

### 错误

在键盘应用程序模式下，NumLock 键不会影响 NumLock 标志设置。

### 参见

`(1)`

### SETMETAMODE

### 名称

`settamode` - 定义键盘 ta 键处理

### 概要

`settamode` `{ta|bit|tabit|esc|prefix|escprefix}`

### 描述

如果没有参数，`settamode` 打印当前的 Meta 键模式。如果带有参数，它设置指示的 Meta 键模式。会报告更改前后的设置。

Meta 键模式对于每个 VT 是特定的（使用的是对应于标准输入的 VT）。可以在 `/etc/rc` 中使用 `settamode` 来定义 Meta 键模式的初始状态，例如：

```
INITTY=/dev/tty[1-8]
for tty in $INITTY; do settamode escprefix < $tty; done
```

### 选项

- `esc` `prefix` `escprefix`

  Meta 键发送一个 Escape 前缀。

- `ta` `bit` `tabit`

  Meta 键设置字符的高阶位。

### 参见

`(1)`

### SETPRIV

### 名称

`setpriv` - 使用不同的 Linux 权限设置运行程序

### 概要

`setpriv` `[options]` `program` `[argunts]`

### 描述

设置或查询在 `(2)` 过程中继承的各种 Linux 权限设置。

### 选项

- `—clear-groups`

  清除附加组。

- `-d`, `—dump`

  转储当前权限状态。可以多次指定以显示额外的、大多无用的信息。与其他所有选项不兼容。

- `—groups` `group`…

  设置附加组。参数是一个逗号分隔的列表。

- `—inh-caps` `(+|-)` `cap`… 或 `—bounding-set` `(+|-)` `cap`…

  设置可继承权限集或权限边界集。参见 `(7)`。参数是 `+cap` 和 `-cap` 条目的逗号分隔列表，分别添加或移除一个条目。`+all` 和 `-all` 可用于添加或移除所有权限。权限集初始化为当前的可继承集（针对 `—inh-caps`）和当前的边界集（针对 `—bounding-set`）。如果你从边界集中移除某项权限而没有同时从可继承集中移除，你很可能会感到困惑。不要这样做。

- `—keep-groups`

  保留附加组。仅在与 `—rgid`、`—egid` 或 `—regid` 一起使用时有用。

- `—list-caps`

  列出所有已知权限。此选项必须单独指定。

- `—no-new-privs`

  设置 `no_new_privs` 位。设置此位后，`(2)` 将不会授予新的权限。例如，setuid 和 setgid 位以及文件权限将被禁用。（执行设置了这些位的二进制文件仍然有效，但它们不会获得权限。某些 LSM，特别是 AppArmor，可能导致执行某些程序失败。）此位由子进程继承且无法取消设置。参见 `(2)` 和 Linux 内核源代码中的 `Documentation/:prctl/:no:_new_:privs.txt`。

  `no_new_privs` 位自 Linux 3.5 起得到支持。

- `—rgid` `gid`, `—egid` `gid`, `—regid` `gid`

  设置实际、有效或两者 gid。`gid` 参数可以作为文本组名给出。

  为了安全起见，如果设置了任何主要 `gid`，你必须指定 `—clear-groups`、`—groups` 或 `—keep-groups` 之一。

- `—ruid` `uid`, `—euid` `uid`, `—reuid` `uid`

  设置实际、有效或两者 uid。`uid` 参数可以作为文本登录名给出。

  设置 `uid` 或 `gid` 不会更改权限，尽管最后的 exec 调用可能会更改权限。这意味着，如果你是 root，你可能想要执行类似以下操作：

  `setpriv` `—reuid=1000—regid=1000—caps=all`

- `—securebits` `(+|-)` `securebit`…
