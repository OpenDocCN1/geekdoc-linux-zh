

## Linux 内核 0.01

```c
/*
 * console.c
 *
 * This module implements the console & functions
 * used con_shak(void)
 * (used for write char() & queue * queue);
 * Hopefully this will be a rather complete VT102 implementation.
 */
/*
 * NOTE!!! We sometimes disable and enable interrupts for a short while
 * (to put a word in radio I/O), but this will work even for keyboard
 * interrupts. We know interrupts aren't enabled when getting a keyboard
 * interrupt, as we use trap-gates. Hopefully all is well.
 */

#include <linux/sched.h>
#include <linux/tty.h>
#include <asm/io.h>
#include <asm/system.h>

#define SCREEN_START 0xB8000
#define SCREEN_END   0xC0000
#define LINES 25
#define COLUMNS 80
#define BEAR 16

extern void keyboard_interrupt(void);

static unsigned long origin=SCREEN_START;
static unsigned long scr_end=SCREEN_START+LINES*COLUMNS*2;
static unsigned long pos;
static unsigned long x,y;
static unsigned long top=0,bottom=LINES;
static unsigned long lines=LINES,columns=COLUMNS;
static unsigned long state=0;
static unsigned long npar,par[NPAR];
static unsigned long qpos=0;
static unsigned char attr=0x07;
```

**你知道吗...**

由林纳斯·托瓦兹编程的第一个 Linux 内核，仅占用了 65KB 的内存。而从 0.01 版本以来，Linux 内核现在拥有超过 1800 万行代码。对于一个如今驱动着纽约证券交易所以及美国国防部核潜艇机群的高校项目来说，这表现相当不错。

## 使用终端创建文件

使用终端，你可以创建文件夹、文件，甚至执行 Linux Mint 应用程序。事实上，即使没有图形用户界面（GUI），你仍然可以通过终端完成相同的工作。

### 更多终端操作

使用终端创建内容并不像初看时那样费力。是的，终端可能对初学者来说显得望而生畏，但一旦掌握，它其实相当直观。

- **步骤 1** 打开终端，确保你位于主目录。如果不是，请使用 **cd ~** 命令将你从当前所在位置返回主目录。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_55_0.png)

- **步骤 2** 让我们从在 Home 内创建一个新文件夹开始，并命名为 **Test**。你需要输入的命令是 **mkdir Test**。输入命令后，按 **Enter** 键创建该文件夹，然后输入 **cd Test** 并按 **Enter**。这将切换目录（因此缩写为 **CD**）到新创建的 Test 文件夹。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_55_1.png)

- **步骤 3** 你的命令行应该会变更到 Test 文件夹，如果你输入 **ls**（列出文件夹内容），文件夹内将没有任何内容，因为你刚刚创建了它。**mkdir** 命令相当自明：Make Directory（创建目录）后跟着你选择的名称。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_55_2.png)

![](img/7801ba6bee6a3a08f7f02897cdbcd867_55_3.png)

- **步骤 4** 要创建一个名为 **Test.txt** 的空文本文件，在终端中输入：**touch Test.txt**。然后你可以使用 **ls** 来查看文件夹中的新文件。Touch 是一个标准的 Linux 命令，允许创建文件而无需打开文本编辑器、保存文件，然后关闭编辑器。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_56_0.png)

- **步骤 5** 假设你现在想创建一个包含一些内容的文本文件，我们将它命名为 Test2.txt。为此，输入：**cat > Test2.txt**。这将创建文件 Test2.txt 并将终端置于编辑模式。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_56_0.png)

- **步骤 6** 你会注意到，光标在 **cat > Test2.txt** 命令下方闪烁，没有通常的提示符。这种编辑模式允许你输入文件将包含的文本。输入一些文本，然后按 **Ctrl+D** 退出并将内容写入文件。

- **步骤 7** 当然，你并不总是需要终端来向文件中输入文本。Mint 自带一个名为 **Xed** 的文本编辑器，类似于 Windows 的记事本。要在 Xed 中查看之前创建的文件，在终端中输入：**xed Test2.txt**，然后按 **Enter**。

- **步骤 8** Xed 是一个图形界面应用程序，你可以使用该应用程序的主窗口及其顶部菜单栏中的 **File > Save**（文件 > 保存）或 **File > Save As**（文件 > 另存为）功能，输入文本并保存该文件（或任何文件）。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_56_1.png)

- **步骤 9** 然而，如果你更喜欢继续留在终端中编辑/保存/创建文件，你可以使用 **Nano**。Nano 是一个简单的基于终端的文本编辑器。要使用示例试用它，输入：**nano Test2.txt**。屏幕底部有一个菜单。要在 Nano 中退出并保存任何内容，请按 **Ctrl+X** 并按照屏幕上的说明操作。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_56_2.png)

![](img/7801ba6bee6a3a08f7f02897cdbcd867_56_3.png)

- **步骤 10** 我们使用终端启动了一个 Mint 应用程序，Xed，但任何应用程序都可以在终端内启动。例如，尝试 **firefox**，然后按 **Enter**。关闭 Firefox 即可返回终端。只要你知道应用程序的名称，就可以从终端运行它。此外，输入 **firefox&** 会打开 Firefox，同时仍允许你使用终端。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_56_4.png)

![](img/7801ba6bee6a3a08f7f02897cdbcd867_56_5.png)

## 创建和删除目录

与在终端中创建文件类似，你也可以创建和删除目录，或者你更习惯称之为文件夹。目录构成了文件系统的结构，如果没有逻辑目录，文件系统将陷入彻底的混乱。

### 管理文件夹

学习如何在终端中创建和删除文件夹是 Mint，乃至整个 Linux 中一项重要的需要掌握的技能。以下是供你练习的基础知识。

- **步骤 1**
  打开终端，输入 `cd ~` 以确保你位于自己的主目录中。现在输入 `ls` 查看主目录中现有的当前文件夹。你会注意到，Mint 中的文件夹以青色（浅蓝色）标签显示。让我们从创建一个新目录开始。输入 `mkdir testdir`。

- **步骤 2**
  如果你再次输入 `ls`，你将看到新目录 `testdir` 已与 Home 区域中的其他目录一起创建。显然，`mkdir` 命令是创建目录的命令，毫无疑问你已经猜到它代表 Make Directory（创建目录）。

- **步骤 3**
  如果你再次输入命令，`mkdir testdir`，你将收到一条消息，内容为：`mkdir: cannot create directory 'testdir': File exists`（mkdir：无法创建目录 'testdir'：文件已存在）。不用说，你在当前目录中只能拥有一个名称唯一的目录。但是，由于 Linux 区分大小写，你可以拥有 TestDir、TestDir、testDir 等等。

- **步骤 4**
  你可以在已创建的目录内部创建目录。例如，使用 `cd testdir/` 进入 testdir 目录，然后使用 `ls` 列出文件夹结构。自然，里面什么都没有，因为你刚刚创建该目录。现在使用 `cd ~` 返回 Home，并输入 `mkdir testdir/reports`。返回 testdir，`cd testdir/`，然后再次 `ls`。

- **步骤 5**
  因此，创建目录的命令相当合乎逻辑。你将创建目录及其内部的任何子目录。但是，如果你想在一个命令中创建一个目录和一个子目录怎么办？确保你在 Home（`cd ~`），然后输入：`mkdir -p Temp/finances`。现在，`cd Temp/`，并 `ls` 列出新目录。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_58_0.png)

- **步骤 6**
  **-p** 选项使得 `mkdir` 命令能够创建子目录以及父目录。在 Linux 中，命令始终遵循相同的结构：命令、选项和参数。在上一步的示例中，命令是（**mkdir**），选项是（**-p**），参数是（**Temp/finances**）。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_58_1.png)

- **步骤 7**
  如果你想深入了解 `mkdir` 命令可用的各种选项，你可以向终端输入 **mkdir -help**。这将提供一个快速帮助指南，详细说明选项以及命令结构的工作方式。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_58_2.png)

- **步骤 8**
  既然我们已经创建了一些目录，让我们看看如何删除它们。首先进入 testdir 目录并列出其内容：**cd testdir/**，然后 **ls**。之前创建的 reports 子目录存在。删除它的一种方法是输入：**rmdir reports**，然后再次 **ls** 以确认它已不存在。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_58_3.png)

- **步骤 9**
  快速警告：在终端中删除目录不会将其放入通过 Nemo 文件管理器的 Mint 回收站。文件也是如此。如果你从终端命令中删除一个目录，它就永久消失了。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_58_4.png)

- **步骤 10**
  Rmdir 仅删除空目录；要删除包含子目录甚至文件的目录，你需要使用 **rm** 命令并加上 **-R** 选项。例如，对于 Temp/finance 目录，使用 **rm -R Temp**。快速的 **ls** 显示父文件夹及其所有内容已被删除。使用此命令时要小心。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_58_5.png)

