

# 任务 7.1：使用文件识别文件类型

UNIX 中最被低估的命令之一是 `file`，它经常被忽视并在系统的某个角落落灰。`file` 命令是一个程序，它可以通过查看文件的前几行轻松地为你提供关于文件内容的良好提示。

遗憾的是，`file` 命令存在一个问题：它并不是 100% 准确的。该程序依赖于文件权限、文件名以及对文本前几行的分析。如果你有一个文件看起来像 C 程序或开启了执行权限，`file` 很有可能将其识别为可执行程序，而不是英文文本文件。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_138_0.png)

你可以通过检查文件类型数据库的大小来确定你版本中 `file` 的准确性。你可以使用 UNIX 命令 `wc -l /etc/*` 来实现。数据库中的条目数量应该在 100 左右。如果数量远少于这个数字，你可能会遇到麻烦。如果多于这个数字，你手里可能掌握了一个非常准确的 `file` 版本！但记住，即使它很小，`file` 仍然可以就文件内容提供非常有价值的建议。

- 1. 登录你的账户并使用 `ls` 命令找到一两个文件进行检查。

```
% ls -F
Archives/
Info/old/
OWL/ PubAccessLists.Z rumors.260ct.Z
LISTS/ bin/ rumors.5Nov.Z
Mail/ educ src/\News/ mailing.bitnet.Z
```

接下来，只需输入 `file` 命令，列出你想分析的每一个文件：

```
% file LISTS rumors.260ct.Z src
LISTS: ascii text
educ: ascii text
rumors.260ct.Z: block compressed 16 bit code data
src: directory
```

从这个示例中，你可以看到 `file` 正确地识别了 `src` 为目录，对压缩文件 `rumors.260ct.Z` 提供了大量信息，并将 `LISTS` 和 `educ` 均标记为纯 ASCII 文本文件。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_138_1.png)

# 深入研究文件

ASCII 是美国信息交换标准，意味着文件包含英文字母、标点符号和数字，但没有其他内容。它没有多种字体、斜体或下划线段，也没有图形。它是 UNIX 中文本的最低公约数。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_139_0.png)

- 2. 现在尝试使用星号 (**)

```
% file *
Global.Software: English text
Interactive.Unix: mail folder
Mail: directory
News: directory
Src: directory
bin: directory
history.usetenet.Z: compressed data block compressed 16 bits
```

星号是 UNIX 中的一个特殊字符。它单独存在时，它告诉系统将其替换为当前目录下所有文件的名称。

这一次你可以开始看到 `file` 是如何区分文件的。使用这个命令，我现在想起文件 `Global.Software` 是英文文本，但 `Interactive.Unix` 实际上是一个电子邮件（`file` 无法区分单个邮件消息和多消息文件夹，因此它总是倾向于说该文件是邮件文件夹)。

- 3. 邮件文件夹对于 `file` 命令来说实际上很有用。在我使用的系统之一，`file` 命令不知道什么是邮件消息，因此在演示准确性如何与文件数据库大小相关时，我要求分析邮件文件夹。

在 Sun 系统上，我让 `file` 分析两个邮件文件夹，结果如下：

```
% file Mail/mailbox Mail/sent
Mail/mailbox: mail folder
Mail/sent: mail folder
```

然而，在 Berkeley UNIX 系统上，这两个文件在分析时有截然不同的结果：

```
% file Mail/mailbox Mail/sent
Mail/mailbox: ASCII text
Mail/sent: shell commands
Mail/sent: English text
```

Berkeley 版 UNIX 不仅没有正确识别文件，甚至不能连贯地误判它们。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_139_1.png)

- 4. `file` 命令局限性的另一个例子是它如何与文件权限交互。使用 `cp` 创建一个新文件并执行此示例，看看你的 `file` 命令如何解释各种变化。

```
% cp _char test
% file test
test: shell commands
% chmod +x test
% file test
test: shell script
```

为此文件添加执行权限导致它的行为像是一个 shell 脚本而不是 shell 命令。

不要将这些示例的结果误认为是 `file` 命令没用以及你不应该使用它的证据。恰恰相反。UNIX 既没有文件命名规范（DOS 有其三字母后缀），也没有通过图标指示文件所有权（Macintosh 通过每个程序添加创建者信息来实现）。事实证明，拥有一个工具帮助确定文件类型而无需实际打开它是至关重要的。

为什么看内容呢？回答这个问题的最好方法是在屏幕上无意显示可执行文件的内容。当它完全是一团糟时，充满了特殊的控制字符，最好的描述就是这会让你的屏幕失控。

# 任务 7.2：使用 file 探索 UNIX 目录

现在你已经知道如何使用 `file` 命令了，是时候漫游 UNIX 文件系统，学习更多在特定目录中可以找到的文件类型。你的系统可能会略有不同——某些目录中的文件肯定会比我在示例中显示的多，但你会很快发现 `file` 可以对文件内容提供有价值的见解。

- 1. 首先。看看系统最顶层 `/` (根目录) 中的文件：

```
% cd /
% ls -CF
-No _rm__ star      flags/      rhf/       user/
OLD/        core        gendix stand/      user/
archive/    dev/        lib*       sys/       user/
ats/        diag*      found-found tftpboot  user/
backup/                     mnt/        tmp/        users/
bin/        etc/        net/        usera/      usr/
% file boot gendix
```

# 深入研究文件

core: 来自 "popper" 的核心文件
gendix: 独立版本 1
tftboot: 指 /usr/tftboot 的符号链接

ASCII 是美国信息交换标准，意味着文件包含英文字母、标点符号和数字，但没有其他内容。它没有多种字体、斜体或下划线段，也没有图形。它是 UNIX 中文本的最低公约数。

`file` 命令详细解释了可执行二进制文件，它是独立的。格式为 i386，且该文件不需要库或其他文件——它是独立的。

对于 `gendynix`，格式类似，但增加了一条 `boot` 未标出的信息：该可执行文件已剥离符号（stripped）。

在此输出中看到的最重要的单词是 `executable`（可执行的）。这个示例来自一台运行基于 Berkeley 4.3 的 DYNIX 计算机。它就是那台在识别邮件文件夹方面有问题机器。

当程序在 UNIX 中意外崩溃时，操作系统会尝试留下该程序正在使用的内存快照，以帮助调试。处理这些文件可能是困难的——通常留给每个站点的少数专家，因为里面还有一些信息。最好、最简单的方法是使用 `file` 命令检查它。你可以在前面的列表中看到 `file` 将文件识别为崩溃的程序映像，并进一步提取了最初失败的程序名称 `getty`。当这种故障发生时，UNIX 会创建一个故障时的内存映像，这被称为转储（core dump）。

列表第四项提供了一种理解符号链接的简单方法，在 `-CF` 输出中通过特殊后缀 `#` 表示，在上一个示例中为 `tftboot*`。使用 `file`，你可以看到根目录下的 `tftboot` 文件实际上是指向文件系统其他处同名文件 `/usr/tftboot` 的符号链接。

不同机器上的输出格式存在差异。示例显示了在 Sun Microsystems 工作站上检查类似文件时生成的内容：

```
% file boot core kadb tamp
boot: sparc executable
core: core file from "popper"
```

