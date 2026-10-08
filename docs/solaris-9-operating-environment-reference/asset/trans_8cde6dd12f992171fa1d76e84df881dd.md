

# 1503

-rjobid 刷新任务 jobid。触碰与 jobid 关联的文件，使其修改时间被设置为当前时间。此调整可以防止守护进程删除该任务，直到该任务的修改时间达到守护进程设置的限制。

# 远程系统状态

以下选项提供了远程系统性能信息，例如平均传输速率或队列时间。你可以仅在使用 -t 选项时使用 -c 和 -d 选项。

- -c 计算平均队列时间。如果不使用 -c 选项，则计算平均传输速率。例如，命令

```
castle@uustat -teagle -d50 -c
```

产生如下格式的输出：
过去 50 分钟 eagle 的平均队列时间为: 5 seconds
不带 -c 参数的相同命令产生如下格式的输出：
a2000.88 bytes/sec

- -number 指定分钟数，以覆盖计算时默认的 60 分钟。这些计算基于可选性能日志中包含的信息，因此可能不可用。计算只能从性能日志清理后的时间开始。

- -tsystem 报告远程系统过去 60 分钟的平均传输速率或平均队列时间。

# 用户或系统特定状态

以下选项提供了 uuc 连接到其他系统的通用、远程系统特定和用户特定的状态。你可以使用 uustat 指定以下任一或两个选项。你可以配合 -s 选项使用 -j 选项列出显示的任务总数。

- -system 报告远程系统 system 所有 uuc 请求的状态。

- -user 报告用户 user 请求的所有 uuc 请求的状态。

-s 和 -u 选项的输出格式如下：

```
eagleL1bd7 4/07-11:07 S eagle dan 522 /home/dan/A
eagleClib8 4/07-11:07 S eagle dan 59 D.3b2al2ce4924
```

第一个字段是按日期/时间划分的任务 ID。如果任务正在发送文件，则字段为 S；如果任务正在请求文件，则为 R。下一个字段是要传输文件的系统，随后是队列该任务的用户 ID。下一个字段包含文件大小，或者在远程执行的情况下，包含命令名称。在此示例中，rmail 是用于远程邮件的命令。

# 1504

# uustat

当此字段包含大同时，也会显示文件名。文件名可以是用户指定的名称，也可以是内部名称（例如 D.3b2alce4924），该名称为远程执行关联的数据文件（在此示例中为邮件）创建。

报告任务状态。

- - q 队列的任务。传输尚未开始。
- r 运行的任务。传输已经开始。
- i 中断的任务。传输已开始但在文件完全传输之前已终止。
- - c 完成的任务。任务传输成功。

你可以以任意组合使用参数，但必须指定任意一个参数。你还可以在 -s 和 -u 选项配合使用 -s。其输出与 -s 和 -u 的输出完全相同，只是任务状态作为最后一个输出单词追加在。完成任务的输出格式如下：eagleClbd3 completed

当你不指定任何选项时，uustat 会向标准输出写入当前用户所有 uucp 请求的状态。

# 环境变量

请参考 environ(5) 了解影响 uustat 执行的以下环境变量的描述：LC_CTYPE, LC_MESSAGES, LC_TIME, TZ 和 NLSPATH。

# 退出状态

- - 0 成功完成。
- >0 发生错误。

# 文件

- - /var/spool/uucp/
暂存目录。
/var/uucp/.Admin/account
计数日志。
/var/uucp/.Admin/perlog
性能日志。

# 属性

请参考 attributes(5) 了解以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
|可用性 | SUNwdnuu |

# 参见

uucp(1C), attributes(5)

# auto, uupick
1505

诊断
当正在记录计算所需的数据时，t 选项不产生消息。

# auto, uupick — 公用 UNIX到UNIX 系统文件复制

# 概要
/usr/bin/uupick [-mp] source-file...destination
/usr/bin/uupick [-s system]

# 描述
uuto 使用 uucp(C) 将 source-file 发送到 destination；它允许本地系统控制文件访问。源文件名是你系统上的路径名。destination 的格式为：
system[!system]...user

其中 system 取自 uupick 已知的系统名称列表。user 是指定系统上某人的名称。
文件（如果你指定了目录，则是子树）被发送到系统上的 PUBDIR，其中 PUBDIR 是 uucp 源中定义的公共目录。默认情况下，该目录是 /var/spool/receive/user/uucppublic。具体来说，文件被发送到 PUBDIR/receive/user/system-files。

接收者通过 mail(1) 通知文件到达。

> 注意 — 要发送以点开头的文件（例如 .profile），你需要包含点。例如，以下文件名是正确的：

.profile

以下文件名是错误的：

*profile

uupick 接收者通过 mail(1) 通知文件到达。

uupick 接收并发往用户的文件。具体来说，uupick 搜索 PUBDIR 发往用户的文件。

uick 接收来自 system 的文件。uupick 读取标准输入中的行以确定文件的处置。

当此字段包含大同时，也会显示文件名。文件名可以是用户指定的名称，也可以是内部名称（例如 D.3b2alce4924），该名称为远程执行关联的数据文件（在此示例中为邮件）创建。

报告任务状态。

- - q 队列的任务。传输尚未开始。
- r 运行的任务。传输已经开始。
- i 中断的任务。传输已开始但在文件完全传输之前已终止。
- - c 完成的任务。任务传输成功。

你可以以任意组合使用参数，但必须指定任意一个参数。你还可以在 -s 和 -u 选项配合使用 -s。其输出与 -s 和 -u 的输出完全相同，只是任务状态作为最后一个输出单词追加在。完成任务的输出格式如下：eagleClbd3 completed

当你不指定任何选项时，uustat 会向标准输出写入当前用户所有 uucp 请求的状态。

# 环境变量

environ(5) 了解影响 uuto 和 uupick 执行的环境变量：LC_TYPE, LC_MESSAGES 和 NLSPATH。

# 退出状态

0 成功完成。
>0 发生错误。

# 文件

PUBDIR /var/spool/ucublic 公共目录。

# 1506 uuto

EOT (d) 与 q 相同。

# 选项

- m 在拷贝完成后发送邮件。
- p 将源文件复制到暂存目录。
- s 仅搜索 PUBDIR 发往系统的文件。

# 操作数

destination 格式为：system-name!user
其中 system-name 取自 uucp 已知的系统名称列表；见 uname。user 参数是某人的登录名。
source-file 是要复制到 destination 的本地系统文件路径名。

# 1507

uupick

m [dir] 将条目移动到目录 dir。如果不指定 dir，默认是当前目录。
a [dir] 与上述相同，发往 system 的所有文件。

command-string 由一个或多个看起来像 shell 命令行的参数组成，但可以在命令和文件名前加上 system-name，将其解释为本地系统。

文件名可以是以下之一：

* 绝对路径名。
* 前缀为 -xxx 的路径名，其中 xxx 是指定系统上的登录名，并替换为该用户的登录目录。

其他所有内容都以当前目录为前缀。

例如，命令获取：

- q 停止。
- d 与 q 相同。

# uux

uux 收集来自多个系统的零或多个文件，在指定系统上执行命令并将标准输出发送到指定系统的文件。

> 注意 — 出于安全考虑，大多数安装限制了代表来自 uux 请求的可执行命令列表，仅允许接收邮件（见 mail(1)）。远程执行权限定义在 /etc/uucp/Permissions。

# 概要

```
/usr/bin/uux [-] [-bcCjnprz] [-anime] [-grade] [-sfilename]
[-xdebug-level] command-string
```

# 描述
uux 收集来自多个系统的零或多个文件，在指定系统上执行命令并将标准输出发送到指定系统的文件。

