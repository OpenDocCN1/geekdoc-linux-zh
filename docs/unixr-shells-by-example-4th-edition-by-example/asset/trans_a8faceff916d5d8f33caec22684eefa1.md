

## 11.8.4 转义元字符

要将元字符用作字面字符，请使用反斜杠防止元字符被解释。

### Example 11.30

```sh
1  $ ls
abc file1 youx
2  $ print How are you?
How are youx
3  $ print How are you\?
How are you?
4  $ print when does this line \
> ever end\?
when does this line ever end?
```

### Explanation

- 1. 列出当前工作目录中的文件。注意文件 `youx`。
- 2. shell 会对问号执行文件名扩展。当前目录中以 `you` 开头并后跟恰好一个字符的任何文件都会被匹配并替换到字符串中。文件名 `youx` 将被替换到字符串中，读作 `How are youx`（可能不是你想要的结果）。
- 3. 通过在问号 (`?`) 前加上反斜杠，它被转义，这意味着 shell 不会尝试将其解释为通配符。
- 4. 通过在换行符前加上反斜杠，换行符被转义。直到字符串以换行符终止，都会显示二级提示。问号 (`?`) 被转义以防止文件名扩展。

## 11.8.5 波浪号和连字符扩展

波浪号字符由 Korn shell（源自 C shell）采用用于路径名扩展。单独的波浪号求值为用户主目录的完整路径名。当波浪号后附加用户名时，它会扩展为该用户的完整路径名。

连字符字符指的是之前的工作目录；`OLDPWD` 也指的是之前的工作目录。

### Example 11.31

```sh
1  $ echo ~
/home/jody/ellie
2  $ echo ~joe
/home/joe
3  $ echo ~+
/home/jody/ellie/perl
4  $ echo ~-
/home/jody/ellie/prac
5  $ echo $OLDPWD
/home/jody/ellie/prac
6  $ cd -
/home/jody/ellie/prac
```

### Explanation

- 1. 波浪号求值为用户主目录的完整路径名。
- 2. 波浪号后跟用户名求值为 joe 的主目录的完整路径名。
- 3. `~+` 记法求值为工作目录的完整路径名。
- 4. `~-` 记法求值为之前的工作目录。
- 5. `OLDPWD` 变量包含之前的工作目录。
- 6. 连字符指的是之前的工作目录；`cd -` 用于切换到之前的工作目录并显示该目录。

## 11.8.6 新的 ksh 元字符

新的 Korn shell 元字符用于文件名扩展，其方式类似于 grep 和 awk 的正则表达式元字符。放在括号内字符之前的元字符控制模式匹配的内容。请参阅表 11.8。

**Table 11.8 Regular Expression Wildcards**

| Regular Expression | Meaning |
| --- | --- |
| `abc?(2\|9)1` | `?` 匹配括号内模式的零次或一次出现。垂直线表示或条件；例如，2 或 9。匹配 `abc21`、`abc91` 或 `abc1`。 |
| `abc*([0-9])` | `*` 匹配括号内模式的零次或多次出现。匹配后跟零个或多个数字；例如，`abc`、`abc1234`、`abc3` 或 `abc2`。 |
| `abc+([0-9])` | `+` 匹配括号内模式的一次或多次出现。匹配后跟一个或多个数字；例如，`abc3` 或 `abc123`。 |
| `no@(one\|ne)` | `@` 匹配括号内模式的恰好一次出现。匹配 `noone` 或 `none`。 |
| `no!(thing\|where)` | `!` 匹配除括号内任何模式所匹配的字符串之外的所有字符串。匹配 `no`、`nobody` 或 `none`，但不匹配 `nothing` 或 `nowhere`。 |

### Example 11.32

```sh
1  $ ls
abc abc1 abc122 abc123 abc2 file1 file1.bak file2 file2.bak none nonsense nothing nowhere one
2  $ ls abc?(1|2)
abc abc1 abc2
3  $ ls abc*([1-5])
abc abc1 abc122 abc123 abc2
4  $ ls abc+([1-5])
abc1 abc122 abc123 abc2
5  $ ls no@(thing|ne)
none nothing
6  $ ls no!(one|nonsense)
none nothing nowhere
```

### Explanation

- 1. 列出当前工作目录中的所有文件。
- 2. 匹配以 `abc` 开头并后跟零个字符或括号内两种模式之一的文件名。匹配 `abc`、`abc1` 或 `abc2`。
- 3. 匹配以 `abc` 开头并后跟零个或多个 1 到 5 之间的数字的文件名。匹配 `abc`、`abc1`、`abc122`、`abc123` 和 `abc2`。
- 4. 匹配以 `abc` 开头并后跟一个或多个 1 到 5 之间的数字的文件名。匹配 `abc1`、`abc122`、`abc123` 和 `abc2`。
- 5. 匹配以 `no` 开头并后跟恰好 `thing` 或 `ne` 的文件名。匹配 `nothing` 或 `none`。
- 6. 匹配以 `no` 开头并后跟除 `one` 或 `nonsense` 之外的任何内容的文件名。匹配 `none`、`nothing` 和 `nowhere`。

## 11.8.7 The noglob Variable

如果设置了 `noglob` 变量，则关闭文件名替换，这意味着所有元字符都代表自身；它们不作为通配符使用。这在像 grep、sed 或 awk 这样的程序中搜索包含元字符的模式时很有用。如果未设置 `noglob`，则所有不希望被解释的元字符都必须用反斜杠转义。

