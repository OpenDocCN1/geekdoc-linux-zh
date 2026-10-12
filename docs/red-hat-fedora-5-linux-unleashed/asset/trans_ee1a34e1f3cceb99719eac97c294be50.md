
地址、访问的新闻组以及使用的身份验证方法类型。身份验证部分的语法如下：

```text
auth name {
    hosts: hostlist
    auth: auth-program
    res: res-program
    default: defuser
    default-domain: defdomain
}
```

**name** 值用作标签，以唯一标识该身份验证定义。身份验证定义使用参数和值来识别其操作。**hosts** 参数使用 **hostlist** 值来标识由该身份验证定义覆盖的各个远程主机。这些可以通过使用主机名或数字 IP 地址，以及匹配的通配符字符来列出。

你可以使用 **res** 参数来指定一个身份验证程序，根据连接的详细信息来验证该连接。或者，你可以使用 **auth** 参数来指定一个身份验证程序，该程序可以使用用户 ID/密码对来验证连接。如果你有兴趣对远程新闻服务器进行身份验证，你应该查阅 INN 文档，因为这是一个相当复杂的过程。

访问定义定义了针对特定新闻阅读器群体的访问限制类别和权限。访问定义的语法如下：

```text
access name {
    users: identity-wildmat
    newsgroups: group-wildmat
    access: permissions
}
```

**name** 值必须与相应的身份验证定义匹配。在访问定义中定义的参数仅适用于相应身份验证定义中定义的主机。**users** 参数将访问规则限制为值中列出的特定用户组。如果不存在 **users** 参数，则访问规则适用于所有用户。**newsgroups** 参数定义了该组可以访问哪些新闻组，而 **access** 参数定义了该组拥有哪些访问权限。权限定义如下：

- R—允许只读访问。
- P—允许发布文章。
- A—允许发布经过审核的文章（使用版主）。
- N—允许使用 NEWSNEWS 命令。
- L—允许向设置为禁止本地发布的新闻组发布内容。

以下是一个示例 readers.conf 文件，它允许所有本地新闻阅读器读取并向所有新闻组发布文章。

```
# readers.conf
auth "localhost" {
    hosts: "localhost, 127.0.0.1, 192.168.1.100, stdin"
    default: "<localhost>"
}

access "localhost" {
    users: "<localhost>"
    newsgroups: "*"
    access: RPA
}
auth "locallnet" {
    hosts: "192.168.*"
    default: "<user>"
    default-domain: "isp.net"
}

access "locallnet" {
    users: "*@isp.net"
    newsgroups: "*"
    access: "RP"
}
```

此处展示的示例 readers.conf 文件定义了两个不同的用户组。第一个组称为 localhost，它允许本地主机、地址 127.0.0.1、地址 192.168.1.100（本地主机的网络地址）以及任何使用标准输入的连接到新闻服务器。Fedora 提供的未修改的 readers.conf 文件仅允许本地主机上的用户访问。

第二个组定义了位于 192.168. 网络上的任何客户端；它允许网络上的任何客户端读取和发布所有新闻组。你可以根据网络需要调整这些地址。

## active 和 newsgroups 文件

active 和 newsgroups 文件虽然未被明确标识为配置文件，但对于新闻服务器的运行至关重要。这些文件控制你的新闻服务器可以处理哪些新闻组。新闻服务器处理的每个新闻组都必须在 active 和 newsgroups 文件中有一个条目。如果通过使用 Fedora RPM 包安装，这两个文件都位于 /var/lib/news 目录中。

active 文件的语法如下：

```
newsgroup	first	last	post
```

新闻服务器处理的每个新闻组都在 active 文件的单独一行中定义。默认的 Fedora INN 配置提供了一个骨架 active 文件，该文件定义了多个特殊新闻组：

```
control 0000000000 0000000001 n
control.cancel 0000000000 0000000001 n
control.checkgroups 0000000000 0000000001 n
control.newgroup 0000000000 0000000001 n
control.rmgroup 0000000000 0000000001 n
junk 0000000000 0000000001 n
```

如果你正在运行独立新闻服务器，这个默认文件就足够了。该文件的第一个字段定义新闻组名称。第二个和第三个字段定义第一篇和最后一篇文章的序列号。最后一个字段定义是否允许在该新闻服务器上对该新闻组进行发布。默认新闻组设置为 n 以防止发布。

control 和 control.cancel 新闻组用于接收 NNTP 控制文章，以便在新闻服务器上执行维护。随着远程站点创建新的新闻组并删除旧的新闻组，控制文章会被发送到新闻服务器以执行这些任务。control 系列新闻组处理这些文章。此外，还创建了 junk 新闻组来处理未正确发布且无处可去文章。

newsgroups 文件与 active 文件是并行的；它必须包含与 active 文件相同的新闻组定义。

## history 文件

同样在 /var/lib/news 目录中还有 INN history 文件。这些文件用于维护每个已发布到每个新闻组的文章的实时索引。至关重要的一点是，这些文件不能被篡改，因为如果它们与实际新闻组文章不同步，新闻服务器在检索文章时会出现问题。

history 文件有两个独立的部分：一个文本 history 文件和一组通过使用诸如常见的 Berkeley db 包这样的数据库程序创建的二进制索引文件。在启动 innd 守护进程之前，你必须创建这两组文件。

你使用 /var/lib/news/bin/makehistory 命令基于服务器上当前的新闻组文章（应该没有任何文章）来创建文本 history 文件。Fedora 提供了一个空白的 history 文件。

在创建文本 history 文件后，你创建二进制索引文件。你使用 /usr/lib/news/bin/makedbz 程序将文本 history 文件转换为二进制索引文件。makedbz -i 命令创建以下三个独立的二进制文件：

- history.n.dir
- history.n.index
- history.n.hash

你应该将这些文件重命名为标准的 history 文件名（history.dir、history.index 和 history.tag），以便 innd 程序能够识别它们。在创建 history 文件后，你终于可以启动新闻服务器了。

## 运行 innd

使用 `/usr/lib/news/bin/inndstart` 程序是启动 `innd` 守护进程的最佳方式，该进程进而启动其他 INN 包程序。`inndstart` 程序必须从新闻用户 ID 运行。它在后台模式下启动 `innd` 程序以及 `controlohan` 程序。

`innd` 程序在 NNTP TCP 端口上监听新闻馈送和新闻阅读器请求。如果远程新闻阅读器建立连接，`innd` 程序会生成 `active` 程序来验证远程连接并处理新闻阅读器请求。如果传入的文章是控制文章，它们将被传递给 `controlohan` 程序进行处理。

Fedora 已深思熟虑地配置了启动新闻服务器所需的 System V 文件：你可以以适当的方式（`chkconfig`、`ntsysv`、`service` 或 `system-config-services`）来启动服务器。（详见第 15 章“自动化任务”。）以下是一个示例：

```
# /sbin/service inn start
```

当 `innd` 程序正在运行时，你可以使用 `ctlinnd` 程序对其进行控制，语法如下：

```
ctlinnd [-h] [-s] [-t timeout] command [argument...]
```

`-s` 选项会抑制 `ctlinnd` 命令的任何输出。此选项通常用于批处理程序。`-t` 选项指定等待服务器响应的时长（以秒为单位）。如果你正在通过慢速链路连接到服务器，或者正在连接到缓慢的服务器，你可以增加 `timeout` 的值。

命令参数定义了 `ctlinnd` 程序应该对 `innd` 新闻服务器执行哪些操作。`-h` 选项会打印出可用于 `ctlinnd` 的所有可用命令参数的摘要。目前，你可以使用 `newgroup` 命令创建一个供新闻阅读器读取和发送消息的新本地新闻组：

```
$ ctlinnd newgroup local.linux.group y hoyt@maximumhoyt.com
```

`newgroup` 命令使用三个参数：

- 新新闻组的名称
- 一个标志，用于定义要创建的新闻组类型（y 代表常规开放组，m 代表经过审核的组）
- 新新闻组维护人员的电子邮件地址

