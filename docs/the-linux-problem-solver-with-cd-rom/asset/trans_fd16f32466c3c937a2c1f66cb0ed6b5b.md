

# 问题 25

症状：无法 rsh 到远程主机。

问题：你关闭了 rshd。

修复：现在，在你习惯使用 rdist 的同时，你可以做以下两件事之一。

你可以通过对 /etc/inetd.conf 进行适当的更改（参见第 2 章）暂时重新打开 rsh，并在你的 /etc/hosts.deny 文件中添加以下内容：

```
in.rshd: ALL except servername
```

其中 servername 是你运行 rdist 的机器。（不要忘记远程主机上需要有 .rhosts 或 hosts.equiv，因为 .rhosts 本身可能会造成安全漏洞。）

如果，你可以无需密码 ssh 到远程主机（这需要匹配的主机密钥和 authorized keys 或 hosts.equiv），只需将以下代码放入名为（例如）sish 的脚本中：

```
#!/bin/sh
ssh -q $0
```

然后（假设 sish 在当前目录中），你可以使用 rdist 如下：

```
$ rdist -P ./sish
```

（我们稍后会详细介绍如何使用 ssh 与 rdist。）

## 选项

我们现在介绍了 rdist 的一个选项 -P。rdist 有两种类型的选项：普通（常规）和 dist 选项。常规选项与其它程序中的相同：路径名、配置文件、标志等。Dist 选项控制远程分发，并在命令行上使用 -o 指定，如此示例：

```
$ rdist -oremove,younger,verify
```

这一行告诉 rdist 删除存在于远程主机上但不在本地目录中的文件。它还指示 rdist 忽略远程上修改时间比本地副本更新的文件，并仅验证（即说明 rdist 需要做什么）而不实际执行。

Distfile 中的 dist 选项如下所示：

```
( www SRC ) -> ( mikado atlantic )
    install -oremove,younger ;
```

第二行是一个命令。除了指定 dist 选项外，命令还允许通过比较某些文件参数（如日期）实现更严格的分发控制。以下是关于命令的更多内容。

## 命令

### except, except_pat

忽略文件和目录（不更新它们）。except pat 接受正则表达式作为参数并忽略匹配的文件或目录。

示例：

```
except lib ;
except pat ^/usr/local/etc/.*\.conf$ ;
```

**问题 26**

**症状：** 某些文件神秘地没有得到更新。

**问题：** 过度使用 except_pat。

**修复：** 使用 --verify dist 选项并检查输出。尝试让所有表达式以插入符号（^）开头并以美元符号（$）结尾。正则表达式

```
except_pat etc/.*\.conf ;
```

匹配 /etc、/usr/etc 和 /usr/local/etc 中的文件（即，如果这些目录首先在 dist 中指定）。

### install

指定选项或备用安装目录。我们已经在例如

```
install -oremove,iglinks ;
```

的示例中看到过 dist 选项。对于备用安装目录，rdist 的行为取决于源文件。对于 Distfile

```
( stuff ) -> ( atlantic pacific )
    install -oremove newstuff ;
```

文件或目录 stuff 在远程主机上作为 newstuff 分发。然而，下面的 Distfile 演示了不同的场景：

```
( morestuff/one morestuff/two morestuff/3/4 stuff ) -> ( atlantic pacific )
    install -oremove newstuff ;
```

在这种情况下，rdist 将 morestuff/one 和 morestuff/two 放入远程主机上的 newstuff/one 和 newstuff/two，但 morestuff/3/4 变为 newstuff/4，而 stuff 进入 newstuff/stuff！

为什么 rdist 要这样做？它试图匹配项目，用 install 的参数替换尽可能多的基本目录。如果 rdist 确定源路径名是目录（morestuff 和 morestuff/3 的情况），它会用 install 的参数（这里是 newstuff）替换整个路径名。但在我们的示例中，rdist 不确定 stuff 是否是目录。如果 stuff 只是一个文件，尝试将其内容放入 newstuff 就毫无意义

# 问题 27

症状：rdist 对单个参数的行为不同。

问题：rdist 的设计。

修复：如果你的需求比较简单，使用下面的 whole dist 选项（见下文）强制项目出现在目标目录中而不进行任何路径改动。尽量不要对 rdist 命令使用目录选项并带有任何复杂参数，因为 resulting 目录结构可能不可预测。如果需要，请在 Distfile 中拆分它们。

### notify

将 rdist 的结果发送给用户，例如：

```
notify foo@example.com ;
```

此选项只有在你想在同一个 Distfile 中通知不同的人特定更改时才真正有用。否则，你只需将 rdist 的输出记录到文件中并邮件发送给用户。

### cmdspecial, special

当某个文件被分发到机器时，special 指示 rdist 立即在该机器上运行一个程序。以下是 syslogd 及其配置文件的一个示例：

```
special /etc/syslog.conf " /bin/kill -HUP `cat /var/run/syslogd.pid`"
```

