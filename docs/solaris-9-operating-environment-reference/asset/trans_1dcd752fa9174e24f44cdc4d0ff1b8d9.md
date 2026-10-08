

# 696

# llc2_stats

outOfState 在无效状态下接收到的事件数。

allocFail 缓冲区分配失败的次数。

protocolError LLC 协议错误次数，即接收到格式不正确的 PDU，或在期望帧 Y 时接收到帧 X。

localBusy 此组件处于本地忙态且无法接受 I 帧的次数。

remoteBusy 远程连接组件忙碌且无法接受 I 帧的次数。

maxRetryFail 因达到最大重试次数（maxRetry）而导致的失败次数。

ackTimerExp 确认（Acknowledgement）计时器期的次数。

pollTimerExp 轮询（Poll）计时器期的次数。

rejTimerExp 拒绝（Reject）计时器期的次数。

remBusyTimerExp 远程忙态（Remote Busy）计时器期的次数。

inactTimerExp 空闲（Inactivity）计时器期的次数。

sendAckTimerExp 发确认（Send Acknowledgement）计时器期的次数。

# LLC2 状态

| STATION | |
| :--- | :--- |
| ~~ DOWN | 0x00 |
| ~~ UP | 0x01 |
| SAP | |
| ~~ INACTIVE | 0x00 |
| ~~ ACTIVE | 0x01 |
| CONNECTION | |
| ~~ ADM | 0x00 |
| ~~ CONN | 0x01 |
| ~~ RESET_WAIT | 0x02 |
| ~~ RESET_CHECK | 0x03 |

# llc2_stats

```
--SETUP 0x04
--RESET 0x05
--D_CONN 0x06
--ERROR 0x07
--NORMAL 0x08
--BUSY 0x09
--REJECT 0x0a
--AWAIT 0x0b
--AWAIT_BUSY 0x0c
--AWAIT_REJECT 0x0d
```

# timersOn

```
Acknowledgement 0x80
Poll 0x40
Reject 0x20
Remove Busy 0x10
Inactivity 0x08
Send Acknowledgement 0x04
```

# LLC2 Flags

```
P_FLAG 0x80
F_FLAG 0x40
S_FLAG 0x20
REMOTE_BUSY 0x10
RESEND_PENDING 0x08
```

# Attributes

参见 attributes(5) 获取以下属性的描述。

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNW11c |

文件
/dev/llc2 挂隆设备。

# 另请

+   attributes(5)

#为文件创建硬链接或符号链接

 概要

```
/usr/bin/ln [-fns] source-file [target]
/usr/bin/ln [-fns] source-file...
/usr/xpg4/bin/ln [-fs] source-file [target]
/usr/xpg4/bin/ln [-fs] source-file...
```

 描述
有时从多个目录访问同一个文件是有用的。这可以减少磁盘空间占用，并更易于维护多人共用文件的一致性。使用 ln（链接）命令在单个文件系统中的目录项之间创建链接，以便在目录层次结构中的两个或多个位置创建单个文件。

符号链接 (-s) 可以跨文件系统链接文件。符号链接有一个名称和在目录树中的位置，但没有内容。它指向任何其他文件或目录。

使用 ln 命令可以创建硬链接和符号链接。硬链接是文件的指针，与原始目录项无法区分。对文件的任何更改都独立于用于引用该文件的名称而生效。硬链接不能跨越文件系统，且不能引用目录。

默认情况下，ln 创建硬链接。source-file 被链接到 target。如果 target 是目录，则会创建一个名为 source-file 的文件并将其链接到原始 source-file。

在第一个概要形式中，ln 在 target 指定的定义路径下为 source-file 指定的文件创建一个新的目录项（链接）。如果不指定 target，则链接将在当前目录中创建。当最后一个操作数没有指向一个存在的目录时，假设使用第一个概要形式；如果你指定了两个操作数且最后一个不是已存在的目录，则会发生错误。

在第二个概要形式中，ln 在名为 target 的现有目录的定义路径下，为 source-file 指定的每个文件创建一个新的目录项。

```
/usr/bin/ln
```

如果 target 是文件，其内容将被覆盖。如果 /usr/bin/ln 确定 target 的模式禁止写入，它将打印消息（参见 chmod(1)），请求响应并从标准输入读取输入。如果响应为肯定，则允许建立链接；否则，命令退出。

```
/usr/xpg4/bin/ln
```

如果 target 是文件且你没有指定 -f 选项，/usr/xpg4/bin/ln 会向标准错误写入诊断信息，对当前 source-file 不进行任何操作，并继续处理剩余的源文件。符号链接是指向文件的间接指针；其目录项包含它所链接的文件名。符号链接可以跨越文件系统，并可以引用目录。

当你创建一个硬链接且源文件本身是符号链接时，target 是指向符号链接所引用文件的硬链接，而不是指向符号对象本身（source_file）。

文件的权限可能与 -l 显示的 target 权限不同。参见 stat(2) 获取更多信息。

 选项

/usr/bin/ln 和 /usr/xpg4/bin/ln 支持以下选项：

+   -f 即使 target 模式禁止写入也强制链接。
-s 创建符号链接。
-n 如果链接是现有文件，不覆盖文件内容。-f 选项会覆盖此选项。此行为是 /usr/xpg4/bin/ln 的默认行为并被忽略忽略。

# 操作数

source-file 要链接的文件路径。该文件可以是普通文件或特殊文件。如果你指定了 -s 选项，source-file 也可以是目录。

target 要创建的新目录项的路径，或要创建新目录项的现有目录。

# 用法

largefile(5) 关于 ln 在遇到大于2GB (2**31 字节) 文件时的行为。

# 环境变量

environ(5) 关于影响 ln 执行的环境变量描述：LC_TYPE、LC_MESSAGES 和 NLPATH。

# 退出状态

0 所有指定的文件均成功链接。

>0 发生错误。

# 注意事项

符号链接在某些情况下的行为与你预期的不同。对该链接使用 ls(1) 显示的是指向目录的内容，而 ls -l 显示的是链接本身的信息，如下例：

```
castle$ ln -s dir link
castle$ ls link
file1 file2 file3
castle$ ls -l link
lrwxr-wx 1 user      Jan 11 23:27
```

当你使用 cd(1) 进入一个目录时，它会跟踪符号链接。例如，在以下情况中，父目录是 /home/castle：

```
castle$ pwd
/home/castle
castle$ cd link
castle$ pwd
/home/castle/dir
```

