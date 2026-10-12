
这会将`i`重置为`10`。执行`print`命令确认变量的值已重新置，然后执行三次`step`命令，最后再执行一次`print`。你会发现，循环迭代一次后，`i`的值增加了一。除了演示了这些步骤，这些步骤还说明了如何单步执行程序。`step`命令每次执行程序一条语句。

## 调试：GNU gdb

### 第 36 章

> **注意**
> 没有必要输入三次 `step`。`gdb` 会记住最后执行的命令，因此你只需按回车键即可重新执行上一个命令，这真的是一个非常省手指的技巧。这适用于大多数 `gdb` 命令。请查阅文档。

### `gdb`'s notion of variable

At any given time, `gdb` considers a variable either active or inactive. There are a few rules that define what constitutes:
- Local variables in any function are active if control has passed to a function.
- Global variables are always active, regardless of whether the program is running.
- Nonglobal variables are inactive unless the program is running.

So much for variable context. What is `gdb`'s notion of context? The complication arises from the use of `static` variables, which are file-scoped; that is, you can have identically named variables in several files, and they will not conflict. Fortunately, `gdb` has a way to identify which variable you are referring to. It resembles C++'s scope operator.

`file_orclassname::variable` is the name of the variable you want to refer to, and `file_orclassname` is the name of the file or function in which it appears. So, for example, given two source files, `foo.c` and `bar.c`, each containing a variable `baz`, that is declared `static`, to refer to the one in `foo.c` you might write the following:

```
(gdb) print foo.c::baz
```

The single quotes around the filename are required so that `gdb` knows you are referring to a filename. Similarly, given two functions, `blat()` and `splat()`, with each variable name `idx`, the following commands would print the addresses of `idx` in each function:

```
(gdb) print &blat::idx
(gdb) print &splat::idx
```

## Advanced `gdb` Concepts and Commands

This section discusses a few complicated and some commands that will make your `gdb` usage more productive and less frustrating. The concepts include traversing the call stack, working with source files, the `command`, and attaching to a process.

### Table 36.1 COMMANDS FOR WORKING WITH FUNCTIONS

| Command | Description |
| --- | --- |
| `call name(args)` | Call the function named with arguments |
| `finish` | Finish the current function and return value to the caller |
| `return` | Stop the function and return a specified value |

```
(gdb) call index_the_moon(intary)
```

Executes the function `index_the_moon` with `intary` as the argument.

如你所见，`gdb` 停止在第 25 行。通过快速的 `print` 命令可以确认它确实停在我们请求的 `i` 的值上：

```
(gdb) print i
$14 = 15
```

如果你在输入 `run` 命令时程序正在运行，`gdb` 会提示程序已经启动，并询问你是否想从头开始重启它。输入 `yes`（是）。

在命中断点后若要继续执行，只需输入 `continue` 即可。如果你设置了许多断点，并且忘记了设置了哪些以及哪些被触发了，可以使用 `info breakpoints` 来刷新记忆。`delete` 命令允许你删除断点，或者你也可以简单地禁用它们。图 36.2 展示了以下命令之一的用法：

```
(gdb) info breakpoints
(gdb) delete 3
(gdb) disable 4
(gdb) info breakpoints
```
