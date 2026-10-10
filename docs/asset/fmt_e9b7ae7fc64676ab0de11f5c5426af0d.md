
```text
# /etc/cshrc
#
# csh configuration for all shell invocations.
#
# By default, we want this to get set.
# Even for non-interactive, non-login shells.
if (sid > 99 && "id -gn" = "id -un" ) then
    umask 002
else
    umask 022
endif

if ($?prompt) then
    if ($?tcsh) then
        set promptchars='#'
        set prompt='[%n@%m %c]$ '
        # make completion work better by default
        set autolist
    else
        set prompt=\[\$user@\*hostname  -s\]\$\$
    endif
endif
```

`/etc/cshrc` 和 `/etc/bashrc` 文件设置了多种 shell 环境选项。如果你想修改或为系统中所有单个用户提供的 shell 环境增加内容，那么 `/etc/bashrc` 或 `/etc/cshrc` 文件就是合适的地方。

### 设置系统配置文件

分配给每个用户的最基本信息中的一部分是从 `/etc/profile` 文件中添加的。因此，如果你想更改以下任何信息，可以从 `/etc/profile` 开始。`/etc/profile` 文件的内容仅被引入到每个用户的初始登录 shell 中。以下是 `/etc/profile` 中包含的一些值：

- `PATH` — 为 root 用户和所有其他用户分配默认的 `PATH`。你可能需要更改此值，以添加包含所有用户所需应用程序的本地目录的 `PATH`。
- `ulimit -S c 0` — `ulimit` 的 `-c 0` 选项阻止核心文件（通常在进程崩溃时创建）的创建。`-S` 将此设置为“软”选项，因此用户如果愿意，可以启用核心文件功能。
- **环境变量** — 标准操作所需的 shell 环境变量在此文件中分配。这些包括 `USER`（由 `id -un` 命令设置）、`LOGNAME`（与 `USER` 相同）、`MAIL`（设置为 `/var/spool/mail/$USER`）、`HOSTNAME`（设置为命令 `/bin/hostname` 的输出）以及 `HISTSIZE`（将 shell 命令历史设置为 1,000 项）。
- `INPUTRC` — 根据 `/etc/inputrc` 文件的内容，为特定情况设置键盘映射。特别是，`inputrc` 文件确保 Linux 控制台和各个终端窗口（`xterm` 和 `rxvt`）都正常运作。

`/etc/profile` 文件做的最后一件事是查看 `/etc/profile.d` 目录的内容，并引入它找到的文件。每个文件包含定义环境变量或别名的设置，这些设置影响用户如何使用 Shell。例如，`lang.sh` 和 `lang.csh` 文件识别外语文件的位置。`vim` 文件创建别名，使得当输入 `vi` 时，使用的是 `vim`。`which-2.sh` 文件定义了一组由 `which` 命令使用的选项。你可以修改 `profile.d` 文件或添加自己的文件，以为你所有的用户设置环境变量和别名。

#### 将用户账户添加到服务器

当你设置服务器时，通常你希望允许人们向其上传文件或从中下载文件或消息。然而，你可能不希望允许这些人访问整个服务器。你可以在最初创建他们的用户账户时开始限制对这些用户的访问。

为了防止远程用户登录并访问 shell（通过 `ssh`、`telnet` 或其他登录服务），你可以将用户的默认 shell 设置为 `nologin`。例如：

```bash
# useradd -s /sbin/nologin jerryb
```

将 shell 设置为 `nologin` 后，该用户将无法登录服务器以打开 Shell。但是，用户仍然可以使用此账户登录服务器上的 FTP 服务（如果该服务可用且用户有密码）。默认情况下，在该示例中，当用户通过 FTP 登录时，其主目录将是 `/home/jerryb`。（请参阅第 19 章了解如何在 `chroot` 环境中限制此用户仅访问其主目录的方法。）

另一种允许仅通过 FTP 访问服务器方法是使用 `/usr/lib/ftpd-server` 作为用户的登录 shell。虽然这允许用户访问该用户账户可用的整个文件系统，但它限制他们仅能通过安全 FTP 访问服务器。

网络主机的一种常见做法是允许用户将内容放置在服务器上，通常位于该用户的 `/home/username/public_html` 目录中，使用 FTP（但不使用 shell 登录）。然而，管理员可以选择将 Web 内容的位置指定为任何目录，包括系统范围的 Web 服务器目录。以下命令将名为 `webuser` 的用户分配使用 `/var/www/html` 作为其主目录（为了让这起作用，你还应该将文件的所有权更改为属于 `webuser`）：

```bash
# useradd -s /sbin/nologin -d /var/www/html webuser
```

如果你添加一个用户仅用于邮件服务访问，你可能也会选择阻止任何 FTP 访问。做到这一点的一种方法是将用户的主目录指向 `/dev/null`。例如：

```bash
# useradd -s /sbin/nologin -d /dev/null jerryb
```

一旦你设置了受限的用户账户，你可以使用与特定服务相关的功能，进一步定义你的服务器用户可以和不可以访问的内容。

### 创建可移植桌面

Linux 是一个诞生于互联网上的操作系统，因此它具有强大的网络能力并不令人惊讶。这使得 Linux 成为出色的服务器，但也使 Linux 能够成为出色的桌面工作站，尤其是在高度网络化的环境中。Fedora 让你可以轻松地为你的用户设置一个可移植桌面，该桌面可以跟随他们从一台计算机到另一台计算机。在其他领先的桌面操作系统中，这并不那么容易。

通常，Linux 用户的主目录位于 `/home` 目录内。作为一种替代方案，你可以在主目录中创建一个以系统主机名命名的目录。在该目录内，创建用户的主目录。因此，在名为 `dexter` 的 Linux 系统上，用户 `mary` 的主目录将是 `/home/dexter/mary`，而不是 `/home/mary`。这样做有一个非常好的理由。

如果你已登录到 Linux 系统 `ratbert`，并希望访问 `dexter` 上的主目录，就好像它是本地存储的一样，最好的方法是使用网络文件系统（NFS）将 `dexter` 的 `/home` 目录挂载到 `ratbert` 的 `/home` 上。这导致无论登录到哪台机器，你都可以拥有相同的主目录内容。

> **交叉引用：** 你可以在第 17 章中阅读有关 NFS 的更多信息。

要如前所述挂载 `dexter` 的 `/home` 目录，请在 `ratbert` 的 `/etc/fstab` 文件中添加一行类似于以下内容：

```text
dexter:/home /home nfs defaults 0 0
```

另外在 `dexter` 的 `/etc/exports` 目录中添加如下条目：

```text
/home ratbert(sync)
```

现在，当 `ratbert` 启动时，它会自动通过网络挂载 `dexter` 的主分区。这使你能够对待 `dexter` 的 `/home` 上的远程文件和目录，就好像它们本地存储在 `ratbert` 上一样。不幸的是，这具有“覆盖”`ratbert` 实际 `/home` 目录的副作用。

这就是基于系统名的额外目录层派上用场的地方。当 `dexter` 的所有主目录位于 `/home/dexter`，而 `ratbert` 的所有主目录位于 `/home/ratbert` 时，你可以消除一个系统覆盖另一个系统主目录的危险。事实上，让我们将这个例子再进一步：设想一个场景，其中系统 `dexter`、`ratbert` 和 `daffy` 都具有与其他系统共享的可移植桌面。如所示，每个系统的 `/etc/fstab` 和 `/etc/exports` 文件应添加以下行。

**dexter 的 `/etc/exports` 文件：**

```text
/home/dexter ratbert,daffy
```

**dexter 的 `/etc/fstab` 文件：**

```text
ratbert:/home/ratbert /home/ratbert nfs defaults 0 0
daffy:/home/daffy /home/daffy nfs defaults 0 0
```

**ratbert 的 `/etc/exports` 文件：**

```text
/home/ratbert dexter,daffy
```

**ratbert 的 `/etc/fstab` 文件：**
