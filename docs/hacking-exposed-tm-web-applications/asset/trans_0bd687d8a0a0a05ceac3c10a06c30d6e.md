
# 附录 B：Web 攻击工具与技术速查

## 325

| SQL 格式字符（续接） | |
| SQL 格式字符 | 描述 |
| :--- | :--- |
| SET | 分配变量。适用于多行 SQL 语句。 |
| % | 通配符，匹配零或多个字符的任意字符串。 |

| 基础 SQL 注入语法 | |
| 查询语法 | 结果 |
| :--- | :--- |
| OR 1=1 | 创建真条件以绕过逻辑检查。 |
| UNION ALL SELECT field FROM table WHERE condition | 如果 'condition' 为真，则从表中检索所有行（例如 1=1）。 |
| INSERT INTO VALUES('neo','trinity') | 可以绕过身份验证。 |

- @@language
- @@microsoftversion
- @@servername
- @@servicename
- @@version

| 用于枚举 SQL Server 的存储过程 |
| 存储过程 | 描述 |
| :--- | :--- |
| sp_columns <table> | 最重要的是返回表的列名。 |
| sp_configure [name] | 返回内部数据库设置。指定特定设置以仅检索该值——例如，sp_configure 'remote query timeout (s)' |
| sp_dboption | 查看（或设置）用户可配置的数据库选项。 |
| sp_depends <object> | 列出与存储过程相关的表。 |

# 破 Web 应用程序

## 用于枚举 SQL Server 的存储过程（续接）

| 存储过程 | 描述 |
| :--- | :--- |
| sp_helpextext <object> | 描述对象。这对于识别可以执行存储过程的区域更有用。它很少成功执行。 |
| sp_helpextextproc | 列出所有扩展存储过程。 |
| sp_spaceused [object] | 不带参数时，返回数据库名、大小和未分配空间。如果指定了对象，它将适当地地描述行和其他信息。 |
| sp_who2 [username] (以及 sp_who) | 显示用户名、连接的主机、用于连接数据库的应用程序、数据库中执行的当前命令以及其他若干信息。这两个过程都接受一个可选的用户名。这是枚举 SQL 数据库用户（而非应用程序用户）的极佳方法。 |

# MS SQL 参数化扩展存储过程

| 扩展存储过程 | 描述 |
| :--- | :--- |
| xp_cmdshell <command> | cmd.exe 的等效物——换句话说，对数据库服务器的完全命令行访问。假设存在 cmd.exe，因此你只需要输入 'dir' 即可获取目录列表。默认当前目录为 %SYSTEMROOT%\System32。 |

# 附录 B：Web 攻击工具与技术速查

| 扩展存储过程 | 描述 |
| :--- | :--- |
| xp_regread <regkey>, <value> xp_reg* | 读取注册表值。还有其他几个与注册表相关的过程。读取值是最用的。 |
| xp_servicecontrol <action>,<service> | 启动或停止 Windows 服务。 |
| xp_terminate_process <PID> | 根据进程 ID 杀死进程。 |

| 扩展存储过程 | 描述 |
| :--- | :--- |
| xp_loginconfig | 显示登录信息，特别是登录模式（混合模式等）和默认登录。 |
| xp_logininfo | 显示当前登录的账户。仅适用于 NTLM 账户。 |
| xp_msver | 列出 SQL 版本和平台信息。 |
| xp_enumdsn | 枚举 ODBC 数据源。 |
| xp_enumgroups | 枚举 Windows 组。 |
| xp_ntsecc_enumdomains | 枚举网络上存在的域。 |

| 系统表对象 | 描述 |
| :--- | :--- |
| syscolumns | 当前数据库的所有列名和存储过程，不仅仅是主数据库。 |

# 破 Web 应用程序

## SQL 系统表对象（续接）

| 系统表对象 | 描述 |
| :--- | :--- |
| sysobjects | 数据库中的每个对象（如存储过程）。 |
| sysusers | 所有可以操作数据库的用户。 |
| sysfiles | 当前数据库及其日志文件的文件名和路径。 |
| systypes | SQL 定义的数据类型或用户定义的新类型。 |

## 默认 SQL 主数据库表

## 用于 Web 的的常用端口

| 端口 | 典型服务 |
| :--- | :--- |
| 21 | 用于文件传输的 FTP |
| 22 | 用于远程管理的安全 Shell (SSH) |
| 23 | 用于远程管理的 Telnet |

# 附录 B：Web 攻击工具与技术速查 329

## 用于 Web 管理的常用端口（续接）

| 端口 | 典型服务 |
| :--- | :--- |
| 80 | 万维网标准端口 |
| 81 | 备用 WWW |
| 88 | 备用 WWW（也是 Kerberos） |
| 443 | 基于 SSL 的 HTTP (https) |
| 900 | IBM Websphere 管理客户端 |
| 2301 | Compaq Insight Manager |
| 2381 | 基于 SSL 的 Compaq Insight Manager |
| 4224 | 微软应用程序中心管理 |
| 7001 | BEA Weblogic 管理 |
| 7002 | 基于 SSL 的 BEA Weblogic 管理 |
| 7070 | 基于 SSL 的 Sun Java Web Server |
| 8000 | 备用 Web 服务器或 Web 缓存 |
| 8001 | 备用 Web 服务器或管理 |
| 8005 | Apache Tomcat |
| 8080 | 备用 Web 服务器、Squid 缓存控制 (cachemgr.cgi) 或 Sun Java Web Server |
| 8100 | Allaire JRUN |
| 88x0 | 8810, 8820, 8830 等通常属于 ATG Dynamo |
| 8888 | 备用 Web 服务器 |
| 9090 | Sun Java Web Server 模块 |
| 10000 | Netscape 界面（默认） |

# 破 Web应用程序

## 潜在有害的 WebDAV 方法

| 方法 | 描述 |
| :--- | :--- |
| MKCOL | “创建集合”，用于在 Web 服务器上创建集合。 |
| POST | WebDAV 用于提交文件的标准 HTTP 方法。 |
| DELETE | 我们需要说这有什么用？ |
| PUT | WebDAV 用于上传内容的标准 HTTP 方法。 |
| MOVE | 如果无法破坏 Web 服务器，黑客可能只会移动内容。 |
| COPY | 是的，它具有覆盖功能。 |

# 常用密码

| 资源 | 链接 |
| :--- | :--- |
| 厂商默认密码（包括 Compaq Insight） | http://www.astalavista.com/library/auditing/lists/defaultpasswords.shtml |

# 客户端分析

| 任务 | 工具/技术 | 资源 |
| :--- | :--- | :--- |
| 跨站脚本测试 | ScreamingCSS | http://www.devitry.com/screamingCSS.html |
| 跨站脚本测试 | 注入 IFRAME | <iframe src="[link-to_executable]"></iframe> |
| 跨站脚本测试 | 注入 META REFRESH | <META HTTP-EQUIV=Refresh CONTENT="1"; URL=http://redirect_to_here.com/> |
| 跨站脚本测试 | 注入脚本元素 | <script>document.cookie="</script><script>alert('Salut!');</script><script src=""></script> |

# 附录 B：Web 攻击工具与技术速查

| 任务 | 工具/技术 | 资源 |
| :--- | :--- | :--- |
| 恶意 URL | 手动 | http://bigbank.com/script.asp&account=123@evilsite.com |
| 在 Windows 中移除 ActiveX 控制 | 手动 | http://support.microsoft.com/search/preview.aspx?scid=kb;en-us;Q15480 |

此页故意留空

# 附录 C

![](img/2c612d28445b774d9266972920f432d_359_0.png)

# 334 破 Web应用程序

libwhisker 库将许多常用的 Perl 整合到一个基于 HTTP 的资源中。我们在第三章提到它的前身 whisker。Libwhisker 的出现是希望创建一个可以让其他人根据各种用途组合脚本的函数库。

# 附录 C

## WHISKER 内部

Libwhisker 的文档限于函数定义，尽管非常有帮助。对于想要深入研究源码的 Perl 黑客来说，代码也很有可读性。尽管如此，我们希望介绍 libwhisker 的某些功能以及一个基于 libwhisker 的自动 SQL 注入测试脚本。

## http_do_request 函数

Libwhisker 的核心是 `http_do_request` 函数。毕竟，它是发送 URL 请求并接收服务器响应的地方。调用该函数很简单。注意，在调用任何使用 `%hin` 哈作为爬取的函数之前，你必须用 `http_init_request` 函数初始化 `%hin` 哈：

```perl
my $hin, $hout;
http_init_request($hin);
http_do_request($hin, $hout);
```

请求函数作用于两个哈：hin 和 hout。它们的命名约定与设置 HTTP 请求的特定变量有关。例如，此哈包含了传递给函数的自定义标头和 URL。表 C-1 列出了 hin 哈的最常见值以及对每个每个值的描述。

如果你指定了参数，`http_do_request` 函数还可以覆盖这些值。例如，以下代码是请求备用 URL 的示例。$hin['whisker']->['uri'] 的值被设置为 "/admin/menu/user.php"：

```perl
LW::http_do_request($hin, $hout, {'uri'=>'/admin/menu/user.php'});
```
