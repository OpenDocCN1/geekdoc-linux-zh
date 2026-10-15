
此行允许`swatd`运行。如有必要，执行重启`inetd`的命令使其重新读取配置：

```
$ sudo /etc/init.d/openbsd-inetd restart
```

* Restarting superserver `inetd`

现在你可以运行`swat`了：从本地系统启动浏览器并在地址栏中输入`127.0.0.1:901`或`localhost:901`。在提示时输入你的用户名和密码。（必须设置`root`密码才能使用`swat`修改`Samba`配置；请查看第 415 页）。如果你提供了`root`的用户名，你将能够查看信息但无法进行更改。从远程系统，将`127.0.0.1`替换为服务器的IP地址（但请查看安全提示）。如果本地系统运行着防火墙且你想从远程系统访问`swat`，请使用`firestarter`（第 832 页）打开`TCP`端口`901`。

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_818_0.png)

# 设置 Samba 服务器

当你安装`swat`时，它会创建`smb.conf`的副本（第 770 页）。

# 欢迎使用 SWAT！

请通过按钮选择配置操作：

- 守护进程
  - `smbd`: `SMB`守护进程
  - `bind`: `NetBIOS`服务器
  - `swatd`: 控制守护进程
- 文件
  - `smb.conf`: `Samba`配置文件
  - `hosts`: `NetBIOS hosts`文件
  - `smbpasswd`: `SMB`密码文件
- 管理工具

图 23-3 本地`swat`主页

浏览器显示本地`Samba`主页（图 23-3）。此页面包含本地`Samba`文档链接以及下一页列出的按钮。

# 不要允许未加密的远程访问 swat

允许在不安全网络上从远程系统访问`swat`。当你这样做并登录时，`root`密码将以明文形式通过你使用的任何连接发送，并很容易被嗅获。如果你想在不安全网络上访问`swat`，请使用`ssh`转发端口`901`（第 645 页）。

# 第 23 章 SAMBA：LINUX 与 WINDOWS 的文件和打印机共享

`HOME`链接到本地`Samba`文档。当你点击`Samba`单词（注意不是图标，而是`Samba/swat`主页上`Documentation`单词之前的那个）时，`swat`会显示`Samba`的`man`页面，该页面定义了每个`Samba`程序。

`GLOBALS`编辑`smb.conf`中的全局参数（变量）。

`SHARES`编辑`smb.conf`中的共享信息。

`PRINTERS`编辑`smb.conf`中的打印机信息。

`WIZARD`重写`smb.conf`文件，移除所有注释和指定默认值的行。

`STATUS`显示激活的连接、激活的共享和已打开的文件。停止并重启`smbd`和`nmbd`守护进程。

`VIEW`显示由`smb.conf`中的默认值和设置确定的配置参数子集（点击`Full View`全全视图）或全部（点击`Normal View`正常视图）。

`PASSWORD`管理`Samba`密码。

建立基础`Samba`设置非常简单，这样你就可以从`Windows`系统处理`Linux`目录层次结构。要设置安全连接或使用特殊功能则需要更多工作。以下示例基于`Ubuntu Linux`自带的`smb.conf`文件创建了一个基础设置。

`swat`帮助每个`swat`默认参数旁边都有一个标记为`Next`的按钮。点击`Help`将打开一个新浏览器窗口，其中包含对参数的说明。每个参数都有一个`Set Default`按钮，可以将参数设置为默认值（不一定是`Ubuntu`提供的初始值）。

对于此示例，请勿点击任何`Set Default`。在页面上进行更改并在点击页面顶部菜单按钮之前，确保点击每个页面顶部的`Commit Changes`（提交更改）。否则，`swat`将丢弃你的更改。

`GLOBALS`页面要按照此操作，请先点击`Samba/swat`主页顶部的`GLOBALS`。保持所有内容为当前设置，有两个例外：`allows host`（允许的主机）和`hosts deny`（拒绝主机）。设置这些参数可以通过限制`Samba`响应的客户端来使服务器更安全。滚动到`Security Options`（安全选项）底部，将`allows host`设置为你想要访问本地系统共享和打印机的名称或`IP`地址。如果`allows host`中有任何地址，或者`hosts deny`设置为`ALL`，你必须同样在`allows`中添加`0.0.0.0`，以便可以使用带有空格和逗号的各种页面。更多信息见第 771 页。完成`GLOBALS`页面后点击页面顶部附近的`Changes`（更改）。

`SHARES`下一步点击顶部的`SHARES`。页面底部会出现两个按钮和两个框（图 23-4）。在`Create Share`按钮旁边的文本框中，输入你想要分配给该共享的名称。当你从`Windows`映射（挂载）共享时，将使用此名称。点击`Create Share`。要修改现有共享，点击标记为`Create Share`的下拉列表中的共享名称，然后点击`Create Share`。这些任一操作都会扩展`Share Parameters`（共享参数）页面，显示有关所选共享的信息。

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_819_0.png)

# 设置 SAMBA 服务器

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_820_0.png)

图 23-4 共享参数页面

# 如果无法再次使用 swat

如果你无法再次使用`swat`，可能是错误地更改了`hosts allow`设置。在这种情况下，你可能需要手动编辑`/etc/samba/smb.conf`并修复包含`hosts allow`单词的行：

```
# grep hosts smb.conf

hosts allow = 0.0.0.0, 192.168.0.8

hosts deny = ALL
```

前面的条目仅允许来自`192.168.0.8`的访问。它们也允许`swat`工作。在更改`smb.conf`后不需要重启`Samba`。

将`path`设置为`Linux`服务器上共享的绝对路径，并将`comment`设置为有助于你记住共享所在位置的字符串。`hosts allow`和`hosts deny`的值取自全局参数。确保`read only`、`guest ok`和`browsable`按你的意愿设置。`Available`必须设置为`YES`，否则你将无法访问该共享。完成`SHARES`页面后点击`Commit Changes`。如果你想查看有多少参数，点击页面顶部的`Advanced`。

# 手动配置 SAMBA 服务器

`smb.conf`文件控制`Samba`工作的大多数方面。以下内容分为几个章节：

## GLOBALS

- `interfaces` `Samba`使用的网络以空格分隔的列表。以接口名称（如`eth0`）或`IP`地址/掩码对的形式指定（第 445 页）。
- `server` `Windows`消息在多处显示的字符串。在字符串内部，`Samba`将`%v`替换为`Samba`版本号，将`%h`替换为主机主机名。
- `workgroup` 服务器所属的工作组。设置为与使用此服务器的`Windows`客户端相同的工作组。

## SECURITY

- `encrypt` 设置`YES`仅接受客户端的加密密码。`Windows 98`和`NT 4.0 Service Pack 3`默认使用加密密码。此参数使用`smbpassword`进行身份验证，除非你将`security`设置为`SERVER`或`DOMAIN`，在这种情况下`Samba`将使用另一个服务器进行身份验证。
- `guest account` 分配给以访客身份登录或映射为访客的用户用户名；仅当`guest`（第 776 页）设置为`YES`时有效。此用户名应存在于`/etc/passwd`中，但不应能够登录系统。通常`guest account`被分配为`nobody`，因为`nobody`账户可以访问文件。如果你在`Linux`系统上将`nobody`账户用于用途，请将此参数设置为除`nobody`的名称。
- `hosts allow` 类似于`/etc/hosts.allow`（第 448 页）；指定允许连接服务器的主机。覆盖`hosts deny`。一种很好的策略是在`hosts deny`中指定`ALL`，并在文件中指定你想要授予访问的主机。以与`hosts allow`相同的方式指定。
- `hosts deny` 类似于`/etc/hosts.deny`（第 448 页）；指定不允许连接服务器的主机。被`hosts allow`覆盖。如果你在此文件中指定`ALL`，请在`hosts allow`中包含本地系统 (`127.0.0.1`)。以与`hosts deny`相同的方式指定。
- `invalid users` 不允许使用`Samba`登录的用户

## SHARES

- `name` 你想要分配给该共享的名称。当你从`Windows`映射（挂载）共享时，将使用此名称。
- `comment` 有助于你记住共享所在位置的字符串。
- `path` `Linux`服务器上共享的绝对路径。
- `read only` 共享是否为只读。
- `guest ok` 访客是否无需密码即可访问共享。
- `browsable` 共享是否在`Samba`网络浏览器中可见。
- `limit` 访问该共享的最大用户数。

## PRINTERS

- `name` 打印机共享的名称。
- `device` 打印机设备的路径（例如`/dev/lp0`）。
- `comment` 有助于你记住打印机位置的注释字符串。
- `valid` 打印机当前可用。
- `browsable` 打印机是否在`Samba`网络浏览器中可见。
- `printer` `CUPS`看到的打印机名称。
- `queue` 打印机的`CUPS`队列名称。
- `shared` 打印机是否共享。
- `coment` 访客用户是否可以向打印机打印。
- `path` 打印池程序程序的路径。
- `spool` 打印池程序目录路径。

# 772 第23 章 SAMBA：LINUX 和 WINDOW 文件与打印机共享

`map guest` 定义了登录失败时何时映射到访客账户。当安全（第 772 页）未设置为`SHARE`时非常有用。

- `Never`: 仅当用户显式提供`guest`作为用户名并留空密码时，才允许访客登录。

- `Bad User`: 将任何尝试以不存在的用户身份登录的操作均视为访客登录。此参数存在安全风险，因为它允许恶意用户快速获取系统上的用户列表。

- `Bad Password`: 对于任何输入错误密码的用户，静默地以访客身份登录。此参数可能会让忘记密码的用户感到困惑，因为她会在不知情的情况下以访客身份登录，并突然发现可见的共享资源比平时少了。

`Default`: `Never`

`Ubuntu`: `Bad User`

`passwd backend` 指定`Samba`存储密码的方式。设置为`ldaps`用于`LDAP`，`smbpasswd`用于`Samba`，或`tdbsam`（易用数据库）密码存储。参阅第 766 页关于使用`smbpasswd`更改`Samba`密码的说明。

`Default`: `smbpasswd`

`Ubuntu`: `tdbsam`

`passwd chat` `Samba`在调用`passwd`程序时使用的图表脚本。如果不遵循此脚本，`Samba`将不会转换密码。仅在`unix sync`（第 773 页）设置为`YES`时使用。

```
Default: *password* %n*new*password* %n\n*changed*

Ubuntu: *Enter\s\*password:* %n\n*Retype\s\*password:* %n\n*#password*updatedsuccessfully.*
```

`passwd program` `Samba`用于设置`Linux`密码的程序。`Samba`将`%u`替换为用户的用户名。

`Default`: `none`

`Ubuntu`: `/usr/bin/passwd %u`

`security` 定义客户端何时以及如何将用户名和密码信息传输到服务器。选择以下选项之一：

- `USER`: 导致`Samba`在用户在`Samba`服务器上登录时，要求`Windows`用户提供用户名和密码。使用此设置，你可以使用：
  - `usname map`（第 773 页）将`Samba`用户名映射到`Linux`用户名
  - `encrypt passwords`（第 771 页）对密码加密（推荐）
  - `guest account`（第 771 页）将用户映射到访客账户

- `SHARE`: 导致`Samba`不按用户对客户端进行身份验证。相反，`Samba`使用`Windows 9x`设置，其中每个共享可以为读取或完全访问设置单独的密码。此选项与更多版本的`Windows`不兼容。

- `SERVER`: 导致`Samba`使用另一种`SMB`方法来验证用户名和密码。如果远程验证失败，本地`Samba`服务器将尝试像安全设置为`USER`那样验证用户名和密码。

- `DOMAIN`: `Samba`将加密的密码传递给`Windows NT`域控制器进行验证。要使`DOMAIN`起作用，必须在`smb.conf`中正确设置`workgroup`参数（第 771 页）。

- `ADS`: 指令`Samba`使用`Active Directory`（活动目录）服务器进行身份验证，允许`Samba`服务器作为原生`Active Directory`成员参与。（`Active Directory`是`Windows 2000`及更高版本使用的集中式信息系统。它取代了`Windows NT`及早期版本使用的`Windows`域。）

`Default`: `USER`

`unix password` `YES` 导致当关联用户更改`Samba`密码时，`Samba`更改该用户的`Linux`密码。

`Default`: `NO`

`Ubuntu`: `YES`

`update` `YES` 允许用户从明文密码迁移到加密密码——而无需在服务器上登录（前提是设置为`YES`且`encrypt passwords`设置为`NO`）。当每个用户在服务器上使用明文`Linux`密码登录时，`smpasswd`会加密并存储密码。在用户转换后，将其设置为`NO`并加密`passwords`设置为`YES`。

`Default`: `NO`

`username map` 映射文件名（通常为`/etc/samba/smusers`），用于将`Windows`客户端的用户名映射到`Linux`服务器上的用户名。此参数仅在安全（第 772 页）设置为`USER`时有效。文件的每行以服务器（`Linux`）用户名开头，后紧跟一个空格、一个等号、另一个空格以及一个或多个空格分隔的客户端（`Windows`）用户名。星号 (`*`) 匹配任何客户端用户名。

此文件经常将`Windows`用户名映射到`Linux`用户名，以便文件共享。以下是一个示例文件：

```
$ cat /etc/samba/smusers

# Unix_name SMB_name ...

root = admin

guest = pcguest
```
