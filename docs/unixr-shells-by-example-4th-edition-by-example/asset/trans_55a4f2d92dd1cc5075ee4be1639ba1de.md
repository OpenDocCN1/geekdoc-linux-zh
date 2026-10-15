

## EXPLANATION (CONTINUED)

- 3 read 命令如果没有参数，会从用户接受一行输入并将其分配给内置变量 REPLY。
- 4 在 shell 执行变量替换后，print 函数会打印字符串，显示内置 REPLY 变量的值。
- 5 如果 read 命令后面的变量附加了问号（?），问号后的字符串会显示为提示。用户输入存储在变量位置中。

### 12.2.1 read and File Descriptors

系统启动时，会打开三个称为流的文件（stdin、stdout 和 stderr）并分配给文件描述符数组。前三个文件描述符 0、1 和 2 分别用于标准输入、标准输出和标准错误。下一个可用的文件描述符是文件描述符 3。-u 选项允许 read 命令直接从文件描述符读取。

### EXAMPLE 12.6

(The Command Line)

```
1 $ cat filex
Captain Kidd
Scarlett O'Hara
2 $ exec 3< filex    # filex is assigned to file descriptor 3 for reading
3 $ read -u3 name1  # read from filex and store input in variable, name1
4 $ print $name1
Captain Kidd
5 $ read -u3 name2
$ print $name2
Scarlett O'Hara
6 $ exec 3<&-       # close file descriptor 3
7 $ read -u3 line
ksh: read: bad file unit number
```

## EXPLANATION

- 1 filex 的内容被显示。
- 2 exec 命令用于打开文件描述符 3 以从 filex 读取。
- 3 read 命令直接从单元 3（文件描述符 3，filex）读取一行并将该行分配给变量 name1。
- 4 存储在 name1 中的行被打印。
- 5 文件 filex 仍然打开，此 read 命令从文件中读取下一行并将该行存储在变量 name2 中。
- 6 文件描述符 3（单元 3）被关闭。filex 不再打开。
- 7 因为文件描述符 3（filex）已被关闭，read 命令在尝试从该描述符向变量 line 读取输入时失败。

### 12.3 Arithmetic

Korn shell 支持整数和浮点运算，但浮点运算仅在 1988 年之后版本的 Korn shell 中可用。typeset 命令用于分配类型。有关 typeset 命令，请参阅表 12.3。

### Table 12.3 typeset and Arithmetic

| Command | Alias | Meaning |
|---|---|---|
| typeset -i variable | integer variable | variable is only allowed integer assignment |
| typeset -i# |  | # is the base number for the integer |
| On Versions of ksh Newer Than 1988 |  |  |
| typeset -F variable |  | Floating-point number assignment |
| typeset -E variable | float variable | Floating-point number assignment |

### 12.3.1 The Integer Type

变量可以用 typeset -i 命令或其别名 integer 声明为整数。如果尝试分配任何字符串值，ksh 会返回错误。如果分配浮点数，小数点和小数部分将被截断。可以使用 integer 别名代替 typeset -i。数字也可以用不同的进制表示，例如二进制、八进制和十六进制。

### EXAMPLE 12.8

```
1  $ typeset -i num or integer num    # integer is an alias for typeset -i
2  $ num=hello
   /bin/ksh: hello: bad number
3  $ num=5 + 5
   /bin/ksh: +: not found
4  $ num=5+5
   $ echo $num
   10
5  $ num=4*6
   $ echo $num
   24
6  $ num="4" * 6"
   $ echo $num
   24
7  $ num=6.789
   $ echo $num
   6
```

## EXPLANATION

- 1. 使用 -i 选项的 typeset 命令创建整数变量 num。
- 2. 尝试将字符串 hello 分配给整数变量 num 会导致错误。
- 3. 除非使用 (()) 运算符（参见第 662 页的“Arithmetic Operators and the `let` Command”），否则空白必须加引号或删除。
- 4. 删除空白并执行算术运算。
- 5. 执行乘法并将结果分配给 num。
- 6. 对空白加引号以便执行乘法并防止 shell 展开通配符（*）。
- 7. 由于变量被设为整数，数字的小数部分被截断。

### 12.3.2 Using Different Bases

数字可以用十进制（基数 10）、八进制（基数 8）等表示，使用 typeset 命令并使用 -i 选项和基数。

### EXAMPLE 12.9

```
1
$ num=15
2
$ typeset -i2 num   # binary
$ print $num
2#1111
3
$ typeset -i8 num   # octal
$ print $num
8#17
4
$ typeset -i16 num  # hex
$ print $num
16#f
5
$ read number
2#1101
$ print $number
2#1101
6
$ typeset -i number
$ print $number
2#1101
7
$ typeset -i10 number  # decimal
$ print $number
13
8
$ typeset -i8 number   # octal
$ print $number
8#15
```

> 1. 在 1988 年之后版本的 Korn shell 中，可使用大于 36 的基数。

