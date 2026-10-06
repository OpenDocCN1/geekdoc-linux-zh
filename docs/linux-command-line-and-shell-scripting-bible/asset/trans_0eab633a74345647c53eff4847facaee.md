

# 第二部分 Shell 脚本基础

## 字符串长度

在尝试评估变量是否包含数据时，`-n` 和 `-z` 比较非常有用：

```bash
$ cat test10
#!/bin/bash
# testing string length
val1=testing
val2=''

if [ -n $val1 ]
then
    echo "The string '$val1' is not empty"
else
    echo "The string '$val1' is empty"
fi

if [ -z $val2 ]
then
    echo "The string '$val2' is empty"
else
    echo "The string '$val2' is not empty"
fi

if [ -z $val3 ]
then
    echo "The string '$val3' is empty"
else
    echo "The string '$val3' is not empty"
fi
$ ./test10
The string 'testing' is not empty
The string '' is empty
The string '' is empty
$
```

此示例创建了两个字符串变量。`val1` 变量包含一个字符串，而 `val2` 变量被创建为空字符串。随后进行了以下比较：

`if [ -n $val1 ]`
判断变量长度是否非零，确实如此，因此处理 `then` 部分。

`if [ -z $val2 ]`
判断 `val2` 变量长度是否为零，确实如此，因此处理 `then` 部分。

`if [ -z $val3 ]`
判断 `val3` 变量长度是否为零。该变量在 Shell 脚本中从未被定义，因此表明字符串长度仍然为零，即使它未被定义。

## test 命令文件比较

| 比较 | 描述 |
| :--- | :--- |
| -d file | 检查文件是否存在且是一个目录。 |
| -e file | 检查文件是否存在。 |
| -f file | 检查文件是否存在且是一个文件。 |
| -r file | 检查文件是否存在且可读。 |
| -s file | 检查文件是否存在且不为空。 |
| -w file | 检查文件是否存在且可写。 |
| -x file | 检查文件是否存在且可执行。 |
| -O file | 检查文件是否存在并属于当前用户。 |
| file-nt file2 | 检查 file1 是否比 file2 新。 |
| file-ot file2 | 检查 file1 是否比 file2 旧。 |

> 注意：空变量和未初始变量可能会对你的 Shell 脚本产生灾难性的影响。当我们不确定变量的内容时，在将其用于数字或字符串比较之前，最好先使用 `-n` 或 `-z` 测试该变量是否包含值。

## 文件比较

最后一类 `test` 比较可能是 Shell 脚本中最强大且最常用的比较方法。`test` 命令允许你测试 Linux 文件系统上文件和目录的状态。表 9-3 列出了这些比较。

这些条件让你你能够在 Shell 脚本中检查文件系统中的文件，它们通常被用于访问文件的脚本中。由于被频繁使用，让我们逐一查看它们。

## 检查目录

`-d` 测试检查指定的名称在系统中是否以目录的形式存在。如果你尝试向某个目录写入文件，或者在尝试切换目录位置之前，这是一个很好的做法：

```bash
$ cat test1
#!/bin/bash
# look before you leap
if [ -d $HOME ]
then
echo "Your HOME directory exists"
cd $HOME
ls -a
else
echo "There's a problem with your HOME directory"
fi

$ ./test11

Your HOME directory exists
Drivers ICEAuthority recently
. emacs.ds joomla redhat
4rich evolution .lessh rpm.list
backup.zip .fontconfig metacity passansson
.bash_history .gconf store
.bash_logout .gconf mozilla store.sql

bash_profile gimp-2.2 store.zip
.bashrc myprop Templates
.bittrent gnome myproblem test
.ccache gnome2 myprog testl1
.config gnome2.private .mysql.History thumbnails
Desktop gphphit nautilus Trash
dmc gstreamer-0.10 openoffice.org.20 Videos
Documents gtk-bookmarks Pictures viminho
Download gtkrc-1.2-gnome2 Public
$
```

示例代码使用 `-d` 测试条件来检查用户的 `HOME` 目录是否存在。如果存在，它将继续使用 `cd` 命令切换到 `HOME` 目录并执行目录列表。

## 检查对象是否存在

`-e` 比较允许你在尝试在脚本中使用对象之前检查该文件或目录对象是否存在：

```bash
$ cat test12
#!/bin/bash
# checking if a directory exists
if [ -e $HOME ]
then
echo "OK on the directory, now let's check the file"
# checking if a file exists
if [ -e $HOME/testing ]
then
# the file exists, append data to it
echo "Appending date to existing file"
date >> $HOME/testing
else
# the file doesn't exist, create a new file
echo "Creating new file"
date > $HOME/testing
fi
else
echo "Sorry, you don't have a HOME directory"
fi
$ ./test12
OK on the directory, now let's check the file
Appending date to existing file
```

`-e` 比较允许你在尝试使用对象之前检查其是否存在（注：OCR 文本在此似乎合并了逻辑/重复，但逻辑流遵循检查存在性）。

## 使用结构化命令

（注：提供的源文件中此部分的 OCR 文本似乎碎片化或重复。根据提供的文本，内容在下方已清理。）

