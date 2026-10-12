
`echo "你的名字下有 $no_logins 个登录进程"`

`echo "你被允许 $no_allowed 次登录(s)."`

```bash
if [ $no_logins -gt $no_allowed ]; then

    echo "你超过了允许限制。"

    echo "请稍后再试。"

    sleep 5

    exit 0

fi
```

```bash
else

echo "你是超级用户，可以随心所登录！"

```
## 转向 Linux 业务桌面

在下面的示例中，你创建一个名为 `user.allow` 的文件，后面跟着一个空格和一个数字，该用户被允许登录数字指定的次数。

`marcel 3`
`tux 2`
`natika 4`

在那个示例中，`marcel` 被允许登录三次，`tux` 被允许两次，`natika` 总共允许登录四次。所有其他用户默认允许登录一次。为了确保每个人都执行此脚本，请向 `/etc/profile` 文件添加此行：

```
/usr/local/.Admin/logtest
```

注意行开头的点，它告诉 shell 来源或执行随后的文件名。

# 附录 B 自动化与脚本

注意在执行 `[-z $no_allowed]` 的代码行中的 `-z` 测试。这会测试变量 `$no_allowed` 以检查其长度是否为零。如果它为零（换句话说，UID 未在 `user.allow_exceptions` 文件列表中），我们将该数字默认设为一。

注意：你的 shell 支持对变量和文件类型进行多种测试。例如，你可以测试字符串长度是否为零（如你在示例中使用 `-z` 所的那样）、测试文件是否可执行（`-x`），或者文件是否存在（`-e`）。系统内置了许多此类测试可用于文件或变量。若要查看 shell 支持哪些类型的测试，请输入 `man test`。

因此，如果你尝试第四次以 ascel 的身份登录，你会收到此消息：

+ 你的名下有... 4 个登录进程。
你被允许登录 3 次。
你已超过了允许的限制。
请稍后重试。

在此时，你会被注销，并且必须开始习惯不要那么贪婪。

## 指定 Shell

如果你查看 `/etc/rc.d/init.d` 目录下的某些启动脚本，或者 `/etc/init.d` 目录，你会注意到它们开头都有一个非常有趣的短结构。以下是我我的 `inet` 启动脚本的前五行：

```bash
root@testsys [/root]$# head -5 /etc/rc.d/init.d/inet

#! /bin/sh

#  inet          启动 TCP/IP 网络服务。此脚本

#             启动互联网网络守护进程。

#  
```

看到开头的这行 `#! /bin/sh` 了吗？这种 hash-bang（散字节）`#!/path_to_shell` 结构是强制使用特定类型 shell 来执行脚本的一种。假设你创建了一个使用 C shell 特有结构来工作的 shell 脚本。让 `bash` 执行执行显然无法得到你想要的结果。此外，还有一些系统函数（如 `at` 命令）会使用 `/bin/sh` 执行它们的所有命令。如果你创建的脚本某些基础 `sh` 无法理解的 bash 命令，该怎么办？

解决方案很简单。只需在你的 shell 脚本顶部加上这一行即可：

```bash
#!/bin/bash
```

现在，即使运行它的 shell 是 `/bin/sh`，它也会切换到 `/bin/bash` 来执行脚本。这也用于定义其他的脚本环境。Perl 脚本开头也有这一行：

```bash
#!/usr/bin/perl
```
