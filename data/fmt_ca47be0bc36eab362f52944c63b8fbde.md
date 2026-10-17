
11. 选择文件中第一个非空字符是 `A` 的行。

    ```bash
    $ egrep '^A' testFile
    A
    AB
    ```

    ```bash
    ABCDEFGHIJKLMNOPQRSTUVWXYZ
    Able was I ere I saw Elba
    $ egrep -n '^A.*' testFile
    1:A
    2:AB
    3:ABC
    4:ABCDEFGHIJKLMNOPQRSTUVWXYZ
    5:Able was I
    ```

    分析：此示例从行首（`^`）开始并查找零或多个空格。这会跳过任何领先空格。如果没有，则什么都不做。表达式中的下一个字符是 `A`，如果不匹配则跳过该行。

12. 选择文件中不以 `A` 到 `G` 开头的行。

    ```bash
    $ egrep -n '[^A-G]' testFile
    6:1A #末尾有一个空格
    7:12AB. #末尾有两个空格
    8:123ABC. #末尾有三个空格
    9:1234ABCD. #末尾有四个空格
    11:DCBA4321
    12:CBA321
    13:BA21
    14:AI
    16:Now is the time,
    18:To come to the aid,
    19:Of their college.
    21:"Quoth the Raven, 'Nevermore'
    24:Madam, I am Adam
    26:UNIX is an operating system.
    27:My favorite operating system is UNIX
    28:UNIX is UNIX
    ```

    分析：在此示例中，我们在 `A` 到 `G` 的范围内使用了补集操作符（`^`）。文件中有二十八行匹配此模式。

13. 查找 `grep` 是否登录了系统。

    ```bash
    $ who | grep 'John'
    ```

## 搜索文件内容

操作系统允许我们根据文件中包含的短语搜索文件。当我们忘记文件名但知道它包含特定的表达式或词组时，这非常有用。虽然 UNIX 没有这种直接的功能，但我们可以使用 `grep` 族来实现。下面的章节演示了这种搜索。

### 搜索特定目录

当我们知道文件所在的目录时，可以简单地使用 `grep`。例如，查找当前目录中至少有一行匹配 `grep` 表达式的文件列表，使用 `-l` 选项。它会打印文件名。

### 在当前目录搜索文本

```bash
$ ls
Raven regexp.dat
$ grep -l 'Raven' *
Raven
```

### 搜索路径下的所有目录

当我们不知道文件所在位置时，必须使用 `find` 命令配合执行命令。`find` 命令执行指定的命令（在本例中为 `grep` 搜索），使用当前目录中的每个文件。它遍历子目录并应用 `grep` 命令，直到所有目录都处理完毕。在节 10.8 中，我们从主目录（`~`）开始。

## 10.8 使用 `find` 和 `grep` 搜索所有目录

```bash
$ find -type f -exec grep "Raven" {} \;
/mnt/staff/gilber/unix10grep/RavenII
/mnt/staff/gilber/unix10grep/TheRaven
/mnt/staff/gilber/unix6filters/TheRaven
/mnt/staff/gilber/unix7comm/TheRaven
/mnt/staff/gilber/unix11sed/TheRaven
/mnt/staff/gilber/unix11sed/readScript
/mnt/staff/gilber/unix11sed/change.sed
/mnt/staff/gilber/unix11sed/raven.txt
/mnt/staff/gilber/unix8vi/TheRaven
/mnt/staff/gilber/unix5lla/TheRaven
/mnt/staff/gilber/unix11/TheRaven
/mnt/staff/gilber/unix3/TheRaven
/mnt/staff/gilber/unix9filters/TheRaven
/mnt/staff/gilber/unix9/TheRavenV1
/mnt/staff/gilber/unix12awk/TheRaven
/mnt/staff/gilber/unix3files/TheRaven
/mnt/staff/gilber/unix3files/TheRavenV1
/mnt/staff/gilber/unix13bourne/TheRaven
/mnt/staff/gilber/unix13bourne/midRaven.scr
