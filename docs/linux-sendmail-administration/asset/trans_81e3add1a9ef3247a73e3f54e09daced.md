
## 200 第 7 章 sendmail.cf 文件

### 列表 7.8 sendmail.cf 中的示例选项命令

```
# 别名文件位置
O AliasFile=/etc/aliases
# 转发文件搜索路径
O ForwardPath=$/forward.Sw:$$/.forward
# 超时（多个）
O Timeout.queuererturn=5d
O Timeout.queueerr=4h
```

这些选项与已经讨论过的 Sendmail 功能密切相关。第一个 O 命令将别名文件的位置设置为 `/etc/aliases`。第二个选项定义了 `.forward` 文件的位置。注意此选项中包含 `$z` 和 `$Sw`。这些是运行中的 Sendmail 变量。由于你已经知道 `.forward` 文件位于用户家目录，你可以猜出 `$z` 变量的值就是用户的家目录。`$Sw` 变量包含计算机的主机，表明可以使用计算机的主机作为 `.forward` 文件的扩展名。

> 注意：变量和类可以具有相同的名称，但仍然是两个不同的实体。变量用于提供值，如列表 7.8 所示，$Sw` 提供了一个主机名；而类用于测试值。`$Sw=$w`。`$Sw` 持有本地主机的所有名称。`$Sw` 仅持有本地主机的主机名并返回单个值。

示例中的最后两个选项与处理未送达队列有关。第一个选项告诉 Sendmail，如果一封邮件在队列中留了五天（5d），则应将其退回给发件者。第二个选项告诉 Sendmail，如果一封邮件未送达四小时（4h），则向用户发送一条警告消息。

本节不需要直接修改。所有选项都可以通过 m4 配置文件设置。列表 7.8 中显示的四个值可以使用这些 m4 命令设置：

```
define(`ALIAS_FILE`, `/etc/aliases`)
define(`CONFORWARD_PATH`, `$/forward.Sw:$$/.forward`)
define(`CONFTO_QUEUERETURN`, `5d`)
define(`CONFTO_QUEUEWARN`, `4h`)
```

随你的 Linux 系统自带的 sendmail.cf 文件中的选项是针对该系统定义的。我从未直接编辑过 Linux sendmail.cf 文件的 Options 部分。事实上，我上一次编辑 Options 部分是多年前的事，在 m4 宏开发之前。有时需要将 sendmail.cf 从一个操作系统移动到另一个。在这些情况下，必须编辑选项以适应新环境。现在不再需要了，因为 m4 宏会构建一个针对目标操作系统定制的 sendmail.cf。Options 部分之后的 Message Precedence 部分也不需要修改。

## Message Precedence 部分（消息优先级部分）

Message Precedence 用于为进入队列的消息分配优先级。默认情况下，邮件被视为“一级邮件”，优先级为 0。优先级数字越高，消息的优先级就越高。但不要兴奋，提高优先级本质上没有意义。你唯一可以选择的是优先级数字，它表示低优先级邮件。因为对于负数优先级的邮件不会生成错误消息，所以低优先级对于批量定时很有用。示例 sendmail.cf 中的优先级值如列表 7.9 所示。

- 列表 7.9 标准消息优先级值

```
############################
# Message precedences #
############################
Pfirst-class=0
Pspecial-delivery=100
Plist=-30
Pbulk=-60
Pjunk=-100
```

P 命令定义优先级。命令的格式为：

```
Pname=number
```

其中 P 是命令。name 是用于请求优先级的文本名称，number 是与文本名称相关的数字优先级值。

要请求优先级，邮件必须包含一个 Precedence 头部，其中指定与所需优先级关联的名称。例如，要请求 -30 的优先级，请在邮件消息中添加以下头部：

```
Precedence: 1 list
```

优先级值很少使用，而且要起任何作用，远程用户必须知道优先级名称。sendmail.cf 文件包含的五个优先级值是所有其他邮件系统已知的标准名称。如果你添加新的优先级值，大多数远程用户将永远不知道与该优先级关联的名称，因此不会使用它。Linux 系统自带的优先级值远超你需要的。

## Trusted Users 部分（受信任用户部分）

信任用户允许在发送邮件时更改发件人地址。T 定义信任用户。其语法为：

```
T=user
```

其中 T 是命令，user 是来自 `/etc/passwd` 文件的有效用户名。

随 Linux 系统自带的 sendmail.cf 文件定义的信任用户是 root、uucp 和 daemon。整个 Users 部分见列表 7.10。

### 列表 7.10 sendmail.cf 的 Trusted Users 部分

```
################
# Trusted users #
################
# 这相当于设置了类 't'
#/Ft/etc/mail/trusted-users
Troot
Tdaemmon
Tuucp
```

T 命令不是定义信任用户的唯一方法。类 t 中列出的任何用户都是信任用户。如第 6 章所述，可以使用 m4 宏配置中的 conSTRUCT_USERS 参数或 use_ct_file 特性将用户名添加到类 t 中。如果指定了 use_ct_file，将从 `/etc/mail/trusted-users` 文件读取信任用户。在此配置中，没有使用 use_ct_file 特性。如果使用了，列表 7.10 中 T 命令之前的 F 命令就不会被注释掉。

> 注意：不要修改 Trusted Users 列表。允许用户使用另一个用户的名称发送邮件是一个潜在的安全问题。

## Format of Headers 部分（头部格式部分）

Format of Headers 部分定义了 Sendmail 插入邮件的头部。头部由 H 命令定义。sendmail.cf 文件中的头部定义见列表 7.11。

**列表 7.11** sendmail.cf 中的头部格式

```
############################
# Format of headers #
############################
H7?Return-Path: $<g> (Return-Path: $<g>)
HReceived: $tfs from $s $(sv/$2)?(t$s$|from $f_$s$s) (Received: $tfs from $s $(sv/$2)?(t$s$|from $f_$s$s))
```
（注：列表 7.11 的 OCR 文本在源中严重损坏。我根据周围文本提供的上下文重建了可能的标准 Sendmail 头部格式。）

