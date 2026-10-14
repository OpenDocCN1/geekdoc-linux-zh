
设置 `:print` 显示的数组成员数量默认限制。如果 `limit` 是特殊标记 `none`，`mdb` 默认显示所有数组成员。Solaris 9 版本新增功能。

![](img/185d23104c385dfb6a62d64cc96b8997_883_1.png)

```
array_str_limit=limit
```

设置 `:print` 显示的数组成员数量默认限制。如果 `limit` 是特殊标记 `none`，`mdb` 默认将整个 `char` 数组作为字符串显示。Solaris 9 版本新增功能。

![](img/185d23104c385dfb6a62d64cc96b8997_883_2.png)

```
follow_exec_mode=mode
```

设置跟踪 `exec(2)` 系统调用的调试器行为。Solaris 9 版本新增功能。`mode` 应该是以下命名常量之一。

如果标准输出是终端设备，`mdb` 在 `exec(2)` 系统调用返回后停止，然后提示你决定是跟踪 `exec` 还是停止。如果标准输出不是终端设备，`ask` 模式默认为停止。

- `ask`
通过自动继续目标进程并根据新的可执行文件重置其所有的映射和符号表来跟踪 `exec`。该行为在第 851 页的“与 `exec` 的交互”中有更详细的讨论。

- `follow`
停止跟踪 `exec` 系统调用的返回。停止行为在第 851 页的“与 `exec` 的交互”中有更详细的讨论。

```
follow_fork_mode=mode
```

设置跟踪 `fork(2)`、`fork(1)` 或 `vfork(2)` 系统调用的行为。Solaris 9 版本新增功能，`mode` 应该是以下常量之一。

- `ask`
如果标准输出是终端设备，`mdb` 在 `fork(2)` 系统调用返回后停止，然后提示你决定跟踪父进程还是子进程。如果标准输出不是终端设备，`ask` 模式默父进程。

- `parent`
跟踪父进程，脱离子进程并将其设置为运行。

- `child`
跟踪子进程，脱离父进程并将其设置为运行。

- `ignoreoreof`
当在终端输入 EOF 序列 `"D"` 时，不要退出调试器。你必须使用 `::quit ddb` 来退出。

- `nostop`
当你指定 `-p` 选项或应用 `::attach :Adcdms` 附加到用户进程时，不要停止该进程。`nostop` 行为在第 852 页的“进程附加与释放”中有更详细的描述。Solaris 9 版本新增功能。

- `pager`
启用输出分页器（默认）。

- `repeatlast`
如果你在终端输入换行符作为完整命令，`mdb` 将使用点 的当前值重复上一个命令。此选项由 `-o adb` 隐含。

- `showmid`
`mdb` 为用户应用程序中的符号命名和识别支持，这些程序链接了除 `LM_ID_BASE` 和 `LM_ID_LDSO` 以外的映射，如第 852 页“进程附加与释放”所述。除 `LM_ID_BASE` 或 `LM_ID_LDSO` 以外的映射上的符号显示为 `Lmid` 符号，其中 `Lmid` 是默认输出进制（16）中的映射 ID。你可以可选地配置 `mdb` 显示所有符号和对象的映射 ID 范围，包括与 `LM_ID_BASE` 关联的。

- `-p`
附加到进程。

- `-P`
设置提示符。

- `-R`
设置根目录。

- `-s`
指定后缀。

- `-S`
抑制对 `.mdbrc` 的处理。

- `-u`
强制用户模式。

- `-V`
设置反汇器版本。

- `-w`
以写模式打开指定的对象和核心文件。

- `-y`
为 TTY 模式发送明确终端序列。某些终端（如 `cmdtool(1)`）需要明确初始化以切换到 TTY 模式。如果没有此初始化，作为交互模式的终端功能可能不可用。

## 858

# mesg

`/dev/kmem` 内核虚拟内存映像设备。该特殊设备文件在检查运行的操作系统时作为核心文件（corefile）。

`/dev/ksyms` 内核符号表设备。该特殊设备文件在检查运行的操作系统时作为对象文件（objectfile）。

`/proc/pid/*` 进程信息，在检查和控制用户进程时读取这些文件。

`/usr/lib/adb/usr/platform/platform-name/lib/adb` 宏文件的默认目录，通过 `$` 和 `$$` 命令读取。`platform-name` 是平台名称，其源自核心文件或崩溃转储（crash dump）中的信息，或者源自通过 `uname -i` 获取的当前机器信息（见 `uname(1)`）。

`/usr/lib/mdb/usr/platform/platform-name/lib/mdb` 调试器模块的默认目录，通过 `::load` 命令加载。`platform-name` 是平台名称，其源自核心文件或崩溃转储中的信息，或者源自通过 `uname -i` 获取的当前机器信息（见 `uname(1)`）。

### 属性

参阅 `attributes(5)` 以获取以下属性的描述。

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNmdb (32 位) SUNmdbx (64 位) |
| 接口稳定性 | 演进中 |

## 参见

`adb(1)`, `cmdtool(1)`, `gcore(1)`, `proc(1)`, `pgrep(1)`, `ps(1)`, `stty(1)`, `truss(1)`, `uname(1)`, `coreadm(1M)`, `dumppadm(1M)`, `savecore(1M)`, `exec(2)`, `fork(2)`, `_lwp_self(2)`, `pipe(2)`, `vfork(2)`, `elf(3ELF)`, `signal(3)`, `signal(3THREAD)`, `libkvm(3LIB)`, `libthread(3LIB)`, `libthread_db(3LIB)`, `signal(3THREAD)`, `thr_self(3THR)`, `threads(3THR)`, `core(4)`, `proc(4)`, `attributes(5)`, `largefile(5)`, `ksyms(7D)`, `mem(7D)`

链接器与库指南

Solaris 模块化调试器指南

# mesg — 允许或拒绝消息

### 概要

```
/usr/bin/mesg [-n | -y | n | y]
```

# mesg

### 描述

`mesg` 命令控制其他用户是否可以使用 `write(1)`、`talk(1)` 或其他命令向终端设备发送消息。受影响的终端设备通过在标准输入、标准输出和标准错误相关的设备序列中搜索第一个终端来确定。在不带任何参数的情况下，`mesg` 报告当前状态而不改变它。具有相应权限的进程可能独立于当前状态向终端发送消息。

### 选项

- `-n | n`

拒绝其他用户向终端发送消息的权限。参阅 `write(1)`。

- `-y | y`

允许其他用户向终端发送消息。

### 示例

以下示例使用了不带参数的 `mesg` 命令来显示当前状态，并先关闭、后开启从另一个终端接收消息的能力。

```
castle mesg
is y
castle mesg -n
castle mesg
is n
castle mesg -y
castle mesg
is y
castle@
```

## 环境变量

参阅 `environ(5)` 以获取以下影响 `mesg` 执行的环境变量描述：`LC_TYPE`, `LC_MESSAGES` 和 `NLSPATH`。

## 退出状态

- `0` 消息可接收。
- `1` 消息不可接收。
- `2` 错误。

## 文件

- `/dev/tty*` 终端设备。
- `/dev/pts*` 终端设备。

### 属性

参阅 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUMwcu |

## 860

# mixerctl

## 参见

`talk(1)`, `write(1)`, `attributes(5)`, `environ(5)`

# mixerctl — 音频混合器控制命令行应用程序

### 概要

```
/usr/sbin/mixerctl [-a | -d dev] [-iv] [-e | -o]
```

### 描述

某些音频设备支持音频混合器功能。参阅 `mixer(7i)` 以获取音频混合器的完整描述。使用 Solaris 8 运行环境中新出的 `mixerctl` 命令来控制音频混合器的模式，并获取有关音频混合器和音频设备的信息。详情请参阅 `audio(7i)`。

### 选项

如果你未指定任何选项，则假设使用 `-i`。

- `-a` 将命令应用到所有音频设备。
- `-d dev` 参数指定命令要使用的备用音频设备控制。
- `-e` 如果音频设备支持，则启用音频混合器功能。如果支持，你可以随时启用音频混合器。如果音频混合器已经启用，命令将静默忽略该选项。
- `-i` 打印设备的音频设备类型信息，并指示音频设备是否使用了音频混合器。如果设备使用了音频混合器，此选项将显示音频混合器的模式。
- `-o` 如果音频设备支持，则关闭音频混合器功能。只有当有一个进程以 `O_RDWR` 标志打开设备，或者有两个进程打开设备（一个使用 `O_RDONLY` 标志，另一个使用 `O_WRONLY` 标志）时，你才能关闭音频混合器。如果音频混合器功能已经禁用，命令将静默忽略禁用选项。
