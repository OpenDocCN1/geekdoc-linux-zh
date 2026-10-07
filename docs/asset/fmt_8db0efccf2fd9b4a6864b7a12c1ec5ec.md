
追踪（Tracing）是一种非常有用的调试技术，shell 在评估每个语句之前会将其写入标准输出，让你看到将运行的命令。要启用追踪，请使用带有 `-x` 标志的 `set` 命令。

以下示例显示了为什么这些选项很有用：

```bash
# 创建 effective-shell 文件夹。
mkdir -p ~/effective-shell
```

```bash
# 下载并解压 effective-shell 示例。
samples_uri='https://effective-shell.com/downloads/effective-shell-samples.tar.gz'
wget -c "${samples_uri}" -O - | tar -xz ~/effective-shell
```

如果没有 `set -e` 选项，如果 `mkdir -p` 命令失败，脚本将继续运行。具体来说，它将尝试向一个不存在的文件夹下载并解压文件。为什么 `mkdir -p` 会失败？即使文件夹已存在 `mkdir -p` 也会成功，但如果指定位置有一个文件，它仍然会失败；如果你没有创建文件夹的相应权限，你必须小心你认为会成功运行的命令，等等。

此代码段的第二部分使用 `wget` "web get" 命令下载示例并将结果通过管道到 `tar` 以提取它们。在这种情况下，如果你只设置了 `-e` 且 `wget` 失败（例如地址错误或你离线了），shell 将继续运行脚本的后续命令并调用 `tar`，这将不会按预期工作。

（注：原文中存在大量重复段落，译文已根据要求去重处理。）

你也可以在 `if...else` 语句中使用 `declare` 来检查变量是否已设置：

```bash
if declare -p -A my_options 2>1 /dev/null; then
    echo "$my_options exists"
else
    echo "$my_options does not exist"
fi
```

除非你显式在变量不存在时打印消息，否则你需要像这里将输出重定向到 `/dev/null` 来隐藏它的错误输出。你也可以使用这些 `declare` 技巧来显示所有已声明的函数、检查函数的值，或检查某个函数

# 取消值

使用 `unset`（“取消变量或函数”命令）来清理你不再需要的变量和函数：

```bash
# 从 shell 会话中移除 "is_even" 函数。
unset -f is_even
```

取消变量和函数是非常重要的，特别是在 `.bashrc` 或 `.bash_profile` 文件中。这些文件在 shell 启动时被加载以应用自定义设置，留下不必要的值可能会无意中与其他配置或脚本发生冲突。第 15 章涵盖了 `.bashrc` 和 `.bash_profile` shell 初始化文件以及关于配置 shell 的许多细节。

请注意，如果用户只是在子shell 中运行脚本，除非使用 `EX` 设置变量，否则没有变量会被保留。

# 捕获信号和事件

`trap`（“捕获信号和事件”）命令指定了当 shell 接收某些信号或发生特定条件（如脚本退出或函数返回）时运行的命令。

`trap` 的一个常见用法是在脚本执行被中断时创建一个清理函数——例如，当用户按下 CTRL-C 取消脚本执行时（这会发送 INT，或“中断”信号）：

```bash
#为 effective-shell 下载创建一个临时文件夹。
source="https://effective-shell.com/downloads/effective-shell-samples.tar.gz"
tmp_dir=$(mktemp -d 2>/dev/null || mktemp -d 'effective-shell')
tmp_tar="$tmp_dir/effective-shell.tar.gz"
```

```bash
# 当脚本退出或被取消时定义一个清理函数。
cleanup() {
    if [ -e "$tmp_tar" ]; then rm "$tmp_tar"; fi
    if [ -d "$tmp_dir" ]; then rm -rf "$tmp_dir"; fi
}
```

```bash
# 在中断、终止信号和退出时清理。
trap --cleanup INT TERM EXIT

# 下载样本。
curl --fail --compressed -q -s "${source}" -o "${tmp_tar}"

# 提取样本。
tar - xf "${tmp_tar}" -C "${tmp_dir}"
```

此脚本设置了一个 `trap`，在脚本退出或中断时清理临时文件夹。它首先定义了一个名为 `cleanup` 的函数，然后使用 `trap` 命令确保在发送 INT 或 TERM 信号或脚本退出时会调用清理函数。

使用 `trap` 对于执行时间较长的脚本非常有用。例如，此脚本从网上下载 effective-shell 样本，如果用户遇到网络连接问题，他们可能会因为下载过久而反复取消脚本。`trap` 命令确保了临时文件夹会被清理。

在某些情况下你可能会看到 `INT` 写为 `SIGINT`。信号名称开头的 `SIG` 是可选的，但并不是所有 shell 都支持它，可以使用信号编号代替。因此，`SIGINT`、`INT` 和 `2` 都是 `trap` 命令的等效选项。`INT` 最具移植性且易于阅读，所以我推荐使用。运行 `man signal` 可以查询所有信号及其信号编号。

你也可以使用 `trap` 来防止用户中断你的脚本，在此例中：

```bash
interrupt_count=0
if [ $interrupt_count -lt 1 ]; then
  echo "取消此操作可能会导致错误。"
  echo "如果你确定要取消，请再次按下 Ctrl-C。"
  interrupt_count=$((interrupt_count + 1))
else
  # 惯例使用状态码 130 表示中断的脚本。
  echo "正在取消长时间操作"
  exit 130
fi
```

```bash
trap on_interrupt INT
total_time=0
while true; do
  echo "长时间操作：已过去 ${total_time} 秒"
  sleep 3
  total_time=$((total_time + 3))
done
```

运行此脚本时，用户必须按下两次 CTRL-C 才能取消操作：

```bash
$ ~/effective-shell/scripts/long-operation.sh
长时间操作：已过去 0 秒
长时间操作：已过去 3 秒
长时间操作：已过去 6 秒
^取消此操作可能会导致错误。
如果你确定要取消，请再次按下 Ctrl-C。
长时间操作：已过去 9 秒
长时间操作：已过去 12 秒
^正在取消长时间操作
```

要求用户确认取消可以帮助他们避免误操作。警告消息还会告诉他们如果在脚本完成前取消可能会发生什么。以下列表了关于 `trap` 条件的一些其他细节：

- 你可以使用 `trap -1` 或 `kill -1` 来列出可用的信号，`EXIT` 和 `RETURN` 等特殊条件不会被列出。要查找它们，请在 shell 中输入帮助命令。

- 要停止处理某个信号，使用 `trap SIGNAL`，这意味着 shell 在接收到信号时不会执行任何命令。

- 要重置 `trap`，运行 `trap SIGNAL` 将移除任何 trap 处理器。

- 测试 trap。

36 - hello

37 - hello

当你将彩虹输出写入文件时，你会得到如下内容：

$ rainbow hello >> text.txt

$ cat -v text.txt

+   31 - ^[0;32mhello[0m

32 - ^[0;32mhello[0m

33 - ^[0;33mhello[0m

34 - ^[0;34mhello[0m

35 - ^[0;35mhello[0m

36 - ^[0;36mhello[0m

37 - ^[0;37mhello[0m

`-v` 参数告诉 `cat` 使转义字符可见。如果你在文本编辑器中打开文件，你会看到这些转义字符。

`rainbow` 函数的问题在于当你将结果写入文件时，它会添加颜色转义序列。在大多数情况下，这并不是你想要的。像 `ls` 这样的命令在将输出写入文件时是不包含颜色代码的。

没有万无一失的方法可以避免这个问题，但最常用的方法是使用 `test` 命令的 `-t` 表达式来检查输出是否为终端设备（如第 11 章解释过的，`expression` 和 `test expression` 是等价的）：

```bash
if [ -t 1 ]; then
    echo "We are writing to a terminal"
else
    echo "We are not writing to a terminal"
fi
```

如果提供的文件描述符与终端相关，则 `-t` 测试返回成功。此示例中的 `1` 是标准输出（stdout）流的文件描述符（如果不熟悉，请参阅第 2 章）。

你可以如下将其应用到 `rainbow` 函数中：

```bash
rainbow () {
    local message="$1"
    local reset='\[[0m'
    for ((color=31; color<=37; color++))
    do
        color_code="\[[0;${color}m"
        if [ -t 1 ]; then
            printf "${color} - ${color_code}${message}${reset}\n"
        else
            printf "${color} - ${message}\n"
        fi
    done
}
```

# 现在执行 rainbow > test.txt

输出文件将不再包含 ANSI 转义序列。要了解更多关于 `-t` 测试的信息，请运行 `man test`。

最后一个格式技巧：你可以使用 `tput`（“查询 terminfo 数据库”）命令以一种稍微对用户友好且易读的方式查找转义序列：

```bash
bold=$(tput bold) # 设置格式为“粗体”
green=$(tput setaf 2) # 设置 ANSI 前景色为绿色。
reset=$(tput sgr0) # 重置颜色。
echo -e "${bold}${green}apples${reset}" 
```

我的终端中执行此代码会返回以下输出，其中单词 apples 显示为粗体绿色：

Do you like apples?

`~/effective-shell/scripts/common.sh` 脚本包含了彩色输出，还会检查是否应该打印颜色代码，因此你可以将其作为脚本的参考。

虽然 `tput` 代码并不完全直观，但它们比原始的 ANSI 转义序列更具读性。如果某个功能（如粗体格式）不可，`tput` 命令将失败，让你能够构建能够适应不同终端能力的脚本。

# 检查操作系统

不同的 Unix 和 Linux 版本在行为上时而并不一致。虽然编写可以跨系统使用的脚本是理想的，但并不总是可能的。有时你能够检查特定的操作系统并采取适当的操作。

你可以使用配合 `uname`（“显示操作系统名称”）的 `case` 语句来检查操作系统（第 11 章深入讲解了 `case`）：

```bash
case "$(uname)" in
  MacOS)
    os="MacOS"
    ;;
  Linux)
    os="Linux"
    ;;
  CYGWIN*|MINGW32*|MSYS*|MINGW*)
    os="Windows"
    ;;
  SunOS)
    os="Solaris"
    ;;
  *)
    echo "Unsupported operating system"
    exit 1
    ;;
esac
echo "Your OS is: ${os}"
```

`~/effective-shell/scripts/common.sh` 脚本会检查操作系统是否为 macOS。如果是，它会将 `sed` 等文本命令临时设置别名，为 GNU 的等效命令，因为 macOS 版本的命令基于 BSD，且参数略有不同。在编写需要同时兼容 macOS 和 Linux 的 shell 脚本时，请参考 `common.sh`。

# 检查已安装的程序

有很多方法可以判断命令是否可用。正确且性最好的选项是使用所示的 `command -v`：

```bash
if ! -v "curl" >/dev/null 2>&1; then
  echo "curl' is not installed, please install and try again"
fi
```

当你使用 `command` 时，你会忽略错误输出和标准输出；否则，如果命令不存在，你会看到错误信息；如果存在，你会看到命令的详情。

`~/effective-shell/scripts/common.sh` 脚本在 macOS 上运行时会检查是否安装了某些 GNU 版本的工具。如果你需要在脚本中检查命令是否存在，可以将其作为指南。

# 显示菜单

`select` 命令打印一个菜单并允许用户进行选择。它不是 POSIX 标准的一部分，但在 bash 和类 bash shell 中是用的。下面的示例使用 `select` 让用户选择他们喜欢的水：

```bash
select fruit in Apple Banana Cherry Durian
do
  case $REPLY in
    Apple) echo "You chose apple"; break ;;
    Banana) echo "You chose banana"; break ;;
    Cherry) echo "You chose cherry"; break ;;
    Durian) echo "You chose durian"; break ;;
    *) echo "Invalid selection" ;;
  esac
done
```

## 在 Shebang 中配置选项

有时，你会看到 shell 脚本带有包含选项的 shebang，例如：

```
#!/usr/bin/bash -ex
```

# # 下方是脚本内容...

在这种情况下，-ex 标志会被传递给 bash 程序，启用“发生错误时退出”（exit on error）和“跟踪”（trace）选项。

但虽然你可以在脚本中指定程序参数，这并不意味着你应该这样做。这样做是有风险的，原因有两个。

首先，这种模式要求你知道 shell 的安装路径。如果你阅读了第 9 章，就会知道应该使用 #/usr/bin/env 来在 PATH 中搜索 shell，而不是假设你知道用户将其安装在了哪里。

其次，并不是所有参数在不同操作系统上的处理方式都是一致的。例如，在某些 Unix 系统上，以下 shebang 将带有 -e 参数运行：

```
#!/usr/bin/env bash -e
```

然而，在许多发行版中，只会传递一个参数，在这种情况下 -e 参数将被静默忽略。这对于任何阅读你代码的人来说都会令人困惑。处理这些问题的折中方案是为 env 使用 -s（"split”）参数，但再次，这可能会让读者感到困惑。

## 在 Shell 脚本中使用复杂逻辑

尽管 shell 已经存在了几十年，但它的变化微乎其微。它是 Unix 系统以及整个 shell 天赋的见证。

然而，shell 通常并不是处理复杂逻辑或工作的最佳选择。shell 脚本非常适合简单任务和创建工具来帮助你简化工作，但它们也面临着许多挑战。语法可能会让人困惑，让跨多个系统的脚本变得具有挑战性，而且没有足够的特性来帮助你编写健壮的代码。

也许 shell 脚本中最大的反模式就是让它们变得过大，并试图让它们做太多事情。在某个一点，你几乎可以使用像 Python（在所有系统上可用）这样的专用编程语言或你使用的其他语言，为你的问题创建一个更具移植性、有效且易于维护的解决方案。

这是一个我将在第 21 章详细讨论的话题，目前我建议遵循这条经验法则：一旦你的脚本开始变得超过一页，或者需要花费几分钟才能理清楚，你可能已经到了使用编程语言是更好选择的节点。

## 总结

本章描述了几个你可以整合到 shell 脚本中的有用模式，帮助你成为更高效的 shell 用户。你学习了如何处理某些用户行为、为 shell 输出添加语法高亮、检查操作系统和安装的程序等。你还看到了一些反模式——即你可能在别人的脚本中发现的坏习惯，但在你自己的脚本中应该避免这些习惯。

在第四部分中，你将学习如何自定义你的 shell 和环境，以便它们更适合你的特定需求和用例。

## 第四部分

构建你的工具箱

# 15

# 配置你的 shell

一旦你掌握了 shell 的基础知识，就可以准备好自定义它以满足你的特定需求和偏好了。本章介绍了各种 shell 配置文件，解释了它们的工作原理，并涵盖了你使用最适合你的选项来配置 shell 的许多方法。

## 交互式 shell

交互式 shell 是任何将其输入、输出和错误流（分别为 stdin、stdout 和 stderr）连接到终端的 shell，这实际上意味着交互式 shell 是你通过键盘和显示器进行交互的 shell。当你使用 shell 或像 GNOME Terminal 或 KDE 的 Konsole 等终端模拟器输入命令时，你正在运行一个交互式 shell。

## 默认 shell 启动文件

当交互式 shell 启动时，它执行的操作之一是运行 ~/.bashrc 文件中的所有命令。这个启动文件是你最常用来配置 shell 的文件。
