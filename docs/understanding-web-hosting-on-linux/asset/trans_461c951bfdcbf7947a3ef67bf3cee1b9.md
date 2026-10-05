

# 使用 Bash Shell 183

| 表 12.4: 引用字符串中的特殊字符 |
| 字符 | 含义 |
| --- | --- |
| ' | 单引号对内的文本被视为字面量。Shell 变量和元字符不会被替换为解释后的值。 |
| " | 与单引号类似，但 shell 变量会被替换为它们的值。 |
| ` | 反引号内的文本将作为子命令执行，其输出将用在包裹它的命令中。 |
| \ | 反斜杠后的字符被视为字面量；忽略任何元字符的含义。如果反斜杠是行的最后一个字符，它向 shell 信号指示将有延续行。 |

下面的三个命令会导致执行结果差异巨大：

```bash
$ echo '$PATH'
PATH
echo "PATH"
/bin:/usr/bin/X11R6/bin:/usr/local/bin:home/donat/bin
echo $PATH
/bin:/usr/bin/X11R6/bin:/usr/local/bin:home/donat/bin: No file or directory
```

在第一个命令中，反引号内的字符串包含一个 UNIX 命令 `pwd` 的名称。`pwd` 命令列出当前工作目录……第二个命令将 `PATH` 包含在双引号中，因此 bash 获取 `PATH` 变量的值并列出。在最后一个命令中，bash 假设反引号内的文本包含一个有效的命令。

在命令中使用反引号的更好的示例如下：

```bash
$ CLASSPATH=$CLASSPATH:pwd /xml4j.jar
```

在这个命令中，反引号内的字符串包含一个 UNIX 命令 `pwd` 的名称。`pwd` 命令列出当前工作目录。在 Java 开发过程中，我们经常修改 `CLASSPATH` 以包含各种 Java 归包。修改 `CLASSPATH` 的一种方法是将当前目录更改到文件存储所在，然后使用上述命令，如下：

```bash
$ /opt/java/jdom-b6/lib
$ ls *.jar
ant.jar collections.xerces.jar
$ CLASSPATH=$CLASSPATH:pwd /xerces.jar
```

# 别名 (Aliases)

这里介绍的最后一个高级 shell 特性是别名。`alias` 工具允许你为命令字符串分配一个名称。学习别名的好方法是查看 Red Hat 为你设置的别名。你可以通过带有 `-p` 选项的 `alias` 命令查看系统中所有的别名。以下显示了登录到我们的 Red Hat 7.1 系统时的结果：

```bash
alias -p
alias ls='ls --color=tty'
alias ll='ls -l --color=tty'
alias l='ls -d [a-zA-Z]* --color=tty'
alias rm='rm -i'
alias mv='mv -i'
alias cp='cp -i'
alias which='alias /usr/bin/which --tty-only-read-alias-show-dot-show-tilde'
```

当你对 Red Hat 的默认别名使用 `ls` 命令时，你实际上在使用一个名为 `ls` 的别名。该别名调用实际的 `ls` 命令，但在设置 `--color-tty` 默认选项之前。Red Hat 还创建了一个名为 `ll` 的别名，它带带了“长列表”选项的 `ls` 命令。

Red Hat 为 shell 命令 `rm`、`mv` 和 `cp` 创建了别名，以将其默认选项设置为 `-i`，这使得这些命令会交互式地提示用户确认是否真的想要删除、移动或复制该文件。如果你犯了错，你可能想从 `/root/.bash_profile` 中删除这些别名（或者直接使用 `-f` 选项强制它们在无提示的情况下运行——但仅在你确定命令将按预期工作时）。

我们使用别名在切换目录时避免输入全名。确实，单词补全可以帮你快速输入目录名，但远没有一个简单的别名快。在本章前面，我们讨论了使用单词补全来避免输入长目录 `/opt/tomcat/webapps/WEB-INF/classes/com/manta`。相反，你可以创建一个 `cpmanta` 别名，这将切换到该目录变得轻而易举：

```bash
alias cpmanta='cd /opt/tomcat/webapps/manta/WEB-INF/classes/com/manta'
```

创建此别名后，你可以将其放入 `.bash_profile` 中，这样每次登录时都可以使用。

# 章节复习

# 核心术语

| aliases | CLSPATH | piping |
|---|---|---|
| bash shell | dot profile | Q shell |
| Bourne shell | grep | recursive |
| C shell | Korn shell | redirection |
| cat | PATH | variables |

# 复习题

1. 在命令中，安培符 `&` 的作用是什么？
2. "GUI" 代表什么？
3. 在 UNIX 环境中，什么是 shell（壳）？
4. "bash" 是什么缩写？

# 编程作业

# 练习 1：创建目录报告

1. 创建一个列出你的家目录内容的报告文件。
   a) 在报告文件中包含一个包含全名和目录名的表头。
   b) 确保列表包含每个文件的大小。
2. 使用 Java `jar` 工具，列出 `/opt/tomcat/lib` 中 `servlet.jar` 的内容。
3. 使用 `find` 命令：
   a) 列出 `/opt/tomcat` 下所有的 HTML 文件。
   b) 列出 `/opt/tomcat/examples` 下所有的 HTML 文件。
4. 管道 (Piping)：
   a) 使用 `find` 命令列出 `/opt/tomcat/lib` 中所有的文件。
   b) 使用 `find` 命令列出 `/opt/tomcat/examples` 中所有的文件。
   c) 使用 `find` 命令使用 `-name` 参数列出 `/opt/tomcat/examples` 中所有的 HTML 文件：
   $ find /opt/tomcat/examples -name "*.html"

# 练习 2：环境变量

1. 列出所有环境变量。
2. 使用你的姓创建一个新的环境变量。（记住，环境变量使用大写字母。）将该环境变量的值设置为你的名。
3. 使用以下方法向环境变量添加内容：
   a) 将你的当前目录更改为 `/opt/tomcat/lib`。
   b) 使用反引号修改 `CLASSPATH`：
   $ CLASSPATH=$CLASSPATH:`pwd`
4. 列出所有环境变量。将输出重定向到打印机。

# 练习 3：练习通配符 Globbing 

1. 查找 `/opt/tomcat/examples` 下所有名称中包含 "lo" 的文件。将输出重定向到打印机。
2. 查找所有名称中包含数字的文件。将输出重定向到打印机。
3. 查找所有名称中包含大写字母的文件。将输出重定向到打印机。

# 练习 4：创建别名

1. 列出所有当前别名。
2. 创建一个启动 Tomcat 的别名。注意 Tomcat 使用以下命令启动：
```bash
# sh /opt/tomcat/bin/startup.sh
```
3. 列出所有当前别名。将输出重定向到打印机。

