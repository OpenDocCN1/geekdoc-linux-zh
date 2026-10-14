
当`/etc/postfix/main.cf`修改后，使用`postfix reload`重启 Postfix。为了确保 Postfix 接收到更改，使用`postfix -a`。

（注：由于原文后部分存在大量重复内容，此处已按要求执行了翻译并保持了结构。）

## 为 root 邮件设置别名

在使用 Cyrus 环境时，需要考虑的一点是，任何不在数据库中的邮件都将被拒绝。对于 root 用户也是如此。在 Cyrus 这种情况下，我们可以为 root 的邮件设置别名：

1. 打开`/etc/aliases`文件并添加条目：
   `root: justin`
   这告诉 Postfix root 的邮件应该投递到 justin。
2. 当`/etc/aliases`修改后，运行`postfix`命令：

```
bible:~ # postfix new
```
3. 你需要运行`postfix`数据库以提交新的别名。

第 17 章 ✦ 邮件服务器 – Sendmail, Qpopper 和 Cyrus 493

## 选择邮件客户端

当你的邮件服务器配置完成后，你需要能够读取你的电子邮件。你会发现许多邮件客户端，最流行的是`mutt`、`pine`、`kmail`和`evolution`。我们将简要描述所有系统的优点以及它们的常用场景。

## 命令行客户端

如果你只有命令行访问你的邮件，你可能想使用`mail`或`mutt`。

### mail

`mail`命令是最基础的邮件客户端，用于通过命令行发送和接收邮件。如果你想用`mail`命令发送邮件，只需`mail`你想发送邮件的人。

```
bible-- # mail just@wiley..com

Subject: Hello

This is a test

EOT
```

在这里我们请求了邮件的主题，并准备好输入邮件正文。注意在整个交易过程中我们没有得到任何建议。这是典型的 Unix 命令的精妙之处！

当消息输入后，你需要单独一行输入一个点并按 Enter/Return。这将把邮件发送给指定的接收者。

要使用`mail`命令读取邮件，在命令行中输入`mail`并按 Enter/Return。

你会看到信箱中的邮件列表供你阅读。读取消息，只需输入你想读取的邮件编号：

```
bible-- # mail

mailx version 10.6 11/15/03. Type ? for help.

"/var/mail/justin/": 1 message 1

>N 1 just@wiley.com  Thu Sep 30 11:30  14/452  "Hello there"

&
```
