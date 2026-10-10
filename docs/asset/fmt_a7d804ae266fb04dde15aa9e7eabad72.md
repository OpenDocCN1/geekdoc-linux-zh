
### `[-]isig`

启用中断、退出和挂起特殊字符

### `[-]noflush`

在中断和退出特殊字符后禁用刷新

### `[-]prterase`

等同于 `[-]echoprt`

### `[-]tostop`

停止尝试向终端写入的后台作业

### `[-]xcase`

配合 `icanon`，使用 `` ` `` 作为大写字母的转义

### 组合设置：

#### `[-]LCASE`

等同于 `[-]lcase`

#### `cbreak`

等同于 `-icanon`

#### `cbreak`

等同于 `icanon`

#### `cooked`

等同于 `brkint` `ignpar` `ipost` `isig` `icanon`，并将 `eof` 和 `eol` 字符重置为其默认值

### STTY

#### `cooked`

与 `raw` 相同

#### `crt`

与 `echo` `echoctl` `echoke` 相同

#### `dec`

与 `echo` `echoctl` `echoke` `ixany` `intr` `^c` `eras` `0177` `kill` `^u` 相同

#### `deccntl`

与 `deccnx1` 相同

#### `ek`

与 `ek` 相同

#### `evenp`

与 `parenb` `-parodd` `cs7` 相同

#### `-evenp`

与 `-parenb` `cs8` 相同

#### `[-]lcase`

与 `xcase` `iucll` `olcuc` 相同

#### `litout`

与 `-parenb` `-istrip` `-opost` `cs8` 相同

#### `-litout`

与 `parenb` `istrip` `opost` `cs7` 相同

#### `nl`

与 `-icrnl` `-onlcr` 相同

#### `-nl`

与 `icrnl` `-inlcr` `-igncr` `onlcr` `-ocrnl` `-onlret` 相同

#### `oddp`

与 `parenb` `parodd` `cs7` 相同

#### `-odd`

与 `-parenb` `cs8` 相同

#### `[-]parity`

与 `[-]evenp` 相同

#### `pass8`

与 `-parenb` `-istrip` `cs8` 相同

#### `-pass8`

与 `parenb` `istrip` `cs7` 相同

#### `raw`

与 `-ignbrk` `-brkint` `-ignpar` `-parmrk` `-inpc` `-istrip` `-inlcr` `-igncr` `-icrnl` `-ixon` `-ixoff` `-icanon` `-opost` `-isig` `-iucl` `-ixany` `-imaxbel` `-xcase` `min` `1` `time` `0` 相同

#### `-raw`

与 `cooked` 相同

#### `sane`

与 `cread` `-ignbrk` `brkint` `-inlcr` `-igncr` `icrnl` `icanon` `ixtenh` `echo` `echoe` `echok` `-echonl` `-noflsh` `-ixoff` `-iutf8` `-iucll` `-ixany` `imaxbel` `-xcase` `-olcuc` `-ocrnl` `opost` `-ofill` `onlcr` `-onocr` `-onlret` `nl0` `cr0` `tab0` `bs0` `vt0` `ff0` `isig` `-tostop` `-ofdel` `-echoprt` `echoctl` `echoke` `-extproc` 相同，并将所有特殊字符恢复为其默认值

处理连接到标准输入的 tty 线路。如果没有参数，则打印波特率、线路规程以及相对于 `stty sane` 的偏差。在设置中，`CHAR` 被视为字面值，或者编码为 `^c`、`0x37`、`0177` 或 `127`；特殊值 `^-` 或 `undef` 用于禁用特殊字符。

### 作者

由 David MacKenzie 编写。

### 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 请向 <http://translationproject.org/> 报告 `stty` 翻译错误

### 版权

Copyright © 2015 Free Software Foundation, Inc. 许可证 GPLv3+：GNU GPL 第 3 版或更高版本 <http://gnu.org/licenses/gpl.html>。这是自由软件：您可以自由修改和重新分发它。在法律允许的范围内，NO WARRANTY（无保修）。

### 另请参阅

完整文档位于：<http://www.gnu.org/software/coreutils/stty>

或本地通过：`info '(coreutils) stty invocation'`

### SU

### 名称

`su` - 使用替代用户和组 ID 运行命令

### 概要

```
su [选项] [-] [用户 [*参数*...]]
```

### 描述

`su` 允许使用替代用户和组 ID 运行命令。

如果不带参数调用，`su` 默认以 *root* 身份运行交互式 shell。

为了向后兼容，`su` 默认不更改当前目录，并且仅设置环境变量 `HOME` 和 `SHELL`（如果目标 *user* 不是 *root*，则还设置 `USER` 和 `LOGNAME`）。建议始终使用 `--login` 选项（而不是其快捷方式 `-`）以避免因混合环境而产生的副作用。

此版本的 `su` 使用 PAM 进行身份验证、账户和会话管理。因此，其他 `su` 实现中的配置选项（例如对 wheel 组的支持）必须通过 PAM 进行配置。

### 选项

- `-c`, `--command=*command*`

  将 *command* 传递给 shell 并附带 `-c` 选项。

- `-f`, `--fast`

  向 shell 传递 `-f`，这可能有用也可能无用，具体取决于 shell 类型。

- `-g`, `--group=*group*`

  指定主组。此选项仅对 root 用户可用。

- `-G`, `--supp-group=*group*`

  指定辅助组。此选项仅对 root 用户可用。

- `-`, `-l`, `--login`

  以登录 shell 启动，并具有类似真实登录的环境：

  - 清除除 `TERM` 以外的所有环境变量

  - 初始化环境变量 `HOME`、`SHELL`、`USER`、`LOGNAME` 和 `PATH`

  - 更改到目标用户的主目录

  - 将 shell 的 argv[0] 设置为 `'-'` 以使 shell 成为登录 shell

- `-m`, `-p`, `--preserve-environment`

  保留整个环境，即不设置 `HOME`、`SHELL`、`USER` 或 `LOGNAME`。如果指定了 `--login` 选项，则此选项被忽略。

- `-s`, `--shell=*shell*`

  运行指定的 *shell* 而不是默认 shell。要运行的 shell 根据以下规则按顺序选择：

  - 使用 `--shell` 指定的 shell

  - 如果使用 `--preserve-environment` 选项，则为环境变量 `SHELL` 中指定的 shell

  - 目标用户 passwd 条目中列出的 shell

  - `/bin/sh`

  如果目标用户拥有受限 shell（即未列在 `/etc/shells` 中），则除非调用者是 root，否则忽略 `--shell` 选项和 `SHELL` 环境变量。

- `-V`, `--version`

  显示版本信息并退出。

- `-h`, `--help`

  显示帮助文本并退出。

### 信号

在收到 `SIGINT`、`SIGQUIT` 或 `SIGTERM` 时，`su` 终止其子进程，随后使用收到的信号终止自身。

#### 配置文件

`su` 读取 `/etc/default/su` 和 `/etc/login.defs` 配置文件。以下配置项与 (1) 相关：

`FAIL_DELAY` (number)

身份验证失败时的延迟秒数。该数字必须是非负整数。

`ENV_PATH` (string)

为普通用户定义 PATH 环境变量。默认值为 `/usr/local/bin:/bin:/usr/bin`。
