

备份现有的 /etc/proftpd.conf 文件，因为你即将创建自己的版本。打开你喜欢的编辑器，继续阅读以了解如何创建自己的 proftpd 配置文件。

让我们定义一些描述服务器的选项。将以下内容写入你的配置文件中：

```
ServerName    "powered by SuSE Linux"
ServerType    inetd
ServerAdmin   ftpadmin@localhost
AllowOverwrite on
```

第一个标签 ServerName，是显示给连接 FTP 客户端的字符串。ServerType 告诉 proftpd 它是如何启动的。该选项接受两个值之一——inetd 或 standalone。在你的情况下，它使用 inetd，因为你使用 inetd 运行 proftpd 服务器。如果你打算通过直接执行它来手动运行 proftpd，你将把 standalone 作为 ServerType 的值输入。

下一个选项是 ServerAdmin，它是该服务器管理员的电子邮件地址——也就是你自己。你为电子邮件地址输入什么并不重要，因为它不会影响服务器的运行。

最后，选项 AllowOverwrite，当设置为 on 时，告诉 proftpd 允许覆盖文件。这使你的用户能够覆盖他们之前上传的文件。此选项的默认行为是 off，因此如果你希望它为 on，你应该明确指定。一般来说，建议你将其设为 on。

现在你可以保存此文件并尝试连接到你的服务器。你会发现服务器运行得相当不错，即使配置文件非常小。这是因为 proftpd 对所有其他选项使用默认值。

让我们更进一步。再次使用你喜欢的编辑器打开配置文件。假设你希望你的服务器在有人连接到它时显示一条消息，也许用一些关于你的服务器的文本。使用 DisplayConnect 标签并为其提供一个文件作为值：

```
DisplayConnect /etc/myftpmessage
```

每次客户端连接到你的服务器时，你指定的文件的内容都会显示给用户。确保你确实创建了此文件并在其中放入一些文本。现在你需要定义一些超时。使用 TimeoutIdle 标签告诉 proftpd 在断开空闲连接之前等待多长时间。空闲连接可能是已连接但未执行任何操作的 FTP 客户端，或是连接后崩溃而未先断开的客户端。无论哪种情况，你的服务器都会为该无用的连接占用系统资源。如果你将 TimeoutIdle 设置为秒为单位的某个值，空闲连接将在时间用完时被终止。此标签的默认值为 600 秒，但如果你输入 0 秒，就会关闭此功能。最好还是保留它，因此将其添加到你的配置文件中：

```
TimeoutIdle  500
```

另一个超时标签是 TimeoutLogin，即 proftpd 等待客户端输入用户名和密码的秒数。此选项的默认值为 300 秒，因此将其添加到文件中：

```
TimeoutLogin  300
```

FTP 服务器的唯一目的是传输数据。因此，如果客户端连接但不执行任何数据传输，它就会浪费你的资源。使用 TimeoutNoTransfer 来断开连接到你的服务器但未发出任何命令以启动数据传输的客户端。此选项的默认值为 600 秒：

```
TimeoutNoTransfer  600
```

现在你的配置文件应该看起来像这样：

```
ServerName    "powered by SuSE Linux"
ServerType    inetd
ServerAdmin   ftpadm@localhost
AllowOverwrite on
DisplayConnect /etc/myftpmessage
TimeoutLogin  300
TimeoutNoTransfer 600
```

这是一个用于基本 FTP 服务器的良好配置文件。它将允许你的所有用户使用 ftp 在其账户之间传输文件。此外，此配置仅允许你的用户登录。要了解如何允许非用户或匿名人员访问你的机器，请继续阅读下一节。

## Anonymous FTP

如果你熟悉 FTP，你可能已经注意到当前配置不允许匿名用户。FTP 服务器允许在你的系统上拥有账户的用户登录，但不允许其他人。然而，你可能希望允许其他非系统用户或匿名用户访问你的 FTP 服务器。拥有匿名用户使你能够向公众公开某些文件以供下载——例如，SuSE Linux FTP 站点使用匿名登录允许任何人下载 SuSE Linux。

要使 proftpd 允许匿名用户登录，你必须编辑其配置文件。将以下内容添加到配置文件中：

```
<Anonymous /usr/local/ftp>
    User          ftp
    Group         public
    UserAlias     anonymous ftp
    MaxClients
    DisplayLogin  msgs/welcome.msg
```

```
DisplayFirstChdir  .message
<Directory *>
  <Limit WRITE>
    DenyAll
  </Limit>
</Directory>
</Anonymous>
```

匿名用户有一个特殊的分组标签 <Anonymous>，它将所有特定于匿名用户的选项分组在一起。第一个选项是匿名用户登录后将被放置的目录的位置。对于 SuSE Linux，这配置为 /usr/local/ftp，使标签变为 <Anonymous /usr/local/ftp>。

SuSE 已准备好目录 /usr/local/ftp 用于匿名连接。如果你查看该目录的内容，你会看到它使用标准布局：

```
drwxr-xr-x 10 root root 4096 Jan 26 02:44 .
drwxr-xr-x 20 root root 4096 Jan 21 11:57 ..
drwxr-xr-x 2 root root 4096 Dec 12 10:03 bin
drwxr-xr-x 2 root root 4096 Dec 12 10:03 dev
drwxr-xr-x 2 root root 4096 Dec 12 10:03 etc
drwxr-xr-x 2 root root 4096 Nov 9 09:29 lib
drwxr-xr-x 2 root root 4096 Dec 12 10:03 msgs
drwxr-xr-x 2 root root 4096 Nov 9 09:29 pub
drwxr-xr-x 3 root root 4096 Dec 12 10:03 usr
```

接下来的两个标签 user 和 group 告诉 proftpd 当匿名用户登录时使用哪个用户或组运行。这提供了安全性，因为 proftpd 将以用户 FTP、组 public 的权限运行，SuSE Linux 已将其配置为在系统中几乎没有权限。

UserAlias 标签告诉 proftpd anonymous 和 ftp 是同一个用户。这使人们可以使用用户名 anonymous 或 ftp 登录——两者最终都将被视为匿名。

MaxClients 标签是一个重要的标签。你不希望你的系统资源被数百个登录到你的服务器的匿名用户完全消耗。设置此标签为某个数字将限制允许的匿名连接数量。在你的情况下，只允许 10 个匿名连接。

DisplayLogin 定义了一个文件，其内容 proftpd 将在匿名用户连接时显示给他们。如你所见，我们指定的文件是 msgs/welcome.msg，它位于 /usr/local/ftp/msgs。你可以使用任何你想要的文件，如果它在 /usr/local/ftp 内部，你可以使用相对路径名。

DisplayFirstChdir 以 .message 作为参数。因此，用户第一次将目录更改为包含该文件的目录时，其内容会显示给用户。此文件可用于保存描述用户将在该目录中找到的内容的文本。

接下来的选项块以 <Directory> 标签开始。此标签为特定目录设置选项。你为目录 * 设置选项，这里是 /usr/local/ftp 中的所有目录。为了控制连接用户对这些目录的操作，使用 <Limit> 标签。要了解其工作原理，让我们查看 <Directory> 块以及其中如何使用 <Limit>。

<Directory> 块指示 proftpd 你即将为目录 * 设置特定选项。在此特定配置中，使用以下内容：

```
<Limit WRITE>
DenyAll
</Limit>
```

这拒绝所有（DenyAll）客户端写入这些目录。客户端可以读取，因为你没有提及 READ，但他们不能写入任何内容。这是一个用于匿名用户的良好配置，因为它防止他们将文件转储到你的硬盘上。如果你仍然不确定 <Limit> 标签的工作原理，不用担心；我们很快会更多地讨论它。只要确保你理解它在此特定配置中的作用即可。

最后，</Anonymous> 标签结束匿名部分。

## Setting Up User Ratios

FTP 服务器可以为各种目的设置。你可以设置 FTP 服务器以使你的用户能够在其主账户之间传输文件，从而使他们的生活更轻松。你可以设置服务器以使用户能够从你的机器下载数据，使其成为数据存储库。有时，你可能希望控制人们如何从你的服务器传输文件。考虑以下场景。

假设你创建了一个托管艺术图像的 FTP 服务器，并且你希望人们使用你的服务器作为交换场所来交换他们的艺术。感兴趣艺术的人可以登录到你的服务器下载其他艺术家上传的图像。过了一段时间，你注意到很多人只是登录、下载图像，然后从不上传任何内容。你的服务器已经失去了其基本目的——促进艺术交流。你如何迫使用户停止滥用你的服务器并开始上传一些图像。你可以使用 DisplayConnect 标签在连接时显示一条消息，但这可能不够有力。这就是比率发挥作用的地方。

比率使你能够设置人们如何下载和上传文件到你的服务器的规则。例如，你可以设置一条规则，强制用户每下载一个文件就上传一个文件。这应该能保持你在服务器上的艺术交流。比率非常灵活，并且在帮助控制滥用方面非常有用。

要设置比率，你必须在 proftpd 中启用该功能。为此，在你的配置文件中将标签 Ratios 设置为 on：

```
Ratios on
```

![](img/659f91d9da7b29976c0625e2e9628511_390_0.png)

