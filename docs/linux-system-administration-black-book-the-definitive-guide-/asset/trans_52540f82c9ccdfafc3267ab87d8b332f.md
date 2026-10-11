

## 13. Apache Web 服务器

17. 将光标向下移动至以 **allow** 开头的行。
18. 如果你当前不在插入模式（Insert mode）中，请输入 “i”。
19. 将 *.your_domain.com* 更改为你自己的 *.domain.extension*。保留前面的点。
20. 如果你愿意，可以更改该部分的其他任何内容。小心不要让外部人员获取有关你 Web 服务器的任何信息。这些信息可能会对你不利。
21. 将光标向下移动到下一个部分，该部分以这一行开头：

```
Alias /doc /usr/doc
```

22. 如果你不需要通过中央 Web 服务器提供对 Linux 文档的访问权限，请注释掉此部分，使其看起来如下所示：

```
#Alias /doc /usr/doc
#<Directory /usr/doc>
#order deny,allow
#deny from all
#allow from localhost
#Options Indexes FollowSymlinks
#</Directory>
```

23. 如果你想保留此部分，请决定是否需要对其进行更改，然后实施这些更改。
24. 现在，向下移动到以这一行开头的部分：

```
#<Location /cgi-bin/php*>
```

25. 如果你认为有人试图入侵你的机器或 Web 服务器，或者你出于好奇想看看他们是否正在尝试这样做，请取消注释此部分，使其看起来像这样：

```
<Location /cgi-bin/php>
deny from all
ErrorDocument 403 http://phf.apache.org/phf_abuse_log.cgi
</Location>
```

26. 添加你可能需要添加的其他任何部分。
27. 按 Esc 键，然后输入 “ZZ” 以保存并关闭文件。

### 配置 httpd

为了进行初始访问配置，请执行以下操作：

1. 登录到你要用作 Web 服务器的机器，并拥有 root 权限。
2. 输入 `/etc/httpd/conf/httpd.conf`。
3. 输入 `/ServerType` 并按 Enter 键，跳转到以下行：

```
ServerType standalone
```

4. 如果你有特定原因要通过超级守护进程（superdaemon）运行此 Web 服务器，则输入 `i` 进入插入模式，然后将该行更改为：

```
ServerType inetd
```

5. 将光标向下移动到以下内容：

```
Port 80
```

6. 如果你将 **ServerType** 设置为 **inetd**，请通过在其前面添加井号来注释掉此行。
7. 如果你有原因将此服务器运行在非标准端口上，请仔细选择一个新的端口号，并将 `80` 更改为新值。查看 */etc/services* 以获取哪些进程使用哪些端口的列表。
8. 将光标向下移动到以下行：

```
HostNameLookups off
```

9. 如果你想要记录访问你机器的主机的名称信息，请输入 `i` 进入插入模式（如果你尚不在该模式下），并将该行更改为：

```
HostNameLookups on
```

10. 如果你想要记录访问你机器的主机的名称信息，并且在安全性上更加谨慎，请输入 `i` 进入插入模式（如果你尚不在该模式下），并将该行更改为：

```
HostNameLookups double
```

11. 将光标向下移动到以下行：

```
ServerAdmin root@localhost
```

12. 如果你尚不在插入模式中，请输入 `i`，并将 **root@localhost** 更改为你想要用作服务器管理员的联系电子邮件地址。
    人们通常会创建一个邮件别名，类似于 webadmin。
13. 现在，向下移动到这一行：

```
ServerRoot /etc/httpd
```

只有当你计划将 /etc/httpd 的全部内容移动到其他位置时，才更改此值。

14. 使用光标向下移动到：

```
#BindAddress *
```

15. 如果你打算设置虚拟主机，请考虑取消注释此行的注释。
16. 将光标向下移动到：

```
ErrorLog logs/error_log
```

17. 如果你不想将错误日志保存到 $ServerRoot/logs/error_log，请更改此行以反映日志应存放的位置。
18. 向下移动到以下行：

```
LogLevel warn
```

19. 如果你想使用不同的日志级别，请将 **warn** 更改为第 9 章中描述的级别之一。
20. 将光标向下移动到 **LoadModule** 语句开始的部分。
21. 浏览主列表。如果你想移除你不打算使用的功能，请参阅 **www.apache.org/docs/mod/** 作为起点。你还可以将此作为研究区域，用于决定取消注释哪些被注释掉的模块。
22. 确保你所需的所有 Apache 功能都在这里都有体现。如果没有，找到你需要的模块，并在 **LoadModules** 部分的末尾按照以下格式添加语句：

```
#Additional modules I needed to add.
LoadModule module_name directory/library_file.so
```

23. 向下移动到 **AddModule** 命令列表。
24. 如果你取消注释了 **LoadModule** 部分中的任何模块，或者注释掉了任何模块，请确保对模块对应的 **AddModule** 项做相同的操作。
25. 如果你已经在 **LoadModule** 列表末尾添加了模块，请调查它们在层级中需要在何处激活，并按以下格式添加相应的行：

```
AddModule module_name.c
```

26. 参见即将出现的“定制你的日志”章节，了解如何调整你的日志文件。如果你想要对站点访问进行大量的统计分析，这是一个好主意。
27. 向下移动到：

```
#LockFile /var/lock/httpd.lock
```

28. 如果 ServerRoot 位于另一台机器上通过 NFS 挂载的分区中，请取消注释此行的注释。你的锁文件必须位于本地文件系统中。
29. 继续向下移动到：

```
#ServerName new.host.name
```

30. 如果你的 Web 服务器的主机名未设置为 **www**，你很可能希望取消注释此行的注释并将其更改为：

```
ServerName www.domain.extension
```

**注意：** 你还需要为你在此处设置的名字设置名称解析。

31. 分析如表 13.1 和 13.2 中所述的时间和相关进程项目，以确保它们符合你的实际情况。如果不符合，请适当更改。

**提示：** 这两种指令类型都有合理的默认值。通常，除非你将来注意到负载问题或响应时间问题，否则最好不要调整它们。如果这种情况发生，请查看与进程相关的值。

32. 将光标向下移动到：

```
#ProxyRequests On
```

33. 如果你正在使用代理防火墙，请取消注释此行的注释。否则，你不需要激活此服务。
34. 确定你是否希望使用*缓存*——它保存从其他服务器请求的 Web 页面副本——以加快用户的加载时间。如果是，请取消注释以下每个语句的注释，并调整其设置以适合你的需求：

```
#CacheRoot /var/cache/httpd
#CacheSize 5
#CacheGcInterval 4
#CacheMaxExpire 24
#CacheLastModifiedFactor 0.1
#CacheDefaultExpire 1
#NoCache a_domain.com another_domain.edu joes.garage_sale.com
```

35. 如果你想设置虚拟 Web 托管，请转到下一节“设置虚拟 Web 服务”。
36. 按 Esc 键，然后输入 “ZZ” 以保存并关闭文件。

| 相关解决方案： | 所在页码： |
| :--- | :--- |
| 分析日志 | 281 |
| 设置代理防火墙 | 289 |

### 设置虚拟 Web 服务

要在你的 Apache 服务器上设置虚拟 Web 托管，请执行以下操作：

1. 登录到你要用作 Web 服务器的机器，并拥有 root 权限（如有必要）。
2. 输入 `/etc/httpd/conf/httpd.conf` 以打开文件（如有必要）。
3. 输入 `/VirtualHost` 以跳转到文件的虚拟托管部分。
4. 使用光标向下移动到以下部分：

```
#<VirtualHost host.some_domain.com>
#ServerAdmin webmaster@host.some_domain.com
#DocumentRoot /www/docs/host.some_domain.com
#ServerName host.some_domain.com
#ErrorLog logs/host.some_domain.com-error_log
#TransferLog logs/host.some_domain.com-access_log
#</VirtualHost>
```

5. 将光标向下移动到该部分最后一行的下方。
6. 输入 "o" 在当前位置下方的插入模式中新建一行。
7. 确保在注释部分的结尾和你将添加内容的位置之间有一个空行。
8. 你需要做的第一件事是为 localhost 添加一个条目。此条目以以下内容开头：

```
<VirtualHost 127.0.0.1>
```

9. 接下来，设置人们如需联系 Web 管理员时可写入的电子邮件账户，这可能类似于以下内容：

```
ServerAdmin you@animals.org
```

10. 每个 Web 服务器都应拥有自己的根目录。按以下方式设置：

```
DocumentRoot /home/httpd/html/animals.org
```

11. 现在，你需要定义此虚拟主机指的是什么。对于 localhost，将其指向你想使用的默认 Web 服务。这可能意味着类似于以下内容：

```
ServerName www.animals.org
```

12. 设置此虚拟服务器要使用的传输和错误日志，并关闭语句。你可能会使用：

```
#ErrorLog logs/animals.org-error_log
#TransferLog logs/animals.org-access_log
```

13. 现在，进入实际工作。为此虚拟主机创建一个 `<Directory>` 指令。在基本层面上，以下内容可能是合适的：

```
<Directory /home/httpd/html/animals.org>
Options ExecCGI Indexes Includes
</Directory>
```

请记住，如果需要，你可以使 `<VirtualHost>` 指令像主 /etc/httpd.conf 文件一样复杂。

14. 最后，用以下内容关闭语句：

```
</VirtualHost>
```

