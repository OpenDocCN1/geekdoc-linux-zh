
> 注意
如果某些映射文件不存在，可能会显示非致命错误。这些错误不影响 NIS 的功能。

如果你输入 y，ypinit 在遇到第一个问题时就会退出；然后你可以修复问题并重新启动 ypinit。如果这是你第一次运行 ypinit，则推荐此操作。如果你更愿意继续，可以手动尝试修复可能出现的所有问题，然后重新启动 ypinit。

5. ypinit 会询问是否可以销毁 /var/yp/<domainname> 目录中的现有文件。

此消息仅在之前安装过 NIS 时显示。你必须回答 yes 才能安装新版本的 NIS。

6. ypinit 构造服务器列表后，会调用 make。

make 命令使用位于 /var/yp 中的 makefile 包含的指令。它会清除你指定的文件中剩余的注释行，然后在它们上运行 makedbm，创建适当的映射并为每个映射建立主服务器的名称。

7. 要启用 NIS 作为命名服务，请输入

```
cp /etc/nsswitch.nis /etc/nsswitch.conf
```

此命令用默认的 NIS 方向的交换文件替换当前交换文件。你可以根据需要编辑此文件。有关此文件内容的信息，请参阅“名称服务开关”部分。

主映射创建完成后，你可以在主服务器上启动 NIS 守护进程。

## 在主服务器上启动和停止 NIS

要在主服务器上启动 NIS 服务，需要在服务器上启动 ypserv 并运行 ypbind。守护进程 ypserv 在 NIS 映射中查找后会回答客户端的信息请求。你可以通过从命令行运行 /usr/lib/netsvc/yp/ypstart 脚本来启动服务器上的 NIS 服务。在通过运行 ypinit 配置 NIS 主服务器后，ypstart 会在系统启动时自动被调用以启动 ypserv。

要停止 NIS 服务，请在服务器上按如下方式运行 ypstop 命令：

/usr/lib/netsvc/yp/ypstop

## 名称服务开关

设置 NIS 服务的下一步是设置名称服务开关，这涉及编辑 /etc/nsswitch.conf 文件。名称服务开关控制客户端工作站或应用程序如何获取网络信息。名称服务开关通常简称为“开关”。开关决定应用程序用于获取命名信息的使用哪些命名服务以及顺序。它是一个名为 nsswitch.conf 的文件，存储在每个系统的 /etc 目录中。

每个工作站在其 /etc 目录中都有一个名为 nsswitch.conf 的名称服务开关文件。也在每个系统的 /etc 目录中，你会找到可作为 nsswitch.conf 文件使用的模板，这些模板在表 18.5 中描述。无论你选择哪种名称服务，选择适当的名称服务开关模板，自定义它，然后将其重命名为 nsswitch.conf。

### 表 18.5
名称服务开关模板文件

| 名称 | 描述 |
|------|-------------|
| nsswitch.files | 当要在 /etc 目录中使用本地文件且不存在名称服务时使用此模板。 |
| nsswitch.nis | 使用 NIS 数据库作为除 passwd、group、automount 和 aliases 映射之外的所有信息的首要来源。这些被定向为首先使用本地 /etc 文件然后使用 NIS 数据库。 |
| nsswitch.nisplus | 使用 NIS+ 数据库作为除 passwd、group、automount 和 aliases 表之外的所有信息的首要来源。这些被定向为首先使用本地 /etc 文件然后使用 NIS+ 数据库。 |

### 表 18.5 继续
名称服务开关模板文件

| 名称 | 描述 |
|------|-------------|
| nsswitch.dns | 设置名称服务以搜索除 hosts 条目之外的所有条目的本地 /etc 文件。hosts 条目被定向为使用 DNS 进行查找。 |
| nsswitch.ldap | 使用 LDAP 作为除 passwd、group、automount 和 aliases 表之外的所有信息的首要来源。这些被定向为首先使用本地 /etc 文件然后使用 LDAP 数据库。 |

查找在加载 Solaris 8 时安装的 /etc/nsswitch.nis 模板文件。此模板文件包含 NIS 服务和本地文件使用的默认开关配置。当首次安装 Solaris 8 发行版软件时，如果你指定 NIS 为默认名称服务，模板文件将被复制到 /etc/nsswitch.conf。如果在软件安装期间选择“files”作为默认名称服务，/etc/nsswitch.conf 将从 nsswitch.files 创建，其内容如下：

```
#
# /etc/nsswitch.files:
#
# An example file that could be copied over to \
/etc/nsswitch.conf; it
# does not use any naming service.
#
# "hosts:" and "services:" in this file are used only if \
the
# /etc/netconfig file has a "." for nametoaddr_libs of \
"inet" transports.

passwd:  files
group:  files
hosts:  files
networks: files
protocols: files
rpc:  files
ethers:  files
netmasks: files
bootparams: files
publickey: files
# At present there isn't a 'files' backend for netgroup; \
the system will
# figure it out pretty quickly, and won't use netgroups at \
all.
netgroup: files
automount: files
aliases: files
services: files
sendmailvars: files
```

如果你在软件安装期间未选择 NIS 作为名称服务，你可以按如下方式手动将此文件移入位置：

```
cp /etc/nsswitch.nis /etc/nsswitch.conf
```

默认的 /etc/nsswitch.nis 文件如下所示：

```
#
# /etc/nsswitch.nis:
#
# An example file that could be copied over to /etc/nsswitch.conf; it
# uses NIS (YP) in conjunction with files.
#
# "hosts:" and "services:" in this file are used only if the
# /etc/netconfig file has a "-" for nametoaddr_libs of "inet" transports.
# the following two lines obviate the "+" entry in /etc/passwd and /etc/group.
passwd:  files nis
group:   files nis
# consult /etc "files" only if nis is down.
hosts:   xfn nis [NOTFOUND=return] files
networks: nis [NOTFOUND=return] files
protocols: nis [NOTFOUND=return] files
rpc:     nis [NOTFOUND=return] files
ethers:  nis [NOTFOUND=return] files
netmasks: nis [NOTFOUND=return] files
bootparams: nis [NOTFOUND=return] files
publickey: nis [NOTFOUND=return] files
netgroup: nis
automount: files nis
aliases:  files nis
# for efficient getservbyname() avoid nis
services: files nis
sendmailvars: files
```

/etc/nsswitch.nis 文件的每一行标识特定类型的网络信息，例如主机、密码和组；后面跟着一个或多个源，例如 NIS+ 表、NIS 映射、DNS 主机表或本地 /etc。源是客户端查找网络信息的位置。例如，系统应首先在 /etc/passwd 文件中查找 passwd 信息。然后，如果在其中找不到登录名，则需要查询 NIS 服务器。

名称服务开关文件列出了许多类型的网络信息，称为数据库，以及用于解析的名称服务源，以及应搜索源的顺序。表 18.6 列出了可在该文件中指定的有效源。

### 表 18.6
数据库源

| 源 | 描述 |
|---|---|
| files | 指客户端本地的 /etc 文件 |
| nisplus | 指 NIS+ 表 |
| nis | 指 NIS 表 |
| User | 适用于 printers 条目 |
| dns | 仅适用于 hosts 条目 |
| ldap | 指字典信息树 (DIT) |
| compat | 支持过去在 passwd 和 group 信息中使用的旧式“+”语法。 |

如前面的 nsswitch.nis 模板文件所示，名称服务开关文件可以为多个条目包含操作值。当命名服务搜索指定的源（如本地文件或 NIS）时，源会返回状态码。这些状态码在表 18.7 中描述。

### 表 18.7
名称服务搜索状态码

| 源 | 描述 |
|---|---|
| SUCCESS | 请求的条目已找到 |
| UNAVAIL | 源不可用 |
| NOTFOUND | 源中不包含此类条目 |
| TRYAGAIN | 源返回“我很忙，请稍后再试”消息 |

对于每个状态码，存在两种可能的操作：

- 继续 尝试下一个源
- 返回 停止查找条目
