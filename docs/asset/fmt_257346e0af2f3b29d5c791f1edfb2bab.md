
这会检查 `$var` 的值是否为零并且文件不存在（注意表达式中 `!` 的使用）。

8. `test` 还有第二种形式。不显式调用 `test`，而是可以用方括号包围条件表达式：

```
[ -f file ]
```

这样做使 shell 程序更易读。事实上，你很少会看到 `test` 显式出现，如前所示。

还要注意空格：如果不使用此处所示的空格，特别是方括号与表达式元素之间的空格，shell 会报错。

`test` 命令是 shell 编程中最常用的命令之一。它对于理解接下来的两个 shell 脚本编程任务——条件表达式和循环——至关重要。

## 任务 16.4：条件表达式

有时，在编写程序时，你只想在满足特定条件表达式时执行某个操作。Shell 编程通过 `if` 命令、`case` 命令和两个特殊的命令分隔符为你提供了这种能力。

### 1. `if` 命令

`if` 命令是最常见的条件命令。它的形式如下：

```
if
  conditional-expression
then
  command-block
fi
```

命令块是一条或多条 shell 命令的序列。第一个命令块，即条件表达式，总是被执行。最后执行的语句的返回值用于确定是否执行第二个块。条件表达式最常用的序列是 `test` 命令 in its `[ ]` notation:

```
if
  [ -f $file ]
then
  echo $file is a regular file
fi
```

This `if` statement notifies the user that a file is a regular file. If the file is not a regular file (such as a directory), the condition fails and the shell doesn’t execute the `echo`, with the result that you don’t see an output message.

### 2. `else` 分支

Sometimes, you might want output regardless of the situation. In the preceding case, you might be interested in the status of the file even if it is not a regular file. You can expand the `if` command with the `else` keyword to provide that second option:

```
if
  [ -f $file ]
then
  echo $file is a regular file
else
  echo $file is not a regular file
fi
```

This statement provides output regardless of the status of the file.

### 3. `&&` 与 `||` 简写

For these simple tests and output, the shell provides a second, quicker means of executing the `if` statement. If the two commands are joined by `&&`, the second command is executed if the first command is evaluated as true. If the commands are joined by `||`, the second command is executed if the first is false. The preceding command would, therefore, look like this:

```
[ -f $file ] && echo $file is a regular file
[ -f $file ] || echo $file is not a regular file
```

```
then
    echo $file is a directory
else
    echo $file is not a regular file or a directory.
fi
```

This command first tests to see whether the file is a regular file; if it is not, it checks to see whether it is a directory; if it is neither, it gives the generic “not a regular file or directory” message. You can expand any `if` statement with an unlimited number of `elif` branches.

One nice thing is that you can indent your code to make things easier to understand, and you can also compress the statements themselves with the use of the semicolon, so the preceding listing could be more compactly written as:

```
if [ -f $file ] ; then
    echo $file is a regular file
elif [ -d $file ] ; then
    echo $file is a directory
else
    echo $file is not a regular file or a directory
fi
```

Note that the `then` should appear on a second line, so the semicolon after the expression is necessary. (Many shell programmers leave the `then` on its own line, even though it’s not quite as space efficient.)

## 5. `case` 命令

At some point, `if-then-else` code can become confusing. When you have many possible branches, you should use the `case` command. The syntax is a bit more complicated than the syntax for `if`:

```
case string in
pattern) command-block ;;
pattern) command-block ;;
...
esac
```

If you were looking for possible values for a variable, you could use `case`:

```
echo What do you want:
read var remainder
case $var in
house)   echo The price must be very high;;
car)     echo The price must be high;;
popsicle) echo The price must be low;;
*)       echo I do not know the price;;
esac
```

This `case` statement follows an input request and gives the user a rough idea of the price. A case list can contain any number of items. Note the special `;;` notation, which denotes the end of a case statement.

Here’s another example, a mini file command:

```
case $filename in
