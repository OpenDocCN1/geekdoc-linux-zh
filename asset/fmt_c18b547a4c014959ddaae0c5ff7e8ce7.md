
# 16.13. 解决方案：shell 扩展

# 17. 文件通配 (file globbing)

*   17.1. * 星号
*   17.2. ? 问号
*   17.3. [] 方括号
*   17.4. a-z 和 0-9 范围
*   17.5. `$LANG` 和方括号
*   17.6. 防止文件通配
*   17.7. 练习：shell 通配
*   17.8. 解决方案：shell 通配

# 第 12 章 命令与参数

本章通过仔细观察`命令`和`参数`来向你介绍`shell 扩展`。了解`shell 扩展`非常重要，因为你 Linux 系统上的许多`命令`在执行之前会经过`shell`处理并极有可能被修改。

大多数 Linux 系统使用的命令行界面或`shell`被称为`bash`，它代表`Bourne again shell`（再次的 Bourne 壳）。`bash` shell 结合了来自`sh`（原始的 Bourne shell）、`esh`（C shell）和`ksh`（Korn shell）的特性。

本章经常使用`echo`命令来演示 shell 特性。`echo`命令非常简单：它回显它收到的输入。

```
paul@laika:~$ echo Burtonville
Burtonville
paul@laika:~$ echo Smurfs are blue
Smurfs are blue
```

## 12.1. 参数

shell 的主要功能之一是执行命令行扫描。当你在 shell 的命令提示符处输入命令并按回车键时，shell 将开始扫描该行，将其切割成各个参数。在扫描行的过程中，shell 可能会对你输入的参数进行许多更改。

这个过程被称为 shell 扩展。当 shell 完成对该行的扫描和修改后，它就会被执行。

## 12.2. 空格移除

由一个或多个连续空格（或制表符）分隔的部分被视为独立的参数，任何空格都会被移除。第一个参数是要待执行的命令，任何其他参数都会传递给该命令。shell 实际上是将你的命令切割成一个或多个参数。

这解释了为什么以下四个不同的命令行在 shell 扩展后是相同的。

```
paul@RHELv4u ~$ echo Hello World
Hello World
paul@RHELv4u ~$ echo Hello World
Hello World
paul@RHELv4u ~$ echo Hello
Hello World
paul@RHELv4u ~$ echo Hello World
Hello World
```

`echo`命令将显示它从 shell 接收到的每一个参数。`echo`命令还会在收到的参数之间添加一个新的新空格。

## 12.3. 单引号

你可以通过对空格加引号来防止空格被移除。被引号括的字符串的内容被视为一个参数。在下面的截图中，`echo`接收到

```
[paul@RHEL4b ~]$ echo 'A line with single quotes'
A line with    single quotes
[paul@RHEL4b ~]$
```

## 12.4. 双引号

你也可以通过对空格加双引号来防止空格被移除。与上面相同，`echo`只接收到一个参数。

```
[paul@RHEL4b ~]$ echo \"A line with double quotes"
A line with    double quotes
[paul@RHEL4b ~]$
```

在书的后续部分，当我们讨论变量时，我们将看到单引号和双引号之间的重要区别。

## 12.5. `echo` 与引号

带引号的行可以包含`echo`命令识别的特殊转义字符（当使用`echo -e`时）。下面的截图显示了如何使用`\n`表示换行，以及使用`\t`表示制表符（通常是八个空格）。

```
[paul@RHEL4b ~]$ echo -e \"A line with \n newline"\ line with
a newline
[paul@RHEL4b ~]$ echo -e \"A line with \n newline"\ line with
a newline
[paul@RHEL4b ~]$ echo -e \"A line with \t tab"\ line with
 a tab
[paul@RHEL4b ~]$ echo -e \"A line with \t tab"\ line with
 a tab
[paul@RHEL4b ~]$
```

`echo`命令生成的不仅仅是空格、制表符和换行符。请查看手册页（man page）获取选项列表。

## 12.6. 命令

### 12.6.1. 外部命令还是内置命令？

并不是所有命令都是 shell 外部的，有些是内置的。外部命令是拥有自己的二进制文件并存在于文件系统某处的程序。许多外部命令位于`/bin`或`/sbin`。内置命令是 shell 本身不可或缺的一部分。

### 12.6.2. `type`

要确定给 shell 的命令是作为外部命令执行还是内置命令执行，请使用`type`命令。

```
paul@laika:-$ type cd
cd is a shell builtin
paul@laika:-$ type cd
```

（注：原文文本中存在大量重复和 OCR 错误，此处已根据核心信息进行清理和翻译。）

## 12.9. 练习：命令与参数

*   1. 这一行中有几个参数（不包括命令本身）。
    ```
    touch /etc/cron/cron.allow 'file 42.txt' "file 33.txt"
    ```
*   2. `tac`是 shell 内置命令吗？
*   3. `rm`有别名吗？
*   4. 读取`rm`的帮助页，确保你理解`rm`的`-i`选项。创建并删除一个文件来测试`-i`选项。
*   5. 执行：`alias rm='rm -i'`。用测试文件测试你的别名。这是否按预期工作？
*   6. 列出所有当前别名。
*   7a. 创建一个名为 'city' 的别名，输出你的家乡。
*   7b. 使用你的别名测试它是否工作正常。
*   8. 执行`set -x`显示每个命令的 shell 扩展。
*   9. 通过执行你的`city`和`rm`别名来测试`set -x`的功能。
*   10. 执行`set +x`停止显示 shell 扩展。
*   11. 删除你的`city`别名。
*   12. `cat`和`passwd`命令的位置在哪里？
*   13. 解释以下命令之间的区别：
    ```
    echo
    /bin/echo
    ```
*   14. 解释以下命令之间的区别：
    ```
    echo Hello
    echo -n Hello
    ```
*   15. 显示 A B C，其中 B 和 C 之间有两个空格。
*   (可选) 16. 完成以下命令（不要使用空格）以精确显示以下输出：
    ```
    4+4   =8
    10+14 =24
    ```
*   17. 使用`echo`精确显示以下：
