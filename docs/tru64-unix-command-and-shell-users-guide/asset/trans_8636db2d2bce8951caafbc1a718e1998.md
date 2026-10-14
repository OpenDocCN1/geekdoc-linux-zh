

如果你通过输入 q 或 quit 而不是 x 来退出 mailx，任何你之前阅读但未删除的消息都会被添加到你主目录中名为 mbox 的先前未删除消息文件末尾。

## 11.3.2 回复消息

回复邮件消息与发送邮件消息类似。你在编辑、放弃或在消息中包含文件时有相同的选项，如第 11.2 节所述。

要回复你刚刚读完的消息的发件人，请在 mail 提示符下输入大写 R（reply）命令，如示例 11-6 所示。

### 示例 11-6：回复消息

```
Message 3:
From: deede e Mon Jul 20 14:13:32 1999
Date: Mon, 20 Jul 1999 14:13:05 -0400
From: deede e (DeeDee Smith)
To: jones, mays@sf24.usernet, susannah@artwrk
Subject: Testing text-processing software

I think we should test the new text processing
software on the older machines as well as the
newer. Remember that many customers still have
the older models.

? R
To: deede e
Subject: Re: Testing text-processing software

I agree. Also, we should test different machine
configurations to determine if, for example,
it performs satisfactorily when run remotely.
.
EOT
?
```

在你输入 R 之后，收件人和主题行会显示出来，使你能够验证自己是否正在回复预期的收件人。

如果你输入小写 r，回复将被发送给原始邮件的收件人以及发件人；在示例 11-6 中，将发送给 mays@sf24.usernet 和 susannah@artwrk，以及 deede e。

### 注意

要仅回复邮件消息的发件人，请在 mail 提示符下输入大写 R。要回复邮件消息的发件人及所有收件人，请在提示符下输入小写 r。

在示例 11-6 中，Cc: 提示未出现，因为用户 jones 的 .mailrc 文件不包含 set askcc 命令。

## 11.3.3 保存消息

如果你通过输入 q 命令（而不是 x 或 exit 命令）离开 mailx，你刚刚阅读的消息将被存储在你主目录中的 mbox 文件中。

为了更有效地存储邮件消息，你可以将它们保存为单独命名的文件或保存在文件夹中，如以下各节所述。

### 11.3.3.1 将消息保存到文件

有几种类型的邮件你可能想保存到文件中：

- 你阅读的简短但重要的消息
- mailx 返回给你的地址错误的邮件消息
- 你想稍后打印并阅读的长消息

要保存你阅读的简短消息或 mailx 返回给你的邮件消息，请在 mailx 提示符下输入 s 命令并提供文件名。

返回的消息显示在以下 mailx 命令输出的第二项中：

```
orange% mailx
Mail $Revision: 1.1.4.7 $ Type ? for help.
"/usr/spool/mail/jones": 2 messages 1 new 1 unread
U 1 root Mon Jul 20 10:39 14/438 "System news"
>N 2 MAILER-DAEMON Wed Aug 5 09:39 19/498 "Returned mail: User unknown"
?
```

如以下示例所示，用户 Jones 决定将上一个示例中的返回消息保存到文件 verify-resend 中，作为在重新发送之前找到正确地址的提醒。

```
:
>N 2 MAILER-DAEMON Wed Aug 5 09:39 19/498 "Returned mail: User unknown"
? s verify-resend
```

文件 verify-resend 保存在当前目录中，除非指定了显式路径名。例如，用户 Jones 也可以通过输入以下命令将其保存到名为 fix-later 的子目录中：

```
? s fix-later/verify-resend
```

要保存长消息而不逐行阅读全部文本，请按 Ctrl/C 停止消息滚动并显示 mailx 提示符。现在你可以保存（或删除）该消息。在以下示例中，用户 Jones 在消息 1 中收到一份 20 页的报告，并按 Ctrl/C 访问 mailx 提示符，在那里输入保存文件的命令：

```
? 1
Message 1:
From smith Wed Aug 5 16:43:42 1999
Date: Wed, 5 Aug 1999 16:43:41 -0400
From: smith (Cassandra Smith)
To: jones
Subject: 20-page report: host configuration results

Mortimer,

Here's the report on host configuration that the
Ctrl/C
Interrupt
?s sys-config-report
"sys-config-report" [New file] 2147/48353
?dp
:
```

在前一个示例中，创建文件后，用户 Jones 在 mailx 提示符下输入 dp（即 delete-proceed）以防止大型 20 页文件被保存到 mbox 中，并开始阅读下一封邮件。否则，也可以输入 mailx 命令 d（delete）并按回车键来实现同样的目的。

### 11.3.3.2 将消息保存到文件夹

为了便于参考并最小化 mbox 文件的大小（它本身就是一个文件夹），你可以将消息保存到称为文件夹的文件中。在使用 mbox 以外的文件夹之前，你必须在主目录中创建文件夹子目录，并在 .mailrc 文件中添加指向该文件夹的指针。例如，如果你在主目录中创建一个名为 sys-config 的目录，你必须在 .mailrc 文件中添加以下行：
set folder=sys-config.

要将消息添加到文件夹，请使用 mailx 命令 s 和文件夹名称。例如，要将有关主机配置的消息与其他主题相关的消息一起保存，请将其写入名为 sys-config 的文件夹，如下所示：

