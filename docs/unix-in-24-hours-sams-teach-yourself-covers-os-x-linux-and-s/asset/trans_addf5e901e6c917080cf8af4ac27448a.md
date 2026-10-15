
+   /
+   /.nfs4
+   /var
+   /var/info
+   /var/inf/usr_share_info_dir.backlink
+   /var/info/usr_share_info_dir
+   /var/db
+   /var/db/ipf
+   /var/sadm
+   /var/sadm/pkg

该文件包含多少行？

点击此处查看代码图片

```
$ wc -l ~/.locate.db
173251 /export/home/taylor/.locate.db
```

你的结果实际上可能还要大得多。

## 3. 数据库构建完成后，创建一个使用 grep 实现轻松搜索文件的脚本，同样很简单：

点击此处查看代码图片

```
#!/bin/sh

# locate - search the locate database for the specified pattern

locatedb="$HOME/.locate.db"

if [ $# -eq 0 ] ; then
    echo "Usage: locate pattern"
    exit 0
fi

exec grep -i "$@" $locatedb
```

就是这么简单。条件语句会检查传给脚本的参数个数，以确保用户指定了模式；`$#` 就是参数个数本身。不过，最后一行需要稍作解释。Shell 脚本是在登录 shell 的副本中运行的。（嗯，严格来说，它们是在第一行指定的 shell 中运行的，因此才有特殊的 `#!` 表示法。）这意味着 shell 脚本会消耗内存、需要自己的进程等等。如果脚本调用某个程序，该程序也会单独运行，因此如果 shell 脚本调用 grep，就会有三个进程在运行：登录 shell、脚本的子 shell 和 grep 本身。

为简化一点，特殊的 `exec` 命令不是添加子进程，而是用指定的命令替换当前子 shell。基本上，它节省了一个进程，但 shell 脚本在遇到该 `exec` 后就会立即结束，因为运行它的 shell 已被指定的命令替换。

特殊符号 `$@` 会将传给脚本的所有参数一并转交给 grep 命令。

## 4. 解释得够多了。来运行几次我们的新脚本吧！首先，有多少个 C 源文件？第一次尝试可能会直接用 `.c` 作为模式，但那会是个错误。你之前应该还记得，grep 使用正则表达式，而 `.c` 会匹配任意字符后跟一个 c，并且出现在行中任意位置：

```
$ ./mylocate ".c" | wc -l
134933
```

第一个技巧是转义句点，这样它就不会被视为正则表达式标记。要做到这一点，只需在句点字符前加上反斜杠：

```
$ ./mylocate "\.c" | wc -l
3245
```

好多了！但它仍会匹配类似 sample.css 的文件，因为其中嵌入了 `.c` 模式。要强制模式只匹配行尾，请添加 `$` 正则表达式标记：

点击此处查看代码图片

```
$ ./mylocate "\.c$" | wc -l
144
```

这就说得通了！现在再确认一下它是否如你所想：

点击此处查看代码图片

```
$ ./mylocate "\.c$" | head -5
/usr/demo/net-snmp/demo_module_8/melLoadGroup.c
/usr/demo/net-snmp/demo_module_8/demo_module_8.c
/usr/demo/net-snmp/demo_module_2/demo_module_2.c
/usr/demo/net-snmp/demo_module_5/demo_module_5.c
/usr/demo/net-snmp/demo_module_1/demo_module_1.c
```

## 5. 要让这成为你整体环境的一部分，还有一步：把它添加到 PATH 中，这样你就可以直接输入命令名称而不必费周折。最好的长期解决方案是在你的主目录中创建一个新的 bin 目录，然后将其用作你创建的新脚本和命令的仓库：

```
$ cd
$ mkdir bin
```

现在将你的脚本移入这个新目录，并将它们标记为可执行：

```
$ cd bin
$ chmod +x *
```

然后修改你的 PATH，让 shell 知道要在这个新目录中查找命令。这可以在命令行中完成。不过，如果你把它追加到 `.profile` 文件中，就会永久生效，而不是只持续到你注销：

点击此处查看代码图片

```
$ echo 'export PATH="$PATH:$HOME/bin"' >> ~/.profile
```

就是这样。现在你只需输入命令名称（也就是你的 shell 脚本的确切名称），它们就会像 `ls` 列出文件、`ssh` 安全连接到另一台 Unix 服务器那样被运行。

这第一个脚本演示了许多有用的 shell 脚本编程技术，包括充分利用 Unix 提供的所有能力。同样重要的是，你现在知道了如何向 PATH 添加新目录，以及如何将 shell 脚本变成新命令。
