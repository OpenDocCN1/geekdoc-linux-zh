
```bash
counter=0
INPUT=/tmp/input_file
while read -r
do
  ((counter++)) # 给计数器加1。
  print "This is record number $counter"
done < $INPUT
```

还有其他实现相同的方法，但它们通常要慢得多！

# 如何设置你的 PROFILE

在你的家目录下，有两个文件由系统管理员设置的文件：

如果你使用 Korn shell，文件名为 `.profile` 和 `.kshrc`

如果你使用 bash shell，文件名为 `.bash_profile` 和 `.bashrc`

在修改它们之前，始终保存一份原始文件的副本：

```bash
cp .profile .profile_Apr15
```

```bash
cp .bashrc .bashrc_Apr15
```

## 这里是我自定义 .profile 的方式

这是文件 `/home/larry/.profile`

# 获取别名和函数

在同时按下 Control+H 时删除之前输入的字符：

`"H"` 在使用 vi 时允许自动缩进。

`set -ignore` # 将变量取消，只需。

`set -u` # 显示未设置的消息。

`export EDITOR=/usr/bin/vim`

`export VISUAL=/bin/vim`

`export SHELL=/bin/ksh`

`export PERL5=/usr/lib/perl/5.8`

`export ORACLE_HOME=/dbms/app/product/99.4`

`export PS1='$ # 你的提示符后面跟着一个空格。`

`set -a -a` 会导出 profile 中所有的变量

# .profile

## 这里是我自定义包含别名的文件的方式

这是文件 `/home/larry/.kshrc`

```bash
if [ -f /etc/kshrc ]; # 如果 /kshrc 文件存在，那么
    source /etc/kshrc # 然后源化它。
fi
```

### 2. Korn 简介，第 42 页

```bash
alias cd=cd /home/larry/DOC-alias-15
alias ddoc=cd /home/larry/DOC-alias-15
alias cds=cd /home/larry/SCRIPTS-alias-15
alias cbd=cd /home/larry/SCRIPTS-alias-15
alias cdp=cd /home/larry/PERL-alias-15
alias cdr=cd /home/larry/ROSETTA-alias-15
alias cdt=cd /home/larry/ROSETTA:LOG-alias-15
alias cdi=cd /home/larry/INT_TEST-alias-15
alias cvs=cd /home/larry/SYS_TEST-alias-15
alias cdsql=cd /home/larry/SQL-alias-15
alias dcdgi=cd /usr/lib/cups/cgi-bin,alias-15
alias via=vi /home/larry/DOC/acronyms
alias vit=vi /home/larry/DOC/todo
alias if=clear,for:pwd
export PS1=$$
set o vi # 允许你使用 vi 编辑命令行上的命令。
# .kshrc
```

另见：Larry Smith 使用 Unix 类 编辑器 (`W.LarrySmithBooks.com`)

# 别名

如果你使用 ksh shell，你的 profile 在 `$HOME/.profile`，别名在 `$HOME/.kshrc`

如果你使用 bash shell，你的 profile 在 `$HOME/.bash_profile`，别名应该在 `$HOME/.bashrc`

`aliases` 是命令快捷方式；它们设置非常简单，能节省你大量的时间和麻烦。我的建议是：设置它们并使用它们

你的 profile 文件应该包含类似这样的一行：

```bash
if [ -f ~/.kshrc ]; then ~/.kshrc
```

那一行允许你使用任何你放入 `.kshrc` 的别名

以下是我放在我的 `/home/larry/.kshrc` 中的三个别名示例：

注意：命令末尾的符号后必须有一个单引号 (`''`)：

```bash
alias cd=cd /home/larry/DOC-alias-15
alias ddoc=cd /home/larry/DOC-alias-15
alias cds=cd /home/larry/SCRIPTS-alias-15
alias cbd=cd /home/larry/SCRIPTS-alias-15
alias cdp=cd /home/larry/PERL-alias-15
alias cdr=cd /home/larry/ROSETTA-alias-15
alias cdt=cd /home/larry/ROSETTA:LOG-alias-15
alias cdi=cd /home/larry/INT_TEST-alias-15
alias cvs=cd /home/larry/SYS_TEST-alias-15
alias cdsql=cd /home/larry/SQL-alias-15
alias dcdgi=cd /usr/lib/cups/cgi-bin,alias-15
alias via=vi /home/larry/DOC/acronyms
alias vit=vi /home/larry/DOC/todo
alias if=clear,for:pwd
```

# 第 2 部分，Korn 简介，第 48 页

注意：`ls -lto` 类似于 "`ls -l`，但它不打印文件所有者 (`o`)，不打印组 (`g`)，并且按照时间顺序 (`t`) 从最旧的文件到最近更新的文件 (`-r`) 列出文件。"

我的第三个“命令快捷方式”是对上述命令的轻微变体：

`alias cdsql=/home/larry/SQL;clear;lsrtail -15;pwd`

我不是切换目录到 `/home/larry/SCRIPTS`，而是 `cd` 到 `/home/larry/SQL`，我在那里存放了我的数据库脚本。

在设置别名（`alias`）时，重要的是像示例（上文）所示使用单引号。切勿使用反引号（graves）、波引号（ticks）或引号来设置别名。（如果你想理解最后这句话的意思，请查看此书中名为 `backquotes.ticks.graves_and_qx.ksh` 的脚本）。

## 如何使用本书

- 1. 对你来说，从头到尾读这本书既不是必要的也不是明智的。
- 2. 浏览目录（其中列出了书中每一个脚本/程序）。列出了每个脚本的难度级别（简单 `EASY`、中等 `MEDIUM` 或挑战性 `CHALLENGING`），并提供了它的“用途” (`PURPOSE`)。

本书按脚本名称的字母顺序排列的。

请允许我再次强调：

本书是按脚本名称字母顺序排列的！

如果你想找到一个使用 "`find`" 命令的脚本，它位于 "`F`" 部分下的 "`find.ksh`"。

如果你在寻找如何使用 "`cut`" 命令的真实世界示例，请查看 "`C`" 部分：有一个名为 "`cut.ksh`" 的脚本。

脚本的名称会告诉你它将为你执行什么：

同名为 "`calculate_average_and_percentage.ksh`" 的脚本将计算平均值和百分比。
- 3. 本版书籍包含一个扩展索引。

去书的末尾；去浏览吧！索引中的每一项都会指向一个特定的脚本或文件。
- 4. 如果你买了这本书的 PDF 版并想查看名为 "`calculate_average_and_percentage.ksh`" 的脚本，请使用 PDF 的“查找”功能来查找该名称。（同时按 CONTROL 键和 'F' 键，在 Adobe Acrobat 屏幕右上角的文本框中输入 "`calculate_aver`"，按回车）。

名为 "`calculate_average_and_percentage.ksh.OUTPUT`" 的文件显示了该脚本产生的输出。
- 5. 找到你感兴趣的脚本；阅读它，然后运行它。

大多数脚本包含一个标记为“另” (`SEE ALSO`) 的部分，列出了类似的脚本。
- 6. 找到一个可以执行你老板想要完成的任务。去执行！
- 7. 如果你的目标是学习另一种语言，如 Perl 或 Bash，请浏览本书的第 3 和 4 部分。第 3 部分向你展示 Shell 命令（如 "`cut`"）以及对应的 Perl 命令 ("`split`")。第 4 部分向你展示 Perl 命令（如 "`split`"）以及对应的 Bash 或 Korn 命令 ("`cut`")。这两个部分都告诉你是使用每个命令的脚本名称。

假设你已经查看了名为 "`calculate_average_and_percentage.ksh`" 的脚本，并知道如何使用 Perl 编写相同的脚本。在该系列的第 2 本中找到名为 "`calculate_average_and_percentage.pl`" 的脚本：
