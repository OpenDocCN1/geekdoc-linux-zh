
1. 切换到您的 `myscripts` 目录。显示该目录中文件的详细列表。记录您在第 5 章练习中复制的文件的拥有者和权限。记录 `mycal` 和 `mycat` 的权限：

```
$ cd myscripts<Enter>
$ ls -l<Enter>
```

2. 对 `/usr/bin` 目录中原始的 `cal` 和 `cat` 文件执行详细列表，并将权限与 `myscripts` 目录中的权限进行比较：

```
$ ls -l /usr/bin/cat /usr/bin/cal<Enter>
```

3. 更改 `myscripts` 目录中 `mycal` 和 `mycat` 的修改时间。检查时间是否已更改：

```
$ touch mycal mycat<Enter>
$ ls -l<Enter>
```

描述 `touch` 命令的另一种用法。

4. 执行必要的命令，以便您可以在主目录中通过名称 `home_mycal` 来引用 `myscripts` 目录中的 `mycal` 文件。

```
$ ln mycal ../home_mycal<Enter>
$ ls -l mycal<Enter>
$ ls -l /home/tsamx/home_mycal<Enter>
```

或者

```
$ ls -l ../home_mycal<Enter>
```

比较两个文件的详细信息。有区别吗？链接计数是多少？

5. 将目录更改为您的主目录。执行 `home_mycal`：

```
$ cd<Enter>
$ ./home_mycal<Enter>
```

> 注意：由于 Linux 中默认路径的限制，仅输入 `home_mycal` 将无法工作。

输出看起来像什么？现在，更改 `home_mycal` 文件的权限，使得您（该文件的所有者）只有只读权限。尝试运行 `mycal` 命令：

```
$ chmod 455 home_mycal<Enter>
$ ls -l home_mycal<Enter>
$ myscripts/mycal<Enter>
```

你能做到吗？为什么或为什么不？

删除 `home_mycal`：

```
$ rm home_mycal<Enter>
```

这会删除 `myscripts/mycal` 吗？为什么或为什么不？

```
$ ls -l myscripts/mycal<Enter>
```

将目录更改为 `myscripts` 目录。使用符号表示法配合 `chmod` 命令，从 `mycat` 文件中移除其他权限位上的读权限。检查新权限：

```
$ cd myscripts<Enter>
$ chmod o-r mycat<Enter>
$ ls -l mycat<Enter>
```

使用八进制表示法，更改 `mycat` 的权限，使得所有者权限位设置为只读，其他任何人没有权限。检查新权限：

9. 针对 `.bash_profile` 文件执行 `mycat` 命令：

```
$ mycat ../.bash_profile<Enter>
```

或者

```
$ mycat /home/teanxxx/.bash_profile<Enter>
```

成功了吗？发生了什么？

10. 将你的主目录设为当前目录。检查确认你位于主目录：

```
$ cd<Enter>
$ pwd<Enter>
```

11. 修改 `myscripts` 目录的权限，使你对该目录仅拥有只读访问权限：

```
$ chmod u-wx myscripts<Enter>
```

或者

```
$ chmod u=r myscripts<Enter>
```

或者

```
$ chmod 455 myscripts<Enter>
```

12. 使用长列表格式检查你是否正确设置了权限：

```
$ ls -l /home/teanxxx<Enter>
```

或者

```
$ ls -ld myscripts<Enter>
```

13. 尝试获取目录内容的简单列表。再尝试使用长列表：

```
$ ls myscripts<Enter>
$ ls -l myscripts<Enter>
```

成功了吗？为什么成功或失败？

14. 尝试执行 `mycal`：

```
$ myscripts/mycal<Enter>
```

成功了吗？为什么成功或失败？

15. 尝试删除 `mycal`：

```
$ rm myscripts/mycal<Enter>
```

成功了吗？为什么成功或失败？

16. 将 `myscripts` 的权限恢复为其原始形式 `rwxr-xr-x`，然后删除 `mycal`：

```
$ chmod 755 myscripts<Enter>
$ rm myscripts/mycal<Enter>
```

17. 尝试其他权限组合。完成后，务必将所有者权限改回 `rwx`。

参见附录 B 获取答案。

## 测验

> **注意** 问题 1、2 和 3 基于一个名为 `reporta` 的文件，该文件具有以下权限设置：`-rwxr-xr-x`。

- 1. 该文件模式用数字（八进制）表示是什么？

- 2. 使用符号格式将文件模式更改为 `-rwxr--r--`。

- 3. 使用数字（八进制）格式重复问题 2 的操作。

- 4. 假设 `jobs` 目录包含 `joblog` 文件。使用 `ls -lR` 应该可以验证这一点：

```
$ ls -lR<Enter>
total 8
drwxr-xr-x5 perez knights2 4096 Jun 17 08:09 jobs
./jobs:
total 8
-rw-rw-r--1 perez knights2 100 Jun 18 13:22 joblog
```

Nicholas 是 `knights2` 组的成员，他可以修改 `joblog` 文件吗？

- 5. 此问题基于以下列表。假设 `jobs` 目录包含 `work` 目录，而 `work` 目录中又包含 `joblog` 文件：

```
$ ls -lR<Enter>
total 8
drwxr-xr-x5 perez knights2 4096 Jun 17 08:09 jobs
./jobs:
total 8
drwxrwxr-x2 perez knights2 4096 Jul 21 09:41 work
./jobs/work:
total 8
-rw-rw-r--1 perez knights2 100 Jun 18 13:22 joblog
```

Nicholas 是 `knights2` 组的成员，他可以修改 `joblog` 文件吗？

- 6. 此问题基于以下列表。假设 `jobs` 目录包含 `work` 目录（注意 `work` 的权限已更改），而 `work` 目录中又包含 `joblog` 文件：

```
$ ls -lR<Enter>
total 8
drwxr-xr-x 5 perez knights2 4096 Jun 17 08:09 jobs
./jobs:
total 8
drwxrwxrwx    2  perez knights2 4096 Jul 21 09:41 work
./jobs/work:
total 8
-rw-rw-r--    1  perez knights2 100 Jun 18 13:22 joblog
```

Nicholas 是 `knights2` 组的成员，他可以将 `joblog` 文件复制到他的主目录吗？

参见附录 C 获取答案。

# 章节

## Shell 基础

一旦登录到 Linux 系统，你就会接触到 shell——通常指我们在本章中详细讨论的 Bash 变体。Shell 程序是操作系统的一个接口，它将你输入的命令（或来自其他源的输入）转换为操作系统的指令。DOS 的 `command.com` 程序基本上做的是同样的事情。

本章描述了基本 Linux shell 的细节。尽管重点在于 Bash，但我们会介绍 `tcsh` shell 的元素，并包含与某些其他 shell 相关的命令变体。

了解 shell 如何处理你的输入会使你成为更高效、更有效的 Linux 用户和系统管理员。当你看到如何使用通配符、元字符和管道来自定义输入时，你将开始理解它们的力量。

### Linux/UNIX Shells

Shell 只是访问 Linux / UNIX 的接口之一。还有其他接口，如我们将在第 14 章“Linux X 窗口系统”中讨论的 X 窗口系统。请记住，任何 shell 只是一个接口程序，并不是操作系统本身。登录并输入用户名和密码后，操作系统会启动 shell 程序。一方面，如果你使用的是基于命令行的 shell，那么 shell 程序会通过提供命令行提示符来响应你，例如

```
[username@hostname /directory]$
```

或者，如果你是 root 用户，你会看到

```
[root@hostname /root directory]#
```

正如你注意到的，在这本书中，我们将这些提示符分别简写为 `$` 和 `#`。

另一方面，X 窗口系统作为 shell，会向你展示一个 GUI 桌面图像。
