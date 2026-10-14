
```
/home/alberto/test/todo.txt
/home/alberto/file.txt
/home/alberto/file3.txt
/home/alberto/file1.txt
/home/alberto/file2.txt
/home/alberto/afile.txt
find: /tmp/XF86Setup5909: Permission denied
find: /tmp/kfm-cache-0: Permission denied
find: /tmp/kfm-cache-100: Permission denied
find: /tmp/XF86Setup6565: Permission denied
find: /tmp/otherMail: Permission denied
find: /tmp/XF86Setup514: Permission denied
/tmp/file.txt
```

在这个示例中，我想查找 `/home/alberto` 或 `/tmp` 中所有文件名以 `.txt` 结尾的文件。请注意，我用引号将表达式括起来，以避免 shell glob（解释并展开）星号本身。请注意，在结果中，`find` 无法搜索我没有权限的目录。

尽管正则表达式有助于查找匹配项，但它仍然区分大小写；扩展名为 `.TXT` 的文件不会被找到。将 `-name` 选项替换为 `-iname` 可使搜索不区分大小写，因此以 `.txt` 和 `.TXT` 结尾的文件都会被找到：

```
[alberto@digital alberto]$ find /home/alberto /tmp -iname "*.txt" -print
/home/alberto/intro.txt
/home/alberto/Desktop/Trash/intro.txt
/home/alberto/FILE.TXT
/home/alberto/.netscape/cache/0F/cache3603EFAF0010427.txt
/home/alberto/intro2.txt
/home/alberto/kdetools.txt
/home/alberto/Hello World.txt
/home/alberto/test/test.txt
/home/alberto/test/todo.txt
/home/alberto/file.txt
/home/alberto/file3.txt
...
```

`find` 命令提供了多种选项，包括按修改日期和访问日期搜索文件的功能。此外，`find` 还能够使用找到的文件作为命令的参数来执行命令。这是通过 `-exec` 选项完成的。以下是一个示例：

```
[alberto@digital alberto]$ find /home/alberto -iname "*.txt" -exec wc {} \;
     22      329     1896 /home/alberto/intro.txt
     22      329     1896 /home/alberto/Desktop/Trash/intro.txt
      0        0        0 /home/alberto/FILE.TXT
     10       50      785 /home/alberto/.netscape/cache/0F/cache3603EFAF0010427.txt
     44      329     1894 /home/alberto/intro2.txt
    197      330     2403 /home/alberto/kdetools.txt
      1        1        8 /home/alberto/Hello World.txt
      0        0        0 /home/alberto/test/test.txt
      0        0        0 /home/alberto/test/todo.txt
      0        0        0 /home/alberto/file.txt
      0        0        0 /home/alberto/file3.txt
      0        0        0 /home/alberto/file1.txt
      0        0        0 /home/alberto/file2.txt
      0        0        0 /home/alberto/afile.txt
```

请注意，在此示例中，在调用 `wc` 命令之后，有一对大括号 `{}`。这些大括号会被与搜索匹配的文件名替换——然后它就成为 `wc` 命令的参数。还请注意，在末尾有一个分号 `;`。它告诉 `find` `-exec` 选项已完成。为了避免 shell 将分号解释为命令组，分号后面跟着反斜杠 `\`。

Previous Table of Contents Next

## Complete Idiot's Guide to Linux

Publisher: Macmillan Computer Publishing

Author(s): Manuel Ricart

ISBN: 078971826x

Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

## Locating Files: locate

正如你所能看出，查找文件需要很长时间。`find` 命令需要搜索磁盘以查找你指定的文件。如果你是在文件名上进行搜索，有更好的、更快的办法：`locate`。

`locate` 命令通过预先构建所有已知文件名的数据库来获得其速度。不是扫描磁盘来匹配，而是使用复杂的数据库技术来瞬间找到文件——或者接近瞬间。这一特性的缺点是，如果你要搜索的文件是在数据库更新后创建的，数据库中就不会有它的条目，因此 `locate` 就无法找到它。通常这不是问题，因为 `locate` 每天大约在凌晨 5:55 更新其数据库。什么，你的电脑在那个时间没有开机？好吧，你也可以手动运行该命令。

### Building the locate Database: updatedb

要创建 `locate` 数据库，你必须以 root 身份并发出命令 `/usr/bin/updatedb`。该程序运行需要一段时间，但完成后，你就可以开始使用了。

### Finding a File: locate

要搜索文件，只需输入其名称或其部分名称（无通配符），任何与搜索匹配的文件路径都将被打印出来。以下是一个示例：

```
[root@digital alberto]# locate telnet
/mnt/cdrom/col/install/RPMS/netkit-telnet-0.12-1.1386.rpm
/usr/bin/telnet
/usr/include/arpa/telnet.h
/usr/lib/xemacs-19.16/etc/w3/telnet.xbm
/usr/lib/xemacs-19.16/lisp/comint/telnet.elc
/usr/man/man1/telnet.1.gz
/usr/man/man8/in.telnetd.8.gz
/usr/man/man8/telnetd.8.gz
/usr/sbin/in.telnetd
/var/lib/LST/contents/netkit-telnet
/var/lib/LST/installed/netkit-telnet
```

剩下的就是你决定想要哪个文件了！不坏。相同的命令如果使用 `find` 命令可能需要 10 分钟才能完成。

### Finding Files that Contain a Word or Pattern: grep

而 `find` 命令根据文件系统属性（文件名、修改时间等）查找匹配项，`grep` 命令则在文件中搜索模式。例如，如果你想查找包含单词 `command` 的文件，可以这样用 `grep`：

```
[alberto@digital alberto]$ grep command *.txt
intro.txt:Through a command line interface
intro.txt:The UNIX shell is not going away anytime soon. For this reason it is a lso covered in detail. In order for you to gain expertise an facility using Linux you have to be as comfortable in a command line environment as you are in a graphical one.
intro2.txt:Through a command line interface
intro2.txt:using Linux you have to be as comfortable in a command line
```
