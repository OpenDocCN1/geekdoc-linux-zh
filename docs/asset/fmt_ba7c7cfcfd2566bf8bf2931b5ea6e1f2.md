
`| ll | ls -d.* --color=tty | 列出目录名和以 * 开头的隐藏文件（文件），并对屏幕输出着色 |`

`| l | ls -l --color=tty | 显示详细目录信息（彩色） |`

`| ls | ls --color=tty | 以短格式（彩色）显示目录内容 |`

以下是一些你可能想要包含在别名列表中的常见拼写纠正错：

```bash
alias pdw=pwd
alias mroe=more
alias fiel=file
```

你可能想添加一个别名，将熟悉的命令翻译成 Linux 格式：

```bash
alias dir="ls -l"
```

导航类别名也很有用：

```bash
alias up="cd.."
```

你可以为常用（但很麻烦）的命令创建别名，例如解压 tar 包：

```bash
alias unpack="tar -zxvf"
```

第四个预定义别名是给习惯使用 vi 编辑器的 UNIX 用户准备。Linux 不再包含 vi，但它包含一个改进了很多的替代品 vim。那种在 vi 中打字的奇特习惯现在启动的是新程序 vim。

要显示开启连接的程序列表（例如网络浏览器或流媒体音频），请创建此别名：

```bash
alias netcon="netstat -p | grep -v'unix'"
```

这些只是你可能在 shell 中发现的惊人别名。继续阅读了解如何自己创建一些别名。

## 创建简单的省时别名

创建别名很容易。这里有一个示例，为我们最常见的打字错误创建一个别名：但如果你在命令行上使用 `-i`，`rm` 会要求你确认它想要删除的每个文件。当你每次执行 `rm *.gz` 时，这可能是救星（第一个命令中 `*` 之后的额外空格告诉 rm 删除你目录中的所有内容——这通常不是你想要的）。

```bash
$ alias pdw=pwd
```

现在，我们想知道当前目录，但不小心输入了 `pdw`，bash 通过将命令翻译为正确的 `pwd` 来帮助我们。

```bash
alias rm="rm-i"
alias cp="cp-i"
alias mv="mv-i"
```

bash 仅当别名是命令行中的第一个单词时才会展开它。我们最喜欢的别名修复了拼写错误，创建了快捷方式，并在我们忘记时提供帮助。

## 使用别名处理复杂命令

（注：此处由于原文存在大量重复且不完整的英文，已根据上下文逻辑进行了整合处理）

# 瞬间监控你的系统

两步走：配置（在这种情况下，使用所有默认选项）并制作。当 `loadcode` 完成时，给自己赋予超级用户权限并执行 `make install`。

# 为 loadcode 添加计时器

别名和函数可以协同工作。这里有一个别名，它会在 `loadcode` 运行完成后让你的电脑发出哔声（假设你已经正确配置了声卡）。它有点像微波炉上的计时器。

`loadcode` 只是你为一组命令命的名字。命令会一个一个执行，如果出现问题，脚本也会继续运行。你可以通过添加一些错误检查来改进：

```bash
alias beep="tput bell inside the loadcode module, or just use it the command line, like:
```

```bash
function loadcode() {
  if wget -q -O $1 | tar -xvf -
  then
    cd $(basename $1 .tar.gz) || return 1
    ./configure && make
  else
    echo "Can't download $1"
  fi
}
```

```bash
$ loadcode
ftp://ftp.gnu.org/gnu/barcode/barcode-08.var.tar.gz; beep
```

当 `loadcode` 完成工作时你会听到声音。如果你网络连接缓慢，`loadcode` 可以接收任务并运行。

现在，如果发生错误，`loadcode` 就会失败，而不是以它那种快乐（且误导）的方式继续下去。新版本的 `loadcode` 显示了检查错误状况的方法：

# 瞬间监控你的系统

到为止，你已经看到了为命令行设计的函数和别名，但你也可以从命令行启动图形化程序。这里有一个别名，可以启动一个新的 x 窗口来显示 `top` 命令的输出（类似于一个自制的系统监控器）：

- 第一条命令现在封装在一个语句中。如果 `wget` 或 `tar` 命令失败（即它们以非零返回码退出），`loadcode` 跳到 `else` 子句并显示友好的错误信息。`loadcode` 跳到 `then` 子句。

- 如果你解压的目标遵循通常的命名约定，`cd` 命令可能会失败。为了捕捉这类问题，`loadcode` 使用 `||`（逻辑或）运算符在 `cd` 命令失败时退出。你可以将其读为“要么 cd 成功，要么返回 1”。

- 如果你没有要安装的包所需的依赖项，`configure` 命令也会失败。在这种情况下，`loadcode` 使用 `&&` 运算符来捕捉配置失败。你可以将其读为“执行 configure，如果成功则执行 make”。

```bash
alias top="xterm -e top &"
```

定义此之后，只需输入 `xterm` 即可打开一个运行 `top` 命令的新窗口（见图 10-1）。

如果你想运行一个具有更复杂命令行的程序，只需定义一个函数。例如，以下函数打开一个新窗口，显示文件的最后五行，并在文件添加内容时作为新文本继续显示：

```bash
function xtail() {
  xterm -e "tail -f $1 &"
}
```

## 技术 10：使用别名和函数让生活保持简单

你知道 `tar` 命令（至少是 GNU 版本的 `tar`）可以处理未压缩、gzip 压缩和 bzip2 压缩归包。很容易创建一个带有正确标志set的封装函数来调用 `tar`。`tar` 函数（见列表 10-1）使用文件来确定给定归包是否压缩，如果压缩，使用了哪种压缩方法。`tar` 比此技术中的其他函数长得多，因此我们在列表中包含了两个节省时间的特性：

![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_78_0.png)

保存中间结果的局部变量：

- 你可以在不使用局部变量的情况下重写此函数，但维护它将耗费更多时间。

- 帮助未来维护者理解我们逻辑的注释：bash 语法可能会变得非常晦涩，现在对代码进行注释将将在将来为你节省大量时间。

**图 10-1：** 在你的窗口中运行 `top`。

如果你有超级用户权限，可以使用 `xtail` 系统日志文件：

```bash
## xtail /var/log/messages
```

# 更简单的解压方式

你还可以通过创建适应命令行参数的自适应函数来节省时间：

**列表 10-1：** 根据文件类型选择正确的程序

```bash
function tarls {
  # 确定我们正在处理什么类型的文件。

  local filetype      # 来自 file 命令的输出
  local type         # 去掉文件名的 $filetype
  local compressype # $filetype 的第一个单词
  local tarflags     # 传递 tar 命令的标志

  # 给参数如：
  # icons.tgz
  # filetype 将包含
  # icons.tgz: gzip compressed data

  filetype=$($1)

  # 现在从 $filetype 中剥离前面的文件名
  # 留下
  # gzip compressed data

  type=$(echo $filetype | cut -d: -f2-)
  # 最后，从 $type 中获取第一个单词
  # 留下
  # gzip

  compresstype=$(echo $type | cut -d' ' -f 1)

  case $compresstype in
    gzip) tarflags=-ztvf;
    bzip2) tarflags=-jtvf;
    posix) tarflags=-tvf;
    *) echo "Unknown archive type"; return 1;
  esac

  tar $tarflags $1
}
```

## 第二部分

## 充分利用你的文件系统

Rich Tennant 著《第五波浪》

![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_81_0.png)

> “到为止，他叫来了眼镜蛇、两条蟒蛇和一群蜥蜴，但还没有我们正在寻找的文件。”

## 11 技术 在 Windows 世界中共享文件和打印机

## 通过以下节省时间

- 使用 `Samba` 配置

- 从 `Windows` 获取文件

- 从 `Windows` 获取打印机

- 使用 `Samba`

## 在 Windows 世界中共享文件和打印机
