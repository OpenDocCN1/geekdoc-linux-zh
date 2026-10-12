
文件的权限。关于设置用户目录和文件的更多信息，请参阅有关控制 FTP 访问权限的相关章节。

## 添加有用的信息

Red Hat Linux 计算机上的 FTP 服务已配置为自动显示消息，并在用户浏览你的站点过程中，于不同时间点提醒用户 README 文件的存在。然而，安装 FTP 后，这些文件并不存在。因此，为了帮助浏览你的站点，你需要创建这些文件。

## 创建 README 文件

README 文件是提供软件包内容信息的一种标准方法，或者在本例中，是提供 FTP 目录内容信息的方法。默认情况下，你的 FTP 服务器被配置为在用户登录或进入包含 README 文件的目录时，提醒用户该文件的存在。以下是 /etc/ftpaccess 文件中实现此功能的条目：

```
readme    README*      login
readme    README*      cwd=*
```

README 末尾的星号表示匹配所有以“README”一词开头的文件（例如 README.info、README-help 或 README.txt）。README 文件通常是纯文本，因此任何人都可以阅读。你可以使用任何文本编辑器创建一个。将一个 README 文件添加到 /var/ftp 目录中（用于描述 FTP 服务器的内容），或者添加到任何你希望向进入该目录的用户描述其内容的目录中。

进入包含 README 文件目录的用户将会看到一条消息，告知他们该 README 文件的存在。他们必须自行打开该文件才能查看其内容。以下是用户在登录后看到的示例：

```
230-Please read the file README
230- it was last modified on Thu May 23 16:46:20 02 0 days ago
```

## 创建消息文件

如果你想确保用户在登录或进入特定目录时看到一条消息，你可以创建 welcome.msg 和 .message 文件。你可以使用任何文本编辑器创建这些文件。/etc/ftpaccess 文件中的两个条目定义了如何设置读取这些消息文件：

```
message   /welcome.msg   login
message   .message       .cwd=*
```

你可以在 FTP 用户的主目录（对于匿名用户通常是 /var/ftp）中创建一个 welcome.msg 文件。它应该是一个纯文本消息。当用户首次登录到你的 FTP 服务器时，该消息将显示。在每个目录中，你可以创建一个 .message 文件。当用户进入该目录时，.message 文件的内容将被显示。与 welcome.msg 文件一样，.message 文件也应该是纯文本。

## 更改 FTP 登录问候语

当用户登录到你的 FTP 服务器时，他们会看到几段标准问候语。你可以通过在 /etc/ftpaccess 文件中添加信息来更改他们所看到的问候语及其包含的内容。

### 更改初始问候语

如果你不改变任何设置，登录到 FTP 服务器的用户不会看到太多信息。用户登录到你的 FTP 服务器时的默认问候语看起来像这样：

```
$ ftp maple
Connected to maple.
220 maple FTP server (Version wu-2.6.2-5) ready.
Name (maple:mike):
```

这就是完整的问候语。为了缩短用户看到的问候语，你可以在 /etc/ftpaccess 文件中如下设置问候语选项为 brief 或 terse：

```
greeting terse
```

terse 选项会在登录提示符之前显示较短的输出。这是一个示例：

```
$ ftp maple
Connected to maple.
220 FTP server ready.
Name (maple:mike):
```

### 更改 FTP 服务器主机名

通常，当有人连接到你的 FTP 服务时，系统的主机名会被显示。如果你想分配一个仅适用于连接到你的 FTP 服务器的特定主机名，你可以在 /etc/ftpaccess 文件中更改该名称。以下是你需要输入的行示例：

```
hostname ftpnine
```

下次 FTP 用户连接时，该用户将看到主机名为 ftpnine。

### 在登录前添加消息

如果你希望用户在连接到你的 FTP 服务后、在登录提示符出现前看到一条消息，你可以使用 /etc/ftpaccess 文件中的 banner 选项来实现。首先，你需要创建一个包含你要打印的消息的文本文件。然后，添加一行 banner 指向该文件（相对于系统根目录，而不是 FTP 相对根目录）。例如：

```
banner /etc/ftpbanner.msg
```

在此示例中，下次用户连接到 FTP 服务时，/etc/ftpbanner.msg 文件的内容将在连接消息之后、登录提示符出现之前显示。

## 控制 FTP 访问权限

你虽然开放计算机供公众访问，但这并不意味着你必须允许所有人滥用你的计算资源。在 /etc/ftpaccess 文件中，你可以准确定义哪些目录是可读和可写的。你可以限制同时访问你的 FTP 服务器的用户数量。你还可以为个人或群组设置资源权限或限制。以下部分描述了你的一些选项。

### 创建用户类

通过设置用户类，你创建了一种将不同资源访问权限分配给不同用户组的方法。任何不属于任何类的用户将无法访问你的 FTP 服务器。这就是为什么默认类包含所有用户，如下所示：

```
class       all     real,guest,anonymous      *
```

你需要做的第一件事是决定哪些用户组需要单独处理。一种有效的技术是将本地用户定义为一个类，将所有其他用户定义为另一个类。class 关键字允许你基于网络地址以及该地址内的用户类型（即 real、guest 或 anonymous）来分配类。例如，你可能希望为你的互联网域内的所有用户分配一组权限，并为其他人分配另一组权限。以下是操作方法：

```
class       home    real,guest,anonymous      10.0.0.0/8
class       world   real,guest,anonymous      *
```

在此示例中，来自网络号为 10.0.0.0（可能是你的本地网络）的主机地址的所有用户都被分配给“home”类。来自其他任何网络的用户被分配给“world”类。你可以使用域名代替网络号。

> **注意：** 网络地址后的 /8 是子网掩码的简写。它表示最左边的八位代表网络。因此，在此示例中，数字 10 代表网络号，接下来的三个八位组代表单个主机地址。

如前所述，定义在每个类中的用户类型由以下关键字之一表示：

- **real** — 适用于在本地计算机上拥有登录帐户的用户。
- **guest** — 适用于在 /etc/ftpaccess 文件中指定为 guestusers 或 guestgroups 的具有真实登录帐户的用户。
- **anonymous** — 适用于以任何匿名用户名登录的人。

分配了类名后，你可以为这些类中的任意一个分配限制或权限。

### 允许上传传入文件

默认情况下，匿名用户不被允许向你的 FTP 服务器上传文件。为了发生上传，你必须在 /etc/ftpaccess 文件中明确允许上传，使用 upload 参数。此外，还有特定参数涉及访客和匿名用户是否可以删除、覆盖、重命名文件或目录，或更改权限。（请记住，允许公共上传文件到 FTP 服务器可能存在严重的安全风险。）

### 开放目录用于上传

你需要向 /etc/ftpaccess 添加信息，以便 FTP 用户能够向你的 Red Hat Linux 系统上传文件。以下是两个使用 upload 参数允许 ftp 用户上传文件的示例：

```
upload  /var/ftp  /incoming  yes  mike  sales  0600
upload  /var/ftp  /testdir   yes  ftp   ftp    0666
```

这些示例使你能够向匿名用户的主目录（/var/ftp）中的 /incoming 和 /testdir 目录上传文件。用户对 /incoming 目录（及其子目录）的写权限是以用户 mike 和组 sales 的身份进行的。文件以 0600 权限写入（因此只有 mike 可以读取和写入文件）。在第二个示例中，使用 ftp 用户和组权限来创建文件，其读/写权限是开放的（0666）。

> **交叉引用：** 如果你不记得诸如 0666 和 0600 之类的权限设置意味着什么，请参阅第 3 章中关于访问权限的描述。这些是与 chmod 命令一起使用的常见选项，用于更改访问权限。

允许上传权限也允许这些用户拥有创建目录（在上传区域内）的权利。要禁止创建目录，在 upload 行的末尾（在权限数字之后）添加 nodirs 关键字。要在某个实例中启用创建目录的能力（如果它是关闭的），在行末尾添加 dirs 关键字。

upload 参数另一个有用的选项是 class 选项。class 选项允许你为特定类的用户设置上传权限。以下是使用 class 选项的示例：

```
upload  class=home  /var/ftp/incoming/local  yes  ftp  guest  0666
```

在此示例中，结合前面的示例，任何匿名用户都可以写入 /incoming 目录，但只有属于名为 home 的类的用户才能写入 /incoming/local 目录（位于 /var/ftp 目录内）。此情况下的权限
