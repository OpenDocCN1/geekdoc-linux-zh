
bash$ `su` -

```
## 7.4.4. 系统关机

切换回 root 登录的 `tty1`。

```bash
bash# `shutdown -h now`
```

# 第 8 章：填补空白

## 8.1. 分析

根磁盘从最初作为一个静态链接的 shell 以来，已经走了很远的路。它现在与流行的现成发行版共享许多特性。例如，它具有：

- 几个如 `cat`、`ls` 等常用实用工具。
- 自动检查并挂载文件系统的启动脚本。
- 优雅关机能力。
- 对多用户和虚拟终端的支持。

作为最后的测试，我们可以根据文件系统层次结构标准 (`FHS`) 对根文件系统进行要求（我们将忽略 `/usr` 层次结构中空间限制的限制）。与 `FHS` 要求相比，唯一缺失的文件是 `/bin` 目录中的几条命令。具体来说，根磁盘缺少以下命令：

- `more`
- `ps`
- `sed`

除了所需的命令外，根据 `FHS` 将 "`ed`" 编辑器列表作为选项包含进来可能会很好。它没有 `vi` 或 `emacs` 那么健壮，但它可以工作并且应该适合微小的根文件系统。

因此，为了完成项目的这个阶段，我们需要实现以下目标：

- 添加 `more`、`ps` 和 `sed` 命令。
- 安装可选的 `ed` 编辑器。

## 8.2. 设计

### 8.2.1. more

`util-linux` 自带有一个 `more` 命令，但它在本项目中无法工作。原因在于库依赖项和空间限制。`util` 提供的 `more` 需要 `libncurses` 或 `libterm` 才能工作，而根磁盘软盘上没有足够的空间来容纳所有内容。因此，为了有一个 `more` 命令，我们必须自己创建一个。

`more` 命令用于逐页显示文件。它有点像一个在 25 行处会暂停的 `cat` 命令。基本逻辑概述如下：

- 读取文件的一的一行。
- 在屏幕上显示该行。
- 如果已经显示了 25 行，则暂停。
- 循环并再次执行。

当然，对于当屏幕尺寸与我们的预期不符时该怎么办遗漏了一些细节，但总的来说，它是对 `more` 功能的合理表示。鉴于这个简单的程序逻辑，编写一个短的 shell 脚本来模拟 `more` 的基本功能应该并不困难。`BASH(1)` 手页和 `Adv-BASH-Scripting-Guide` 将作为参考。

### 8.2.2. more 设备文件

`more` 脚本需要访问尚未位于磁盘上的设备文件。具体来说，`more` 需要 `stdin`、`stdout` 和 `stderr`，顺便它还应该检查任何缺失的 `/dev` 文件。Linux 标准基础 (`Linux Standard Base`) 要求 `/dev` 目录中存在 `null`、`zero` 和 `tty`。`null` 和 `tty` 已经在项目之前的阶段存在，但我们仍然需要 `/dev/zero`。我们可以参考 Linux 源代码文档目录中的 `devices.txt` 来获取主设备和次设备号。

### 8.2.3. ps, sed & ed

通过我们使用过的互联网资源加上一个新网站，可以找到这三个软件包。"`sed`" 和 "`ed`" 包可以在与 `BASH`（GNU FTP 服务器）相同的地方找到。`procs` 包在 `Ibiblio LSM` 搜索中出现，但它是一个旧版本。为了找到最新版本，我们可以访问网站 `http://freshmeet.net` 并在 `projects` 中搜索 "`procs`"。

因此，"`sed`" 和 "`ed`" 包的 GNU 基础配置脚本非常容易构建。"`procs`" 没有配置 脚本，这并没有让事情变得困难。我们只需要读取包的 `README` 文件来了解如何设置各种选项。我们可以使用这些选项来避免安装和链接的复杂性。设置 `SHARED=0` 会让 `proc` 成为 `ps` 的而不是独立的共享库。

## 8.3. 构建

### 8.3.1. 编写 "more" 脚本

使用文本编辑器创建以下脚本并将其保存为 `~/staging/bin/more.sh`

```bash
#!/bin/sh

#
# more.sh     模拟 "more" 二进制的基本功能，
#               不需要 ncurses 或 termcap 库。
#
# 假设输入来自 STDIN，除非提供了一个有效的文件
#   命令行参数。

if [ -f $1 ]; then
  INPUT="$1"
else
  INPUT="/dev/stdin"
fi

# 将 IFS 设置为换行符。详情见 BASH(1) 手页。

IFS=$'\n'

# 如果终端维度尚未作为 shell 变量设置，
# 则猜测为 80x25。

if [ "$COLUMNS" = "" ]; then
  let COLUMNS=80
fi

if [ "$LINES" = "" ]; then
  let LINES=25;
fi

# 初始化行计数变量

let LINE_COUNTER=$LINES

# 逐行读取输入并显示到 STDOUT，直到
# 页面填充。在 STDERR 上显示“Press <Enter>”消息。

while read -r line; do
  echo "$line"
  let LINE_COUNTER=$((LINE_COUNTER - 1))
  if [ $LINE_COUNTER -le 0 ]; then
    echo "Press <Enter>" >&2
    read -r
    let LINE_COUNTER=$LINES
  fi
done < "$INPUT"
```
