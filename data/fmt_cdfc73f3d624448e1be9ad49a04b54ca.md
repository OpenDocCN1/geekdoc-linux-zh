
# trap decode to catch security attacks
```
decode: root ← remove this line.
```

# Person who should get's mail
```
#root: marc
```

- For the changes to take effect you will need to run:
  `[root@]# /usr/bin/newaliases`

为了使更改生效，你需要运行：
  `[root@]# /usr/bin/newaliases`

Copyright 1999 - 2000 Gerhard Maurani, Open Network Architecture ® and OpenDocs Publishing

## Server Software (Mail Network Services)

CHAPTER 5

### Prevent your Sendmail being abused by unauthorized users

Sendmail now includes powerful Anti-Spam features, which can help prevent your mail server from being abused by unauthorized users. To do this, edit your `/etc/mail/sendmail.cf` file and make a change to the configuration file to block spammers.

Sendmail 现在包含了强大的反垃圾邮件功能，可以帮助防止邮件服务器被未经授权的用户滥用。要做到这一点，请编辑你的 `/etc/mail/sendmail.cf` 文件并对配置文件进行更改以拦截垃圾邮件发送者。

Edit the `sendmail.cf` file (`vi /etc/mail/sendmail.cf`) and change the line:
- `O PrivacyOptions=authwarnings`

To read:
`O PrivacyOptions=authwarnings.goaway`

修改为：
`O PrivacyOptions=authwarnings.goaway`

Setting the "goaway" option causes Sendmail to de-disapp all SMTP "EXPN" commands, it also causes it to reject all SMTP "VERB" commands and to disapp all SMTP "VRFY" commands. These changes prevent users from using the "EXPN" and "VRFY" commands in Sendmail.

设置 "goaway" 选项会导致 Sendmail 禁用所有的 SMTP "EXPN" 命令，它还会导致拒绝所有 SMTP "VERB" 命令并禁用所有的 SMTP "VRFY" 命令。这些更改防止了用户在 Sendmail 中使用 "EXPN" 和 "VRFY" 命令。

### Restrict who may examine the queue contents

Ordinary, anyone may examine the mail queue contents by using the `mailq` command. To restrict who may examine the queue contents, you must specify the `restrictmailq` option in `/etc/mail/sendmail.cf` file. With this option, Sendmail allows only users who are in the same group as ownership of the queue directory (`root`) to examine the contents. The queue directory to be fully protected with mode `0700`, while selected users are still able to see the contents.

通常，任何人都可以使用 `mailq` 命令查看邮件队列内容。要限制谁可以查看队列内容，你必须在 `/etc/mail/sendmail.cf` 文件中指定 `restrictmailq` 选项。通过此选项，Sendmail 仅允许与队列目录所有者（`root`）处于同一组的用户查看内容。队列目录将使用模式 `0700` 进行完全保护，而选定的用户仍然能够看到内容。

Edit the `sendmail.cf` file (`vi /etc/mail/sendmail.cf`) and change the line:
- `O PrivacyOptions=authwarnings.goaway`

To read:
`O PrivacyOptions=authwarnings.goaway,restrictmailq`

- Now we change the mode of our queue directory to be fully protected:
`[root #]# /etc/rc chmod 0700 /var/spool/mqueue`

现在我们将我们的队列目录模式更改为受完全保护：
`[root #]# /etc/rc chmod 0700 /var/spool/mqueue`

- Now re-start the sendmail process manually for the change to take effect:
```
[root #]# /etc/rc.d/init.sendmail
Shutting down sendmail: [ OK ]
Starting sendmail: [ OK ]
```
现在手动重启 sendmail 进程以使更改生效：
```
[root #]# /etc/rc.d/init.sendmail
Shutting down sendmail: [ OK ]
Starting sendmail: [ OK ]
```

NOTE: We have added the "goaway" option to our line "PrivacyOptions=" in `sendmail.cf`. We now continue by adding the "restrictmailq" option to this line.

注意：我们在 `sendmail.cf` 的 "PrivacyOptions=" 行中添加了 "goaway" 选项。现在我们继续在此行添加 "restrictmailq" 选项。

Any non-privileged user who attempts to examine the mail queue content will get this message:
```
[user #]/usr/bin/mailq
You are not permitted to see the queue
```
任何非特权用户尝试查看邮件队列内容都将收到此消息：
```
[user #]/usr/bin/mailq
```
你没有权限查看队列

### Limit queue processing to "root"

Ordinary, anyone may process the queue with the "-q" switch. To limit queue processing to "root" and the owner of the queue directory, you must specify the "restrictmailq" option in the `/etc/mail/sendmail.cf` file.

通常，任何人都可以使用 "-q" 选项处理队列。要将队列处理限制为 "root" 和队列目录的所有者，你必须在 `/etc/mail/sendmail.cf` 文件中指定 "restrictmailq" 选项。

Edit the `sendmail.cf` file (`vi /etc/mail/sendmail.cf`) and remove the following lines:

（注：原文此处为 "remove the following lines" 实际上为 "change"，按原意翻译）

Edit the `sendmail.cf` file (`vi /etc/mail/sendmail.cf`) and remove the following lines:

编辑 `sendmail.cf` 文件（`vi /etc/mail/sendmail.cf`）并删除以下行：
- `O PrivacyOptions=authwarnings.goaway`

To read:
