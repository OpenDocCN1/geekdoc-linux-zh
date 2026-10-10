
测试命令失败，Bash shell 执行了 if-then 语句的 else 部分。

## 检查空文件

你应该使用 -s 比较运算符来检查文件是否为空，特别是在你不希望删除非空文件的时候。请注意，当 -s 比较成功时，表明文件中包含数据：

```
$ cat is-it-empty.sh
#!/bin/bash
# Check if a file is empty
#
file_name=$HOME/sentinel
echo
echo "Checking if $file_name file is empty..."
echo
#
# Check if file exists and is a file.
#
if [ -f $file_name ]
then
    # File does exist. Check if it is empty.
    #
    if [ -s $file_name ]
    then
        echo "The $file_name file exists and has data in
        it."
        echo "Will not remove this file."
    else
        echo "The $file_name file exists, but is empty."
        echo "Deleting empty file..."
        rm $file_name
    fi
else
    echo "The $file_name file does not exist."
fi
$ ls -sh $HOME/sentinel
4.0K /home/christine/sentinel
$ ../is-it-empty.sh
Checking if /home/christine/sentinel file is empty...
The /home/christine/sentinel file exists and has data in it.
Will not remove this file.
$ 
```

首先，-f 比较测试文件是否存在。如果文件存在，则触发 -s 比较来确定文件是否为空。空文件将被删除。你可以从 `ls -sh` 命令中看到，sentinel 文件并非为空（4.0 K），因此脚本不会删除它。

## 检查是否可写入文件

-w 比较运算符用于确定你是否有权限向某个文件写入数据。can-I-write-to-it.sh 脚本仅仅是 can-I-read-it.sh 脚本的一个更新版本。现在，该脚本不再检查你是否可以读取 item_name 文件，而是检查你是否有权限向文件写入：

```
$ cat can-I-write-to-it.sh
#!/bin/bash
# Check if a file is writable

item_name=$HOME/sentinel
echo
echo "Checking if you can write to $item_name..."
#
# Check if file exists and is a file.
# if [ -f $item_name ]
then
        # File does exist. Check if can write to it.
        # if [ -w $item_name ]
        then
            echo "Writing current time to $item_name"
            date +%H%M> > $item_name
        #
        else
            echo "Sorry, write access to $item_name is denied."
        fi
#
else 
echo "Sorry, the $item_name does not exist"
echo "or is not a file."
fi
$
$ ls -o $HOME/sentinel
-rw-rw-r-- 1 christine 32 May 25 17:08
/home/christine/sentinel
$
$ ./can-I-write-to-it.sh
Checking if you can write to /home/christine/sentinel...
Writing current time to /home/christine/sentinel
$
```

变量 item_name 被设置为 `$HOME/sentinel`，该文件允许用户进行写入访问（有关文件权限的更多信息，请参阅第 7 章“理解 Linux 文件权限”）。因此，当脚本运行时，-w 测试表达式返回非零退出状态，then 代码块被执行，向 sentinel 文件写入了时间戳。

当通过 `chmod` 移除 sentinel 文件的用户写入权限时，-w 测试表达式返回非零状态，且时间戳未写入文件：

```
$ chmod u-w $HOME/sentinel
$
$ ls -o $HOME/sentinel
-r---rw-r-- 1 christine 37 May 29 12:07
/home/christine/sentinel
$
$ ./can-I-write-to-it.sh
Checking if you can write to /home/christine/sentinel...
Sorry, write access to /home/christine/sentinel is denied.
$
```

可以再次使用 `chmod` 命令授予用户的写权限。这将使写测试表达式返回零退出状态，并允许尝试向文件写入。

## 检查是否可运行文件

-x 比较运算符是一种便捷的确定你是否具有特定文件执行权限的方法。虽然大多数命令可能不需要这一点，但如果你从 shell 脚本中运行大量脚本，这可能很有用：

```
$ cat can-I-run-it.sh
#!/bin/bash
# Check if you can run a file
#
item_name=$HOME/scripts/can-I-write-to-it.sh
echo
echo "Checking if you can run $item_name..."
#
# Check if file is executable.
#
if [ -x $item_name ]
then
        echo "You can run $item_name."
        echo "Running $item_name..."
        $item_name
#
else
        echo "Sorry, you cannot run $item_name."
#
fi
$
$ ./can-I-run-it.sh

Checking if you can run /home/christine/scripts/can-I-write-
to-it.sh...You can run /home/christine/scripts/can-I-write-to-it.sh.
Running /home/christine/scripts/can-I-write-to-it.sh... [...] 
$
$ chmod u-x can-I-write-to-it.sh
$
$ ./can-I-run-it.sh

Checking if you can run /home/christine/scripts/can-I-write-
to-it.sh... Sorry, you cannot run /home/christine/scripts/can-I-write-
to-it.sh.
$
```

这个示例 shell 脚本使用 -x 比较运算符来测试你是否具有执行 can-I-write-to-it.sh 脚本的权限。如果是，它将运行该脚本。在第一次成功运行 can-I-write-to-it.sh 脚本后，权限发生了变化。这一次，-x 比较失败，因为 can-I-write-to-it.sh 脚本的执行权限已被移除。

## 检查所有权

-o 比较运算符允许你轻松测试你是否是某个文件的所有者：

```
$ cat do-I-own-it.sh
#!/bin/bash
# Check if you own a file
#
if [ -o /etc/passwd ]
then
    echo "You are the owner of the /etc/passwd file."
#
else
    echo "Sorry, you are NOT /etc/passwd file's owner."
#
fi
$
$ whoami
christine
$
$ ls -o /etc/passwd
-rw-r--- 1 root 2842 Apr 23 15:25 /etc/passwd
$
$ ./do-I-own-it.sh
Sorry, you are NOT /etc/passwd file's owner.
$
```

该脚本使用 -o 比较运算符测试运行该脚本的用户是否是 /etc/passwd 文件的所有者。由于脚本是在除 root 以外的用户账户下运行的，因此测试失败。

## 检查默认组成员资格

-G 比较运算符检查文件的组，如果该组与用户的默认组匹配，则比较成功。这在某些情况下可能会引起混淆，因为 -G 比较运算符仅检查脚本用户的默认组，而不是用户所属的所有组。以下是一个示例：

```
$ cat check_default_group.sh
#!/bin/bash
# Compare file and script user's default groups
#
if [ -G $HOME/TestGroupFile ]
then
    echo "You are in the same default group as"
    echo "the $HOME/TestGroupFile file's group."
#
else
    echo "Sorry, your default group and $HOME/TestGroupFile"
    echo "file's group are different."
#
fi
$
touch $HOME/TestGroupFile
$
ls -g $HOME/TestGroupFile
-rw-rw-r-- 1 christine 0 May 29 13:58
/home/christine/TestGroupFile
$
./check_default_group.sh
You are in the same default group as
the /home/christine/TestGroupFile file's group.
$
groups
christine adm cdrom sudo dip plugdev lpadm inxd sambashare
$
chgrp adm $HOME/TestGroupFile
$
ls -g $HOME/TestGroupFile
-rw-rw-r-- 1 adm 0 May 29 13:58 /home/christine/TestGroupFile
$
./check_default_group.sh
Sorry, your default group and /home/christine/TestGroupFile
file's group are different.
$
```

脚本第一次运行时，$HOME/TestGroupFile 文件属于 christine 组，-G 比较成功。接下来，该文件所属的组被更改为 adm 组，用户也是该组的成员。然而，-G 比较失败了，因为它仅比较用户的默认组，而不考虑任何其他组成员资格。

## 检查文件日期

最后一组比较涉及比较两个文件的创建时间。这在编写用于安装软件的脚本时非常有用。

有时，你不想安装一个比系统上已安装文件更旧的文件。

-nt 比较运算符确定一个文件是否比另一个文件更新。如果文件更新，则其文件创建时间更近。-ot 比较运算符确定一个文件是否比另一个文件更旧。如果文件更旧，则其文件创建时间更早：

```
$ cat check_file_dates.sh
#!/bin/bash
# Compare two file's creation dates/times
#
if [ $HOME/Downloads/games.rpm -nt $HOME/software/games.rpm ]
then
    echo "The $HOME/Downloads/games.rpm file is newer"
    echo "than the $HOME/software/games.rpm file."
#
else
    echo "The $HOME/Downloads/games.rpm file is older"
    echo "than the $HOME/software/games.rpm file."
#
fi
$
$ ./check_file_dates.sh
The /home/christine/Downloads/games.rpm file is newer
than the /home/christine/software/games.rpm file.
$
```

脚本中的这两个比较都没有先检查文件是否存在。这是一个问题。尝试这个测试：

```
$ rm $HOME/Downloads/games.rpm
$
$ ./check_file_dates.sh
The /home/christine/Downloads/games.rpm file is older
than the /home/christine/software/games.rpm file.
$
```

这个小例子表明，如果其中一个文件不存在，-nt 比较将返回错误的信息。务必确保在使用 -nt 或 -ot 比较之前，文件是存在的。

## 考虑复合测试

