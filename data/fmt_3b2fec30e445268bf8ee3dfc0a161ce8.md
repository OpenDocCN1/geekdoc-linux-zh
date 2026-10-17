
类似地，在`sendmail`确定邮件具有本地目的地之后，它必须知道该邮件要发送到哪里。下一条目确定这一点。“who”参考指的是主机。如果主要邮件服务器不是处理本地邮件的那一个，你需要填写处理该邮件的主机名。

```
# who gets all local email traffic ($R has precedence for unqualified names)
DH
```

在此之后，你有另一个键控数据库。这次是一个去引号数据库。去引号指的是移除之前应用程序需要添加以处理元字符和其他特殊文本的引号。去引号数据库用于防止垃圾邮件。

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_396_0.png)

```
# dequoting map
Kdequote dequote
```

接下来是一组确定`sendmail`如何将发件人姓名和位置写入你的邮件头的类选项。选项是`CE`、`CL`和`CM`。`CE`和`CL`在以下列表的注释文本中进行了描述。然而，`M`类描述引用了变量`$M`，其中包含有关你想使用何种伪装（masquerading）信息的数据。如你所见，默认情况下使用类`E`。这确保了如果每台机器都有特定的管理员——或者机器被分组并由单个管理员负责每组——打算发给该机器超级用户的邮件会直接发往该处。

> **提示：** 使用类`E`允许你设置一个自动转发，将你管理的每台机器的邮件发送到你选择的某个中心位置。这使你能够保持头部信息完整，以免对邮件来自哪台机器产生混淆，同时免去你每天在所有机器上以`root`身份登录的麻烦。

```
# class E: names that should be exposed as from this host,
# even if we masquerade
# class L: names that should be delivered locally, even if we have a relay
# class M: domains that should be converted to $M
#CL root
CE root
```

`CM`列出了在你控制下哪些域名应该转换为单一域名用于邮件目的，而`DM`指定了用于伪装的实际域名。通常，这个术语指的是你的`domain.extension`，伪装是为了使你的所有邮件看起来都来自该域名本身，而不是来自单独的机器。

```
# who I masquerade as (null for no masquerading) (see also $=M)
DM
```

小写宏通常不是用户定义的。`n`宏定义命令指的是打印错误消息时使用的守护进程名称：

```
# my name for error messages
DnMAILER-DAEMON
```

在此之后，类`P`以值`REDIRECT`创建。该术语通常用于创建针对旧用户账户的弹回消息，这些账户包含指向其新电子邮件地址的指针。

```
CPREDIRECT
```

最后，`/etc/sendmail.cf`本地信息部分的最后一项是：

```
# Configuration version number
DZ8.9.3
```

这一行简单地创建了一个名为`Z`的宏，其内容为`8.9.3`。

当然，`/etc/sendmail.cf`的内容远不止于此。如果您打算进行大范围更改，我建议您直接去编辑宏文件，而不要编辑此文件。但是，如果您只需要做一些微小的改动，请参见“即时解决方案”部分中的“微调您的 `/etc/sendmail.cf`”。

> **提示**：`sendmail`自身的文档在（Red Hat 中）位于`/usr/doc/sendmail/doc/op.ps`。这是一个 PostScript 格式的文件。在图形界面中，输入`gv /usr/doc/sendmail/doc/op.ps`即可在 GhostView PostScript 查看器中阅读此文件。

## 邮件列表

电子邮件服务中的一项实用功能是邮件列表，这是一个完全通过电子邮件运行的在线讨论论坛——尽管它可能有其他服务的接口，如 Web 浏览器。当某人向邮件列表发布消息时，该帖子会重新分发给列表上的每个人，通常在发件人字段中显示该消息来自列表本身。

在这里，区分邮件列表和垃圾邮件很重要。垃圾邮件通常是不需要的垃圾邮件。邮件列表由选择加入的人组成。偶尔，其他人可能会出于恶意或玩笑将某人添加到列表中，但作为一般规则，列表中的人希望留在其中。或者，至少在项目团队或其他小组中，他们是必须留在那里的。

Linux 用户可以获取各种邮件列表程序。表 12.8 列出了一些流行的程序。

> **注意**：`Ezmlm`列表服务器需要`qmail`服务器，可从`www.qmail.org`获取。`Smartlist`服务器需要`procmail`。

表 12.8 流行的 Linux 邮件列表软件。

| 软件 | 主页 |
| --- | --- |
| Ezmlm | www.ezmlm.org |
| Listserv | www.lsoft.com |
| Majordomo | www.greatcircle.com/majordomo |
| Smartlist | www.procmail.org |

## 即时解决方案

### 安装所有组件

如果您刚刚安装了系统，或者从未认真坐下来配置过`sendmail`，请执行以下操作：

1. 以`root`身份登录到希望作为您的邮件服务器的机器。
2. 将 Red Hat CD-ROM 放入 CD-ROM 驱动器。
3. 输入`mount /mnt/cdrom`将其挂载到您的文件系统上。
4. 输入`cd /mnt/cdrom/RedHat/RPMS`进入软件包目录。
5. 输入`rpm -q sendmail`查看是否已安装邮件服务器。
6. 如果未安装邮件服务器，输入`rpm -ivh sendmail-8*`并按`Tab`键补全文件名，然后按`Enter`键安装软件包。
7. 输入`rpm -ivh sendmail-cf*`并按`Tab`键补全文件名，然后按`Enter`键安装软件包。

> **注意**：其他发行版有其自身的方法来处理组成完整`sendmail` + IDA 工具的辅助组件。本章各处提供了一些提示，以帮助您找到需要处理的文件。

### 在命令行上配置您的 sendmail 服务器

要从命令行从头开始配置`sendmail`服务器，请执行以下操作：

1. 以`root`身份登录到希望作为您的邮件服务器的机器。
2. 输入`cd /usr/lib/sendmail-cf/`进入包含需要编辑的宏文件的目录。

> **注意**：在某些发行版中，会提供一个`/etc/sendmail.mc`文件供您开始使用。请查找该文件，或尝试使用搜索工具查找以`.mc`结尾的文件。此外，请查阅您的发行版文档，了解您的特定发行版关于设置`sendmail`的说明。本节中的说明通常适用于大多数宏配置文件。

3. 输入`cp redhat.mc redhat-original.mc`以保存默认宏配置文件的原始副本。
4. 输入`vi redhat.mc`打开默认宏配置文件。
5. 该文件的第一行是：

```
divert(-1)
```

但是，它没有关闭`divert`语句。将光标移动到减号上。

6. 输入`xx`删除`-1`。
7. 输入`i`进入插入模式。
8. 输入`0`将`divert`语句更改为关闭语句，以便文件中的所有文本都不被忽略。
9. 按`Esc`键返回命令模式。
10. 输入`/REBUILD`并按`Enter`键跳转至可能想要编辑的`define`宏语句部分。
11. 使用本章前面提供的表 12.6 作为指南，更改其中任何必要的项目。
12. 同样，更改下方`FEATURE`部分中的任何项目。
13. 按`Esc`键确保处于命令模式。
14. 输入`G`跳转到文件末尾。
15. 将光标移动到行的开头：

```
FEATURE('accept_unresolvable_domains')
```

16. 输入`i`进入插入模式。
17. 输入`dnl`以防止使用此功能。除非关闭它会导致部分用户遇到问题，否则应避免使用它。
18. 按`Esc`键，然后输入`ZZ`保存并关闭文件。
19. 如果您选择的功能或宏需要创建特定文件，请转到相应部分。例如，“构建 `CW` 文件”、“构建 `Mailer` 表”、“构建虚拟寻址表”和/或“构建访问数据库”。
20. 重复步骤 19，直到构建完所有必要的文件。
21. 转到“保护您免受垃圾邮件”部分，然后返回步骤 22。
22. 转到“在命令行上构建 `sendmail.cf`”部分。

### 在命令行上构建 sendmail.cf

要创建您的主要`sendmail`配置文件，请执行以下操作：
