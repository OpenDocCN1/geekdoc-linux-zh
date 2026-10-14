
```bash
$ cat checkargs
case $1 in
  -([a-z])
    print "Lowercase argument given: $1" ;;
  -([A-Z])
    print "Uppercase argument given: $1" ;;
  @([1-9]*([0-9]))
    print "Integer argument given: $1" ;;
  "")
    print "No argument given" ;;
  *)
    print "Invalid argument given" ;;
esac
```

这里是示例输出：

```bash
$ checkargs -a
Lowercase argument given: -a
$ checkargs 999
Integer argument given: 999
$ checkargs -z
Invalid argument given: -z
$ checkargs
No argument given
```

## 第8 章：编写 Korn Shell 脚本

```sh
for FILE in $@
do
    print "Copying $FILE to ukas"
    uucp $FILE ukas
done
```

现在用 `uucp` 将一个文件复制到 `ukas`：

```sh
$ myuucp chap1
Copying chap1 to ukas
```

或者将所有 `chap` 文件复制到 `ukas`：

```sh
$ myuucp chap*
Copying chap1 to ukas
Copying chap2 to ukas
Copying chap3 to ukas
...
```

如果没有参数，则什么都不显示：

```sh
$ myuucp
$
```

### 其他 `for` 语法

`for` 命令也可以在不带单词参数列表的情况下的情况下使用：

```sh
for variable
do
    commands
done
```

# Korn Shell 用户与编程手册

命令会为每个位置参数执行一次，并且变量被设置为后续的每个位置参数。这等同于：

```sh
for variable in "$@"
do
    commands
done
```

`myuucp` 脚本可以修改为使用这种格式，并保持相同的功能。

```sh
$ cat myuucp
for FILE
do
    print "Copying $FILE to ukas"
    uucp $FILE ukas
done
```

使用这种格式在一行内输入 `for` 命令：

```sh
for var in word1 word2...wordn; do commands; done
or
for var ; do commands; done
```

注意 `do` 和 `done` 命令之前的分号 `;` 字符。这是为了将 `do` 和 `done` 命令与之前的命令隔开。

## 第8 章：编写 Korn Shell 脚本

### `if` 命令

`if` 命令用于在给定条件为真时执行命令。`if` 命令的基本语法为：

```sh
if command1
then
    commands
fi
```

如果 `command1` 返回零退出状态，则执行 `then` 和 `fi` 之间的命令。否则，跳过这些命令。例如，如果 `ANSWER` 被设置为 `YES`，则执行 `print` 命令。

```sh
if [[ $ANSWER = YES ]]
then
    print "Ok, the answer is $ANSWER"
fi
```

这是一个 Korn shell 脚本，它使用 `if` 命令在尝试复制文件之前检查文件是否存在。

```sh
$ cat fileck
FILE=$1
if [ -f $FILE ];
then
    print "Copying $FILE to PUBDIR"
    cp $FILE /usr/spool/uucppublic
fi
```

我们可以再添加一个 `if` 命令来检查参数数量。如果命令行参数少于一个，则打印用法信息并退出脚本。

```sh
$ cat fileck
if (($# < 1))
then
  print "Usage: $0 file"
  exit 1
fi
FILE=$1
if [[ -f $FILE ]]
then
  print "Copying $FILE to PUBDIR"
  cp $FILE /usr/spool/uucpublic
fi
```

`fileck` 中的命令行参数检查可以使用 `&&` 运算符写成如下所示：

```sh
((# < 1)) && { print "Usage:$0 file"; exit 1; };
```

这个版本更加紧凑，尽管比之前使用 `if` 命令的版本可读性稍差。

如果你想在一行内提供 `if` 命令，请使用这种格式：

```sh
if command1 ; then command2 ; fi
```

需要 `;` 字符来将 `then` 和 `fi` 与之前的命令隔开。

### 其他 `if` 语法：`else`

这种形式的 `if` 命令用于在条件为真时执行一组命令，在条件为假时执行另一组命令。

```sh
if command1
then
    commands
else
    commands
fi
```

如果 `command1` 返回零退出状态，则执行 `then` 和 `else` 之间的命令。如果 `command1` 返回非零退出状态，则执行 `else` 和 `fi` 之间的命令。在这个示例中，如果 `ANSWER` 是 `YES`，则执行 `print` 命令。否则，退出：

```sh
if [[ $ANSWER = YES ]]
then
    print "Ok, the answer is $ANSWER"
else
    exit 1
fi
```

我们可以为 `fileck` 中的 `if` 命令添加 `else` 部分，以确保文件在被复制之前存在：

```sh
$ cat fileck
if (($# < 1))
then
    print "Usage: $0 file"
    exit 1
fi
FILE=$1

if [[ -f $FILE ]]
then
    print "Copying $FILE to PUBDIR"
    cp $FILE /usr/spool/uucpublic
else
    print "$FILE non-existent"
    exit 2
fi
```

这里是一些示例输出：

```text
$ fileck
Usage: fileck file
$ fileck nofile
nofile non-existent
$ fileck log.out
Copying log.out to PUBDIR
```

注意 `exit 1` 用于用法错误，而 `exit 2` 用于文件不存在错误。在 Korn shell 脚本中（尤其是大型脚本），为不同类型的错误条件使用不同的退出码是一个好习惯。这对于调试很有帮助。

```text
$ fileck; print $?
Usage: fileck file
1
$ fileck nofile; print $?
nofile non-existent
2
$ fileck log.out; print $?
Copying log.out to PUBDIR
0
```

### 其他 `if` 语法：`elif`

这种 `if` 命令的形式用于当条件为真时执行一组命令，当另一个条件为真时执行另一组命令，当所有条件都不满足时执行 `else` 命令。

```sh
if command1
then
  commands
elif command2
then
  commands
...
elif commandn
then
  commands
else
  commands
```

如果 `command1` 返回零退出状态，则执行 `then` 对应的命令；如果 `command2` 返回零退出状态，则执行 `elif` 对应的命令；以此类推，如果所有条件都不满足，则执行 `else` 对应的命令。这种 `if` 命令的形式比示例更容易解释：

```sh
USERS=$(wc -l)
if ((USERS == 1))
then
  print "One user"
elif ((USERS == 2))
then
  print "Two users"
elif ((USERS == 3))
then
  print "Three users"
else
  print "Four or more users"
fi
```

# Korn Shell 用户与编程手册

### `while` 命令

这是另一种循环命令。`while` 命令的语法为：
