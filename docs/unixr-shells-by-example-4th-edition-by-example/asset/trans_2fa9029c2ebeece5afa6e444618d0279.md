

## 13.9.4 大括号展开

花括号匹配逗号分隔的字符串列表中的任意一项。通常这些字符串是文件名。左花括号之前的任何字符称为前导（preamble），右花括号之后的任何字符称为后缀（postamble）。前导和后缀都是可选的。花括号内不能有未加引号的空白字符。

### 示例 13.44

```text
1 $ ls
 a.c b.c abc ab3 ab4 ab5 file1 file2 file3 file4 file5 foo
 faa fumble
2 $ ls f{oo,aa,umble}
 foo faa fumble
3 $ ls a{[.c],b[3-5]}
 a.c ab3 ab4 ab5
4 $ mkdir /usr/local/src/{old,new,dist,bugs}
5 $ chown root /usr/ucb/{ex,edit} /usr/lib/{ex?.??s,how_ex}
6 $ echo fo{jo, um}:
 fo{jo, um}:
7 $ echo {mam,pap,ba}a
 mama papa baa
8 $ echo post{script,office,ure}
 postscript postoffice posture
```

### 说明

- 1 列出当前目录中的所有文件。

- 2 列出以 f 开头且后面跟着字符串 oo、aa 或 umble 的文件。花括号内的空格会导致错误消息 `Missing }`。

- 3 列出以 a 开头且后面跟着 .c、c，或 b3、b4、b5 的文件。（方括号可以在花括号内部使用。）

- 4 将在 /usr/local/src 中创建四个新目录：old、new、dist 和 bugs。

- 5 将 /usr/ucb 目录下的文件 ex 和 edit 以及 /usr/lib 目录下名为 ex 后跟一个字符、一个点以及至少一个字符的文件和名为 how_ex 的文件的所有者改为 root。

- 6 如果花括号内有任何未加引号的空格，将不会进行大括号展开。

- 7 大括号展开不一定会导致文件名的扩展。在此示例中，后缀 a 被添加到花括号内的每个字符串之后，并在展开后回显输出。

- 8 前导是字符串 post，后跟花括号内包含的逗号分隔列表。执行大括号展开后，显示生成的字符串。

## 13.9.5 转义元字符

要将元字符用作字面量字符，请使用反斜杠来防止元字符被解释。

### 示例 13.45

```text
1  $ ls
   abc file1 youx
2  $ echo How are you?
   How are youx
3  $ echo How are you\?
   How are you?
4  $ echo When does this line \
   > ever end\?
   when does this line ever end?
```

### 说明

- 1 列出当前工作目录中的文件。（注意文件 youx。）

- 2 shell 会对 `?` 执行文件名扩展。当前目录中任何以 y-o-u 开头且后面恰好跟一个字符的文件会被匹配并替换到字符串中。文件名 youx 将被替换到字符串中，结果显示为 `How are youx`（这可能不是你想要的结果）。

- 3 通过在问号前加反斜杠，问号被转义，这意味着 shell 不会尝试将其解释为通配符。

- 4 换行符通过在其前面加反斜杠来转义。次提示符会一直显示，直到字符串以换行符终止。问号（`?`）被转义以保护它免受文件名扩展的影响。

## 13.9.6 波浪号与连字符展开

bash shell（从 C shell 引入）采用波浪号进行路径名扩展。单独的波浪号计算为用户主目录的完整路径名。当波浪号后跟用户名时，它会扩展为该用户的完整主目录路径。

当加号跟在波浪号后面时，PWD（当前工作目录）的值替换波浪号。波浪号后跟连字符会被替换为上一个工作目录；OLDPWD 也指上一个工作目录。

如果用双引号或单引号将波浪号括起来，波浪号将不会被扩展。

### 示例 13.46

```text
1 $ echo ~
/home/jody/ellie
2 $ echo ~joe
/home/joe
3 $ echo ~+
/home/jody/ellie/perl
4 $ echo ~-
/home/jody/ellie/prac
5 $ echo $OLDPWD
/home/jody/ellie/prac
6 $ cd -
/home/jody/ellie/prac
```

### 说明

- 1 波浪号计算为用户主目录的完整路径名。

- 2 用户名前的波浪号计算为 joe 的主目录的完整路径名。

- 3 `~+` 记法计算为工作目录的完整路径名。

- 4 `~-` 记法计算为上一个工作目录。

- 5 OLDPWD 变量包含上一个工作目录。

- 6 连字符指上一个工作目录；`cd -` 会进入上一个工作目录并显示该目录。

## 13.9.7 控制通配符（Globbing）

如果设置了 bash 的 noglob 变量，或者给 set 命令加上 `-f` 选项，文件名替换（称为 globbing）将被关闭，这意味着所有元字符都表示它们本身；它们不会被用作通配符。这在用 grep、sed 或 awk 等程序搜索包含元字符的模式时很有用。如果未设置 globbing，则所有元字符都必须用反斜杠转义以关闭通配符解释。

内置的 shopt 命令（bash 版本 2.x）也支持控制 globbing 的选项。

### 示例 13.47

```text
1 $ set noglob or set -f
2 $ print * ?? [] ~ $LOGNAME
* ?? [] /home/jody/ellie ellie
3 $ unset noglob or set +f
4 $ shopt -s dotglob # Only available in bash versions 2.x
5 $ echo *bash*
.bash_history .bash_logout .bash_profile .bashrc bashnote bashtest
```

