
## 创建目录并安装字体

以下行对于支持 Adobe Type 1 字体是必需的：

`Load "type1"`

以下行对于支持 TrueType 字体是必需的：

`Load "freetype"`

上述行必须位于 `XF86Config` 中以下标题之下：

`Section "Modules"`

您还需要确保在 `Files` 部分中存在适当的字体目录，以容纳新字体。

查找 `XF86Config` 中以 `FontPath` 开头的行。如果您正在安装 TrueType 字体，我建议在文件中的最后一个 `FontPath` 语句之后添加以下行，以容纳所有的 TrueType 字体：

`FontPath "/usr/X11R6/lib/X11/fonts/TrueType/"`

添加此行后，保存文件并退出编辑器。

现在，您必须创建该目录。以 root 身份执行以下命令：

`mkdir /usr/X11R6/lib/X11/fonts/TrueType`

该命令为 TrueType 字体创建目录。

当字体目录准备就绪后，将您想要添加的字体的字体文件复制到相应的目录中。Type 1 字体应复制到 `/usr/X11R6/lib/X11/fonts/Type1`，而 TrueType 字体应复制到 `/usr/X11R6/lib/X11/fonts/TrueType`。字体只需要读访问权限，因此您可能需要更改字体的权限，使所有人都只有读权限。您可以使用以下命令完成此操作：

`chmod 444 fontname`

这里，`fontname` 当然是您刚安装的字体名称。（请确保您当前位于正确的字体目录中。如果需要有关基本 shell 命令和目录导航的帮助，请参阅第 7 章“使用 Shell”。）

接下来，您必须运行几个程序以正确设置字体。

要设置 TrueType 字体，您需要程序 `ttmkfdir`。它在 FreeBSD 端口集合中可用，位于 `x11-fonts` 目录下。要设置 Adobe Type 1 字体，您需要程序 `type1inst`，它也可在 FreeBSD 端口集合的 `x11-fonts` 目录下找到。有关如何从端口集合安装软件的信息，请参阅第 14 章。

在您将字体复制到相应目录后，确保您在该目录中，并在命令提示符下输入以下命令之一。

对于 TrueType 字体：

```
ttmkfdir > fonts.scale
```

对于 Adobe Type 1 字体：

```
type1inst > fonts.scale
```

现在您必须再运行一个命令；`mkfontdir` 命令识别新字体并将它们添加到字体配置文件中。要设置可缩放字体（如 Type 1 和 TrueType），您需要使用 `-e` 选项运行该命令。再次确保您位于复制字体的目录中，然后从提示符发出以下命令：

```
mkfontdir -e /usr/X11R6/lib/font/encodings
```

接下来，重启 X-Windows（如果您当前正在其中），新的字体即可供使用。

> **注意**
>
> 每当您向系统添加新字体时，必须重复 `ttmkfdir` 或 `type1inst`，然后执行 `mkfontdir` 过程。

## 使用远程 X-Windows 客户端

由于 X-Windows 的设计，应用程序可以在主机上运行，并将其输出和输入重定向到远程主机。使用远程客户端在某些情况下非常有用，例如，如果服务器上有图形应用程序，而您需要从工作站控制它们。从某种程度上说，这种远程使用类似于简单地使用 Telnet 或 SSH 登录远程系统，然后运行基于文本的应用程序。应用程序实际上是在服务器上运行的；输出和输入只是被发送到您的系统。X-Windows 将此概念扩展到图形应用程序以及基于文本的应用程序。但是，此功能默认是禁用的，在使用之前需要启用它。

使用远程客户端时令人困惑的一点是，在处理 X-Windows 时，客户端和服务器的术语是相反的。在网络术语中，您认为客户端是运行位于另一个称为服务器的系统上的应用程序的主机。然而，在 X-Windows 中，服务器运行在本地系统上，而客户端位于远程系统上。基本上，X-Windows 中的客户端是在 X-Windows 系统下运行的任何程序。为了更加令人困惑，您的 X-Server 可能正在运行位于远程系统的客户端，而该客户端实际上是一个服务器。例如，您可能将位于远程系统的图形数据库管理客户端加载到您的 X-Server 上。在这种情况下，您的客户端位于远程系统，但该远程系统是一个数据库服务器。

为了使这些正常工作，您希望显示远程 X-Windows 应用程序的输出并控制其输入的系统必须运行一个 X-Server。然而，X-Server 不必在同一类型的系统上。X-Server 可以运行在另一个 FreeBSD 系统、Linux 系统、Solaris 系统或 Mac OS X 系统上。系统甚至不必是基于 Unix 的系统。有适用于 Windows 的 X-Server 可以显示在 FreeBSD 上运行的远程 X 应用程序。目前，其中大部分是商业软件。但 Xfree86 正在移植到 Windows，因此很快就会有适用于 Windows 系统的免费 X-Server 可用。

默认情况下，您的 X-Server 不允许远程应用程序显示在您的屏幕上。有几种常见的方法来允许此行为。最常见但也是安全性最低的方法是使用 `xhost`。

### 使用 xhost 允许显示远程应用程序

`xhost` 允许在不同系统上运行的远程应用程序在您的本地系统上显示，并从您的系统获取输入。要查看当前的 `xhost` 配置设置，请输入不带参数的 `xhost`。默认的 `xhost` 配置将返回以下内容：

```
bash$ xhost
access control enabled, only authorized clients can connect
bash$
```

在这种情况下，只有在该系统的授权列表中出现的、在远程系统上运行的应用程序才允许在此系统上显示。此外，当前列表为空，意味着当前没有客户端被授权将显示发送到该系统。

如果您希望能够在名为 `lion` 的主机上运行远程应用程序，您需要将其添加到授权列表。为此，请使用以下命令：

```
bash$ xhost +lion
lion being added to access control list
bash$
```

如果您现在不带任何参数输入 `xhost`，系统将响应如下：

```
access control enabled, only authorized clients can connect
INET:lion.samplenet.org
```

远程主机 `lion` 现在可以在本地系统上显示其 X-Windows 应用程序。

这种设置的问题在于，`lion` 上拥有账户的任何人可以将显示发送到您的系统。在有不可信用户的环境中，这可能是一个主要的安全问题。因此，在这些环境中使用 `xhost` 不是一个好主意。还有其他更安全的可用方法。这些方法将在本章后面简要讨论。

此外，如果您使用 `xhost`，最好在需要之前仅授权主机，并在完成对远程应用程序的工作后尽快撤销授权。要从主机撤销授权，您可以使用如下命令：

```
bash$ xhost -lion
lion being removed from access control list
bash$
```

远程主机 `lion` 无法再在此系统上显示应用程序。

还有一种方法可以完全禁用 `xhost` 中的访问控制，以便任何客户端都可以连接到系统。这可能永远不是一个好主意，因为它是一个严重的安全隐患。但如果出于某种原因您想这样做，可以使用以下命令：

```
bash$ xhost +
access control disabled, clients can connect from any host
bash$
```

要重新启用访问控制，请输入 `xhost -`。系统将响应如下：

```
access control enabled, only authorized clients can connect
```

> **警告**
>
> 由于 `xhost` 涉及的安全隐患，至少您希望配置防火墙以阻止内部网络之外的未经授权用户访问 `xhost` 使用的端口。`xhost` 使用 6000 到 6063 端口。有关配置防火墙的更多信息，请参阅第 29 章“网络安全”中的“配置防火墙”部分。

在配置系统以允许远程应用程序在其上显示之后，您需要连接到远程系统并启动应用程序。您可以通过 Telnet、SSH 或 `rlogin` 完成此操作（如果远程系统支持从您的系统使用 `rlogin`）。

