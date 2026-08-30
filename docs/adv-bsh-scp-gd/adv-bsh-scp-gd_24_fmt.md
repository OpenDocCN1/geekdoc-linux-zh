
# 第十九章 Here 文档

> 原文：[`tldp.org/LDP/abs/html/here-docs.html`](https://tldp.org/LDP/abs/html/here-docs.html)

| | **现在就做，孩子们。** |
|---|------------------------|
| | *--Aldous Huxley, *Island*** |

*here document* 是一种特殊用途的代码块。它使用一种 I/O 重定向的形式将命令列表传递给交互式程序或命令，例如 `ftp`、`cat` 或 *ex* 文本编辑器。

```
COMMAND <<InputComesFromHERE
...
...
...
InputComesFromHERE
```

*limit string* 界定了（框架）命令列表。特殊符号 `<<` 在限制字符串之前。这具有将命令块输出重定向到程序或命令的 `stdin` 的效果。它类似于 `interactive-program < command-file`，其中 `command-file` 包含

```
command #1
command #2
...
```

*here document* 的等效形式如下所示：

```
interactive-program <<LimitString
command #1
command #2
...
LimitString
```

选择一个足够不寻常的 *limit string*，这样它就不会出现在命令列表中并引起混淆。

注意，*here document* 有时与非交互式实用程序和命令一起使用，效果很好，例如 `wall`。

**示例 19-1\. *广播*: 向所有登录用户发送消息**

```
#!/bin/bash

wall <<zzz23EndOfMessagezzz23
E-mail your noontime orders for pizza to the system administrator.
    (Add an extra dollar for anchovy or mushroom topping.)
# Additional message text goes here.
# Note: 'wall' prints comment lines.
zzz23EndOfMessagezzz23

# Could have been done more efficiently by
#         wall <message-file
#  However, embedding the message template in a script
#+ is a quick-and-dirty one-off solution.

exit
```

即使像 *vi* 文本编辑器这样的不太可能的候选者也适合使用 *here document*。

**示例 19-2\. *dummyfile*: 创建一个两行的虚拟文件**

```
#!/bin/bash

# Noninteractive use of 'vi' to edit a file.
# Emulates 'sed'.

E_BADARGS=85

if [ -z "$1" ]
then
  echo "Usage: `basename $0` filename"
  exit $E_BADARGS
fi

TARGETFILE=$1

# Insert 2 lines in file, then save.
#--------Begin here document-----------#
vi $TARGETFILE <<x23LimitStringx23
i
This is line 1 of the example file.
This is line 2 of the example file.
^[
ZZ
x23LimitStringx23
#----------End here document-----------#

#  Note that ^[ above is a literal escape
#+ typed by Control-V <Esc>.

#  Bram Moolenaar points out that this may not work with 'vim'
#+ because of possible problems with terminal interaction.

exit
```

上述脚本同样可以用 `ex` 实现，而不是 `vi`。包含 `ex` 命令列表的 *here document* 足够常见，可以形成一个自己的类别，称为 *ex 脚本*。

```
#!/bin/bash
#  Replace all instances of "Smith" with "Jones"
#+ in files with a ".txt" filename suffix. 

ORIGINAL=Smith
REPLACEMENT=Jones

for word in $(fgrep -l $ORIGINAL *.txt)
do
  # -------------------------------------
  ex $word <<EOF
  :%s/$ORIGINAL/$REPLACEMENT/g
  :wq
EOF
  # :%s is the "ex" substitution command.
  # :wq is write-and-quit.
  # -------------------------------------
done
```

与 "ex 脚本" 类似的是 *cat 脚本*。

**示例 19-3\. 使用 *cat* 的多行消息**

```
#!/bin/bash

#  'echo' is fine for printing single line messages,
#+  but somewhat problematic for for message blocks.
#   A 'cat' here document overcomes this limitation.

cat <<End-of-message
-------------------------------------
This is line 1 of the message.
This is line 2 of the message.
This is line 3 of the message.
This is line 4 of the message.
This is the last line of the message.
-------------------------------------
End-of-message

#  Replacing line 7, above, with
#+   cat > $Newfile <<End-of-message
#+       ^^^^^^^^^^
#+ writes the output to the file $Newfile, rather than to stdout.

exit 0

#--------------------------------------------
# Code below disabled, due to "exit 0" above.

# S.C. points out that the following also works.
echo "-------------------------------------
This is line 1 of the message.
This is line 2 of the message.
This is line 3 of the message.
This is line 4 of the message.
This is the last line of the message.
-------------------------------------"
# However, text may not include double quotes unless they are escaped.
```

用于标记 here 文档限制字符串的 `-` 选项 (`<<-LimitString`) 抑制输出中的前导制表符（但不包括空格）。这可能在使脚本更易读时很有用。

**示例 19-4\. 多行消息，抑制了制表符**

```
#!/bin/bash
# Same as previous example, but...

#  The - option to a here document <<-
#+ suppresses leading tabs in the body of the document,
#+ but *not* spaces.

cat <<-ENDOFMESSAGE
	This is line 1 of the message.
	This is line 2 of the message.
	This is line 3 of the message.
	This is line 4 of the message.
	This is the last line of the message.
ENDOFMESSAGE
# The output of the script will be flush left.
# Leading tab in each line will not show.

# Above 5 lines of "message" prefaced by a tab, not spaces.
# Spaces not affected by   <<-  .

# Note that this option has no effect on *embedded* tabs.

exit 0
```

*here document* 支持参数和命令替换。因此，可以将不同的参数传递给 *here document* 的主体，从而相应地改变其输出。

**示例 19-5\. 带有可替换参数的 here 文档**

```
#!/bin/bash
# Another 'cat' here document, using parameter substitution.

# Try it with no command-line parameters,   ./scriptname
# Try it with one command-line parameter,   ./scriptname Mortimer
# Try it with one two-word quoted command-line parameter,
#                           ./scriptname "Mortimer Jones"

CMDLINEPARAM=1     #  Expect at least command-line parameter.

if [ $# -ge $CMDLINEPARAM ]
then
  NAME=$1          #  If more than one command-line param,
                   #+ then just take the first.
else
  NAME="John Doe"  #  Default, if no command-line parameter.
fi  

RESPONDENT="the author of this fine script"  

cat <<Endofmessage

Hello, there, $NAME.
Greetings to you, $NAME, from $RESPONDENT.

# This comment shows up in the output (why?).

Endofmessage

# Note that the blank lines show up in the output.
# So does the comment.

exit
```

这是一个有用的脚本，其中包含带有参数替换的 *here document*。

**示例 19-6\. 将文件对上传到 *Sunsite* 入口目录**

```
#!/bin/bash
# upload.sh

#  Upload file pair (Filename.lsm, Filename.tar.gz)
#+ to incoming directory at Sunsite/UNC (ibiblio.org).
#  Filename.tar.gz is the tarball itself.
#  Filename.lsm is the descriptor file.
#  Sunsite requires "lsm" file, otherwise will bounce contributions.

E_ARGERROR=85

if [ -z "$1" ]
then
  echo "Usage: `basename $0` Filename-to-upload"
  exit $E_ARGERROR
fi  

Filename=`basename $1`           # Strips pathname out of file name.

Server="ibiblio.org"
Directory="/incoming/Linux"
#  These need not be hard-coded into script,
#+ but may instead be changed to command-line argument.

Password="your.e-mail.address"   # Change above to suit.

ftp -n $Server <<End-Of-Session
# -n option disables auto-logon

user anonymous "$Password"       #  If this doesn't work, then try:
                                 #  quote user anonymous "$Password"
binary
bell                             # Ring 'bell' after each file transfer.
cd $Directory
put "$Filename.lsm"
put "$Filename.tar.gz"
bye
End-Of-Session

exit 0
```

引用或转义 here 文档头部的 "limit string" 禁止其主体内的参数替换。原因是 *引用/转义 limit string* 有效地转义了 `$`、`` ` ``、`\` 特殊字符，并使它们被字面地解释。（感谢 Allen Halsey 指出这一点。）

**示例 19-7\. 关闭参数替换**

```
#!/bin/bash
#  A 'cat' here-document, but with parameter substitution disabled.

NAME="John Doe"
RESPONDENT="the author of this fine script"  

cat <<'Endofmessage'

Hello, there, $NAME.
Greetings to you, $NAME, from $RESPONDENT.

Endofmessage

#   No parameter substitution when the "limit string" is quoted or escaped.
#   Either of the following at the head of the here document would have
#+  the same effect.
#   cat <<"Endofmessage"
#   cat <<\Endofmessage

#   And, likewise:

cat <<"SpecialCharTest"

Directory listing would follow
if limit string were not quoted.
`ls -l`

Arithmetic expansion would take place
if limit string were not quoted.
$((5 + 3))

A a single backslash would echo
if limit string were not quoted.
\\

SpecialCharTest

exit
```

关闭参数替换允许输出文本。生成脚本甚至程序代码是这种用途之一。

**示例 19-8\. 生成另一个脚本的脚本**



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`。

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
