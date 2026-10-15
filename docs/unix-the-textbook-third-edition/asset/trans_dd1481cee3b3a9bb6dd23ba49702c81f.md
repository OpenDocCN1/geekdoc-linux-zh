

```
exit 1
else
    directory="$1"    # If one command line argument and it is a
                        # directory, prepare to perform the task
fi
# Get file count in the given directory; for empty directory,
# display a
# message and quit.
file_count=`ls $directory | wc -w`  # Get count of files in the
                                    # directory
if [ $file_count -eq 0 ]            # If no files, display error
                                    # message
then
    echo "$directory: Empty directory."
    exit 0
fi
# For each file in the directory specified, add the file size
# to the running total. The more command is used to output file
# names one per line so can read command can be used to read
# file names.
sum=0 # Running sum initialized to 0.
ls "$directory" | more |
while read file
do
    file="$directory"/"$file"  # Store the relative path name for
                                  # each file
    if [ -f "$file" ]            # If it is an ordinary file
    then # then
        set -- `ls -l "$file"`  # Set command line arguments
        sum=`expr $sum + $5`      # Add file size to the running
                                  # total.
    fi
# Code to decrement the file_count variable and display the
# final sum if the last file has been processed.
if [ "$file_count" -gt 1 ] # Are more files left? If so,
                            # continue.
then
    file_count=`expr $file_count - 1`
else
# Spell out the current directory
if [ "$directory" = "." ]
then
    directory="your current directory"
fi
echo "The size of all ordinary files in $directory is $sum bytes."
```
```
fi
done
exit 0
$ 
$ pwd
/home/sarwar/unix3e/ch13
$ ./fs /bin
Usage: ./fs [directory name]
$ ./fs unix3e
unix3e: File does not exist
$ ./fs ~/unix3e
The size of all ordinary files in /home/sarwar/unix3e is 0 bytes.
$ ./fs ..
The size of all ordinary files in .. is 0 bytes.
$ ./fs .
The size of all ordinary files in your current directory is 4716 bytes.
$ ./fs /
The size of all ordinary files in / is 10238 bytes.
$ ./fs /bin
The size of all ordinary files in /bin is 1635367 bytes.
$ ./fs dir1
dir1: Empty directory.
$
```

## EXERCISE 13.1

创建 `addall` 脚本到你的目录中，并用斐波那契数列的前 10 个数字运行它。结果是什么？程序是否产生正确的结果？如果你不熟悉斐波那契数列，请浏览以下网站：http://en.wikipedia.org/wiki/Fibonacci_number。

## 13.3 THE HERE DOCUMENT

Bourne shell 的 here document 功能允许你将脚本中命令的标准输入重定向，并将其附加到脚本内的数据中，以特定格式包装，如下所述。显然，此功能适用于从标准输入获取输入的命令。该功能主要用于显示菜单，尽管此功能还有一些其他重要用途。维护数据在脚本内部的优点是消除了如果数据保存在单独文件中所需额外的文件操作，如打开和读取。结果是程序运行速度更快。以下是 here document 的简要说明。

### SYNTAX

```
command << [-] input_marker
... input data ...
input_marker
```

目的：使用 here document 中的数据作为输入来执行命令——数据位于输入开始和结束标记 input_marker 之间

input_marker 是你选择用来为 command 包装输入数据的字符串。结束标记必须单独占一行，并且不能被任何空格包围。命令和变量替换在 here document 数据被定向到命令的 stdin 之前执行。可以使用引号来防止这些替换或在 here document 中包含任何引号。input_marker 可以用引号括起来以防止整个文档中的任何替换，如：

```
command << 'Marker'
...
'Marker'
```

在 `<<` 后使用连字符 `-` 可以删除 here document 中各行以及结束 here document 的标记的开头制表符（不是空格）。此功能允许 here document 和分隔标记符合脚本的缩进。以下会话说明了这一点：

```
while [ ... ] do
grep ... <<- DIRECTORY
    John Doe ...
    ...
    Art Pohn ... DIRECTORY
...
done
```

最后一点，但非常重要：使用 here document 的命令的输出和错误重定向必须在命令行中指定，而不是在结束 here document 的标记之后。同样，将命令的标准输出通过管道与其他命令连接也是如此，如以下会话所示。请注意，`grep ... <<- DIRECTORY 2> errorfile | sort` 命令可以被 `(grep ... 2> errorfile | sort) <<- DIRECTORY` 替换。

```
while [ ... ] do
    grep ... <<- DIRECTORY 2> errorfile | sort John Doe ...
```
