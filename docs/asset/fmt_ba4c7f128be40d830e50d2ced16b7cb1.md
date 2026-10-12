
`cp messages messages.`

`STATUS=$?`

`if [ "$STATUS" -eq 0 ]`

`then`

`    compress messages.1 & # 在后台运行 compress`

`else`

`    echo "Could not make copy of the original log file" >&2`

`fi`

```
如果上一个示例中的 cp 命令失败，可能是由于目录权限问题、文件系统满或磁盘本身出现问题。并不是所有命令在这种失败情况下都会返回非零值。正如你所看到的，测试比较命令根据比较是否有效返回 0 或 1。
```

`firstname="john"`

`lastname="smith"`

`[ "$firstname" = "$lastname" ]`

`echo $? # 这会打印 1，因为它们不相等`

`[ "$firstname" = "john" ]`

`echo $? # 这会打印 0，因为它们相等`

### 使用不冲突的临时文件

如果你编写了一个许多人认为很有用的脚本，那么可能许多人会同时运行它。如果该脚本在运行时需要打开临时文件，你需要采取措施，防止一个脚本副本覆盖另一个同时运行的脚本副本的临时文件。坦率地说，`$$` 变量允许你做到这一点。每当你运行脚本时，`$$` 被设置为脚本的进程 ID（PID）。系统上运行的每个作业在进程或程序运行时都会获得唯一的 PID。`$$` 允许你拥有自己的 PID。

如果两个用户同时运行同一个脚本，无论它们包含什么文件名，都在不同的进程 ID 下运行，因此一个用户不会与另一个运行相同脚本的用户创建的文件冲突。因此，你应该将 `$$` 变量作为脚本需要创建的任何文件名的一部分。

假设你想编写一个脚本，读取文件并为文件中所有行添加行号。`nl` 命令可以完成此工作的一部分：它会为所有行编号，但仅限于输出中的行。要修改原始文件，你必须将 `nl` 的输出保存到临时文件，然后用临时文件替换原始文件：

```
if [ "$#" -ne 1 ];
then
echo "Error: This script needs 1 argument" >&2
exit 3
fi
nl "$1" > /tmp/nm$$ "$1"
# 对 $1 指定的文件运行 Unix nl 命令
#并将结果保存到临时文件中，该文件
# 不与其他同时运行相同脚本的
# 用户发生冲突。如果 nl 执行成功，
#
```

## 第六部分 脚本编程

## 第 28 章 编写 Bourne Shell 脚本

### 将所有参数传递给另一个命令

现在你知道如何使用 `$#` 计算传递给脚本的参数数量，但如何获取参数本身的实际列表呢？特殊变量 `$*` 包含了该列表。

如果你想让脚本使用 `ls` 对你在命令行指定的任何文件进行详细列出，你可以这样写：

```
if [ "$#" -eq 0 ];
then
  echo "This script takes at least one argument" >&2
  exit 2
fi
ls -l $*
```

如你所见，`ls` 获取了你传递给脚本的所有命令行参数。因此，如果脚本命名为 `lister` 并你这样运行它：

```
./lister core /tmp/test
```

它等同于输入以下内容：

```
ls -l core /tmp/test
```

### 结束脚本并设置完成状态

当脚本完成工作并准备终止时，显式地返回退出状态比让 shell 返回上一个执行命令的退出状态要好。这在你因为错误条件退出时尤为如此，因为你想向任何可能调用你脚本的脚本发出通知。而且，通常如果脚本正常退出，给出零（0）退出状态是很好的，这样任何可能调用你脚本的脚本都可以检查你的退出状态并确信一切正常。你给出的任何退出状态都将是你脚本的状态：

```
cp acme /tmp/archive {};
STATUS=$?
if [ "$STATUS" -ne 0 ]; then
    echo "Error: copy failed" >&2
    exit 1
fi
exit 0
```

### 标准退出错误

#### 给出正确的用法错误

在第 1 章“UNIX 和 Shell 简介”中，你学到了在 UNIX 中没有消息就是好消息。许多初学者会看到命令弹出一个 Usage（用法）消息，却没有意识到命令已经失败。当你看到 Usage 这个时，请想：“错误，你误用了命令”。这里是正确的用法：

在上一个示例中，`cp` 命令无效的，因为没有给出目标文件。生成了用法错误，显示了输入命令所需的语法。

这是一个示例，说明了你应该放在每个脚本中的第一个测试。在这个示例中，你拥有脚本的第一部分，它可以将文件复制到归档位置，压缩归档，然后删除原始文件。它要求你提供至少一个文件名来执行此操作：

```
if [ "$#" -eq 0 ];
then
    echo "Error: no filenames given" >&2
    echo "Usage: $0 filename ..." >&2
    exit 1
fi
```

为你的脚本构造正确的用法消息，注意消息必须以以下之一开头：

Usage:
usage:

然后在消息中放入命令名称。或者，可以使用 `$0` 变量来插入当前脚本的名称，如下两个示例所示：

Usage: myscript
Usage: $0

然后指定命令允许的任何选项，随后跟上所有以单单词描述的允许参数。使用方括号 `[]` 来指示可选元素：

```
Usage: $0 [-fip] filename username dir-to-process
```

以下示例是不正确的，因为最后一个参数没有被指示为单单词，因此意味着选项之后必须有五个参数：

```
Usage: $0 [-fip] filename username dir to process
```

## 第六部分 第28 章

### 用法信息 (Usage messages)

用法信息应该显示在标准错误输出中，而不是标准输出中。在 `echo` 语句后面附加 `>&2` 可以将输出重定向到标准错误。`>&2` 内部不允许有空格。

`echo "Usage: $0 [-f] filename username dir-to-process" >&2`

这里是一个不正确的用法信息示例：

`echo "Usage: filename does not exist" >&2 # 错误`

上一个例子实际上是一个错误消息，而不是用法信息，因为它没有提供允许的语法。错误消息是有用的，并且可以与用法信息结合使用。以下是两种消息的良好用法：

`echo "Error: filename does not exist" >&2`
`echo "Usage: $0 [-f] filename dir-to-process" >&2`

### 使用 exit 避免深度嵌套

下面的代码写得不好，因为它存在不必要的嵌套且冗肿。这使得代码难以追踪且非常难以修改。错误消息距离对应的错误测试点很远：

```
if [ $# eq 2 ]
  then
    if [ -d $1 ]
      then
        if [ -f $2 ]
          then
            cp $2 $1
          else
            echo Error: $2 not a file >&2
            exit 3
        fi
      else
        echo Error: $1 not a directory >&2
        exit 2
  else
    echo Usage: `basename $0` directory file >&2
    exit 1
fi
```

## 第六部分 脚本编程

## 第28 章 编写 Bourne Shell 脚本

记住 `exit` 会结束程序，你可以大大改进之前的示例；因此，没有必要使用 `else` 关键字。这种认知消除了嵌套（将一个 `if` 语句放在另一个内部）的需求，并允许你编写可读性更高、更容易维护和修改的模块化代码。下面的代码功能与之前相同，但代码更好：

```
if [ $# -ne 2 ]
then
    echo Usage: basename $0 directory file >&2
    exit 1
fi
```

```
if [ ! -d $1 ]
then
    echo Error: $1 not a directory >&2
    exit 2
fi
```

```
if [ ! -f $2 ]
then
    echo Error: $2 not a file >&2
    exit 3
fi
```
