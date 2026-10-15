
`nawk -F:` `/'"$oldname/"'{ $1="$newname"; print $0}' datafile`

```
- 4. 数一下单引号的数量。如果单引号的数量为偶数，则每个引号都有匹配的引号。如果不是，则你遗漏了一步。
- 5. 用双引号将每个 shell 变量括起来。双引号紧紧地包围 shell 变量。
```

`nawk -F:` `/'"$oldname"/ { $1=""$newname""; print $0}' datafile`

## here 文档的问题。

here 文档主要用于在 shell 脚本中创建菜单，通常是错误来源。问题通常出在结束 here 文档的用户定义终止符上。终止符周围不能有空格。所有 shell 都严格遵守此规则，尽管 Bourne、 Bash 和 Korn shell 在某些条件下允许使用制表符。参见以下示例。

### EXAMPLE 15.11

```
#! /bin/ksh

print "Do you want to see the menu?"

read answer

if [[ $answer = y ]]

then

1 cat << EOF    <-- No space after user-defined terminator

1) Steak and eggs

2) Fruit and yogurt

3) Pie and icecream

2 EOF    <-- User-defined terminator cannot have spaces surrounding it

print "Pick one "

read choice

case "$choice" in

1) print "Cholesterol"

;;

2) print "Dieter"

;;

3) print "Sweet tooth"

;;

esac

else

print "Later alligator!"

fi
```

(Output)

file: line 6: here document 'EOF' unclosed

or

file: line 6: syntax error: unexpected end of file (bash)

### EXPLANATION

1 这是 here 文档的开始。`cat` 命令后跟 `<<` 和一个用户定义的终止符，在本例中为 `EOF`。终止符之后的行被用作 `cat` 命令的输入，在屏幕上生成一个选项菜单。当在第 2 行遇到终止符时，输入停止。

### EXPLANATION (CONTINUED)

2 第 2 行的结束符必须与第 1 行的完全一致，否则 here 文档将无法结束。此外，最终的结束符不能被任何空格包围。善意的程序员试图缩进脚本以提高可读性，但在这种情况下对第 2 行的 `EOF` 进行缩进会导致语法错误。解决方法是将终止的 `EOF` 移到最左边的边距，并确保其周围没有空格。`bash`/`ksh`/`sh` shell 允许另一种修复方法，即在 `<<` 符号后加上一个连字符：`cat << -EOF`。这允许你使用制表符（仅限制表符）来缩进第 2 行的最终结束符。

## File-Testing Errors.

如果脚本中使用外部文件，最好在使用它们之前检查文件的某些属性，例如它们是否存在、可读或可写、是否有数据、是否为符号链接等等。各种 shell 的文件测试非常相似，但文件存在性测试有所不同。例如，C、TC 和 Bash shell 使用 `-e` 开关来检查文件是否存在，Korn shell 使用 `-a` 开关，而 Bourne shell 使用 `-f` 开关。TC shell 除外，文件测试开关不能绑定在一起，例如 `-rw` 表示可读和可写。相反，单个文件测试开关位于文件名之前。C shell 对可读、可写和可执行文件的测试示例为 `if (-r filename && -w filename && -x filename)`。TC shell 测试的示例为 `if (-rwx filename)`。

## Checking for File Existence in the Five Shells

在脚本中执行文件测试之前生成了以下错误消息。名为 `db` 的文件不存在。

> `grep: db: cannot open [No such file or directory]`

以下示例演示了如何为每种五种 shell 修复此问题。

### EXAMPLE 15.12

```
(csh/tcsh)

set filedb = db

if ( ! -e $filedb ) then

 echo "$filedb does not exist"

 exit 1

endif
```

```
(sh)

filedb=db

if [ ! -f $filedb ]

then

 echo "$filedb does not exist"

 exit 1

fi
```

### EXAMPLE 15.12 (CONTINUED)

```
(ksh)

filedb=db

if [[ ! -a $filedb ]]

then

  print "$filedb does not exist"

  exit 1

fi
```

```
(bash)

filedb=db

if [[ ! -e $filedb ]]

then

echo "$filedb does not exist"

exit 1

fi
```
