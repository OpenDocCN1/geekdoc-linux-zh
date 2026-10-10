
## BatchMode
## BindAddress
## CanonicalDomains
## CanonicalizeFallbackLocal
## CanonicalizeHostname
## CanonicalizeMaxDots
## CanonicalizePermittedCNAMEs
## ChallengeResponseAuthentication
## CheckHostIP
## Cipher
## Ciphers
## Compression
## CompressionLevel
## ConnectionAttempts
## ConnectTimeout
## ControlMaster
## ControlPath
## ControlPersist
## GlobalKnownHostsFile
## GSSAPIAuthentication
## GSSAPIDelegateCredentials
## HashKnownHosts
## Host
## HostbasedAuthentication
## HostbasedKeyTypes
## HostKeyAlgorithms
## HostKeyAlias
## Hostname
## IdentityFile
## IdentitiesOnly
## IPQoS
## KbdInteractiveAuthentication
## KbdInteractiveDevices
## KexAlgorithms
## LogLevel
## MACs
## NoHostAuthenticationForLocalhost
## NumberOfPasswordPrompts
## PasswordAuthentication
## PKCS11Provider
## Port
## PreferredAuthentications
## Protocol
## ProxyCommand
## PubkeyAcceptedKeyTypes
## PubkeyAuthentication
## RekeyLimit
## RhostsRSAAuthentication
## RSAAuthentication
## SendEnv
## ServerAliveInterval
## ServerAliveCountMax
## StrictHostKeyChecking
## TCPKeepAlive
## UpdateHostKeys
## UsePrivilegedPort
## User
## UserKnownHostsFile
## VerifyHostKeyDNS

### -P port
指定要连接到远程主机上的端口。请注意，此选项使用的是大写字母 ‘P’，因为 `-p` 已被保留用于保留文件的修改时间和权限。

### -p
保留原始文件的修改时间、访问时间和权限。

### -q
静默模式：禁用进度指示器，以及来自 ssh(1) 的警告和诊断消息。

### -r
递归复制整个目录。注意，scp 在树遍历过程中会跟随符号链接。

### -S program
用于加密连接的程序名称。该程序必须能够理解 ssh(1) 的选项。

### -v
详细模式。使 scp 和 ssh(1) 打印关于其进度的调试消息。这对于调试连接、身份验证和配置问题很有帮助。

## EXIT STATUS

scp 的退出状态。

## SEE ALSO

scp(1), ssh(1), ssh-add(1), ssh-agent(1), ssh-keygen(1), ssh_config(5), scp(8)

## HISTORY

scp 基于加利福尼亚大学伯克利分校董事会提供的 BSD 源代码中的 rcp 程序。

## AUTHORS

Timo Rinne 和 Tatu Ylonen。

## SCRIPT

## NAME

script - 记录终端会话的类型脚本

## SYNOPSIS

```
script [options] [file]
```

## DESCRIPTION

script 会记录显示在终端上的所有内容。这对于需要交互会话纸质记录作为作业证明的学生来说非常有用，因为类型脚本文件随后可以使用 a2ps(1) 打印出来。

如果给定了参数 file，script 会将对话保存在该文件中。如果没有给定文件名，对话将保存在文件 typescript 中。

## OPTIONS

- **-a, --append**
  将输出追加到文件或 typescript，保留先前的内容。

- **-c, --command command**
  运行命令而不是交互式 shell。这使得脚本可以轻松捕获那些在 stdout 不是 tty 时行为不同的程序的输出。

- **-e, --return**
  返回子进程的退出代码。使用 sa 格式，在信号终止时的 bash 退出代码为 `128+n`。

- **-f, --flush**
  在每次写入后刷新输出。这对于远程协作非常有用：一个人执行 `mkfifo foo; script -f foo`，另一个人可以使用 `cat foo` 实时监督正在进行的操作。

- **--force**
  允许默认输出目标，即类型脚本文件，成为硬链接或符号链接。该命令将跟随符号链接。

- **-q, --quiet**
  保持安静（不向标准输出或类型脚本文件写入开始和完成消息）。

- **-t, --timing[=file]**
  将时序数据输出到标准错误，或在给定时输出到文件。这些数据包含两个字段，由空格分隔。第一个字段指示自上次输出以来经过了多少时间。第二个字段指示这次输出了多少个字符。可以使用这些信息以现实的打字和输出延迟重放类型脚本。

- **-V, --version**
  显示版本信息并退出。

- **-h, --help**
  显示帮助文本并退出。

## NOTES

script 在分叉的 shell 退出时结束（对于 Bourne shell (sh(1)) 是控制-D，对于 C-shell, csh(1) 是 exit, logout 或 control-d（如果未设置 ignoreeof））。

某些交互式命令，如 less(1)，会在类型脚本文件中产生垃圾数据。script 最适合用于不操纵屏幕的命令，其结果预期与硬拷贝终端相关。

不建议在非交互式 shell 中运行 script。script 的内部 shell 始终是交互式的，这可能会导致意外结果。如果你在 shell 初始化文件中使用了 script，你必须避免进入无限循环。使用例如 profile 文件，它仅由登录 shell 读取：

```
if test -t 0 ; then script exit fi
```

你还应该避免在命令管道中使用 script，因为 script 可能读取比你预期的更多的输入。

## ENVIRONMENT

以下环境变量被 script 使用：

- **SHELL**
  如果变量 SHELL 存在，由 script 分叉的 shell 将是该 shell。如果未设置 SHELL，则假设使用 Bourne shell。（大多数 shell 会自动设置此变量）。

## SEE ALSO

a2ps(1)（用于历史机制），csh(1)。

## HISTORY

script 命令出现在 3.0BSD 中。

## BUGS

script 将所有内容放入日志文件，包括换行符和退格符。这不是普通用户所期望的。

script 主要是为交互式终端会话设计的，当 stdin 不是终端时（例如 “echo foo | script”），会话可能会挂起，因为 script 会话内的交互式 shell 缺少 EOF，而 script 也不知道何时关闭会话。更多信息请参阅 NOTES 部分。

## AVAILABILITY

script 命令是 util-linux 包的一部分，可以从 Linux Kernel Archive 获取

## SCRIPTREPLAY

## NAME

scriptreplay - 使用时序信息重放类型脚本

## SYNOPSIS

scriptreplay [options] [-t] timingfile [typescript [divisor]]

## DESCRIPTION

此程序使用时序信息重放类型脚本，以确保输出按照最初记录 script 时的相同节奏发生。

重放只是再次显示信息；在记录类型脚本时运行的程序不会再次运行。由于只是简单地显示相同的信息，scriptreplay 仅在在与记录类型脚本相同类型的终端上运行时才能保证正常工作。否则，类型脚本中的任何转义字符可能会被 scriptreplay 发送输出的终端以不同方式解释。

时序信息是 script(1) 在使用 -t 参数运行时输出到标准错误的信息。

默认情况下，假设要显示的 typecript 名称为 typescript，但可以指定其他文件名，作为第二个参数或通过选项 -s。

如果指定了第三个参数，它将用作加速倍数。例如，2 的加速使 scriptreplay 以两倍速度运行，0.1 的加速使其比原始会话慢十倍。

## OPTIONS

前三个选项将覆盖旧式参数。

- **-t, --timing file**
  包含 script 时序输出的文件。

- **-s, --typescript file**
  包含 script 终端输出的文件。

- **-d, --divisor number**
  以该倍数加速重放显示。参数是一个浮点数。它被称为除数，因为它将时序除以该因子。

- **-m, --maxdelay number**
  设置转录更新之间的最大延迟为若干秒。参数是一个浮点数。这可用于避免转录重放中的长时间暂停。

- **-V, --version**
  显示版本信息并退出。

- **-h, --help**
  显示帮助文本并退出。

