
## 8. 为 `/etc/sk` 创建 maildrop 目录
`/etc/sk` 的内容将被复制到任何新账户的家目录中：

```
$ maildrmake.maildrop /etc/sk/Maildir
$ maildrmake.maildrop -f Trash /etc/sk/Maildir
```

## 9. 通知 Postfix 重新加载配置，使其启动 maildrop 而不是其内置的 MDA

```
# invoke-rc postfix reload
```

## 10. 安装 Courier-IMAP 守护进程

```
# apt-get install courier-imap
```

> 注意：如果你想允许 POP3 访问，也可以在此步骤中安装 `courier-pop` 软件包。但请记住，POP3 客户端将无法访问其账户下的 Trash 文件夹。

## 11. Debconfi 会询问你是否想为 Web 基础管理创建目录。该界面的功能有限，我建议不要启用它。

你现在拥有了一个功能完全的邮件服务器，可以从任何标准邮件客户端访问它。

# 测试与排排除

测试邮件系统的最佳方法是向你的新地址发送消息。消息可以使用你的邮件客户端发送，也可以从命令行使用 `mail` 程序发送。带有附件的消息可以从命令行使用 `mpack` 发送。

要验证你的病毒扫描器是否正常扫描消息，请尝试给自己发送一个测试文件。`clam-testfiles` 软件包中包含了 ClamAV 应该检测到的病毒文件。使用 `mpack` 发送其中一个文件（例如 `/usr/share/clam-testfiles/` 中的 `test.zip`）到服务器上的地址，并验证它是否被正确处理：

```
# mpack -s "test message" /usr/share/clam-testfiles/test.zip recipient email address
```

> 注意：`mpack` 程序是 `mpack` 软件包的一部分，可能尚未安装。你可以使用 `apt-get` 轻松安装它。

要测试 SpamAssassin，尝试给自己发送看起来像垃圾邮件的消息。通常包含大量字符和符号的消息会收到 SpamAssassin 的高分。

如果某些内容工作不正常，你应该首先检查 `/var/log/mail.log`。如果你在其中没有发现错误消息，请尝试进行搜索。你可以在这里找到解决方案。你还应该检查所有守护进程是否都在运行。两种配置都要求邮件在后台运行。sendmail 配置同样需要 `clamd`、`clamav-milter` 和 `spass-milter` 运行。

# 第 24 章 ♦ 运行邮件服务器 631

任何关于 `clavam-milter` 和 `spass-milter` 未运行的错误将在 `mail.log` 中，格式如下：

```
[...] Milter (clamav): to error state
```

# 配置客户端

支持你配置的协议（第一个为 POP3，第二个为 IMAP）的任何客户端都应该从你的服务器访问邮件。在邮件设置中使用你的服务器名称，如果无法工作，请参考前节的故障排除步骤。你可以通过运行 `maildroprter` 和 `maildroplex` 获取有关 `/etc/maildroprc` 文件功能和语法的更多信息。
