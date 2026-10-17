
```
W: GPG error: http://us.debian.org Testing Release: \
nThe following signatures couldn't be verified because the \
ublic key is not available: \
NO_PUBKEY 01090B31ZD1D90C5F
```

```
W: GPG error: http://us.debian.org unstable Release: \
nThe following signatures couldn't be verified because the \
ublic key is not available: \
NO_PUBKEY 01090B31ZD1D90C5F
```

在这些情况下，`/etc/apt/sources.list`中的相关条目指向密钥环中不存在密钥的库。请参见`apt-key`的man页。

### 第二部分：面向桌面用户的 Ubuntu

### 探索系统：使用 dpkg 及其工具

软件包管理不仅简化了软件的安装、删除和更新，还为询问已安装软件提供了极佳的机会。命令行工具可以轻松查找安装了哪些软件、特定软件包包含哪些文件等。接几节将描述如何回答关于现有软件包的基础问题。

### 列出已安装的软件包

`dpkg -l`命令提供了列出已安装软件包的最简单方法。`--long`可以使用详细格式指定。你可以在不带其他参数的情况下执行此命令，产生系统中安装的所有软件包的详细列表，如下所示：

```
$ dpkg -l
Desired-Unknown/Install/Remove/Purge/Hold
Status-Not/Installed/Config/files/Unpacked/Failed-config/\
// Err?-(none)/Hold/Reinst-required/X+both-problems \
(Status,uppercase-base)
// Name           Version               Description
+++------------------------------------
++ 3dchess        0.8.1-11             3D chess for X11
ii acpi          0.9.1displays information on ACPI
ii acpi-support   0.4                 a collection of useful acpi events
ii acpid         1.0.4-1ubuntu      Utilities for ACPI power management
ii adduser       3.8ubuntu2Add and remove users and groups
```

软件包列表上方的几行标识了每行各个字段的含义以及它们包含的符号。这些信息以一种相当晦涩的形式提供，是为了满足`dpkg`工具产生的终端定向输出的需求。软件包名称、软件包版本和描述的条目非常直观，而第一个字段需要详细的解释。第一个字段中的第一个字符表示软件包的期望状态，即软件包系统认为该软件包应该的状态：

- `h`: 软件包被标记为保持状态（hold），无法更新或删除。

# 第 19 章：添加、删除和更新软件

- `i`: 软件包应该安装。

- `p`: 软件包及其所有相关配置信息将全部清除（purge）。

- `r`: 软件包预计将被删除，但将保留相关的配置文件。

- `u`: 该系统从未在该系统中安装过该软件包，因此其状态未知。

- 第一个字段的第二个字符表示软件包在您系统上的实际状态。该位置的可用指示包括：

    - `c`: 软件包的配置文件已安装，但软件包本身未安装。

    - `f`: 用于完成此软件包配置的脚本（即安装后脚本）由于某些原因失败，因此无法保证软件包已正确安装。

    - `h`: 由于安装过程被中断，该软件包处于部分安装状态。

    - `i`: 软件包已正确安装。

    - `n`: 软件包未安装。

    - `u`: 软件包已检索、解压并部分安装，但未执行其安装后脚本。

- 第三个字符高亮显示与该软件包相关的任何错误。该位置的可用指示包括：

    - 空格：无错误，看起来就像该位置没有任何内容。

    - `H`：软件包已被软件包管理系统本身标记为锁定（hold），这通常意味着该软件包所需的其他软件包尚未安装。

    - `R`：需要重新安装。

    - `X`：软件包既需要重新安装，又被软件包管理系统自动置于锁定状态。

现在我已经解释了软件包条目第一个字段中每个字符的含义，很容易看出`dpkg`输出标题中的ASCII艺术字。这并不完全等同于直观，但在命令行可以显示并易于使用的有限字符内，这就是所能采取的做法。

# 列出您的系统中可用的软件包

上一节解释了如何确定系统中安装了哪些软件包。虽然这很有趣，但也许一个更有趣的问题是：“我的系统中有可用但我尚未安装的软件包？”如上一节所述，`dpkg`命令的`-l`选项在不带其他参数时会显示已安装软件包的列表。你可以为此命令提供参数，以列出匹配该参数的可用软件包（无论已安装还是未安装）。例如，`dpkg -l emacs`命令应该列出所有包名中包含`emacs`字符串的软件包。让我们尝试一下：

```
$ dpkg -l emacs
No packages found emacs.
```

嗯，看起来很奇怪，我实际上正在Ubuntu系统的Emacs中输入这个命令。问题在于，提供给`dpkg`的任何参数都会被用作模式匹配，而我的系统中显然没有名称完全为`emacs`的软件包。让我们再次尝试，使用标准的Linux通配符，在下面的示例中列出名称以`emacs`开头的软件包：

```bash
$ dpkg -l *emacs*
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not-Installed/Config-files/Unpacked/Failed-config/\
Half-installed
| Err?=(none)/Hold/Reinst-required/X=both-problems \
(Status,Err: uppercase:bad)
|| Name Version Description
+++--------------------------+===================
ii emacs-chess 2.0b5-1 client/library for Chess
un emacs-chess-pieces 2.0b5-1 XPM Images of chess pieces
un emacs-goodies <none> (no description available)
un emacs-goodies-extra-el <none> (no description available)
ii emacs21 21.4a-ubuntu2 The GNU Emacs editor
ii emacs21-bin-common 21.4a-ubuntu2 The GNU Emacs shared...
ii emacs21-common 21.4a-ubuntu2 The GNU Emacs shared...
un emacs-el <none> (no description available)
un emacs-nox <none> (no description available)
un emacsen <none> (no description available)
ii emacs-common 1.4.17 Common facilities for
```

这就像一样了！在`dpkg`规范中使用通配符时，你必须通过引号将`dpkg`通配符括起来，以防止它们被命令行解析。

之前的输出显示了一些Emacs软件包，但我可以搜索我的Ubuntu系统是否还有其他的。让我们尝试更通用的搜索，查找名称中包含`emacs`字符串的软件包：
