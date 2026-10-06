

## 第二部分 Shell 脚本基础

```
fi
$ ./test16
The first attempt failed
The second attempt succeeded
$ cat $HOME/test16
The program ran at: 20070930-1620
$
```

这是一个相当复杂的 Shell 脚本！首先，它在你的 HOME 目录下定义了一个日志文件，将该文件名存储在变量 `logfile` 中，创建该文件，然后使用 `chmod` 命令删除了用户的写入权限。接着，它使用 `date` 命令创建变量 `now` 并存储一个时间戳。在完成所有这些操作后，它检查你对该日志文件是否有写入权限（你刚刚删除了该权限）。由于你没有写入权限，你应该会看到失败信息出现。

之后，脚本再次使用 `chmod` 命令为用户授予回写入权限，并尝试运行该文件。这次脚本执行成功了。

## 检查你是否可以运行文件

-x 比较是一种判断你是否拥有特定脚本权限的方便方法。虽然对于大多数命令来说可能不需要，但如果你在 Shell 脚本中运行很多脚本，它就会派上用场：

```bash
$ cat test17
#!/bin/bash
# testing file execution
if [ -x test16 ]
then
  echo "You can run the script"
  ./test16
else
  echo "Sorry, you are unable to execute the script"
fi
$ ./test17
You can run the script:
The first attempt failed
The second attempt succeeded
$ chmod u-x test16
$ ./test17
Sorry, you are unable to execute the script
$
```

这个 Shell 脚本使用 -x 比较来测试你是否拥有执行 test16 脚本的权限。如果是，它就会运行该脚本（注意，即使在 Shell 脚本中，执行不在你 PATH 中的脚本也必须提供其路径）。在第一次成功运行 test16 脚本后，更改它的权限并再次尝试。这次 -x 比较失败了，因为你没有对 test16 脚本的执行权限。

## 检查所有权

-u 比较允许你轻松地测试自己是否为文件的所有者：

```bash
$ cat test18
#!/bin/bash
# check file ownership

if [ -u /etc/passwd ]
then
    echo "You're the owner of the /etc/passwd file"
else
    echo "Sorry, you're not the owner of the /etc/passwd file"
fi
$ ./test18
Sorry, you're not the owner of the /etc/passwd file
$ su
Password:
# ./test18
You're the owner of the /etc/passwd file
#
```

脚本使用 -u 比较来测试运行脚本的用户是否为 /etc/passwd 文件的所有者。脚本第一次在普通用户账户下运行时，因此测试失败了。第二次，我使用了 `su` 命令变成 root 用户，测试成功了。

-G 比较检查文件的默认组，如果它与用户默认组的匹配，则比较成功。这可能会让人有些困惑，因为 -G 比较只检查默认组，而不检查用户所属的所有组。以下是这里的示例：

```bash
$ cat test19
#!/bin/bash
# check file group ownership

if [ -G $HOME/testing ]
then
    echo "You're in the same group as the file"
else
    echo "The file is not owned by your group"
fi
$ ls -l $HOME/testing
-rw-rw-r-- 1 rich 58 2007-09-30 15:51 /home/testing
$ ./test19
You're in the same group as the file
$ chgrp sharing $HOME/testing
$ ./test19
The file is not owned by your group
$
```

## 第二部分 Shell 脚本基础

脚本第一次运行时，$HOME/testing 文件属于 rich 组，-G 比较成功。接着，我将组更改为 sharing 组，我也是该组的成员。然而，-G 比较失败了，因为它只比较默认组，而不是我所属的其他组。

## 检查文件日期

最后一组比较处理两个文件的创建时间。这在编写安装软件的脚本时非常有用。有时你不想安装一个比系统中已安装的文件还要旧的文件。

-nt 比较判断一个文件是否比另一个文件新。如果一个文件较新，它将有更新创建时间。-ot 比较判断一个文件是否比另一个文件旧。如果文件较旧，它将有更早的创建时间：

```bash
$ cat test20
#!/bin/bash
# testing file dates

if [ ./test19 -nt ./test18 ]
then
    echo "The test19 file is newer than test18"
else
    echo "The test18 file is newer than test19"
fi

if [ ./test17 -ot ./test19 ]
then
    echo "The test17 file is older than the test19 file"
fi
$ ./test20
The test19 file is newer than test18
The test17 file is older than the test19 file
$ ls -l test17 test17
```

