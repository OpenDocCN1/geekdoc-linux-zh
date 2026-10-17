
- 你的光标位于以单词 `definition` 开头的第一行。
- 输入字母 `o`。
- 打开一个新行。
- 6 输入 `define(SENDMAIL, BLAME.Group WritablePath$s` 并按 `Esc` 键插入输入文本。
- 7 输入 `iq` 并按回车返回你的值并退出。
- 8 输入 `-m /tmp/sendmail.cf yourdomain.com =` 并按回车。
- 9 输入 `sudo /etc/sendmail.cf /etc/sendmail.cf.date` 并按回车。
- 11 输入 `sudo sendmail -bd -q15`。

## 在 UNIX 中发送电子邮件

你可以在 Mac OS X 的命令行中创建并发送消息，就像在大多数 UNIX 系统中执行一样。你不需要打开邮件客户端。实现此操作最简单、最快的方法是使用 `echo` 命令创建消息，然后将消息通过给 `mail` 命令。例如，你可以在命令行中输入消息并将其添加到用户 `shs` 的收件箱中。

你的收件可以通过多种方式读取你的消息。如果他们像你一样是命令行用户，他们可能选择通过单独的一一行输入 `mail` 来使用 `mail` 命令。当消息出现时，他们可以一次读取一条，或者在不读取的情况下删除它们。如果他们想回复，也可以这样做。`mail` 命令包含自由参数和 `delete` 参数。在有多封邮件的情况下，选择消息编号并按回车。如果你的系统设置了邮件客户端，你可能更喜欢使用这些工具之一打开信箱。

```bash
echo do not forget we have a lunch date today | mail -s "lunch" shs
```

如果你想发送更长的消息，可以运行 `mail` 命令 - 例如 `mail -s shs -` 然后输入你的主题行和消息。当你写完消息后，在单独的一行输入一个点 `.`，系统就会发送。

| Terminal | File | Edit | Scrollback | Font | Window | Help |
|---|---|---|---|---|---|---|
| [ferro:-]mail]user echo "Can you read this?" mail -s "test" user | [ferro:-]user echo "Can you read this?" mail -s "test" user | |
| [ferro:-]mail]user | Subject today's meeting | |
| | I will arrive to meet you this afternoon. Please tell jokes until I get there. I everyone needs to be in a good mood | |
| | Thanks | |
| | EDT | | |
| [ferro:-]user | | | |

## 发送消息

- 1 输入 `echo "Can you read this?"` 后接一个空格。
- 2 输入 `mail -s "test"` 后接一个空格。
- 3 输入你的用户名，并按回车。
- 4 输入 `mail` 后接一个空格和用户名，并按回车。
- 5 在提示符处输入主题行，并按回车。
- 6 输入你的消息，并按回车。
- 7 在单独的一行输入一个点 `.` 并按回车。

邮件系统投递你的消息。

## 安装并使用互联网应用程序

### 额外

虽然 `mail` 命令很有用，但如今的 UNIX 用户更倾向于使用功能更强大的工具来发送和接收电子邮件。毕竟，简单的 `mail` 命令无法正确显示以 HTML 格式到达的电子邮件，也不允许你获取和添加附件。`mail` 命令创建于很久以前，那时电子邮件中还没有使用附件。

`mail` 命令在脚本内部使用也非常有帮助。例如，如果你写了一个脚本来定期检查磁盘空间，你可能希望脚本通过电子邮件将磁盘检查的结果发送给你。你可以在脚本中使用这样一行代码，如 `-k "disk usage" user@domain.com`，它通过 `cron` 每天运行一次，以提醒自己查看磁盘空间。

尽管如此，`mail` 命令继续提供服务。例如，从命令行发送简单的电子邮件可以帮助你判断邮件服务器是否正常。

邮件文件存储在 `/var/mail/` 中。系统中任何有待处理邮件的用户在该目录下都有一个单独文件。索引用户将是 `/var/mail/user`。

```
Terminal File Edit Scrollback Font Window Help

[--] user@mail

Mail version 1 6/6/93. Type 7 for help.

/var/mail/user": 2 messages 2 new

> 1 shs Wed Jun 25 07:07:17 13/359 "test"

> 2 shs Wed Jun 25 07:07:17 18/498 "today's meeting"
```

## 从其他服务器获取邮件

你可以使用 `fetchmail` 工具从远程服务器获取邮件。`fetchmail` 是一个取回和转发工具，支持所有从邮件服务器获取邮件的导入协议。这些包括最流行的 `POP3` 和 `IMAP`，以及其他对等协议：`RPOP`、`NNOP`、`AFOP`、`ETR` 和 `OMDAR`。

... 只有个人用户才能读取此文件。事实上，如果该文件的权限未设置为 `710`，`fetchmail` 会向你发出警告。这意味着所有者具有读取、写入和执行权限，而用户组仅具有执行权限，其他人都无法访问该文件。

与许多工具一样，`fetchmail` 使用一个名为 `.fetchmail` 的配置文件来存储你的账户信息。你可以向 `.fetchmail` 文件中添加以下行：

```
poll mail.mailserver.org protocol POP3 user
nick password wormx name john
```

在这个示例中，`nick` 是远程账户的用户名，而 `john` 是本地用户。你检查是否有可下载邮件的服务器被称为 `.mailserver.org`。如你所见，密码是以明文形式显示的。因此，你必须对 `.fetchmail` 文件设置权限，以便

将密码存储在文件中可以避免你每次使用 `fetchmail` 时都输入。这也允许 `fetchmail` 通过 `cron` 自动运行每日或更频繁的下载。

你的系统必须运行 `fetchmail` 才能正常工作。`fetchmail` 的原理是将邮件传输到你本地系统的 `smtp` 服务器。如果你不发送邮件，可以使用 `.fetchmail` 文件处理入站邮件，将其如下所示：

```
poll mail.mailserver.org protocol POP3 user
nick password wormx name "/usr/bin/fetchmail -d"
```

| 终端 | 文件 | 编辑 | 回滚内容 | 字体 | 窗口 | 帮助 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| [fetchmail:screenshots] user% fetchmail -v --keep -a >> /var/log/fetchmail 2>&1 | | | | | | |
| [fetchmail]- * /home/users/user $ - user echo '11 23' * * /sw/bin/fetchmail -a >> /var/log/fetchmail 2>&1 | | | | | | |
| [fetchmail]- * /home/users/user -a grep cron 338 77 Ss R. 0:00:00 grep cron | | | | |
| [fetchmail]- * /home/users/user exit | | | | |
| [fetchmail]- * /home/users/user cron 5 18 * */users/user/check_space * /dev/null 11 23 * /sw/bin/fetchmail -a >> /var/log/fetchmail 2>&1 | | | | |
| [fetchmail]- user | | | |

## 在命令行上使用 FETCHMAIL

- 输入 `fetchmail -v` 后跟一个空格。
- 输入 `-keep -a` 后跟一个空格。
- `Fetchmail` 从远程服务器下载你的邮件。

## 通过 CRON 运行 FETCHMAIL

- 输入 `crontab -e` 来编辑你的文件。
- 你的 `cron` 文件打开后，`fetchmail` 将每晚 11:11 PM 运行。

![](img/8d9b2c31cb5ebc6571f0b2dfd7c634cf_232_0.png)

## 安装 PINE

`Pine` 是一个基于文本的电子邮件程序，在 UNIX 系统上已多年。你可以使用 `Fink` 或 `FinkCommander` 在你的 Mac OS 系统上安装 `pine`。否则，你可以从 https://www.washington.edu/pine 下载 `pine`。然后你可以按照第 12 章中的描述解压并安装安装文件。

当你第一次运行 `pine` 时，它会在你的主目录中创建一个名为 `pincerc` 的配置文件。该文件允许你修改许多配置参数，例如你在发送的消息中显示的名称。与大多数 UNIX 配置文件一样，任何以 `#` 开头的行都是注释。

要创建应用程序，你可以使用 `build os`。此命令取代了通常的 `make` 命令，并为你的 Mac OS X 构建一个二进制文件。当过程完成后，你将获得一个包含程序的目录，你可以将其复制到系统上的其他位置。你可以参考 `README` 获取可能你的系统相关的说明。

为了方便使用，请确保它在你的搜索路径中。这允许你通过在命令行输入 `pine` 来启动 `pine`。你可以通过输入 `pine` 来验证 `pine` 是否在搜索路径中。此命令会返回 `pine` 可执行文件的完整路径。

如果你设置邮件服务器，某些与 `pine` 结合的其他工具非常有用。`imap`、`ipop2` 和 `ipop3` 是允许邮件客户端下载邮件的服务器。这些工具分别支持 `IMAP`、`POP2` 和 `POP3` 协议。

| 终端 | 文件 | 编辑 | 回滚内容 | 字体 | 窗口 | 帮助 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

```
[[ - ]] user sudo fink install pine

Reload package info...

Information about 769 packages received in 5 seconds.

pine version

pine version 4.4.2

The following package will be installed:

curl -f -O http://fink.washington.edu/pine/pine-4.4.2.tar.gz -C /tmp/directory

execution of curl failed, exit code 19

dncompressing the file "pine-4.4.2.tar.gz"
```

```
[[ - ]] user sudo fink install pine

Reload package info...

Information about 769 packages received in 5 seconds.

pine version

pine version 4.4.2

The following package will be installed:

curl -f -O http://fink.washington.edu/pine/pine-4.4.2.tar.gz -C /tmp/directory

execution of curl failed, exit code 19

dncompressing the file "pine-4.4.2.tar.gz"
```

```
[[ - ]] user sudo fink install pine

Reload package info...

Information about 769 packages received in 5 seconds.

pine version

pine version 4.4.2

The following package will be installed:

curl -f -O http://fink.washington.edu/pine/pine-4.4.2.tar.gz -C /tmp/directory

execution of curl failed, exit code 19

dncompressing the file "pine-4.4.2.tar.gz"
```

```
dncompressing the file "pine-4.4.2.tar.gz"
```

```
[[ - ]] user
```

```
dncompressing the file "pine-4.4.2.tar.gz"
```

```
[[ - ]] user
```

```
dncompressing the file "pine-4.4.2.tar.gz"
```

```
[[ - ]] user
```

```
dncompressing the file "pine-4.4.2.tar.gz"
```

```
[[ - ]] user
```

```
dncompressing the file "pine-4.4.2.tar.gz"
```

```
[[ - ]] user
```

```
dncompressing the file "pine-4.4.2.tar.gz"
```

```
[[ - ]] user
```
