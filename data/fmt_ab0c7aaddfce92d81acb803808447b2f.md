
# arguments are same or different

## Brief Description
Read a line from each file and compare them. If the lines are the same, continue. If they are different, display the two lines and exit. If one of the files finishes before the other, display a message and exit. Otherwise, the files are the same; display an appropriate message and exit

```bash
if [ $# != 2 ]
then
    echo "Usage: $0 file1 file2"
    exit 1
elif [ ! -f "$1" ]
then
    echo "$1 is not an ordinary file"
    exit 1
elif [ ! -f "$2" ]
then
    echo "$2 is not an ordinary file"
    exit 1
else
    :
fi
file1="$1"
file2="$2"

# Open files for reading and assign them file descriptors 3 and 4
exec 3< "$file1"
exec 4< "$file2"

# Read a line each from both files and compare. If both reach EOF,
# then files are the same. Otherwise, they are different. 0<&3 is
# used to attach standard input of the read line1 command to file
# descriptor 3, 0<&4 is used to attach standard input of the read
# line2 command to file descriptor 4.

while read line1 0<&3
do
    if read line2 0<&4
    then
        # if lines are different, the two files are not the same
        if [ "$line1" != "$line2" ]
        then
            echo "$1 and $2 are different."
            echo " $1: $line1"
            echo " $2: $line2"
            exit 1
        fi
    else
        # if EOF for file2 reached, file1 is bigger than file2
        echo "$1 and $2 are different and $1 is bigger than $2."
        exit 1
    fi
done
# if EOF for file1 reached, file2 is bigger than file1. Otherwise,
# the two files are the same. 0<&4 is used to attach standard
# input of read to file descriptor 4
if read line2 0<&4
then
    echo "$1 and $2 are different and $2 is bigger than $1."
    exit 1
else
    echo "$1 and $2 are the same!"
    exit 0
fi
# Close files corresponding to descriptors 3 and 4

exec 3<&-
exec 4<&-
```

![](img/02e070097d401d3bf7de4bf1c470b267_555_0.png)

```bash
$ cat test1
Hello, world!
Not the same!
Another line.
$ cat test2
Hello, world!
$ cat test3
Hello, world!
Not the same!
$ cat test4
This is different file.
Hello, world!
$ ./diff2 file1 file2
Usage: ./diff2 file1 file2
$ ./diff2 test1 test2 test3
Usage: ./diff2 file1 file2
$ ./diff2 test1 test1
test1 and test1 are the same!
$ ./diff2 test1 test3
test1 and test3 are different and test1 is bigger than test3.
$ ./diff2 test1 test2
test1 and test2 are different and test1 is bigger than test2.
$ ./diff2 test2 test3
test2 and test3 are different and test3 is bigger than test2.
$ ./diff2 test1 test4
test1 and test4 are different.
test1: Hello, world!
test4: This is different file.
$
```

`exec` 命令用于打开和关闭文件。`exec 3< "$file1"` 和 `exec 4< "$file2"` 命令打开作为命令行参数传递的文件以供读取，并将它们分配文件描述符 3 和 4。从此时起，你可以使用这些描述符读取两个文件。命令 `read line1 0<&3` 和 `read line2 0<&4` 分别从文件描述符为 3（`file1`）和 4（`file2`）的文件中读取下一行。命令 `exec 3<&-` 和 `exec 4<&-` 关闭两个文件。第一个 `if` 语句 `else` 部分中的冒号符号（`:`）是一个空语句，仅返回 true。你可以使用 Bourne shell 命令 `true` 实现相同目的。顺便说一下，`false` 命令，如人们所期望的那样，返回 false。

在下面的章节练习中，你将使用 `exec` 命令将 shell 的 I/O 重定向到普通文件。Shell 脚本中的 I/O 重定向概念以及使用文件描述符进行文件 I/O 也得到了强化。

## EXERCISE 13.4

编写一个命令，将你的 shell 的 stdin 更改为名为 `data` 的文件，将 stdout 更改为名为 `out` 的文件，两者均在当前工作目录中。如果 `data` 文件包含以下行，执行命令后会发生什么？

```
echo -n "The time now is: "
date
echo -n "The users presently logged on are: "
who
```
