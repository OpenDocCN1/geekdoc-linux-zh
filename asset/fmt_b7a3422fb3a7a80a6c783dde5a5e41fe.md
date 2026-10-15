
# FTP 服务器配置

## 欢迎信息设置

```
$ ftp maple
Connected to maple.
220 FTP server (Version wu-2.6.1(1) Mon Dec 25 09:21:53 EDT 2000) ready,
Name(maple:mike):
```

这是完整的欢迎信息。为了缩短用户看到的欢迎信息，你可以在 `/etc/ftpaccess` 文件中将欢迎选项设置为 `brief`（简短）或 `terse`（精简），如下：

```bash
greeting terse
```

`terse` 选项会在登录提示前显示短得多的输出。以下是一个示例：

```
$ ftp maple
Connected to pine.
220 FTP server ready.
Name(maple:mike):
```

## 修改 FTP 服务器主机名

通常情况下，当有人连接到你的 FTP 服务时，会显示系统的主机名。如果你想分配一个仅适用于连接到 FTP 服务器的特殊主机名，可以在 `/etc/ftpaccess` 文件中进行更改。以下是你需要输入的行示例：

```
hostname ftpppine
```

当 FTP 用户下次连接时，该用户将看到主机名为 `ftpppine`。

## 在登录前添加消息

如果你想在用户连接到 FTP 服务之后、登录提示之前显示一条消息，可以使用 `/etc/ftpaccess` 文件中的 `banner` 选项。首先，你需要创建一个包含你想要打印的消息的文件。接下来，添加一个指向该文件的 `banner` 行（相对于你的系统根目录，即 FTP 相对根目录）。例如：

```
banner /etc/ftpbanner.msg
```

通过这个示例，当用户下次连接到 FTP 服务时，`/etc/ftpbanner.msg` 文件的内容将在连接消息之后、在登录提示出现之前显示出来。

## 控制 FTP 访问

仅仅因为你向公众开放了计算机，并不意味着你必须让所有人滥用你的计算资源。在 `/etc/ftpaccess` 文件中，你可以精确定义哪些目录是可读和可写的。你可以限制同时访问你的 FTP 服务器的用户数量。你还可以为个人或组设置资源的权限或限制。接下来的章节描述了你的一些选项。

## 创建用户类

通过设置用户类（user classes），你创建了一种为不同用户组分配不同资源访问权限的方法。不属于任何类别的用户将无法访问你的 FTP 服务器。默认类包含以下行，涵盖所有用户：

```
class all      real,guest,anonymous *
```

你首先需要做的是决定你想单独处理哪些用户组。一种有效的技术是将本地用户定义为一类，将所有其他用户定义为另一类。`class` 关键字允许你根据网络地址和该地址内的用户类型（即 `real`、`guest` 或 `anonymous`）来分配类。例如，你可能想为你的互联网域范围内的所有用户分配一组权限，并为其他人分配另一组权限。具体方法如下：

```
class home      real,guest,anonymous  10.0.0.0/8
class world     real,guest,anonymous *
```

在这个示例中，所有来自网络号为 `10.0.0.0` 的主机计算机（推测是你的本地网络）的用户都被分配到“`home`”类。来自任何其他网络的用户都被分配到“`world`”类。你可以使用域名代替网络号。

> 网络地址随后的 `/8` 是子网掩码的简写。它表示最左侧的八位代表网络。在本示例中，数字 `10` 代表网络号，接下来的三个字节代表单个主机地址。

如前所述，在每个类中定义的用户类型由以下关键字之一表示：

- `real`—对于在本地计算机上拥有登录账户的用户。
- `guest`—对于在 `/etc/ftpaccess` 文件中指定为客用户或客组的拥有真实登录账户的用户。
- `anonymous`—对于任何以匿名用户名登录的人。

在分配了类名后，你可以为这些任何一类分配限制或权限。

## 允许上传传入的文件

默认情况下，匿名用户不允许向 FTP 服务器上传文件。要进行上传操作，你必须在 `/etc/ftppass` 文件中使用 `upload` 参数显式允许上传。此外，特定参数处理客用户和匿名用户是否可以删除、覆盖、重命名或更改文件和目录的权限。（请记住，允许向你的 FTP 服务器公共上传文件可能会带来重的安全风险。）

## 开放目录用于上传

你需要向 `/etc/ftpaccess` 添加信息，以允许 FTP 用户向你的 Red Hat Linux 系统上传文件。以下是使用 `upload` 参数允许上传的两个示例：

```
upload /var/ftp /incoming yes mike sales 0600
upload /var/ftp /testdir yes ftp ftp 0666
```

这些示例允许你向匿名用户根目录（`/var/ftp`）下的 `/incoming` 和 `/testdir` 目录上传文件。写入 `/incoming` 目录（及其子目录）所需的权限属于用户 `mike` 和组 `sales`。文件以 `0600` 权限写入（因此只有 `mike` 可以读取和写入文件）。在第二个示例中，使用了 `ftp` 用户和组权限来创建文件，并且其读写权限是开放的（`0666`）。

如果你不记得 `0666` 和 `0600` 等权限设置的含义，请参考第 3 章中关于访问权限的描述。这些是常见的。要禁止创建目录，请在末尾添加 `nodirs` 关键字。`upload` 的另一个有用选项是 `class`。`class` 选项允许你为特定类设置权限。示例如下：

```
upload class=/var/ftp /incoming yes
```

在这个示例中，尽管你限制了从 `/incoming` 目录的下载，但现在允许 `world` 类用户下载 `/incoming`。在这种情况下，权限是开放的（`0666`）。

## 第四部分 Red Hat Linux 网络与设置

仅仅使用 `upload` 并不足以确保匿名用户可以向你的 FTP 服务器上传文件。Red Hat Linux 文件和目录的所有权同样适用。例如，如果 `incoming` 目录归 `root` 所有，`700` 权限将不允许，但 `777` 权限则可以。

## 防止文件或目录被检索

使用 `retrieve` 参数，你可以防止特定名称的文件或特定目录的文件被检索。以下是一些示例：

```
noretrieve relative class=world /pub/homestuff
noretrieve absolute /etc/hosts /etc/inittab
noretrieve money
```

在这些示例中，`relative` 和 `absolute` 是关键字，指示文件和目录是相对于 FTP 用户目录（例如 `/var/ftp`）还是相对于系统根目录的绝对路径。第一行表示 `world` 类的任何用户无法检索 `/pub/homestuff` 目录。第二行表示系统的 `/etc/hosts` 和 `/etc/inittab` 文件无法检索。当没有指定路径时，无论匹配的文件位于文件系统的何位置都无法下载。

## 允许文件或目录被检索

如果你使用 `retrieve` 参数阻止了一组文件被检索，你可以使用 `all-retrieve` 参数选择性地允许某些文件和目录被检索。这是一个示例：

```
all-retrieve relative class=world /pub/homestuff/publicfile.txt
```

## 允许权限能力

即使在你允许了用户或用户类向你的 FTP 服务器上传文件后，你仍然对写入和更改文件的某些方面具有某种程度的控制。这些权限能力中的每一个都可以匿名、客或真实用户开启或关闭。你可以为特定的用户类开启或关闭它们。以下是几个示例。默认情况下，当用户拥有上传能力（即写入 FTP 服务器的能力）时，所有这些服务都是开启的。

## 第 20 章 设置 FTP 服务器 723

请记住，无论这些权限能力如何设置，Red Linux 所有权权限仍然适用于文件和目录。例如，如果你被允许使用 `chmod`，你仍然无法使用它来更改他人设置为 `0600` 的文件的权限。

## 启用 chmod

你可以使用 `chmod` 参数来设置用户是否可以更改与文件目录关联的权限。将 `chmod` 设置为 `yes`（允许）或 `no`（禁止）。然后你可以添加一个用逗号分隔的关键字列表，来选择分配权限的用户。以下是一个示例：

```
chmod yes guest,class=home
chmod no anonymous
```

在此示例中，所有访客用户都允许在他们允许上传文件的目录中使用 `chmod` 命令。然而，匿名用户不允许使用 `chmod` 命令更改文件和目录的权限。

## 启用删除

要允许具有 Linux 所有权权限的用户删除文件，请使用 `delete` 参数。这是一个示例：

```
delete yes class=home
delete no anonymous,guest
```

此示例允许任何属于 `home` 类的用户执行删除操作。然而，不允许不允许属于该类的匿名用户或访客用户执行删除。
