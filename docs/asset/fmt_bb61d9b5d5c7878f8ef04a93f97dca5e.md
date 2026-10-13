
### 重启 FTP

在 FTP 服务器关闭后重启，你需要删除由 `ftpshutdown` 命令创建的关闭文件。该文件通常位于 `/var/run/ftp.shutdown`。删除文件后，可以通过运行 `ftpd` 命令重新启动 FTP 服务。

# 第20章 - 设置 FTP 服务器 713

## 获取更多关于 FTP 服务器的信息

有很多资源可以获取更多关于 FTP 服务器的信息。以下是一些选项：

- **FAQ**——最新版本的 WU-FTP 常见问题列表可以从 http://wnu.nl/~koos/wu-ftpd-faq.html 获取。提供了一些实用的答案，该 FAQ 还包含了指向其他帮助文档的链接。
- **RFCs**——这些请求定义了互联网上使用的标准协议。FTP 的主要 RFC 是 RFC959。你可以从互联网上的各种位置获取 RFCs，包括 [FTP 存档](http://www.faqs.org/rfcs)。
- **CERT**——这还提供了关于设置 FTP 服务器的有用文档。[匿名 FTP 滥](http://ftp.cert.org/pub/tech_tips/anonymous_abuses) 描述了如何响应以及从 FTP 服务器恢复。[匿名 FTP 配置指南](http://ftp.cert.org/pub/tech_tips/anonymous_ftp_config) 提供了设置 FTP 区域的通用指南以及设置区域的特定挑战。![](img/176fafe2d0ee75bc0789ee744_.png) 我强烈建议阅读 CERT 的 FTP 文档。这些文档中的技巧将确保你的 FTP 服务器安全，同时让你提供想要共享的服务。
- **邮件列表**——要订阅 WU-FTP 邮件列表，你只需向 list.wust1.edu 发送邮件，正文中包含以下行：

```
SUBSCRIBE WU-FTP <username>
```

如果你想向列表中的所有人发送邮件（在你订阅之后），将邮件地址设置为：`ftpd@mail.wust1.edu`
- **邮件列表存档**——WU-FTP 邮件列表存档维护在 http://www.landfield.com/ftpd/mail-archive。此外，还有一个位于 http://www.landfield.com/ftpd/mail-archive/search.html 的搜索页面。

## 测试你的 FTP 服务器

你可以使用图形界面和命令行工具来访问 FTP 服务器。Linux 中常用的命令行工具是 `ftp` 命令。然而，也有许多图形化 FTP 程序，包括 gFTP 窗口。此外，你的网络浏览器也可以提供访问 FTP 服务器的功能。

通常情况下，从 Netscape 浏览器访问 FTP 站点，可以点击服务器的链接，或者输入类似 `ftp:http://ftp.whatever.com` 的地址。在无需了解的情况下，以匿名用户登录 FTP 服务器。如果你想从 Netscape 测试你的 FTP 服务但使用不同的用户登录，可以通过添加用户名和密码来实现。这些项目随 FTP 站点的 URL 输入 Netscape 的地址栏。以下是一个示例：

```
ftp://mike:99po15@ftp.whatever.com
```
