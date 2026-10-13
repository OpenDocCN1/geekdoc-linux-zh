
```
if ( `echo $1 | awk '( print $1 )'` = "" ) then
    echo You did not supply a subject for the message.
    echo Be sure to enclose it in quotes.
    exit 1
else
    # Get the subject of the message
    set subject=$1
endif

#
# Check for a filename
#
if ( $2 == "" ) then
    echo You did not supply a filename.
    exit 2
else
    # Get the name of the file to send
    set filename=$2
endif

#
# Check that the file exists
#
if ( -f $filename ) then
    echo Sending file $filename
else
    echo File does not exist.
    exit 3
endif

#
# Loop through every login name, but skip the first 17 accounts
foreach user ( `awk -F: '$( print $1 )'` /etc/passwd | tail +17` )
    # Mail the file
    echo Mailing to $user
    mail -s "$subject" user < $filename

    # sleep for a few seconds so we don't overload the mailer
    # On fast systems or systems with few accounts, you can
    # probably take this delay out.
    sleep 2
end
```

该脚本接受两个参数。第一个是电子邮件消息的主题，需要包含引号内。第二个是包含要发送消息的文件名。因此，为了向所有用户发送一封邮件，警告他们即将到来的服务器硬件升级，我可能会执行类似以下的操作：

`mailfile "System upgrade at 5:00pm" upgrade.txt`

# 410 第三部分 管理 Red Hat Linux

`upgrade.txt` 文件包含了要发送给每个用户的消息文本。这种方法真正实用的用点在于，我可以保存这个文本文件，并在下次升级系统时轻松地修改和重新阅读。

使用基于文本的登录而不是图形界面登录，你可以向 `/etc/motd` 文件中添加消息，以便它们到达用户。该文件中的任何文本都将在第一个 shell 提示符出现之前和之后显示在每个用户的屏幕上。

## 总结

Red Hat Linux 系统被用作没有实际用户的单任务服务器这并不罕见。它会静静地坐在服务器房内，提供 Web 页面或处理域名服务，永不崩溃，且很少需要关注。然而，情况并非总是如此。你可能需要支持你的 Red Hat Linux 服务器上的用户，而这可能是你系统管理职责中最挑战性的部分。

Red Hat Linux 提供了多种工具来帮助你完成管理工作。`useradd`、`usermod` 和 `userdel` 命令允许通过命令行轻松操作用户账户数据。`linuxconf` 应用为管理任务提供了一个友好的点击式前端。此外，创建一个支持邮箱箱并构建 shell 脚本来自动化重复性任务将进一步减轻你的负担。Red Hat Linux 构建在丰富的 UNIX 历史之上，提供了一个支持用户多样化需求的理想平台。

# 自动化系统任务

## 本章内容

如果你必须在 Red Linux 系统启动时输入每个需要运行的命令，你将无法完成任何工作。同样，如果你将经常运行的一组命令组合在一起，你的工作会更高效。shell 脚本可以处理这些任务。

- 理解 shell 脚本
- 系统初始化
- 系统启动和关闭
- 调度系统任务

shell 脚本是一组命令、函数、变量或你在 shell 中使用的任何其他内容。这些项目被输入到一个纯文本文件中。然后，该文件就可以作为命令运行。Red Hat Linux 在系统启动期间使用系统初始化脚本来运行启动所需的程序。你可以创建自己的 shell 脚本来自动化你需要经常的任务。

本章提供了 shell 脚本内部原理及其使用方法的简要概述。你将学习 shell 脚本如何负责系统启动期间系统控制台上滚过的消息，以及如何将 shell 脚本用于调度设施（如 `cron` 或 `at`）来简化管理任务。

你还将学习如何调优机器使其在最合适的运行级别启动，并且仅运行所需的守护进程。有了这些理解，你将能够个性化你的环境，并减少重复输入相同命令的时间。

# 理解 shell 脚本

shell 脚本是一个包含命令序列的纯文本文件。它可以是一个你你不希望重复输入的简单单行命令；也可以是一个包含循环、条件语句、数学运算和控制结构的复杂程序；亦或是介于两者之间的任何内容。

## 第三部分 ♦ 管理 Red Hat Linux

shell 脚本等同于 DOS/Windows 中的批处理文件，但通过高级循环结构、逻辑操作符、函数和更大的命令库提供了更大的灵活性和控制力。shell 脚本的语法与编程语言非常相似，并能够处理许多任务。

Red Hat Linux 中提供了近十种 shell，其中某些在交互环境中的功能几乎完全相同。从角度来看，基本上有两种类型：基于 Bourne shell (`sh`) 的和源自 C shell (`csh`) 的。本章中的所有代码和示例都基于 `bash` (Bourne-again shell) 环境，该环境实现了原始 Bourne shell 的超集。事实上，`/bin/sh` 是指向 `/bin/bash` 的符号链接。

C shell 的语法（即命令和选项的构建方式）与 C 语言语言相似。它具有大多数 Bourne shell 不包含的交互能力。每个 shell 都使用不同的配置文件和不同的设置 shell 环境变量的方法。

# 执行 shell 脚本

shell 脚本是包含文本命令、函数、环境变量和/或注释的文件，你可以将其作为命令运行。理论上，shell 是一种组合命令序列的方式，而不是在 shell 提示符处手动输入它们。现实中，shell 脚本可以像任何可执行程序一样复杂。

执行 shell 脚本有两种方法：

- 将文件名作为 shell 的参数（例如 `bash shell_script_file`）。在这种方法，文件不需要具有可执行权限；它只包含 shell 命令。命令行上指定的 shell 将用于解释脚本文件中的命令。这最适用于快速、简单的任务。
- 通过在命令行上指定文件名来执行 shell 脚本。这要求 shell 脚本的第一行包含 shell 的名称。

# 414 第三部分 管理 Red Hat Linux

变量可以包含命令的输出。将变量设置为命令的输出有一个用处，即你可以利用在特定条件下发生变化的信息。在下面的示例中，`MACHINE` 变量被设置为 `uname -n` 命令的输出。这将始终将 `MACHINE` 设置为当前计算机的名称。

```
MACHINE=`uname -n`
```

包含在反引号中的命令在子壳（subshell）中执行，输出结果存储在变量名中。在这种情况下，`-n` 命令输出计算机的主机名（例如 `baskets.redhatsonhistory.com`），并将值赋值给 `MACHINE` 变量。

子壳提供了一种在当前 shell 之外执行命令或系列命令的方法。子壳与当前 shell 的相似之处在于，它会记住来自父 shell 的命令位置和环境变量值。然而，子壳环境的更改不会自动保存回父 shell。

变量还可以取其他变量的值。这是在 shell 脚本运行时利用变化信息的一种方法。例如，shell 脚本可以确定账户余额 (`$CurrentBalance`) 并将该值存储在 `BALANCE` 变量中，从而允许该值被保存为：

```
BALANCE=$CurrentBalance
```

赋值时，只需要变量名。引用时，变量名之前必须带有一个美元符号 (`$`)。

# 在 shell 脚本中执行算术评估

虽然 shell 脚本中的变量可以包含数字，除非内置命令另有说明，否则所有值都被视为数字字符串。整数算术可以使用内置的 `expr` 命令进行。例如，假设变量 `BIGNUM` 包含值 1024，以下两个命令都会将值 64 存储在 `RESULT` 变量中：

```
let Result=$BIGNUM/16
Result=`expr $BIGNUM / 16`
```

虽然 shell 脚本的元素相对自由的（空格或制表符等空白并不重要），但上述两个命令对空格都有特殊要求。`let` 命令要求每个操作数和数学运算符之间不能有空格，而 `expr` 命令要求每个操作数与其运算符之间留空格。
