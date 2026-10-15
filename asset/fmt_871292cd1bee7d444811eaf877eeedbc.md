
`CLSPATH` 代码块中的最后一个条件判断如果原始的 `CLSPATH` 存在，则将其添加到新的环境中。`CLSPATH` 被导出，以便运行 Tomcat 的 shell 可以访问它。

## Command Parameters

下一个代码块是嵌套 `if`，用于处理传递 `tomcat.sh` 的命令行参数。如果你查看嵌套的 `else` 子句，你会发现 `tomcat.sh` 接受 `start`、`env`、`run`、`stop`、`ant` 和 `help`。我们将详细介绍 `start` 和 `stop`。正如你所知的，`ant` 是用于编译整个 Tomcat 产品的设施，而 `jsp` 是预编译 Java Pages 的工具。

`if` 块的顶部检查第一个参数是否为 `start`。如果是，Tomcat 会执行一次 `shift`。`shift` 工具获取参数列表并移出第一个。如果你的参数列表是 `1, 2, 3, 4, 5`，`shift` 将把你的参数列表重置为 `2, 3, 4, 5`。移位后，Tomcat 检查第二个参数（实际上是第一个）是否为 `security`。如果是，Tomcat 将移位参数并启动 Tomcat Java 程序，设置带有安全选项的 `JAVACM` 环境变量。如果没有设置 `security` 参数，则不带安全选项启动 Tomcat 应用。

嵌套 `if` 中的下一个子句（`else-if`）检查调用 `tomcat.sh` 的参数值是否为 `stop`。如果是，`tomcat.sh` 将带有结束 Tomcat 的选项启动 Tomcat Java 程序。如果 Tomcat Web 应用程序没有在其他进程中运行，Tomcat Java 程序将带错误结束；或者，Tomcat Web 服务器将关闭。

`tomcat.sh` 的最后一个子句将 `CLSPATH` 重置为原始值，这是 `tomcat.sh` 之前保存在名为 `oldCP` 的环境变量中的值。

## End of Chapter Review

### Key Terms

| case statements | exit codes | script |
| :--- | :--- | :--- |
| commands | for loop | sourcing |
| conditional expressions | parameters | tilde (~) |
| execution | predicates | while loop |

## Review Questions

1. 为什么你可能需要理解如何编写 shell 脚本？
2. 列出四个特殊变量中的两个。
3. 脚本中什么符号开始注释？
4. 解释“sourcing the script”的意思。
5. 定义术 *predicate*（谓词）。

## Programming Assignment

### Exercise 1: 为 tomcat.sh 启动脚本添加描述性注释

根据本章的讨论，为 `tomcat.sh` 脚本提供大量的注释。（你可能想将其复制到工作目录。）

### Exercise 2: 修复 say.sh 以输出参数而不产生脚本错误

1. 使用几种调用脚本的方法测试 `say.sh` 脚本：
   a) 使用点 (. )
   b) 使用 `source` 命令。
   c) 使用 `sh` 命令。

### Exercise 3: 在脚本中寻找循环

为几个脚本提供注释。建议的脚本是 `/etc/rc.d/init.d` 中的几个，如 `httpd` 和 `postgresql`。（你可能想将其复制到工作目录。）

## Index

A
- `<anchor>` 标签, 79
- 绝对地址, 50
- 账户配置, 37-38
- anchor Reader, 70
- Apache web 服务器，以及 138-139
- alias, 182, 187
- 相对 vs 绝对, 50
- Advanced Docs, 68-69
- Advanced Research Projects (API),
- AIX, 7
- Java 中的内存分配, 87
- Alpha, 58
- America Online, 160
- 接地应用, 173-174
- Java 中的和, 94
- Andresen, 73
- Apache Group, 135, 140
- Apache Software License, 11
- Apache web 服务器, 1, 7, 9, 11, 12, 27, 138, 159
- Apache 中的, 138-139
- 代码, 137
- 由支持, 138-139
- 指令中的, 138
- 结束或排序, 139-141
- httppd 守护进程中的, 137-140, 138
- httppd 脚本, 193, 193
- Java servlets 和, 136-137
- JavaScript Pages (JSP) 和, 107-113
- Load, 138-139
- 模块和核心, 136-137, 136
- 多个实例, 139
- nobody 用户中的, 138
- 补丁, 136-137
- 端口号中的, 138
- 使用的进程, 139-140
- 启动, 137-140
- Tomcat 插件, 141-142
- Apple, 58
- Java applets, 74, 87, 88
- 接口 (API), 30
- 软件, 177
- Java 中的应用程序, 88
- Anywhere, 3
- Java 中的算术运算, 93
- ARPANET, 159-160
- Java 中的数组, 194
- ASCII 文本, 在, 167-168
- 表达式中的星号 (*), 193
- at com, 52
- AT&T, 73
- ATT 命令和 Linux 环境, 52

B
- 后台处理, 173-174
- 反斜线 (\), 28
- 备份和恢复策略, 30-33, 154-155
- shell（另见 scripts）, 50, 171-186
- CLSPATH 变量和, 180
- 通用命令, 175
- 中的 dot profile 文件, 180-181, 181
- 环境变量和, 172, 180-181, 182
- 目录和, 172
- 文件重定向, 172, 175-177, 177
- 文件名通配, 172, 181-182
- Unix 中的 Filters, 177, 179-178
- 前台和后台处理, 173-174
- 命令历史，检索和重复, 175
- PATH 变量, 179-180
- 管道使用, 175
- 定义的 shells, for, 172
- 子进程和, 181
- 替换, 172
- 变量和, 179-180
- 补功能, 174
- BASIC, 4
- BEA, 7, 10
- Bell Labs, 3
- Berkeley Systems (BSD), Unix
- Berners-Lee, Tim, 73
- big 命令, 52
- bin 目录, 53
- 二进制文件, 168
- BITNET, 160
- BBOS, 30, 39, 45
- BlackDown, 9, 27, 88
- Java 中的 statements, 91, 92
- `<BODY>`, 103
- Java 中的构造函数, 94
- boot (boot/device), 29, 30, 35, 56
- boot disk 创建, 37-39
- Borland, 16
- Bourne shell, 172
- Bourne, Step, 177
- `<BR>`, 78
- Java 中的括号, 92
- break statement, 192
- 浏览器-配置, Web sites, 76
- 浏览器, 68, 73, 164
- 列表的系统, 160
- Linux 业务, 24-5, 12-13, 21
- 字节码, 88
- Java 中的, 96-97
- CompuServe, 160
- Java 中的连接, 94
- Java 中的 conditional statements, 90-92
- Linux 的配置和启动, 45-62
- boot options, 46
- 启动中的, 49
- 设备驱动和, 46-47
- 指令, 53, 53
- 文本文件, 55
- 错误消息, 46
- init 程序和在 Java, 47-49
- 配置, 146
- 日志输出, 59
- 脚本中的, 149
- 运行 Linux, 50-59
- 签名, 49-50
- DIR 命令和 Linux 等, 52
- Apache web 服务器, 128
- Java Pages (JS) 和, 107-113
- 指令, 51, 52, 53
- cd 命令和 Linux 等, 52
- CD Object, 52
- `<CENTER>`-tag, 79
- CERN, 73
- 图表, 107
- chat, 160
- HTML 格式中的, 82
- CDK 命令和 Linux 等, 52
- chmod 命令, 52
- IP 地址中的, 160-163
- CLASSA, 160
- Tomcat, 198
- client/server, 58
- 时间设置, 37
- cmd 命令, 52
- COBOL, 87
- 数据库中的列, 115
- 执行在, 53
- bash, 173
- shell 脚本和, 188
- 连接, 150
- JDBC 连接类, 123
- Java 中的常量, 95
- 控制中心, Generic, 144-148
- 常量, 102
- Apache Web 服务器核心模块, 126-137
- 成本效益, 58
- cp 命令, 51, 52, 182
- cpu 使用, 16, 25-26
- 崩溃, 152
- 创建 Network Design (CDWNS), 47
- CREATE TABLE, 117
- cron 守护进程, 154
- 启动中的, 49
- cut 命令, 176, 178
- X 和 Windows, 57-58
- 配置, 149-151
- 编辑: 53
- etc/tcp, 23
- Webcam, 160, 151, 151
- disk Administrator (Microsoft Windows), 28
- Root, 30, 36
- 操作系统 (OS), 41, 52, 171-172
- Linux 发行版, 18-22
- 选择, 20
- 原因, 20
- do 循环, 51, 191-192
- Java 中的空, 191-192
- 文档和帮助文件, 39-41, 63-72
- det web mod, 98, 99-104, 122
- 正规用户, 102
- 货币符号 (S) shell 脚本, 187
- 域名服务 (DNS), 1-2, 16, 168
- 域名名, 163
- domino, 12
- potest, 98, 98, 99, 102-104
- dY 命令和 Linux 等, 52
- dos, 41, 52, 171-172
- dot 操作 shells, and, 58
- dot profile 文件, bash shell, 180-181, 181
- dot 循环, 99
- dow, 90
- 下载 Linux 发行版, 118
- JDBC ServerManager 类, 122-123
- HTML 格式中的 drop lists, 83
- drop 命令, 32, 33, 52
- 动态主机配置协议 (DHCP), 37, 46
- 动态网页页, 77
- 守护进程活动列表, 53

## 目录 · 203

- 电可擦除可编程只读存储器 (EEPROM),
- ELSE;
- else 子句
- 电子邮件, 1, 17, 165-168
- 域名系统 (DNS) 及其, 166-173
- 端口, 165
- 红帽 (Red Hat), 166
- Sendmail 的, 166
- 嵌入式软件, 17
- ENDIF,
- ENDL;
- 增强窗口 (Enrichment windows), 58, 146
- 环境变量, 172; 180-181, 181
- shell 脚本以及 188
- `/etc` 配置, 29, 33, 46
- `/etc` 目录, 53, 154, 172
- `/etc/sk` 目录, 53
- 可执行文件, 97
- 退出状态码, shell 脚本, 190-191
- 表达式
- 星号和模式在其中, 193
- 在 Java Server Pages (JSP), 209
- EXTRACT DOC 命令及其 Linux 等效命令, 52
- 分区格式, 36-37
- HTML 表单, 77, 77, 80-83
- 复选框在, 82
- 下拉列表在, 83
- 连字符 (hyphenlink) 在, 84
- HTML 第二部分, 99-102
- 单选按钮在, 83
- 提交按钮在, 83
- 文本字段在, 82
- 基于主机的 Java , 97
- HOWTO 文件, 39-41, 64, 67, 68
- HTTP, 117
- HTML (参见超文本标记语言)
- `<HTML>` 标签, 78, 103
- HTTP (参见超文本传输协议)
- HTTP 服务器 (另参见 Apache Web 服务器版本), 77-99
- Apache Web 服务器的 httpd 守护进程脚本, 137-140, 131, 183, 193
- HttpServer 类, 99
- HttpRequest/HttpResponse 在, 102-104, 103
- HTTPSession 对象, 74
- `<http->` 标签, 79, 78
- 连字符 (hyphenlink), 84
- 超文本标记语言 (HTML) 参见
- 表单, 73, 77, 77, 78, 79, 以及动态内容和, 97
- 表单设计在, 77, 80-83
- 帮助文档在, 67
- 图像在, 80
- HTML 第二部分, 99-102
- 伪 GUI 的用途, 84
- Servlet API 以及, 99
- 标签在, 103
- Web 超文本传输协议 (HTTP) 参见
- Apache Web 服务器 (HTTP, 服务器), 73, 74, 125, 161, 162
- 客户端请求/响应在, 75-
- 动态内容网关在, 77,
- 代码在, 102
- dnget 在, 98, 99-104
- dopost 在, 99, 98-104
- 动态内容和, 76-77
- GET 命令在, 98, 102-104

## F
- 工厂配置及管理, 149-151
- 设施监控, 154
- 硬盘硬性故障, 152
- FAD 用于, 66-67
- Windows 中的快速写入窗口, 143
- FastConfig Apache Web 服务器以及, 137
- FC DOC 命令及其 Linux 等效命令, 52
- find 命令, 30, 52
- 格式化用于, 52
- 格式和 Linux 等效命令, 27,
- 文件操作符, 190
- 文件安全, 9
- 文件重定向, 172, 175, 177
- 文件系统管理, 152
- 文件系统层次结构 (FSH), 31
- 文件传输协议 (FTP), 8, 34, 74, 161, 164-165, 166
- 文件命名, 172, 181
- 过滤器, 177, 178-189
- FIND DOC 命令及其 Linux 等效命令, 52
- 防火墙, 8, 37
- 固件, 16
- FLUSH, 17
- for 循环-for, 90, 91, 191, 192, 198
- format 命令, 52
- 前台解析, 173-174
- 外键, 在数据库中, 116, 118
- *FORM BODY, 80, 104*
- FORMAT DOC 命令及其 Linux 等效命令, 27, 52

## G
- 比尔·盖茨 (Bill Gates), 4-10
- 网关, 162
- dm 命令, 58
- git, 颜色, 55, 57, 56
- 伪 XML (GNU GPL), 11, 18
- Gerster, 12
- GET 命令, 75, 98, 102-104
- gostview 命令, 60-79
- 全局变量在, 102
- 全局 (在 eliminate 之后)
- Gnino, 2, 52, 37, 186-149
- 获取帮助在, 66-67
- GRPC API, 39, 41
- GNU 修改命令, 39
- GNU/Linux, 17
- 图形界面 (GUI) 另参见 Windows, 2, 10, 2, 154
- HTML, 77, 77, 80-83
- 动态内容和, 76-77
- GET 命令在, 98, 102-104

## H
- 宿主机级 Java 应用, 97
- HOWTO 文件, 39-41, 64, 67, 68
- HTTP, 117
- HTML (参见超文本标记语言)
- `<HTML>` 标签, 78, 103
- HTTP (参见超文本传输协议)
- HTTP 服务器 (另参见 Apache Web 服务器版本), 77-99
- Apache Web 服务器的 httpd 守护进程脚本, 137-140, 131, 183, 193
- HttpServer 类, 99
- HttpRequest/HttpResponse 在, 102-104, 103
- HTTPSession 对象, 74
- `<http->` 标签, 79, 78
- 连字符 (hyphenlink), 84
- 超文本标记语言 (HTML) 参见
- 表单, 73, 77, 77, 78, 79, 以及动态内容和, 97
- 表单设计在, 77, 80-83
- 帮助文档在, 67
- 图像在, 80
- HTML 第二部分, 99-102
- 伪 GUI 的用途, 84
- Servlet API 以及, 99
- 标签在, 103
- Web 超文本传输协议 (HTTP) 参见
- Apache Web 服务器 (HTTP, 服务器), 73, 74, 125, 161, 162
- 客户端请求/响应在, 75-
- 动态内容网关在, 77,
- 代码在, 102
- dnget 在, 98, 99-104
- dopost 在, 99, 98-104
- 动态内容和, 76-77
- GET 命令在, 98, 102-104

## 206 · 索引

红帽 (Red Hat)
email 使用, 165-166
错误表 (errata), 页, 27, 41, 155
HTML 文档中的, 67-68
红帽软件包管理器 (RPM), 31, 38-88
数据库中的 refer用完整性, 116-127
正则表达式, 30
在线搜索中的正则性, 56
关系数据库 (RDB), 9, 10, 27, 115-136
备份, 115
内容, 115-116
其中的类型, 117
定义, 118
DELETE FROM, 121, 122, 1224, 126, 129

DROP 命令, 121
异常处理, 129
索引中的, 117-118, 121
INSERT into, 124, 125, 126, 129
INSERT INTO (SELECT ...) (ODBC), 121-124

JDBC 驱动程序和, 123, 125
djoin 在, 116, 128
键中的, 118
开放数据库连接 (ODBC) 和, 121-124

ORDER BY 子句, 121
使用填充, 157
SQL 中的查询, 99-119
查询结果集中的, 186-189
结果集来自, 120

SELECT 语句中的, 118
集合处理, 123
集合命令中的, 117-118
SQL 中的和, 122
UNIQUE 中的, 118
UNIQUE TO, 120, 123, 126

通配符搜索中的, 116
通配符, 91-116
关系运算符中的, 94
行操作, 28, 35, 37, 154
行操作, 9, 37, 49, 90

点符号 ($) 在, 39, 50, 172
数据库中的行, 119
rp 软件包, 47
rpm 命令中的, 49-52
运行在, 48-49
运行 Linux 命令, 50-59

SAMBA
sawfish 窗口管理器, 146
Java Servlets (JSPs) 中的脚本, 110

编辑器中的搜索, 55-56
主题搜索, 65-66
安全套接层 (SSL), 75, 173
套接字类型, 8-9, 37, 134
排序成本在, 49-50

StartOffice, 3
START DOS 命令和 Linux 等效命令, 52
启动 Apache 服务器和, 137-140
启动 Linux, 45-49
start 命令, 64
有状态协议与协议, 74
JDBC 的 Statement 类, 123
Java 中的语句, 89-92

HTTP 请求/响应中的状态码, 75-76
strder 文件, 176
字符串 ID, 176
字符串文件, 176, 178
存储在, 16
Java 中的字符串, 94-95
字符串比较运算符, 189-190, 101
合并中的, 94, 95
结构化查询语言 (SQL)
命令, 50

HTML 表单中的提交按钮, 83
子进程中的, 181
替换, 172
太阳微系统 (Sun Microsystems), 1, 9, 10, 27, 58-83
超级用户, 49-50
支持成本, 7
对 Apache 的支持, 140
Linux 启动, 7-21
Sun Life, 71-72
交换空间, 26, 28, 35, 36
switch 语句中的, 94, 90, 91
sysybase, 10
同步处理 (SMP), 12
系统日志中的, 153-154

Microsoft Windows 系统注册表, 30
系统软件, 16-173

## T

数据库中的表, 115, 116, 120
HTML 中的标签, 78, 80, 103-104
taneannebrook, 3
archive tag, 155

tar 市场, 33
tar 命令, 53, 52, 105, 115

TCP/IP, 5, 7, 8, 148, 160
telnet, 63
text 标签, 12
HTML 字段中的文本, 82
文本, 45
线程处理, 15
time, 7
timestamp, 117
`<title>` 标签, 103
timoli, 17
time 命令, 52

Tomcat Web 服务器, 112
Apache Web 服务器和, 141-142
106, 141-142
Java 变量, 198
SQL 检查, 157
用户目录, 199
shell 脚本, 187
Torvalds, Linux, 1, 3
所有权成本 (TCO), 21
try 块, 129
type 命令, 52

## V
var 目录, 33, 53
WHERE 子句, 119, 120
while 循环, 191-192, 191
通配符, 181-182
filename 通配符, 197
使用搜索, 119
窗口界面, 5
window 58
窗口管理器, 146
Windows (见 Microsoft Windows)

bash shell 和, 179
CLASSPATH 变量, 180
Java, 92, 93, 95, 96, 102, 103
linux 内核, 146
PATH, 179

## U
UDMAX 驱动器, 25, 26
`<url>` 标签
Java 中的一元运算符, 93
不间断电源 (UPS), 152
UNIQUE, 118
Linux 通用状态, 12-123
加州大学伯克利分校, 32, 176
赫尔辛基大学, 3, 58
Unix 和 Linux, 11-13, 171
unit 循环, 191-192
ub分区, 121, 125
vi 编辑器, 52, 53, 176
29, 176, 178
视频, 146
虚拟控制台, 74
虚拟桌面, 148
虚拟内存, 28
虚拟计算 (VNC), 148
虚拟数据库, 106, 120
Visual Age for Java, 115
WIN 命令和 Linux 等效命令, 52
单词补全, 174
Workplace Office, 3
Workplace Shell, 52
世界维网 (WWW), 160
wristwatch, 185

UPDATE SQL 中的, 120-121
更新和补丁, 27, 41, 155
URL, 75
user /t 目录, 33, 53
Linux 用户支持, 140
用户界面, 119
用户名, 55-56
用户配置, 49-50
用户设计, 31
用户目录, 31, 53, 155
usr/bin, 53
usr/lib, 53
usr/sbin, 53
工具, 49-50

## W
Web 应用服务器, 141-142
Web 托管, 77
Web 服务器, 106
WebSphere, 10
网站用于, 65-66
当, 91
WIN 命令和 Linux 等效命令, 52
zip 命令, 52
