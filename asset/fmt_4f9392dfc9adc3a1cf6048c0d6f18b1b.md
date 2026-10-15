
当你对一个目录只有执行权限时，你可以使用 `ls` 来列出目录的所有内容。你不能在不带参数的情况下使用 `ls`。在下面的示例中，Zach 验证了他是以自己的身份登录的。然后他检查了 Max 的 `info` 目录的权限。你可以通过运行带有 `-d`（目录）和 `-l`（长）选项的 `ls` 来查看目录的内容：

```
$ who am i
zach pts/2 Aug 21 10:02
$ ls -1d /home/max/info
------ 2 max pubs 512 2010-08-21 09:31 /home/max/info
$ ls -l /home/max/info: Permission denied
```

`ls` 显示的 `/home/max/info` 所在行左端的 `d` 表示这是一个目录。Max 拥有读、写、执行权限；组组成员没有访问权限；其他用户只有执行权限，由权限右侧的 `x` 指出。Zach 没有该目录的权限，因此 `cat` 返回了错误。

Zach 指定了他想要获取信息的文件名，他不是在读取新信息，而是在搜索特定的信息，这是他在拥有目录访问权限的情况下允许的。他拥有读取权限，所以他使用 `cat` 显示文件没有问题。但他无法显示 `financial`，因为他没有对它的读取权限：

```
$ ls -1 /home/max/info/financial /home/max/info/notes
-rw-r--r-- 1 max pubs 2010-08-21 09:32 /home/max/info/notes
$ cat /home/max/info/financial
This is the file named notes.
financial.
$ cat /home/max/info/financial: Permission denied
```

Max 给其他人提供了他 `info` 目录的读取访问：

```
$ chmod o+r /home/info
```
