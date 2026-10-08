

# 816

# man

.so man*/ 源文件

sourcefile

你必须使用相对于手册页目录树根的路径名来表示引用。

当第二行或后续任何行以 .so 开头时，man 会忽略它；troff(1) 或 nroff(1) 将按通常方式处理该请求。

# 处理 SGML 手册页

通过存在字符串 \!DOCTYPE，可以识别出被标记为 SGML 标记化格式的手册页。如果文件还包含 SHADOW_PAGE，则该文件引用另一个手册页作为内容。引用通过一个文件实体引用指向包含该文本的手册页。这种机制与 nroff 格式的手册页中使用的 .so 机制相似。

# 缺陷 (Bugs)

手册本应该在排字机或 ASCII 终端上是可以复现的。然而，在终端上，某些信息（例如通过字体更改指示）会丢失。

某些终端无法处理由 -ee（见 eqn(1)）预处理标志产生的垂直运动。为了防止在这些终端上出现乱码输出，当你使用 -e 时，请也使用 -t 来隐式调用 col(1)。这种变通方法的缺点是，即使在那些可以显示上标和下标的终端上，也会消除它们。使用 Control-Q 清除被 eqn(1) 输出困扰的终端。

# 环境变量

请见 environ(5) 以获取以下环境变量的描述，这些变量影响 man 以及 LC_CTYPE、LC_MESSAGES 和 LANGPATH 的执行。

- -PATH 一个由冒号分隔的目录列表；每个目录后面都可以跟一个由逗号分隔的节列表。如果设置，其值将覆盖 /usr/share/man 作为默认目录搜索路径，并覆盖 man.cf 作为默认节搜索路径。-M 和 -s 选项反过来会覆盖这些值。

- -P 一个用于交互式将 man 的输出传递到屏幕的程序。如果没有设置，则使用 -s。详见 more(1)。

- -TCAT 显示 troff 手册页的程序名称。

- -TROFF 当你指定 -t 选项时使用的格式化器名称。如果设置，则使用 troff(1)。

# 退出状态

- 0 成功完成。

- 1 发生错误。

# 文件

- /usr/share/man

标准手册页目录树的根。

# man 817

/usr/share/man/man?/*n 未格式化的 nroff 手册条目。

/usr/share/man/sman?/*n 未格式化的 SGML 手册条目。

/usr/share/man/cat?/*n nroff 格式化的手册条目。

/usr/share/man/fmt?/*n troff 格式化的手册条目。

/usr/share/man/windex/*n 目录索引和关键字数据库。

/usr/share/lib/tmacan/*n 标准 -man man 包。

/usr/share/lib/sgml/locale/C/dtd/*n SSGML 文类型定义文件。

/usr/share/lib/sgml/locale/C/solbook/*n SGML 样式表和实体定义目录。

/usr/share/lib/pub/eqnchar/*n eqn 和 neqn 的标准定义。

man.cf
默认的节搜索顺序。

# 属性 (Attributes)

请见 attributes(5) 以获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| Availability | SUMdoc |
| CSI | 已启用 |

> 注意 - man 命令具备 CSI 能力。然而，由 man 命令调用的某些命令，即 troff, eqn, neqn, refer, tbl 和 vgrind，尚未经过验证具备 CSI 能力。由于此，带有 -t 选项的 man 命令可能无法处理非 EUC 数据。此外，如果使用 man 命令显示需要通过 eqn, neqn, refer, tbl 或 vgrind 进行特殊处理的手册页，则可能不具备 CSI 能力。

# 另参 (See Also)

apropos(1), cat(1), col(1), eqn(1), more(1), nroff(1), refer(1), tbl(1),
troff(1), vgrind(1), whatis(1), catman(1), attributes(5), environ(5),
eqnchar(5), man(5), sgml(1)

# mconnect — 连接到 SMTP 邮件服务器套字

# 概要 (Synopsis)

/usr/bin/mconnect [-p port] [-r] [hostname]

# 描述 (Description)

mconnect 打开到指定主机上邮件服务器的连接，以便可以独立于所有其他邮件软件对邮件服务器进行测试。如果没有提供主机，则将连接到本地主机。服务器期望在此连接上使用简单邮件传输协议 (SMTP)。通过输入 quit 命令退出。输入 EOF 会向服务器发送文件结束符。中断将立即关闭连接并退出。

# 选项 (Options)

- -p port: 指定端口号作为下一个参数，而不是使用默认的 SMTP 端口（数字 25）。
- -r: 禁用默认的行缓冲和输入处理，以原始模式运行。此选项产生的效果类似于对端口号 25 运行 telnet 的效果。

# 文件 (Files)

/etc/mail/sendmail.hf

SMTP 命令的帮助文件。

# 属性 (Attributes)

请见 attributes(5) 以获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| Availability | SUNWcs |

# 另参 (See Also)

telnet(1), sendmail(1), attributes(5), IP6(7)
Postel, Jonathan B., Simple Mail Transfer Protocol, RFC 821, Information Sciences.

# mcs — 操作对象文件的注释部分

# 概要 (Synopsis)

```
/usr/bin/mcs [-c | -d | -p | -V | -a | -n] [string]
```

# 描述 (Description)

# 介绍 (Introduction)

mcs 命令是 Solaris 环境中的一种扩展命令，可以使用它对以下内容进行底层调试和编辑：

* 操作系统。
* 系统崩溃转储。
* 用户进程。
* 用户进程转储。
* 对象文件。

关于 mdb 功能的详细描述，请参阅 Solaris 调试指南。关于目标的详细描述，请见第 82 页。

# 选项 (Options)

你必须指定以下一个或多个选项：

- -a 将字符串添加到 文件的注释部分。如果字符串包含空格，请用引号括起来。
- -c 压缩注释部分。
- -d 删除注释部分。
- -n 指定要访问的注释部分名称。
- -p 在标准输出打印内容。
- -v 输出 mcs 版本号。

# 示例 (Examples)

以下示例打印 elf.file 的内容。
castle% mcs -p elf.file

以下示例将 xyz 添加到 elf.file 的注释部分。
castle% mcs -a xyz.file

# 文件 (Files)

/tmp/mcs* 临时文件。

# 属性 (Attributes)

请见 attributes(5) 以获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| Availability | SUNwbtool |

# 另参 (See Also)

ar(1), as(1), ld(1), elf(3), tmpnam(3), a.out(4), ar(4), attributes(5)

# 概要 (Synopsis)

```
/bin/mdb [-fkmwyAFMS] [-o option] [-p pid] [-s distance] [-I path]
[-L path] [-P prompt] [-R root] [-V dis-version]
[object [core] [suffix]]
```

# 描述 (Description)

# 介绍 (Introduction)

mdb 命令是 Solaris 8 环境中的一种扩展命令，可以使用它对以下内容进行底层调试和编辑：

* 操作系统。
* 系统崩溃转储。
* 用户进程。
* 用户进程转储。
* 对象文件。

关于 mdb 功能的详细描述，请参阅 Solaris 调试指南。关于目标的详细描述，请见第 821 页。Solaris 9 版本中对 mdb 的增强在边缘处用“New”图标标记。

调试是分析软件执行和状态以消除缺陷的过程。传统的调试工具提供了一种控制执行的方法，以便在受控环境中重新执行程序。通过调试器，你可以显示程序数据的当前状态或评估源代码中的表达式。

遗憾的是，这些技术通常不适用于调试以下复杂系统：

* 缺陷可能无法复现且程序状态巨大且分布式的操作系统。
* 经过高度优化、删除了调试信息或本身就是底层调试工具的程序。
* 开发者只能访问事后信息的客户情况。

