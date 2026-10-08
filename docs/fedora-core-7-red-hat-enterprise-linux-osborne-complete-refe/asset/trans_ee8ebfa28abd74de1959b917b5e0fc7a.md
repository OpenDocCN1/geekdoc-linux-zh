

`/etc/samba/smb.conf` 文件存储了各个共享资源的配置，以及适用于所有资源的全局选项。Linux 会在你的 `/etc/samba` 目录中安装一个 **smb.conf** 文件。该文件包含用于你的发行版的默认设置。你可以编辑该文件以根据你自己的需求自定义配置。许多条目都使用分号或 # 符号进行了注释，你可以移除开头的注释符号使其生效。除了直接编辑文件外，你可能还希望使用 SWAT 配置实用工具，它提供了一个易于使用的全屏 Web 页面界面，用于输入共享资源的配置。SWAT 配置实用工具还提供大量帮助功能和文档。有关 Samba 配置参数的完整列表，请查看 **smb.conf** 的手册页（Man page）。`/usr/share/doc/samba*` 目录下的 examples 子目录中提供了一组详尽的 **smb.conf** 文件示例。

在 **smb.conf** 文件中，首先设置全局选项，然后依次是每个共享资源的配置。**smb.conf** 文件的基本组织单元称为*节*（section）。每个资源都有一个独立的节，其中包含其服务名称及其属性的定义。即使是全局选项也放置在一个单独的节中，标记为 **global**。例如，每个用于文件共享的节由目录和允许文件空间用户访问的权限组成。每个共享的节以共享资源的名称标记。特殊的节，称为 **printers** 和 **homes**，为在 Samba 服务器上可访问的用户目录和打印机提供默认描述。在特殊节之后，输入特定服务的节，即对特定目录或打印机的访问。

一个节以一个由方括号括起来的共享资源名称组成的节标签开始。除了特殊节外，节标签可以是您想赋予的任何名称。在节标签之后，在不同的行中输入该服务的不同参数。参数定义了要授予服务用户的访问权限。例如，对于目录，你可能希望它是可浏览的，但只读，并使用特定的打印机。参数以 *参数名* = *值* 的格式输入。你可以在注释行的开头放置分号来输入注释。

下面是一个简单的节配置示例。节标签由方括号括起，后面跟着两个参数条目。**path** 参数指定允许访问的目录。**writable** 参数指定用户是否对该目录及其文件空间具有写访问权限。

```
[mysection]
path = /home/chris
writable = true
```

打印服务具有相同的格式，但需要某些其他参数。path 参数指定打印机 spool 目录的位置。**read-only** 和 **printable** 参数设置为 **true**，表示该服务是只读且可打印的。**public** 表示任何人都可以访问它。

```
[myprinter]
path = /var/spool/samba
read_only = true
printable = true
public = true
```

参数条目常常是同义的，但具有相同含义的不同条目。例如，`read only = no, writeable = yes` 和 `write ok = yes` 都表示同样的意思，即向用户提供写访问权限。`public` 参数是 `guest ok` 的同义词。SWAT 将使用 `guest ok` 代替 `public`，并使用 `read only` 代替 `writeable`。

## SWAT 和 smb.conf

SWAT 是一个基于网络的 Samba 配置工具，使用 Web 页面界面来让你配置 **smb.conf** 文件。SWAT 是配置 Samba 服务器的一种简单方法，提供全范围的配置选项，而不是 system-config-samba 提供的默认选项。SWAT 提供了一个易于使用的 Web 页面界面，带有按钮、菜单和文本框，用于输入值。顶部一个简单的按钮栏允许你选择要配置的节。还有一个按钮栏用于添加密码。要查看 **smb.conf** 文件在 SWAT 更改时的内容，请单击“View”。初始屏幕（HOME）显示 Samba 文档的索引。SWAT 的一个更有用的功能是其上下文敏感帮助。对于 SWAT 显示的每个参数和选项，你可以单击“Help”按钮来显示该选项的详细解释及其使用示例。

### 激活 SWAT

SWAT 通常随 Samba 一起安装。SWAT 是一个 xinetd 服务。作为 xinetd 服务，它将列在 `/etc/services` 和 `/etc/xinetd.d/swat` 文件中。SWAT 程序使用端口 **901**，如 `/etc/services` 文件中指定并在此处所示：

```
swat 901/tcp # Samba Web Administration Tool
```

作为 xinetd 服务，SWAT 将在 `/etc/xinetd.d` 目录中拥有自己的 xinetd 文件，即 `/etc/xinetd.d/swat`。SWAT 默认处于关闭状态，其 **disable** 选项设置为 **yes**。要使用 SWAT，你必须将 **disable** 选项更改为 **no**，如下所示：

```
# default: off
# description: SWAT is the Samba Web Admin Tool. Use swat \
#     to configure your Samba server.  To use SWAT, \
#     connect to port 901 with your favorite web browser.
service swat
    disable = no
    port    = 901
    socket_type     = stream
    wait    = no
    only_from       = 127.0.0.1
    user    = root
    server  = /usr/sbin/swat
    log_on_failure += USERID
}
```

你可以通过使用 `chkconfig` 或 Service Configuration 工具来开启 SWAT 服务，或者手动编辑 `/etc/xinetd.d/swat` 文件并将 **disable** 选项更改为 no 来完成此操作。**chkconfig** 会为你编辑 */etc/xinetd.d/swat* 文件，进行此更改（有关 **chkconfig** 的更多信息，请参见第 21 章）。以下示例展示了如何使用 **chkconfig** 命令启用 SWAT：

```
chkconfig swat on
```

使用 **chkconfig** 时，你不需要手动重启 xinetd 服务器。但是，如果你手动编辑文件，你也必须重启服务器才能使更改生效。你可以简单地使用 **xinetd** 脚本来做到这一点，如下所示：

```
service xinetd restart
```

在使用 SWAT 之前，备份你当前的 **smb.conf** 文件。SWAT 会覆盖原始文件，用自己的较短且更简洁的版本替换它。最初安装的 **smb.conf** 文件列出了大量选项，并附有详细的解释。这是一个很好的学习工具，包含创建各种类型的打印机和目录节的优秀示例。只需创建一个备份副本：

```
cp /etc/samba/smb.conf /etc/samba/smb.bk
```

### 访问 SWAT

你可以通过打开浏览器并输入 IP 地址 127.0.0.1 和端口 901 来启动 SWAT。

```
http://127.0.0.1:901
```

你可以使用 **localhost.localdomain** 代替 127.0.0.1。

```
http://localhost.localdomain:901
```

你可以通过在 Web 浏览器中输入运行它的 Samba 服务器的地址及其端口（901）来从远程位置启动 SWAT。但是，你必须首先在此 */etc/xinetd.d/swat* 文件中启用此功能。目前，此文件中的 **only_from** 行将访问限制为仅限 localhost。要启用来自任何远程系统的访问，只需删除此行。如果你想为特定的某些主机提供访问权限，你可以在 **only_from** 行的 127.0.0.1 之后列出它们。务必在任何更改后重启 SWAT。以下示例启用了来自 127.0.0.1 和 **rabbit.mytrek.com** 的访问：

```
only_from 127.0.0.1 rabbit.mytrek.com
```

在远程系统的 Web 浏览器中输入以下 URL，然后会在 **turtle.mytrek.com** Samba 服务器上显示 SWAT 的 Web 页面界面：

```
http://turtle.mytrek.com:901
```

首先要求你输入用户名和密码。要配置 Samba，你需要输入 **root** 和 root 密码。（如果你是从远程系统连接，则*不建议*以明文输入 root 密码——参见第 29 章。）

