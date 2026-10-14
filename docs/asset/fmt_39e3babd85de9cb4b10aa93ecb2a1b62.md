
在此示例中，有两条来自系统管理员`root`的信息在等待；一条是未读的（第 1 列用`U`表示），来自之前的`mailx`会话，另一条是新的（用`N`表示）。信息末尾的问号（`?`）是`mailx`提示符。你可以在此提示符下输入另一个问号以显示可用的`mailx`命令列表，如标题所示，并在第 11.4 节中描述。

你可以在`mailx`提示符下按下回车键来阅读信息 2，即在等待信息列表中用右尖括号（`>`）表示的信息。示例 11–4 显示了该信息的读取过程。

#### 示例 11–4：阅读 mailx 信息

```
?  Return
Message 2:
From root Wed Aug  4 11:17:36 1999
Date: Wed,  4 Aug 1999 11:17:29 -0400
From: root (system administrator)
To: jones
Subject: Welcome

Welcome to the company computer network.  I’m the
person who manages this system.  If you have
questions or problems, send mail to root.  You
can also send mail to manager or admin; messages
will be forwarded to me.

I will be on vacation for the next two weeks after
this week, starting Monday, August 10.  I’ll be
stdin Space
back on Monday, August 24.
?
```

在示例 11–4 中，显示了`stdin`，因为`PAGER`变量已设置为`more`（默认值）。如果`PAGER`变量设置为`pg`，则不会显示任何内容。此外，`stdin`出现在信息的第 15 行之后，因为用户`Jones`通过在`.mailrc`文件中添加`set crt=15`来自定义了`mailx`环境。在`.mailrc`文件中，`set crt=`指定在调用分页器（`pg`或`more`）显示剩余信息之前一次显示的行数。如示例所示，由于信息长于 15 行，`set crt`指示`mailx`在 15 行后调用分页器。通过按空格键，可以显示信息的下一屏。你应该通过使用`set crt=`来自定义你的`mailx`环境。否则，长邮件信息会快速滚动，需要你快速按下暂停屏幕键。有关自定义`mailx`的更多信息，请参阅第 11.6.2 节和附录 D。

要阅读另一条信息，请在`mailx`提示符下输入信息编号。要再次列出信息，请在`mailx`提示符下输入`h`。在示例 11-5 中，用户`Jones`使用`h`命令列出邮件信息，发现第一条信息仍未读，并在`?`提示符下输入`1`来阅读它。

#### 示例 11-5：阅读另一条 mailx 信息

```
? h
U 1 root  Mon Jul 20 10:39 14/438  "System news"
> 2 root  Mon Jul 20 11:30 11/292  "Welcome"
? 1
Message 1:
From root Mon Jul 20 11:30:07 1999
Date: Mon, 20 Jul 1999 11:30:04 -0400
From: root (system administrator)
To: jones
Subject: System news

The newest release of the text processing
software will be installed after 5 o'clock
today.  Send mail if you have questions or
concerns before or after the installation.

?
```

你正在阅读的信息称为**当前信息**。要重新阅读该信息，请按回车键。要阅读下一条信息，请按`n`。该信息将成为当前信息。你可以通过在每条信息后按`n`来连续阅读所有信息。你可以通过修改附录 D 中描述的`gonext`变量来更改此设置。

#### 11.3.1 删除信息

你的信息会一直保留在`mailx`中，直到你在将其存储到文件或文件夹中之前或之后删除它们。要在阅读后删除当前信息，请在`mailx`提示符下输入`d`（`delete`）命令。要删除不同的信息，请在`mailx`提示符下输入`d`命令，后跟信息编号。你可以通过在`d`命令后列出它们的编号来删除多条信息。例如，在`mailx`提示符下输入以下命令以删除信息 7 和 9：

```
? d 7 9
```

你也可以通过在第一个和最后一个信息之间使用连字符来删除一系列信息。例如，要删除 7 到 11 的信息，请在`mailx`提示符下输入以下命令：

```
? d 7-11
```

如果你不小心删除了信息，可以使用`u`（`undelete`）命令恢复它。例如，要取消删除信息 7，请在`mailx`提示符下输入以下命令：

```
? u 7
```

如果你通过输入`q`或`quit`而不是`x`来退出`mailx`，任何你之前阅读但未删除的消息都会被添加到你主目录中名为`mbox`的先前未删除消息文件末尾。

#### 11.3.2 回复消息

回复邮件消息与发送邮件消息类似。你在编辑、放弃或在消息中包含文件时有相同的选项，如第 11.2 节所述。

要回复你刚刚读完的消息的发件人，请在`mail`提示符下输入大写`R`（`reply`）命令，如示例 11-6 所示。

##### 示例 11-6：回复消息

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

在你输入`R`之后，收件人和主题行会显示出来，使你能够验证自己是否正在回复预期的收件人。

如果你输入小写`r`，回复将被发送给原始邮件的收件人以及发件人；在示例 11-6 中，将发送给`mays@sf24.usernet`和`susannah@artwrk`，以及`deede e`。

##### 注意

要仅回复邮件消息的发件人，请在`mail`提示符下输入大写`R`。要回复邮件消息的发件人及所有收件人，请在提示符下输入小写`r`。

在示例 11-6 中，`Cc:`提示未出现，因为用户`jones`的`.mailrc`文件不包含`set askcc`命令。

#### 11.3.3 保存消息

如果你通过输入`q`命令（而不是`x`或`exit`命令）离开`mailx`，你刚刚阅读的消息将被存储在你主目录中的`mbox`文件中。

为了更有效地存储邮件消息，你可以将它们保存为单独命名的文件或保存在文件夹中，如以下各节所述。

##### 11.3.3.1 将消息保存到文件

有几种类型的邮件你可能想保存到文件中：

- 你阅读的简短但重要的消息

- `mailx`返回给你的地址错误的邮件消息

- 你想稍后打印并阅读的长消息

要保存你阅读的简短消息或`mailx`返回给你的邮件消息，请在`mailx`提示符下输入`s`命令并提供文件名。

返回的消息显示在以下`mailx`命令输出的第二项中：

```
orange% mailx
Mail $Revision: 1.1.4.7 $ Type ? for help.
"/usr/spool/mail/jones": 2 messages 1 new 1 unread
U 1 root Mon Jul 20 10:39 14/438 "System news"
>N 2 MAILER-DAEMON Wed Aug 5 09:39 19/498 "Returned mail: User unknown"
?
```

如以下示例所示，用户`Jones`决定将上一个示例中的返回消息保存到文件`verify-resend`中，作为在重新发送之前找到正确地址的提醒。
