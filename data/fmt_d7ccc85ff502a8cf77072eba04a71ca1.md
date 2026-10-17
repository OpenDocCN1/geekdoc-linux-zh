
别名让创建自定义命令变得简单，这些命令预配置了你最频繁使用的参数和选项。`command` 命令是别名的绝佳候选者，或者因为它是一个非常复杂的命令（见技术 12）。这里有两个执行繁琐工作的别名用于：

`bash` 有一个缺点：你不能将命令参数传递给命令的其他部分。例如，考虑这个：

```bash
alias gf='find' -type f -print0 | xargs
-0 grep -n e *
```

```bash
alias f='find' -name
alias fi='find' -iname
```

`gf` 结合了 `find` 和 `grep`，用于在目录下所有文件中搜索特定文本。你可以这样使用别名：

在定义这些别名后，你可以这样搜索文件（通过名称）：

```bash
$ gf Martini
/recipes/drinks.txt:200: the perfect
Martini
/spories/bond.txt:22: I prefer my
Martinis shaken, not stirred
```

```bash
$ fi myfile.sh
../tmp/myfile.sh
```

只要你想搜索目录中的每个文件，`gf` 别名就能工作，但如果你想搜索 `.txt` 文件和 `.html` 文件呢？你不能通过别名这样做，因为 `-name` 限制符必须位于命令行的中间；它不能在末尾。相反，你需要一个函数，我们将在下一节解释如何创建。

# 使用函数处理繁琐任务

函数比别名更强大，因为你可以向它们传递参数。例如，考虑这个：

```bash
function gf() {
  find . -type f -print0 | xargs -0 grep -n e "$@"
}
```

```bash
alias f='find'
```

`gf` 结合了 `find` 和 `grep`，用于在目录下所有文件中搜索特定文本。你可以这样使用别名：

在定义这些别名后，你可以这样搜索文件（通过名称）：

```bash
$ gf Martini
/recipes/drinks.txt:200: the perfect
Martini
/spories/bond.txt:22: I prefer my
Martinis shaken, not stirred
```

```bash
$ fi myfile.sh
../tmp/myfile.sh
```

## 60 技巧：通过别名和函数让生活简单

你可能知道 `tar` 命令（至少是 GNU 版本的 tar）可以处理未压缩、`gzip` 压缩和 `bzip2` 压缩的包。创建一个包装函数很容易，它可以根据你提供的包使用一组正确的标志来调用 `tar`。该函数（参见列表 10-1）使用命令来判断给定的包是否经过压缩，如果是，则确定[使用的]压缩方法。`tar` 比此技术中的其他函数要长得多，因此我们在列表中包含了节省时间的特性：

- 存储中间结果的局部变量：你可以使用局部变量重写此函数，但维护起来会更耗时。
- 帮助未来维护者理解我们思路的注释：`bash` 语法可能会变得非常晦涩，现在就为代码添加注释将在未来为你节省大量时间。

![](img/907133bedebb1d692bfe1e0f76996df1_77_0.png)

如果你拥有超级用户权限，可以使用 `xtail` 监控系统日志文件：

```bash
# xtail /var/log/messages
```

## 轻松解压的方法

你可以通过创建适应命令行参数的自适应函数来节省时间。

列表 10-1：根据文件类型选择正确的程序

```bash
function tarls () {
  # 确定我们正在处理什么类型的文件。
  local filetype # 来自 file 命令的输出
  local startype # $filetype 的文件名
  local compressype # $startype 的第一个单词
  local tarflags # 给 tar 命令的标志

  # 给定的参数如：
  # icons.tgz
  # filetype 将包含
  # icons.tgz: gzip 压缩数据
  filetype=$(file "$1")

  # 现在剥离文件名
  # 来自 $filetype
  # gzip 压缩数据
  startype=${filetype@*/}

  # 最后，获取第一个单词
  # 来自 $startype
  # gzip
  compressype=$(echo "$startype" | cut -d ' ' -f 1)

  case $compressype in
    gzip) tarflags=-ztvf;
    bzip2) tarflags=-jtvf;
    POSIX) tarflags=-tvf;
    *) echo "未知包类型"; return 1;
  esac

  tar $tarflags "$1"
}
```

# 第二部分：从你的文件系统获取大部分资源

![](img/907133bedebb1d692bfe1e0f76996df1_80.png)

> “到目前为止，它被称为 `Samba`，一组 `python` 和一堆工具，但仍然是我们寻找的文件。”

## 在 Windows 世界中共享文件和打印机

### 技术

![](img/907133bedebb1d692bfe1e0f76996df1_82.png)

大多数网络都有各种计算机。几台 `Linux` 机器、几台 `Windows` 机器或 `Mac` 组合成了快速、多功能且易于使用的网络。我们并不是建议 `Linux` 不是最好的选择，但实际上，仅限 `Linux` 的网络是不可能的。有时 `Linux` 必须学会与 `Windows` 协作。

跨网络共享数据的需求正在增长，但由于网络由各种机器组成，开源软件已经发展出许多（而且是免费的）软件，让你能够快速方便地跨网络共享数据。

在本技术中，我们向向你展示如何跨网络共享数据和打印机。节省时间，节省资金……创建一个更友好的世界。

## 节省时间

- 使用 `SWAT` 配置 `Samba`
- 从 `Windows` 获取 `Linux` 文件
- 从 `Windows` 获取 `Linux` 打印机
- 从 `Linux` 获取 `Windows` 数据

## 什么是 Samba？

大多数人听到 `Samba` 这个词会想到巴西舞。我们更倾向于将其称为 `Samba` 树，一个具有 `Samba` 功能的非洲树。我们不知道 `Samba` 到底是什么，无论如何。

在 `Linux` 世界中，`Samba` 是大多数 `Linux` 发行版包含的一套资源共享工具。你使用 `Samba` 与网络上的其他主机共享 `Linux` 文件系统、目录、文件和打印机。`Samba` 专为与 `Windows` 文件共享和打印机共享功能而设计。每个 `Samba` 连接涉及两个主机：服务器提供资源，客户端访问服务器共享的资源。`Linux` 主机可以作为客户端、服务器或两者。

## 技术 11：在 Windows 世界中共享文件和打印机

在底层，`Samba` 客户端使用 `SMB`（服务器消息块）协议与 `Samba` 服务器交互。`SMB` 也称为 `CIFS`（通用互联网文件系统）。服务器可以暴露两种资源：打印机和共享。共享是一个目录（及其下面的所有子目录）。打印机是……

- `samba-doc` 包含 `Samba` 的文档。
- `samba-swat` 是一个基于浏览器的 `Samba` 配置工具。

`Samba` 已经存在了，而且非常稳定。即使你的网络中没有 `Windows` 计算机，你也可以 `Samba` 共享资源。

如果你想让电脑作为 `Samba` 服务器（也就是说，如果你想暴露电脑上的数据或打印机），你必须安装 `samba-server` 包。然而，我们建议安装所有包，因为这会方便得多。如果你安装了所有包，你的电脑就可以 `Samba` 客户端或服务器，并且还有一个好用的配置工具。

`Samba` 让你可以向世界暴露资源。我们特意选择向世界暴露是为了说明 `Samba` 可以共享你可能想要共享秘密。让 `Samba` 变得相当安全也很容易，这里关于加固系统防止恶意（或无意）滥用的有用提示。

检查你的主机是否已经安装了 `Samba`，打开终端并在以下命令中使用它：

```bash
$ samba-client samba-common samba-swat
```

`SUSE` 使用此命令：

```bash
$ samba-client samba-doc
```

如果你运行的是强制 `Linux` (Mandatory `Linux`)，输入：

```bash
$ samba-server samba-common samba-swat-doc
```
