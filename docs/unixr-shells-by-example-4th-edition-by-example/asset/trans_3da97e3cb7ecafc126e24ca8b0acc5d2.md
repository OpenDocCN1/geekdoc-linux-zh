

# 表 9.5 重定向元字符（续）

| 元字符 | 含义 |
|---|---|
| command >>! file | 覆盖 noclobber 变量；如果文件不存在，则创建该文件并将命令的输出追加到其中。 |
| command >>&! file | 覆盖 noclobber 变量；如果文件不存在，则创建该文件并将输出和错误都追加到其中。 |

## 9.9.1 重定向输入

输入不再来自终端键盘，而是可以从文件重定向。shell 会打开 < 符号右侧的文件，左侧的程序将从该文件读取。如果文件不存在，C shell 会报告错误 No such file or directory。

### FORMAT

```
command < file
```

### EXAMPLE 9.36

```
mail bob < memo
```

### EXPLANATION

文件 memo 由 shell 打开，输入被重定向到 mail 程序。简单地说，mail 程序通过该文件向用户 bob 发送名为 memo 的文件。

## 9.9.2 here document

here document 是将输入重定向到命令的另一种方式。它常用于 shell 脚本中创建菜单和处理来自其他程序的输入。通常，接受键盘输入的程序会用 Ctrl-D (^D) 终止。here document 提供了一种在不输入 ^D 的情况下向程序发送输入并终止输入的替代方法。<< 符号后面跟着一个用户定义的词，通常称为终止符。输入将被定向到 << 符号左侧的命令，直到达到用户定义的终止符。最终的终止符单独占一行，且不能被任何空格包围。here document 中会执行变量和命令替换。 （通常，here document 用于 shell 脚本中创建菜单并为 mail、bc、ex、ftp 等命令提供输入。）

### FORMAT

```
command << MARK
MARK ... input ...
```

### EXAMPLE 9.37

(Without the here document)
(The Command Line)

```
1 % cat
2 Hello There.
How are you?
I'm tired of this.
3 ^D
```

(The Output)

```
4 Hello There.
How are you?
I'm tired of this.
```

### EXPLANATION

- 1. 没有参数的 cat 程序等待键盘输入。
- 2. 用户在键盘上输入内容。
- 3. 用户输入 ^D 以终止向 cat 程序的输入。
- 4. cat 程序将输出发送到屏幕。

### EXAMPLE 9.38

(With the here document)
(The Command Line)

```
1 % cat << DONE
2 Hello There.
How are you?
I'm tired of this.
3 DONE
```

(The Output)

```
4 Hello There.
How are you?
I'm tired of this.
```

### EXPLANATION

- 1. cat 程序将从第一个 DONE 接收输入，直到终止符 DONE。 这些词是用户定义的终止符。
- 2. 这些行是输入。当达到单词 DONE 时，不再接受输入。

### EXPLANATION (CONTINUED)

3 最终的终止符标记输入的结束。此单词两侧不能有任何空格。

4 第一个单词 DONE 与最终单词 DONE 之间的文本是 cat 命令的输出（从“这里”到“这里”），并被发送到屏幕。最终的 DONE 必须靠在左边界，没有空格或其他文本在其右侧。

### EXAMPLE 9.30

(The Command Line)

```
1 % set name = steve
2 % mail $name << EOF
3 Hello there, $name
4 The hour is now `date +%H`
5 EOF
```

### EXPLANATION

1 shell 变量 name 被赋值为用户名 steve。 （通常，此示例会包含在 shell 脚本中。）

2 变量 name 在 here document 中被展开。

3 mail 程序将接收输入，直到达到终止符 EOF。

4 here document 中执行命令替换；即，反引号内的命令被执行，命令的输出在字符串中被替换。

5 达到终止符 EOF，输入到 mail 程序停止。

## 9.9.3 重定向输出

默认情况下，命令或命令的标准输出会发送到终端屏幕。要将标准输出从屏幕重定向到文件，使用 > 符号。命令位于 > 符号的左侧，文件名位于右侧。shell 会打开 > 符号右侧的文件。如果文件不存在，shell 将创建它；如果文件存在，shell 将打开文件并截断它。使用重定向时文件经常会被意外删除。 （可以设置一个特殊的 C/TC shell 变量，称为 noclobber，以防止重定向覆盖现有文件。参见第 439 页的表 9.6。）

### FORMAT

```
command > file
```

