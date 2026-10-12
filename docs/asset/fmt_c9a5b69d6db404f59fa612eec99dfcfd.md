
### 8.3.12：使用 NIS 集中网络用户认证

您应该注意，在本地系统中，`root` 用户具有访问系统上所有文件的绝对权限。然而，在 NFS 挂载目录中，本地 `root` 用户的权限受到严格限制，必须显式地授予访问 NFS 服务器上资源的权限。

这种使用 `mount` 命令的问题在于，每当您重启电脑时，都需要定期为每个远程目录重新执行挂载命令。您可以通过在技巧 8.59 中描述的“通过编辑 `fstab` 文件创建新驱动器挂载”，向 `/etc/fstab` 文件添加目来解决这个问题。

在网络中，用户能够登录任何工作站或服务器，但其用户名和密码始终针对中央用户数据库进行验证，这是非常重要的。通常，用户的用户名和密码信息存储在网络上每个 Linux 系统的本地密码文件中。如果您希望所有用户都能使用相同的用户名、密码、主目录、默认 shell 和其他账户特定信息登录每个系统，那么您将需要在每个系统上复制相同的 `/etc/passwd` 文件，并将对该文件所做的任何更改同步到所有系统。

这种复制和同步的困难可以通过 NIS（网络信息系统）来解决。NIS 最初由 Sun Microsystems 为其 `SunOS` 和 `Solaris` 操作系统开发，可用于集中信息数据库，例如网络上的用户数据库。可以与 NIS 集中化的信息包括 `hosts` 文件、用户数据库、服务列表（如 `/etc/services`）、主机名及其关联的 IP 地址等。

NIS 通过要求在一个位置管理所有这些公共信息，而不是在网络上的每台服务器和工作站上管理，从而简化网络管理。NIS 以客户端-服务器模式工作，将 NIS 数据库放置在一个或多个服务器上，并配置网络上的每其他机器作为客户端。这样，如果用户尝试登录系统（例如），客户端连接到 NIS 服务器来处理用户认证，而不是通过系统的控制台。

关于 Linux 上 NIS 的完整信息可以在 `http://linux.com/howto/NIS-HOWTO.html` 中的 NIS HOW-TO 中找到。

### 8.3.13：安装 NIS 服务器

大多数 Linux 发行版已经包含了 NIS。例如，如果您正在运行 `RedHat` 7，可以使用以下命令检查是否安装了 NIS 服务器：

```
# rpm -qa
```

您的系统应显示如下结果：

```
yptools-2.4
ypbind-1.6
ypserv-3
```

如果缺少这些文件，您需要从光盘安装它们。将光盘插入驱动器并使用以下命令挂载：

```
# mount /cdrom
```

接下来，使用 `rpm` 工具安装每个文件，如下：

```
# rpm -i /cdrom/<file name>
```

您应该将 `<file name>` 替换为下列表中相应的名称：

- `yptools-2.4`
- `ypbind-1.6`
- `ypserv-3`

如果您使用的是其他发行版，请检查其文档；如果发现没有包含 NIS，请查看 `http://linux.com/howto/NIS-HOWTO`。最新版本的 NIS 通常可以在 `ftp://ftp.kernel.org/pub/linux/utils/net/` 找到。

![img/1a9080c03c91a8cc232a677c195]

### 8.3.14：配置您的 NIS 服务器

在网络中，运行 NIS 主服务器是关重要的。可选的是您可以运行一个或多个从服务器作为主服务器的备份并帮助负载均衡。在本技巧中，我们将考虑主 NIS 服务器的配置，因为这对在网络上运行 NIS 是关重要的。

出于示例目的，您将使用 NIS 集中用户和组数据库。为了实现此目的配置 NIS 服务器，请执行以下步骤（这些步骤针对 `RedHat` Linux 7，但通常适用于其他现代发行版）：

1. 使用您喜欢的文本编辑器打开 `/etc/exports` 文件。例如，要使用 Emacs 打开文件，使用命令 `emacs /etc/exports`。
2. 找到以 `all:` 开头的行。该行将包含您想要通过 NIS 提供的数据库列表。条目可以跨行——行尾的反斜杠表示条目在下一行继续。注释以井（`#`）开始并持续到行尾。在 `RedHat` Linux 7 上，该条目如下：

```
all: passwd group hosts rpc services netid protocols mail \
# netgrp shadow publickey networks ethers bootparams
printcap \
# amd.home auto.master auto.home auto.local
passwd.adjunct
# timezone local netmasks
```

3. 为了仅将 NIS 用于您的用户和组数据库，您需要编辑 `all` 条目，使条目中仅包含 `passwd` 和 `group`：

```
all: passwd group
# hosts rpc services netid protocols mail \
# netgrp shadow publickey networks ethers bootparams
printcap \
# amd.home auto.master auto.home auto.local
passwd.adjunct
# timezone local netmasks
```

4. 保存文件并关闭文本编辑器。
5. 用你喜欢的文本编辑器打开 `/var/yp/securenets` 文件。例如，要使用 Emacs 打开文件，请使用命令 `emacs /var/yp/securenets`。`securenets` 文件用于指定哪些主机允许访问 NIS 数据库。
6. 在 `/var/yp/securenets` 文件中，你需要定义一个或多个条目，以指定哪些主机允许访问你的 NIS 服务器。每个条目单独占一行，格式如下：

```
<网络 掩码> <IP 地址>
```

例如，你需要让你的本地主机网络拥有访问权限，使用以下条目：

```
255.0.0.0 127.0.0.0
```

同样，如果你位于本地 C 类网络 1.2.3 上，并希望网络上的所有主机都能访问，你需要以下条目：

```
255.255.255.0 1.2.3.0
```

7. 在向 `/var/yp/securenets` 添加任何所需的条目后，保存文件并关闭文本编辑器。
8. 用你喜欢的文本编辑器打开 `/etc/ypserv.conf` 文件。例如，要使用 Emacs 打开文件，请使用命令 `emacs /etc/ypserv.conf`。`/etc/ypserv.conf` 文件包含了一系列规则，基于主机控制对 NIS 数据库的访问。
9. 在 `/etc/ypserv.conf` 文件中，你可以创建一系列条目，基于主机限制对特定 NIS 数据库映射的访问。每条规则单独占一行，格式如下：

```
<IP 地址>:<NIS 数据库>:<安全设置>:<密码混淆行为>:<密码混淆字段>
```

每个规则中的字段具有以下含义：

- `IP 地址`。该规则所适的主机 IP 地址（例如 1.2.3.4）或网络地址（例如 C 类网络 1.2.3 的 1.2.3）。
- `NIS 数据库`。规则适用的 NIS 数据库名称（例如 `passwd` 或 `group`），或使用星号（`*`）表示所有数据库映射。
- `安全设置`。此字段可以取四个值之一，定义允许访问受规则影响的数据库或数据库的访问类型：
    - `none`：允许所有访问。
    - `port`：允许来自 1024 以下端口的访问；或者如果访问来自 1024 以上的端口，则仅当 `mangle` 设置为 `yes` 时允许访问（见下文）。
    - `deny`：拒绝访问。
    - `des`：需要 DES 认证（某些 Linux 系统不支持此项）。
- `密码混淆行为`。此字段定义了当从 NIS 客户端查看时，应如何从数据库映射中共享密码。如果设置为 `yes`，当请求来自非特权端口（1024 或以上）时，密码字段将被替换为 `x`（换句话说，它被混淆了）。如果设置为 `no`，则密码不被混淆。
- `密码混淆字段`。此字段用数字指示给定数据库中哪一个字段被视为用于混淆目的的密码字段。在 `passwd` 数据库中，这将是第二个字段。

10. 例如，如果你想拒绝来自主机 1.2.3.200 访问 `passwd` 数据库映射，可以使用以下规则条目：

```
1.2.3.200:passwd:deny:yes:2
```
