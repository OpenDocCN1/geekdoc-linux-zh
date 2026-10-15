

| 站点 | 机构及可用信息 |
|---|---|
| ftp.sfu.ca | 旧金山大学。文件：MS-DOS、Mac |
| apotheca.hpl.hp.com | 惠普研究实验室，帕洛阿尔托，加利福尼亚。文件：X11、食谱、cron、map、Modula-3 |
| ftp.sri.com | SRI 国际。文件：提高 Unix 系统安全性的改进 |
| ftp.columbia.edu | 哥伦比亚大学。文件：kermit |

## 表 21.2 一些有趣的 ftp 归档

## 摘要

毫无疑问，sftp 的接口很笨拙。好消息是，大多数人将 Windows 或 Macintosh 系统作为其实际桌面，而这两个系统都有大量优秀的 FTP 和 SFTP 客户端。

大多数现代 FTP 客户端也支持 SFTP，正如我在这一小时开始时所说，除非有令人信服的理由不这样做，否则你真的应该使用安全 FTP 系统进行文件传输。这很明智。

## 工作坊

工作坊总结了你所学到的关键术语，并提出了关于本课主题的一些问题。它还为你提供了下一小时将要学习内容的预览。

## 关键术语

anonymous FTP 该系统响应不需要你在系统上拥有账户的 ftp 查询。广泛用于公共代码存储库和大学文件服务器。

search string 搜索字符串是在搜索中指定的模式。

## 练习

- 1. 使用 telnet 尝试登录表 21.2 中显示的其中一个 FTP 服务器站点。你没有账户，所以在看到 login: 提示后断开连接。
- 2. 使用 ftp 连接到 ftp.columbia.edu 并查看大学为匿名 FTP 用户提供的哪些文件。复制其中一个到你的系统并阅读它，以查看是否正确传输。
- 3. telnet 和 ssh 的主要区别是什么？ftp 和 sftp 呢？哪一个是更好的选择，为什么？

## 下一小时的预览

本课为你提供了互联网基本工具的概览。在下一小时，你将学习如何在你的 Unix 系统上以及互联网上的其他地方搜索特定文件以及如何处理它们。

## 第 22 小时。搜索信息和文件

## 本小时的目标

在本小时，你将学习

- ► 如何使用 `find` 命令及其奇怪的选项
- ► 如何使用 `find` 与 `xargs`
- ► 关于在互联网上处理文件

在 Unix 中寻找你想要的文件，特别是在你想要的时候，是最大的挑战之一。即使是世界上最好的组织方式，具有助记符子目录和仔细命名的文件，也会崩溃，让你对自己说：“我知道它在某个地方，我记得它包含 Acme Acres Construction 的投标以获得那份合同；但无论如何，我就是想不起来它在哪里！”

在本小时，你将学习在 Unix 系统上查找特定信息的复杂方法。功能强大的 `find` 命令及其合作伙伴 `xargs` 是本小时的重点，但你还将学习一些其他非常有用的命令。

## 查找位置

你使用 Unix 越多，就越可能失去对某些文件位置的跟踪。然而，在 Unix 中，有一个很酷的工具可以帮助你再次找到它们。

## 任务 22.1：find 命令及其奇怪的选项

`grep` 系列可以帮助你通过内容查找文件。在 Unix 中还有许多其他查找方法，而这正是 `find` 命令可以提供帮助的地方。此命令的记法与所有其他 Unix 命令完全不同：它使用完整单词的选项而不是单字母标志。例如，使用 `-n pattern` 来匹配文件名时，`find` 使用 `-name pattern`。

此命令的一般格式是指定通过文件系统搜索的起点，然后是所需的任何操作。许多、许多选项中最有用的选项列表显示在表 22.1 中。

| 选项 | 含义 |
|---|---|
| -atime n | 如果文件在 n 天前被访问则为真。 |
| -ctime n | 如果文件在 n 天前被创建则为真。 |
| -exec command | 执行命令。 |
| -mtime n | 如果文件在 n 天前被修改则为真。 |
| -name pattern | 如果文件名与 pattern 匹配则为真。 |
| -print | 打印匹配的文件名。 |
| -type c | 如果文件是类型 c 则为真（如表 22.2 所示）。 |
| -user name | 如果文件由用户 name 拥有则为真。 |

## 表 22.1 find 命令的有用选项

find 命令检查指定的选项，从左到右依次检查，每个遇到文件或目录时检查一次。此外，find 与任何时间相关的命令一起使用时，可以搜索比指定日期更新、更旧或完全相同年龄的文件，分别使用规范 -n、+n 和 n。一些示例将使这一点更清晰。

- 1. 最简单地说，find 可用于创建当前目录下所有文件和目录的列表：

Click here to view code image

```
$ find . -print
.
./OWL
./OWL/owl.h
./OWL/owl
./OWL/owl.c
./OWL/simple.editor.c
./OWL/ask.c
./OWL/simple.editor.o
./OWL/owl.o

lots and lots of output removed

./dead.letter
./who.is.who
./src.listing
./tmp.listing
./wrongwords
./papert.article
```

- 2. 为了将输出限制为仅那些 C 源文件（具有 .c 后缀的文件），我可以在 -print 选项之前使用 -name 选项：

Click here to view code image

```
$ find . -name "*.c" -print
./OWL/owl.c
./OWL/simple.editor.c
./OWL/ask.c
./OWL/handout.c
./OWL/WordMap/msw-to-txt.c
./OWL/WordMap/newtest.c
./OWL/feedback.c
```
