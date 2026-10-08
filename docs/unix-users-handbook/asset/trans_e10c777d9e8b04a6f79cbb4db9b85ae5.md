

## 在 .cshrc 中初始化历史列表

C shell 可以保留您已发出的命令历史记录。如果您希望重新发出某条命令或查看之前发出的命令，可以使用历史列表。

发出的命令通过编号来引用，因此您希望系统名称后出现一个编号。**​.cshrc** 中的以下行提供了系统名称后的一个编号：

```
set prompt = "$system \!: "
sys1 1:
```

我们稍后将讨论 shell 和环境变量，但现阶段只需知道 **$system** 对应系统名称 "sys1" 即可。

您可以指定在发出 **history** 命令时希望保存和查看的先前已发出命令的数量。**.cshrc** 中的以下行将历史列表设置为 20：

```
set history = 20
```

当发出 **history** 命令时，会显示最近发出的 20 条命令。

*savehist* 变量允许您在注销后保存指定数量的历史命令。默认情况下，当您注销时，历史列表会被清除。此变量的值为 20，这意味着在下一次登录时，将保存前一个会话的 20 条命令。

## 命令行历史

您可以通过多种方式查看历史列表。首先，让我们通过简单地发出 **history** 命令来查看最后 20 条命令：

```
sys1 23: history
        4 whoami
        5 pwd
        6 find / -name login -print &
        7 hostname
        8 who
        9 more /etc/passwd
       10 history
       11 history 5
       12 echo $PATH
       13 more .login
       14 cat .login
       15 exit
       16 exit
       17 history -h
       18 pwd
       19 whoami
       20 cd /tmp
       21 cat database.log
       22 cd
       23 history
sys1 24:
```

我们也可以在打印历史列表时省略行号，如下面的示例所示：

```
sys1 24: history -h
pwd
find / -name login -print &
hostname
who
more /etc/passwd
history
history 5
echo $PATH
more .login
cat .login
exit
exit
history -h
pwd
whoami
cd /tmp
cat database.log
cd
history
history -h
sys1 25:
```

接下来，让我们按反序打印历史列表：

```
sys1 25: history -r
25 history -r
24 history -h
23 history
22 cd
21 cat database.log
20 cd /tmp
19 whoami
18 pwd
17 history -h
16 exit
15 exit
14 cat .login
13 more .login
12 echo $PATH
11 history 5
10 history
9 more /etc/passwd
8 who
7 hostname
6 find / -name login -print &
sys1 26:
```

我们还可以选择要从历史列表中打印的事件（命令）数量。下面的示例仅打印历史列表中最后 10 条命令：

```
sys1 26: history 10
17 history -h
18 pwd
19 whoami
20 cd /tmp
21 cat database.log
22 cd
23 history
24 history -h
25 history -r
26 history 10
sys1 27:
```

可以看出，您有多种方式生成先前发出的命令列表。表 7-1 总结了本节中发出的命令。

### 表 7-1 命令行历史

| 命令 | 描述 | 示例 |
| :--- | :--- | :--- |
| history | 生成带有编号的每条命令的历史列表。 | history |
| history -h | 生成不带行号的历史列表。 | history -h |
| history -r | 按反序生成带有编号的每条命令的历史列表。 | history -r |
| history n | 从历史列表中生成最后 n 条带有编号的命令。 | history 10 |

## 重新执行历史列表中的命令

您可以使用多种技术重新执行历史列表中的命令。我们将使用最常用的技术来重新执行历史中的命令。

您可以使用 !! 重复最后一条命令，使用 !2 重复第二条命令，使用 !c 重复以 "c" 开头的最后一条命令。让我们发出 **history** 命令以获取最后 20 条命令的列表，然后重新执行其中的一些：

```
sys1 27: history
      8 who
      9 more /etc/passwd
     10 history
     11 history 5
     12 echo $PATH
     13 more .login
     14 cat .login
     15 exit
     16 exit
     17 history -h
     18 pwd
     19 whoami
     20 cd /tmp
     21 cat database.log
     22 cd
     23 history
     24 history -h
     25 history -r
     26 history 10
     27 history
sys1 28:
```

让我们首先使用 `!!` 重新发出最后一条命令：

```
sys1 28: !!
     history
      9 more /etc/passwd
     10 history
     11 history 5
     12 echo $PATH
     13 more .login
     14 cat .login
     15 exit
     16 exit
     17 history -h
     18 pwd
     19 whoami
     20 cd /tmp
     21 cat database.log
     22 cd
     23 history
     24 history -h
     25 history -r
     26 history 10
27 history
28 history
sys1 29:
```

现在让我们使用 !19 重新发出第 19 条命令：

```
sys1 29: !19
whoami
martyp2
sys1 30:
```

现在让我们使用 !p 重新发出以 "p" 开头的最后一条命令：

```
sys1 30: !p
pwd
/home/martyp2
sys1 31:
```

表 7-2 包含一些常用的历史列表调用命令。

### 表 7-2 从历史列表调用命令

| 命令 | 描述 | 示例 |
|---|---|---|
| !N | 发出第 N 条命令 | !2 |
| !! | 发出最后一条命令 | !! |
| !-N | 发出距最后一条命令第 N 条的命令 | !-N |
| !str | 发出以 str 开头的最后一条命令 | !c |
| !?str? | 发出命令行中任何位置包含 str 的最后一条命令 | !?cat? |
| !{str}str2 | 将 str2 追加到包含 str 的最后一条命令 | !{cd} /tmp |
| ^str1^str2^ | 在最后一条命令中用 str2 替换 str1 | ^cat^more^ |

## .cshrc 中的别名

别名是您为常用命令或命令序列选择的名称。许多别名已为您预定义。

您可以使用 .cshrc 文件作为存储别名的地方，并且每次登录时都会读取这些别名。您还可以在命令行提示符处定义别名，但这些别名在您注销时会被清除。

不带任何参数的 alias 命令会列出所有别名。此列表包括预设别名以及您设置的别名。以下 alias 命令显示了我正在其工作的系统上的所有预设别名：

```
sys1 7: alias
d	dirs
m	more
pd	pushd
pd2	(pushd +2)
po	popd
status	(date; bdf)
sys1 8:
```

您并不局限于仅使用预设别名。要创建自己的别名，您首先发出 alias 命令、别名的名称，然后是在别名被执行时执行的命令或多个命令。

让我们现在创建几个简单的别名。第一个为 history 命令创建了别名 "h"：

```
sys1 1: alias h history
sys1 2: h
	history
```

![](img/75f39fc91296b889c0653851accdfd46_407_0.png)

每次您输入 **h** 时，都会执行 history 命令。

下面的示例创建了一个包含空格的命令别名，因此该命令被单引号包围：

```
alias ls='ls -al'
alias
ls
```

第一条命令为 "ls" 创建了一个执行 **ls -al** 命令的别名。然后我们发出 **alias** 命令以查看新别名是否确实出现在别名列表中。接着我们运行 **ls** 以查看是否执行了 **ls -al**。

在设置别名后，您不必在整个会话期间保留该别名。如果您不喜欢某个别名，可以使用 **unalias** 命令来移除别名。

为了查看 **unalias** 的效果，让我们再次生成别名列表，使用 **unalias** 取消设置 **h** 别名，并运行 **h** 命令以查看它是否确实被移除。

```
unalias h
h
```

当我们发出 **unalias** 来移除 **h** 别名，然后尝试运行 *h* 时，系统提示未找到 *h*。

![](img/75f39fc91296b889c0653851accdfd46_407_1.png)

```
sys1 3:alias proc 'echo "Number of processes are: \c";
ps -ef | wc -l'
			# 外部是单引号
			# 内部是双引号
```

当您运行 **proc** 时，您将看到以下内容：

```
sys1 4: proc
Number of processes are: 44
```

在此命令行中发生了大量的引号处理。要理解此行中发生了什么，请参考表 7-3 以获得帮助。

