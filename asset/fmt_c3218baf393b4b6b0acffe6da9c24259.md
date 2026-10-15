
以下步骤将指导你创建 shell 脚本。你将需要应用 John Muster 所著《UNIX 和 Linux 入门》`McGraw-Hill/Osborne, 2002`中的知识来创建脚本。

### 步骤 1
使用你的用户名和密码登录 Linux 电脑。打开终端窗口。

> 提示
> 记住你在上一个实验中将密码更改为 `2002`。

### 步骤 2
在提示符处输入以下命令创建一个文件：`cat > Workday`

### 步骤 3
创建并保存一个包含主目录文件列表、当前日期和十一月日历的脚本。

### 步骤 4
在运行脚本之前，确保 `Workday` 文件具有执行权限。

### 步骤 5
通过输入 `./Workday` 执行脚本。在提供的空间内记录脚本的结果。

> 提示
> 如果命令 `./Workday` 没有导致脚本执行，请确保 `Workday` 文件的权限可执行。

## 实验分析测试

- 1. 在 Red Hat Linux 7.3 上将密码改为 `password` 的结果是什么？
- 2. `noclobber` 变量是否防止用户向文件添加文本时覆盖文件？给出你的理由。
- 3. 密码文件中哪七个字段？简列列并定义每个字段。
- 4. 如何创建一个合并 `Chapter_1`、`Chapter_2` 和 `Chapter_3` 文件的顺序的文件？
- 5. 执行 `CTRL-D` 和 `CTRL-C` 命令的输出有什么区别？

### 关键术语测验

使用以下词汇完成这些句子。并非所有术语都会被使用。

```
awk
chmod
env
grep
$HOME
noclobber
sort
$USER
variable
wildcard
```

1. ________ 代表你的工作目录位置的变量。
2. ________ 可以代表命令中的一个字符字符串。
3. ________ 命令用于更改文件的权限/模式。
4. 名为 ________ 的变量可以防止实用工具的输出覆盖文件。
5. ________ 显示你的 shell 设置的一些环境变量的输出。

## 实验总结

你现在应该已经熟悉如何指示 shell 连接输入和输出的路径、在命令行中使用特殊字符，以及修改用户环境。你还应该知道如何更改密码以及创建和执行脚本。

## 解决方案

在本节，你将找到实验练习的解决方案。

### 实验解决方案 3.01

以下步骤将帮助 Sam 整理他小说的章节文件：

- **第一步** 你应该已经使用用户名和密码成功登录到 Linux 计算机并打开了终端。
- **第二步** 可以 `cat` 工具在你的主目录下创建 Sam 的章节文件。对于 `Chapter_1`，你应该输入以下内容：

```
cat > Chapter_1
It was a dark and stormy night.
ENTER
Christina unsuccessfully tried to block out the sounds of the thunderstorm.
CTRL-D
```

要创建 `Chapter_2`，你应该输入以下内容：

```
cat > Chapter_2
Christina looked at her watch.
ENTER
He was late.
CTRL-D
```

要创建 `Chapter_3`，你应该输入以下内容：

```
cat > Chapter_3
The sun was setting but Jake didn't care.
CTRL-D
```

- **第三步** 你应该已经使用 `ls` 命令验证主目录下是否已创建所有文件。要检索某个章节的行数、单词和字符数，命令为 `wc filename`。这将产生以下结果：

| 18 | 107 | Chapter_1 |
| 8 | 44 | Chapter_2 |
| 1 | 42 | Chapter_3 |

每一行都表示相应文件的行数、单词数和字符数。

- **第四步** 为了在你的主目录下创建一个名为 `ChapterList` 的组合文件并列出前三个章节的名称，你应该使用 `ls` 工具。正确的命令是 `ls > ChapterList`。结果显示在图 3-1 中。

### 解决方案 59

```
catherine@localhost~
File Edit Settings Help
[catherine@localhost catherine]$ ls > ChapterList
[catherine@localhost catherine]$ more ChapterList
Chapter_1
Chapter_2
Chapter_3
ChapterList
[catherine@localhost catherine]$ 
```

**图 3-1** `ChapterList` 文件内容这将创建一个文件，将目录中所有文件的列表输出合并到一个文件中。内容的顺序将与列出的文件名顺序一致。要按反序对文件排序，你应该执行带有反转参数的 `sort` 工具：`sort -r ChapterList` | `more`。

**第五步** `grep` 工具可用于定位文件中包含**单词**或字符字符串的行。要定位 `Chapter_1` 文件中的单词 `thunderstorm`：

```
grep thunderstorm Chapter_1
```

命令的结果应该列出以下文本：

Christina unsuccessfully tried to block out the sounds of the thunderstorm.

要定位 `Chapter_1` 文件中的单词 `storm`：

```
grep storm Chapter_1
```

命令的结果应该列出以下文本：

It was a dark and stormy night. Christina unsuccessfully tried to block out the sounds of the thunderstorm.

`grep` 工具列出每一行包含字符串 `storm` 的行，因此同时显示了包含单词 `storm` 的句子和包含单词 `thunderstorm` 的句子。

# 第 3 章：工具之旅、Shell 指令与进程

![](img/cd36a0da6ae9e7e1a75c3ec445e7e9b0_77_0.png)

```
### 图 3-2 小说文件中合并的章节
```

File Edit Settings Help

[catherine@localhost catherine]$ cat Chapter_1_Chapter_2_Chapter_3 > Novel

[catherine@localhost catherine]$ more Novel

It was a dark stormy night,

Christina unsuccessfully, she tried to block out the sounds of the thunderstorms.

Christina looked at her watch.

He was late.

The sun was setting but Jake didn't care.

[catherine@localhost catherine]$ 

```

**第六步** 为了创建一个名为 `Novel` 的文件，该文件是三个章节文件的合并，你应该输入：`cat Chapter_1_Chapter_2_Chapter_3 > Novel`。`ls` 命令将把 `Novel` 文件的内容显示在你的屏幕上，如图 3-2 所示。你应该已经成功注销了计算机登录。

## 实验解决方案 3.02

以下文本将帮助 Sam 管理来自工具的输入和输出：

**第一步** 你应该已经使用用户名和密码成功登录到 Linux 计算机并打开了终端窗口。

**第二步** 要创建名为 `Chapter_4` 的文件，你应该执行命令：`cat > Chapter_4` 并输入文本：

He knew that Christina was waiting for him on the other side of the country, yet he didn't feel the need to rush to meet her.

**第三步** 为了检查 `Chapter_4` 的拼写错误，你执行命令 `spell < Chapter_4`。系统应该返回拼写错误的单词 `waiting`。`spell` 命令没有对该单词提供修改建议。

**第四步** 为了输入并对 Sam 小说的潜在标题列表排序，你应该执行命令：

```
sort
Bad Attitudes
Love in Disguise
Never Enough
No Surprises
All or Nothing
CTRL-D
```

排序顺序将按字母顺序直接在原始列表下方列出潜在标题。

**第五步** 两个命令的结果均如图 3-3 所示。你应该已经成功完成了实验并注销了计算机登录。

## 实验解决方案 3.03

以下步骤将帮助 Sam 处理特殊字符：

**第一步** 你应该已经使用用户名和密码成功登录到 Linux 计算机并打开了终端。

**第二步** 通过在提示符处输入 `$HOME`，结果可能类似于：

```
/home/username
```

`HOME` 变量是一个 Shell 变量。当你登录时 Shell 获取了它。

![](img/cd36a0da6ae9e7e1a75c3ec445e7e9b0_78.png)

**图 3-3** 不同命令的结果

# 第 3 章：工具之旅、Shell 指令与进程

**第三步** 在命令提示符处执行 `echo C`。结果是以字母 `C` 开头的文件列表。

**第四步** 为了帮助 Sam 在所有章节中搜索名字，你应该执行 `grep Christina` 以查找 `Christina` 的结果，并执行 `grep Jake` 以查找 `Jake` 的结果。结果应该列出引用这些人物的章节。

**第五步** Sam 应在任何字符前加上反斜杠 `\` 以防止 Shell 解释它。例如：`echo \` 将呈现输出。

**第六步** 你应该执行命令：

```
echo Christina read the sign on the wall. It said \*BEWARE*.
```

此命令指示 Shell 输出句子但不解释字符，结果为：

Christina read the sign on the wall. It said **BEWARE**。

你应该已经成功完成了实验并注销了计算机登录。

## 实验解决方案 3.04

以下步骤将引导你防止文件被覆盖并更新密码：

**第一步** 你应该已经使用用户名和密码成功登录到 Linux 计算机并打开了终端。

**第二步** 为了显示 `Novel` 文件的内容，你应该执行 `more Novel` 命令。`Novel` 文件应该只包含 Sam 小说的前三个章节的文本。你可以通过执行 `cat Novel Chapter_4` 命令来更新 `Novel` 文件以包含 `Chapter_4` 的内容。

**第三步** 为了防止覆盖主目录中的文件，你需要执行 `set -o noclobber` 命令。为了验证你已激活该变量，你应该执行 `set -o noclobber` 命令。这将返回变量列表及其当前状态。`noclobber` 变量应设置为 `On`。

**第四步** 你无法使用图 3-4 所示的 `date` 工具对 `Novel` 文件进行任何更改。你应该通过执行 `set +o noclobber` 命令将 `noclobber` 变量恢复为 `Off` 设置。

**步骤 5** 要更改密码，你只需简单地执行 `passwd` 命令即可。系统会提示你输入当前密码，你应该通过输入密码来响应。随后，系统会提示你输入新密码。此时你应该输入新密码 `mfgw2002`。程序要求你再次输入新密码。如果操作正确，你将不会收到错误，密码将被更改。

**步骤 6** 你应该已经使用你的用户名和新密码成功登录计算机，以确认你确实已经更改了与登录账户关联的密码。完成此操作后，你将成功完成实验，因此可以注销系统。

## 实验解决方案 3.05

以下步骤将指导你创建一个 脚本：

- **第 1 步** 你应该已经使用用户名和密码成功登录 Linux 计算机，并打开了终端窗口。
- **第 2 步** 在提示符处输入命令 `cat > Workday` 创建新文件。
- **第 3 步** 一个满足 Sam 示例脚本如下：

```bash
echo My files to date are
ls
echo Today is
```

# 第 3 章：浏览工具、Shell 指令与进程

```
date
echo My deadlines are the 6th 13th and 24th
cal
CTRL-D
```

**步骤 4** 为了在尝试运行脚本之前确保 `Workday` 文件的权限为可执行，你可以使用 `ls -1 Workday` 命令查看文件权限，如图 3-5 所示。由于文件是刚创建的，它不应该是可执行的，因此你应该通过输入 `chmod +x Workday` 命令更改脚本的权限以允许其执行。

**步骤 5** 通过输入命令 `./Workday` 执行脚本后，你应该已经收到 `ls`、`date` 和 `cal` 命令的输出，并与你输入的文本整合。你应该已经成功完成了实验并注销了计算机。

图 3-5 `Workday` 文件的文件权限

# 第 4 章

## 使用可视化编辑器进行编辑

## 实验练习

- 4.01 在现有文件中工作
- 4.02 在文本文件中导航
- 4.03 创建并追加文本文件
- 4.04 向 Shell 和可视化编辑器下发指令
- 4.05 修改文本

实验分析测试

关键术语测验

实验总结

解决方案

# 第 4 章：使用可视化编辑器进行编辑

现在你应该已经熟悉使用工具创建文本文件。你已经操作过从文件读取输入、更改所读数据并将更改后的数据发送到屏幕、其他文件或工具的工具。本章比使用工具修改文件更进一步一步，引入了被称为 UNIX/Linux 可视化编辑器或 `vi` 的文本编辑器。

强大的 `vi` 编辑器允许用户通过组合按键组合提供所有指令来创建文本。可视化编辑器允许用户访问文件、在文本行之间移动、编辑文件中的内容并读取其他文件。以下实验旨在让你熟悉 `vi` 编辑器、它的命令模式和插入模式以及它提供的所有特性和功能。

20 分钟

## 实验练习 4.01：在现有文件中工作

Sam 想要探索使用可视化编辑器编辑他的小说的可能性。`Novel` 文本文件包含了 Sam 迄今编写的小说的所有章节。他想探索 `vi` 编辑器的命令模式，并在 `Novel` 文件中导航，搜索可能因文件长度过长而需要删除的文本。

### 学习目标

在实验中，你将通过在现有文件中工作来探索可视化编辑器。在本结束时，你将能够：

- 激活可视化编辑器
- 在命令模式下操作

## 实验练习 4.01：在现有文件中工作

- 在文本文件中移动
- 删除文本并撤销文本更改
- 退出可视化编辑器

### 实验材料与设置

你本次实验所需的材料有：

- 安装了 Red Hat Linux 7.3 的计算机
- 铅笔和纸
- 成功完成之前所有的实验

### 开始开始

以下步骤将指导你通过在现有文件中工作来探索可视化编辑器的功能。你将应用在 John Master 编写的《UNIX 和 Linux 入导》`McGraw-Hill/Osborne, 2002` 书中中学的知识使用可视化编辑器进行编辑。

**步骤 1** 使用你的用户名和密码登录 Linux 计算机。打开终端窗口。

> 提示：记住你在上一个实验中应该已经将密码更改为 `MbfGW2002`。

**步骤 2** 通过列出目录内容，确保你的家目录下有 `Novel` 文件。指示 Shell 打开 `Novel` 文件以便你可以查看内容。

**步骤 3** 一旦你通过 Shell 查看了文件内容，就用可视化编辑器打开 `Novel` 文件。文件内容看起来和打开时的一样吗？

**步骤 4** 使用逐行移动的按键导航。哪些键可以逐行向下移动？

**步骤 5** 使用所有可用的方向键进行导航。列出这些键及其对应的方向。

**步骤 6** 输入指令让可视化编辑器在 `Novel` 文件中搜索并将光标移动到 `the`。找到 `the` 第一个出现处后，找到随后的每一个位置。

**步骤 7** 输入指令让可视化编辑器在 `Novel` 文件中搜索并将光标移动到 `rush`。指示 `vi` 删除句子中的 words `rush to`。

**步骤 8** 导航到 `Novel` 文件中的第一行。指示编辑器删除整行。指示 `vi` 撤销对行的更改。

**步骤 9** 将你的更改保存到 `Novel` 文件并退出可视化编辑器。通过向 Shell 执行 `dir` 命令确认你已退出可视化编辑器。更改保存了吗？注销计算机。

## 实验练习 4.02：在文本文件中导航

30 分钟

Sam 发现使用可视化编辑器滚动他的 `Novel` 文本文件需要很长时间。到目前为止，他一直是按行和字符在文件中移动。他想加快在文本文件中导航的过程，并请求你帮助使用增强方向键、行号和目标搜索来实现。

### 学习目标

在练习中，你通过可视化编辑器在文本文件中导航。完成实验后，你将能够：

- 按行和字符在文本文件中导航
- 探索增强方向命令
- 使用行号
- 搜索文本文件

### 实验材料与设置

你本次实验所需的材料有：

- 安装了 Red Hat Linux 7.3 的计算机
- 铅笔和纸

### 开始开始

以下步骤将指导你通过插入模式探索可视化编辑器的功能。你将应用在 John Master 编写的《UNIX 和 Linux 入导》`McGraw-Hill/Osborne, 2002` 书中学的知识使用可视化编辑器在文本文件中进行导航。

**步骤 1** 使用你的用户名和密码登录 Linux 计算机。打开终端窗口。

**步骤 2** 用可视化编辑器打开 `Novel` 文本文件。使用增强方向键在文本文件中导航，遵循以下指令：

- a) 向下 4 行。
- b) 向右移动 6 个空格。
- c) 向上移动 2 行。
- d) 向左移动 4 个空格。

你在文本中的最终位置在哪里？请指示到达每个指令位置时使用的增强方向键或命令。
