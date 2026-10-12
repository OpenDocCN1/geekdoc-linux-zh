

请记住，图形用户界面环境（如 GNOME 和 KDE）提供了许多补充或替代上述所列命令的工具。GUI 工具更容易学习，但一旦你掌握了命令行环境，它们通常更灵活且速度更快。

如果你的关注点是通用的 UNIX 系统，你希望学习常规命令，因为 GUI 环境中的那些强大工具在大多数版本的 UNIX 中是不可用的。

你记住 Linux 安装是可配置的这一点非常重要。这意味着你可以在安装期间选择（配置或挑选）要加载的工具和实用程序。如果你发现本节中的某个命令在你的机器上不工作，最可能的原因是你尚未加载它。

- `.` shell 命令告诉 shell 执行传递给该命令参数的文件中所有命令。这在 bash 或 dksh 中有效。在 csh 中的等效命令是 `source`。以下示例执行命令 `a.do`：
  ```
  . a.do
  ```

- 在任何其他命令后插入的 `&` shell 运算符告诉计算机在后台运行该命令。通过将任务放入后台，用户可以继续使用该 shell 处理其他命令。如果在前景中运行命令，用户无法继续使用该 shell，直到进程结束。

- `|`（管道）shell 运算符用于命令行上不同程序之间，将一个命令的输出“管道”传输到另一个命令。这种操作是 Linux 和 shell 的主要优势之一，可用于由一系列简单程序构建复杂命令。例如，你可以将 `cat` 命令的输出通过 `sort` 命令进行管道传输，以排序文件内容：
  ```
  # cat long_list.txt | sort
  ```

- `>`（标准输出）shell 运算符将程序的输出发送到文件或设备。请谨慎使用此运算符：它会覆盖已存在的文件！要将当前目录的列表保存到文本文件中，请像这样使用 `>` 运算符：
  ```
  # ls > dir.txt
  ```

请注意，如果文件 `dir.txt` 存在，它将被擦除并覆盖为新内容！另外，由于 Linux 的工作方式与其他版本的 UNIX 非常相似，你可以将程序的内容直接发送到设备：
```
# cat welcome.au >/dev/audio
```
这通过直接向 Linux 音频设备发送来播放声音文件。

- `<`（标准输入）shell 运算符用于向程序提供文件内容或来自其他设备或源的输入。例如，你可以将此运算符与 `cat` 命令一起使用来排序文件并保存结果：
  ```
  # sort < unsorted.txt > sorted.txt
  ```

- `>>`（追加）shell 运算符不会替换指定的文件，而是将程序的输出追加到指定文件的末尾。例如，这可以用于构建日志文件：
  ```
  # cat newfile.txt >> oldfile.txt
  ```
  `newfile.txt` 的内容不会覆盖 `oldfile.txt`，而是会追加到其末尾。

- `<<`（称为“此处文档”）shell 运算符用于告诉程序何时到达输入末尾。例如，要将 shell 用作文本编辑器，像这样告诉 shell 当使用单词 `end` 时停止接受输入：
  ```
  # > document.txt << end
  This is a line of text.
  end
  ```
  输入单词 `end` 后，因为告诉 shell 单词 `end` 终止输入，所以 shell 会将你的文本保存到文件 `document.txt`。

## adduser

由 `root`（或其他拥有权限的人）使用的 `adduser` 命令创建新用户。`adduser` 命令后跟要创建的帐户名称：
```
# adduser dppits
```

## alias

**alias** 命令用于创建命令的别名或替代名称。通常，这些别名是实际命令的缩写。在以下示例中，用户（可能是 DOS 用户）正在为目录列表添加 *dir* 的别名：
```bash
alias dir=ls
```
单独键入 *alias* 会给出当前所有别名的列表。这样的列表可能看起来像这样：
```bash
svr01:/home/dpitts$ alias
alias d='dir'
alias dir='/bin/ls SLS_OPTIONS --format=vertical'
alias ls='/bin/ls SLS_OPTIONS'
alias v='dir'
alias vdir='/bin/ls SLS_OPTIONS --format=long'
```

## apropos 参数

apropos 字面意思是适当的或关于（他人）。后跟参数时，**apropos** 在 man 页面中搜索包含该参数的条目，对所有 man 页面执行关键字搜索。这等价于 *man -k 参数* 命令。

## ash

ash 是一个简单的 shell，具有与 *sh*（或 Bourne shell）非常相似的功能。ash shell 由位于 /bin 目录下的符号链接 *ash* 运行。

## at

at 在指定时间运行程序。你可以使用 **at** 命令安排任务或作业在你在命令行或文件中指定的时间运行。

## atq

使用 **atq** 列出等待中的作业队列。**atq** 命令打印 at 命令的等待作业或事件列表（通常位于 /var/spool/at 目录下）。

## atrm

使用 **atrm** 删除指定的作业。**atrm** 命令删除 at 队列中等待的一个或多个作业。**atrm** 命令可由用户或 root 操作员用于删除待定事件（停止 at 命令运行）。

### banner

banner 将大型高质量横幅打印到标准输出。如果省略消息，banner 会提示并从标准输入读取一行。例如，输入 `$ banner hi` 会创建如下横幅：

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_973_0.png)

### bash

bash 是 GNU Bourne Again Shell。作为 Red Hat Linux 的默认 shell，bash 具有许多功能，如命令行编辑、内置帮助和命令历史。bash shell 由位于 /bin 目录下的符号链接 sh 运行。

### batch

batch 命令根据平均负载运行作业。此程序用于在计算机达到由 /proc 目录中 /loadavg 文件中的实时值确定的特定平均负载时运行事件。batch 还有其他选项；详情请阅读 at 命令的手册页。

## bc

作为一种计算器语言，bc 是一个用于构建计算器程序和工具的翻译器和语言。你可以使用这个翻译器和语言来编程自定义计算器。

## bg

bg 命令用于强制暂停的进程在后台运行。假设你在前景中启动了一个命令（未在命令后使用 &），然后意识到它需要一段时间，但你仍然需要你的 shell。你可以使用 Ctrl+Z 将当前进程置于挂起状态。然后你可以让它保持挂起——就像你打电话给电话公司一样——或者你可以键入 bg 将该进程放入后台，释放你的 shell 以执行其他命令。

## bind

在 pksh 中使用，bind 命令允许用户更改键组合的行为，以用于命令行编辑。很多时候，人们将上、下、左和右箭头键绑定为在 Bourne Again Shell (bash) 中按那种方式工作。该命令使用的语法如下：
```
bind 键序列 命令
```
以下示例是创建绑定以在历史列表中上下滚动以及沿命令行左右移动的 bind 命令：
```
bind '^['=prefix-2
bind '^A'=up-history
bind '^B'=down-history
bind '^C'=forward-char
bind '^D'=backward-char
```

## cat

cat 连接文本文件并将它们发送到 stdout。如果文件包含二进制数据而不是文本，cat 的行为就像一个有毛球，将文件中的数据显示在屏幕上（尽管它不是你真正能读到的东西）。你还可以将 cat 的输出重定向到文件。正如你可能猜到的，cat 命令需要显示的内容，其格式如下：
```
cat <filename>
```

