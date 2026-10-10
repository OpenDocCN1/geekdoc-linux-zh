
## 第 22 章：FTP 服务器 477

### 匿名 FTP 服务器目录

如所述，FTP 主目录命名为 `ftp` 并放置在 `/var` 目录下。当用户匿名登录时，他们被放置在此目录中。保护系统的重要部分是防止远程用户通过 FTP 用户访问 `/etc` 目录中的任何文件。由于某种原因，如果您自行设置 FTP 目录，必须使用 `chmod` 命令更改权限，以便远程用户无法访问系统的其余部分。创建一个 `ftp` 目录并使用 `chmod` 命令设置 555 权限以关闭访问：`chmod 555 ftp`。接下来，在 `ftp` 目录创建一个新的 `bin` 目录，存放您想要提供给 FTP 用户的命令。然后创建一个 `etc` 目录，用于存放 `passwd` 和 `group` 文件的副本。再次，其理念是防止 FTP 用户访问 `/etc` 目录中的任何文件。应编辑 `ftp/passwd` 文件，删除系统中普通用户的条目。所有其他用户的密码都应设置为 `x` 以阻止访问。创建一个 `lib` 目录，并存放运行位于 `bin` 目录中命令所需的库文件。

另一种传统的解决方案是创建远程用户所需的某些目录和文件的副本，并将它们放在 `ftp` 目录中。二进制文件放置在 `ftp` 目录中，用户用户使用 `ls` 命令时使用的是 `/bin` 中的那个。无论如何，确保 FTP 目录由 `root` 用户所有，而不是 FTP 用户。使用 `ls -d` 命令检查目录的所有权。

```
# ls -d /var/ftp
```

要更改所有权，您使用 `chown` 命令，如下所示：

```
# chown root.root /var/ftp
```

### 匿名 FTP 文件

位于 FTP 主目录下的 `pub` 目录通常存放供远程用户下载的文件。当用户登录时，他们被放置在 FTP 主目录（`var/ftp`），然后他们可以进入 `pub` 目录以开始访问这些文件（`var/ftp/pub`）。在 `pub` 目录内，您可以添加尽可能多的文件和目录，以便 FTP 将文件传输到您的系统。

在 `pub` 目录下的每个存放 FTP 文件的子目录中，您应该创建一个 `README` 文件和一个 `INDEX` 文件，作为对 FTP 用户的友好。`README` 包含对目录所存文件的简要描述。`INDEX` 文件包含文件列表以及每个文件的描述。

### 使用 rsync 的 FTP

许多 FTP 服务器都支持使用 `rsync` 作为守护进程的 `rsync` 操作。这允许对 FTP 服务器上的文件进行智能更新。你可以更新目录中的多个文件，也可以单个文件（例如大型 ISO 镜像）。

### 使用 rsync 访问 FTP 站点

要使用 `rsync` 服务器访问 FTP 服务器，你需要输入 `rsync` 命令，随后是主机名以及你想要访问的目录路径，或者是 FTP 服务器的其中一个模块。在示例中，用户从 `mytrek.com` FTP 服务器上的目录创建了本地的 `myproject` 目录：

```
$ rsync ftp.mytrek.com::/var/ftp/pub/myproject /home/myproject
```

要查找该站点支持哪些 `rsync` 模块模块，这些模块由站点的 `/etc/rsyncd.conf` 配置文件定义。一个模块只是该目录及其所有子目录。要找到可用的模块，只需在 FTP 站点名后输入双冒号：

```
$ rsync ftp.mytrek.com::

ftp
```

这告诉你 `ftp.mytrek.com` 有一个 FTP 模块。要列出模块上的文件和目录，你可以使用带有 `-r` 选项的 `rsync` 命令。

```
$ rsync -r ftp.mytrek.com::$ftp
```

许多运行 `rsync` 服务器的站点会有 `rsync` 协议，该协议已设置为访问可用的 `rsync` 模块（目录）。例如，可以使用以下 URL 通过 `rsync` 访问 Fedora 发行版的 iblio。该模块名为 `fedora-linux-core`，紧跟主机名之后。

```
$ rsync://distro.ibiblio.org/fedora-linux-core/
```

你可以使用 `rsync` 更新单个文件，例如可能已更改的 ISO 镜像。示例更新了 Fedora 7 ISO 磁盘1。`--progress` 将显示下载进度。

```
$ rsync -a --progress rsync://distro.ibiblio.org/fedora-linux-core/7/i386/isiso/FC-i386-distro.iso
```

### 配置 rsync 服务器

要配置你的 FTP 服务器为 `rsync` 站点的客户端提供服务，你首先需要在服务器上运行 `rsync`。使用 `system-config-services` 或 `chconfig` 开启 `rsync` 守护进程（通常称为 `rsyncd`）。这将通过 `xinetd` 运行 `rsync` 守护进程，使用 `/etc/xinetd.d` 中的 `rsync` 脚本来启动它并设置参数。

```
$ chconfig rsync on
```

当作为守护进程运行时，`rsync` 将读取 `/etc/rsyncd.conf` 文件获取配置选项。在这里，你可以指定 FTP 选项，例如 FTP 文件的位置。

## 第 22 章：FTP 服务器 479

配置文件被分为多个模块，每个模块都有自己的选项。模块是导出树（目录和子目录）的符号表示。模块名被括在括号中，例如用于 FTP 模块的 `[ftp]`。然后你可以为模块输入选项，例如通过使用 `path` 选项指定你站点目录和文件的位置。用户 ID 和组 ID 可以 `uid` 和 `gid` 选项指定。默认值是 `nobody`。这里显示了一个匿名访问的示例 FTP 模块：

```
[ftp]

path = /var/ftp/pub

comment = ftp site
```

对于更受限的访问，你可以添加 `auth users` 来指定授权用户；`rsync` 默认允许所有用户匿名访问。使用 `hosts` 允许或拒绝来控制来自特定主机的访问。可以使用 secrets 文件（如 `/etc/rsync.secrets`）进一步控制访问。这是一个用冒号分隔的用户名和密码列表。

```
aleina:mypass3

larisa:your5
```

受控区域对应的模块看起来如下：

```
[specialftp]

path = /var/projects/special

command = restricted access

auth users = aleina,larisa

secrets file = /etc/rsync.secrets
```

如果你在 FTP 服务器上并想查看哪些模块是可用的，只需输入 FTP 站点加双冒号且什么都不加：

```
$ rsync ftp.mytrek.com::
```

这告诉你有 `ftp.mytrek.com` 有一个 FTP 模块。要列出模块上的文件和目录，你可以使用带有 `-r` 选项的 `rsync` 命令。

```
$ rsync -r ftp.mytrek.com::$ftp
```

许多运行 `rsync` 服务器的站点，其 `rsync` 协议已设置为访问可用的 `rsync` 模块（目录）。例如，可以使用以下 URL 通过 `rsync` 访问 Fedora 发行版的 iblio。模块名为 `fedora-linux-core`，紧跟主机名之后。

```
$ rsync://distro.ibiblio.org/fedora-linux-core/
```

你可以使用 `rsync` 更新单个文件，例如可能已更改的 ISO 镜像。以下示例更新了 Fedora 7 ISO 磁盘1。`--progress` 选项将显示下载进度。

```
$ rsync -a --progress rsync://distro.ibiblio.org/fedora-linux-core/7/i386/isiso/FC-i386-distro.iso
```

### rsync 镜像

某些操作允许使用 `rsync` 执行镜像操作。使用 `rsync`，你不需要复制整个站点，只需复制已更改的文件。以下示例将你的 `mytrek` FTP 站点镜像到本地系统上的 `/var/ftp/mirror/mytrek`：

```
$ rsync -a --delete ftp.mytrek::ftp /var/ftp/mirror/mytrek
```
