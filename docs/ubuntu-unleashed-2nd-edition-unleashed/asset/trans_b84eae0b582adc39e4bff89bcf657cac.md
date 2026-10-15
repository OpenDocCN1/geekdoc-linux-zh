

## 注意

不要在显示横幅中使用你的真实电子邮件地址；你希望其他人能够在必要时访问用户电子邮件。相反，使用一个别名地址，将消息路由到适当的 IT 部门或其他地址。

## 通知用户最后修改日期

readme 行告诉服务器是否应在特定文件最后修改时向用户显示通知。以下是命令：

```
readme <path> {<when {<class>}}
```

path 参数是用户的任何有效路径。可选的 when 参数与消息行中看到的完全相同。class 可以是一个或多个在 class 文件中定义的类型。对于真实用户，path 是绝对路径。对于匿名用户，path 相对于匿名主目录，默认为 /var/ftp。

## 配置系统日志

系统管理的一部分涉及查看日志文件，了解服务器正在做什么，谁访问了它，传输了哪些文件以及其他重要信息。你可以在 /etc/ftpaccess 中使用多条命令来控制 FTP 服务器的日志记录操作。

### 重定向日志记录

此行允许管理员重定向 FTP 服务器日志信息将被记录的位置：

```
log <syslog> {+<xferlog>}
```

默认情况下，命令的信息存储在 /var/log/messages 中，尽管某些软件包中的 man 手册说明此信息将写入 /var/log/xferlog。检查服务器的设置以了解文件传输日志的位置信息。

### 记录所有用户发出的命令

此行启用对用户发出所有命令的日志记录：

```
log commands {<typelist>}
```

typelist 是 anonymous、guest 和 real 的以逗号分隔的列表。如果未给出 typelist，则为所有用户记录命令。某些 wu-ftpd 软件包将所有文件传输的日志记录设置为 /var/log/xferlog（见下一节）。然而，你可以向 ftpaccess 添加 log 命令并使用 commands 关键字来捕获用户操作。日志记录将被打开，用户操作将被捕获在 /var/log/messages 中。以下是示例日志文件：

```
Oct  6 12:21:42 shuttle2 ftpd[5229]: USER anonymous
Oct  6 12:21:51 shuttle2 ftpd[5229]: PASS phudson@widget.com
Oct  6 12:21:51 shuttle2 ftpd[5229]: ANONYMOUS FTP LOGIN FROM 192.168.2.31
  [192.168.2.31], phudson@widget.com
Oct  6 12:21:51 shuttle2 ftpd[5229]: SYST
Oct  6 12:21:54 shuttle2 ftpd[5229]: CWD pub
Oct  6 12:21:57 shuttle2 ftpd[5229]: PASV
Oct  6 12:21:57 shuttle2 ftpd[5229]: LIST  ""
Oct  6 12:21:59 shuttle2 ftpd[5229]: QUIT
Oct  6 12:21:59 shuttle2 ftpd[5229]: FTP session closed
```

示例日志显示了匿名登录的用户名和密码条目。CWD 条目显示使用 cd 命令导航到 pub 目录。请注意，显示的命令不一定反映用户输入的语法，而是列出 FTP 服务器收到的相应系统调用。例如，LIST 条目实际上是 ls 命令。

### 记录安全违规和文件传输

在 /etc/ftpaccess 配置文件中还有两个有用的日志命令。此行启用安全违规的日志记录：

```
log security [<typelist>]
```

违规行为将针对 anonymous、guest 和 real 用户进行记录，如 typelist 中指定——与其它 log 命令相同。如果未指定 typelist，将记录所有用户的安全违规。

此行写入服务器收发的所有文件的日志：

```
log transfers [<typelist> [<directions>]]
```

typelist 与 log commands 和 log security 行中看到的相同。directions 是以逗号分隔的关键字列表，inbound 用于上传文件，outbound 用于下载文件。如果未给出 directions，则将记录上传和下载的文件。默认情况下已启用入站和出站日志记录。

## 配置权限控制

控制用户活动是保护系统服务器的重要组成部分。ftpaccess 文件包含多条命令，使你能够确定用户在 FTP 会话期间可以和不可以执行的操作。你可以使用这些权限控制来允许用户更改文件权限、删除或覆盖文件、重命名文件以及以默认权限创建新文件。你将在以下各节中学习如何使用所有这些 ftpaccess 文件命令。

