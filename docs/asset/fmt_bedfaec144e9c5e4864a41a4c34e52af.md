
## 变量作为配置参数

```
$j="/jail";
mariadb {
    path="$j/mariadb";
    --snip--
}
```

如果我必须将监狱移动到新的文件系统或池，我可以通过修改变量来更新 `jail.conf`，而不是编辑每个定义。

### 作为变量的参数

一旦你定义了监狱参数，就可以将其用作变量。每个监狱至少有一个参数：`name`。你可以使用这些参数来进一步扩展默认设置。

```
$j="/jail";
path="$j/$name";
host.hostname="$name.mwl.io";

mariadb {
    ip4.addr="203.0.113.221";
}
```

通过设置全局默认 `path` 为 `$j/$name`，我消除了为每个单独监狱定义 `path` 的需求。

你可以通过将参数括在花括号内来使用包含点号的多项参数。虽然这对 `mount.devfs` 这样的参数没有意义，但对于每个监狱的参数，如 `host.hostname`，则很有用。

```
path = "/jail/${host.hostname}";
```

我更喜欢将监狱放在以较短名称命名的目录中，而不是以主机名命名，但请随意遵循你自己的偏好。

将参数和变量与连贯的目录布局结合使用，可以让你将每个监狱定义压缩为单个配置语句。

## 测试和配置监狱

一旦你有了监狱的文件，就把自己锁定在里面。运行 `jail(8)` 命令在监狱内部运行单个命令。你需要四个参数：路径、监狱名称、主 IP 地址和要运行的命令。

```
##### jail <path to jail> <jail name> <jail IP> <command>
```

在此示例中，我使用位于 `/jail/mariadb`、名为 `mariadb`、IP 地址为 `203.0.113.51` 的监狱，运行命令 `/bin/sh`：

```
##### jail /jail/mariadb mariadb 203.0.113.51 /bin/sh
#
```

运行 `ls(1)`。你位于监狱文件系统的根目录中。这个监狱并非完全处于单用户模式，但这里除了 `/bin/sh` 外没有其他程序在运行。你可以进行一些基本设置，但即使 `devfs(5)` 也未挂载。

```
##### ps
ps: /dev/null: No such file or directory
```

是的，正常的监狱启动过程会挂载 `/dev` —— 但监狱没有用户账户，没有 `root` 密码，没有运行中的守护进程，绝对没有任何可选组件。在启动监狱之前配置它。

## 从宿主机窃取的内容

一些宿主机设置信息在监狱内也很有用。你可以将这些信息从宿主机复制到监狱，但必须从宿主机执行此操作，而不是从监狱执行。

每个监狱执行自己的 DNS 解析。你可以将宿主机的 `/etc/resolv.conf` 复制到监狱中。

你的监狱可能共享与宿主机相同的时间区。将宿主机的 `/etc/localtime` 复制到监狱中，或在监狱内运行 `tzsetup(8)` 以选择新的时区。

### 创建 /etc/fstab

许多程序和脚本（包括 `/etc/rc`）期望找到 `/etc/fstab`，如果它不存在就会报错。在真实服务器上要求 `/etc/fstab` 是完全合理的，但被隔离的机器不需要文件系统表。创建一个空的文件系统表。

```
##### touch /etc/fstab
```

我不介意不快乐的程序。我只是不想听它们抱怨。

### 创建 /etc/rc.conf

你要么从宿主机管理所有监狱，要么通过 SSH 管理监狱。你需要为 `sshd` 添加一个 `/etc/rc.conf` 条目。

```
sshd_enable="YES"
```

在创建此文件时添加你希望的任何其他设置。如果你知道某些设置是软件包需要的，提前设置它们并无坏处。

### 用户账户和 Root 密码

你只能在 `jail` 内部添加用户账户和修改密码。使用 `passwd(1)` 设置 `root` 密码，并运行 `adduser(8)` 添加至少一个用户，以便进行 SSH 访问。虽然 SSH 并非访问主机（`host`）的唯一方式，但在大多数情况下它是更便捷的选择。

## Jail 的启动与停止

主机将每个 `jail` 视为一个独立的服务，类似于 `sshd(8)`、Web 服务器或其他任何守护进程。是的，每个 `jail` 可能会运行许多需要独立管理的服务，但从主机的角度来看，每个 `jail` 都是一个包含一组进程的单实体。这正是主机与 `jail` 之间隔离的一部分。

使用 `service(8)` 来启动、停止和重启 `jail`。你需要提供一个额外的参数，即 `jail` 的名称。FreeBSD 会在启动时自动启动它们，但系统运行后，你可以单独停止、启动和重启它们。让我们关闭我的数据库 `jail` 并重新启动它。

```
##### service jail stop mariadb
##### service jail start mariadb
```

我可以使用重启命令，但在这里页面上看起来不会那么 impressive。

如果你省略 `jail` 名称，`service(8)` 命令将影响 FreeBSD 在启动时启动的所有 `jail`。

```
##### service jail restart
Stopping jails: httpd mariadb.
Starting jails: mariadb httpd
```

这允许你一致地重新初始化你的生产环境 `jail` 基础设施。

FreeBSD 默认启动 `/etc/jail.conf` 中列出的所有 `jail`。正如第 568 页“启动时的 Jails”中所述，你可以在 `/etc/rc.conf` 中更改此设置。`service(8)` 命令可以控制那些不会自动启动的 `jail`，但必须通过名称指定它们。

## Jail 依赖关系

如果你有大量 `jail`，在 `/etc/rc.conf` 中列出启动顺序可能会变得繁琐。你通常最常需要设置启动顺序以保持服务依赖关系。然而，与其在 `rc.conf` 中定义顺序，你可以使用 `depend` 选项告诉某个 `jail` 它依赖于另一个 `jail`。

```
httpd {
    ip4_addr="203.0.113.232";
    depend=mariadb;
}
```

Jail `httpd` 在 jail `mariadb` 运行之前不会启动。`depend` 语句会覆盖 `rc.conf` 中的 `jail_list` 条目。

## 管理 Jails

虚拟化并不会让系统管理任务消失；它只是为执行典型的系统管理任务增加了更多选项。以下是一些此类选项。

### 查看 Jails 和 Jail ID

使用 `jls(8)` 查看系统中当前正在运行的所有 `jail`。

```
###### jls
 JID  IP Address     Hostname            Path
  29  203.0.113.221  mariadb.mwl.io      /jail/mariadb
  30  203.0.113.222  httpd.mwl.io        /jail/httpd
  31  203.0.113.223  test.mwl.io         /jail/test
```

每个 `jail` 都有一个唯一的 `jail` ID，即 `JID`。`JID` 类似于进程 ID；虽然每个 `jail` 都有一个 `JID`，但分配给某个 `jail` 的具体 `JID` 在每次启动该 `jail` 时都会改变。我们将使用 `jail` ID 或名称来执行各种 `jail` 管理任务。

我们还会看到每个 `jail` 的 IP 地址、主机名以及 `jail` 文件的路径。你无法直接获取 `jail` 名称，但对于那些使用基于 `jail` 名称的主机名的人来说，猜出 `jail` 名称没有任何问题。

### Jail 中的进程

Jail 中的进程都像其他 Unix 进程一样获得进程 ID。进程 ID 并非 `jail` 独有的；它们在主机、该 `jail` 以及其他所有 `jail` 之间共享。你不会发现重复的进程 ID。

Jail 中的进程在 `ps(1)` 中使用 `-j` 标志时会显示出来。

```
###### ps -ax
PID  TT  STAT     TIME  COMMAND
  0   -  DLs      2:56.24 [kernel]
  1   -  ILs      0:00.07 /sbin/init -
--snip--
35002 -  SsJ      0:00.01 /usr/sbin/syslogd -s
35129 -  IsJ      0:00.00 /usr/sbin/sshd
--snip--
```

进程 ID `35002` 和 `35129` 位于 `jail` 中。

使用 `ps(1)` 的 `-j` 标志和 `jail` 名称来查看特定 `jail` 的进程。

```
###### ps -ax -J test
PID  TT  STAT     TIME  COMMAND
35561 -  IsJ      0:00.01 /usr/sbin/syslogd -s
35652 -  IsJ      0:00.00 /usr/sbin/sshd
35661 -  SsJ      0:00.03 sendmail: accepting connections (sendmail)
--snip--
```

使用 `-j 0` 可以排除 `ps(1)` 输出中的所有 `jail` 进程，从而让你更轻松地调试主机。

像 `pgrep(1)`、`pkill(1)` 和 `killall(1)` 这样的命令都接受 `-j` 参数，以便你指定 `jail`。如果你更喜欢使用 `pgrep(1)` 查看进程信息，请使用 `pgrep -lfj` 以及 `jail` 名称或 `JID`。

```
###### pgrep -lf -J mariadb
PID  TT  STAT     TIME  COMMAND
35002 -  SsJ      0:00.01 /usr/sbin/syslogd -s
35129 -  SsJ      0:00.00 /usr/sbin/sshd
35158 -  SsJ      0:00.02 sendmail: accepting connections (sendmail)
--snip--
```

为什么 Sendmail 在这个 `jail` 中运行？让我们终止它。

```
###### pkill -9 -J mariadb sendmail
```

再次运行 `pgrep` 显示 Sendmail 已停止运行。

如果你想了解哪些进程正在某个 `jail` 中运行，这效果很好，但有时你有一个进程 ID 并且必须确定它属于哪个 `jail`。这时候你需要 `ps(1)` 的 `-o` 选项。该选项支持许多关键字，可以以常规命令行标志不支持的方式调整 `ps(1)` 的输出——具体来说，`-o jail` 会增加一列，显示进程所在的 `jail` 名称。

```
###### ps -ax -o jail | grep 39415
39415 mariadb - IsJ 0:00.00 /usr/local/libexec/mysql
```

此进程在 `jail` `mariadb` 中运行。

### 在 Jails 中运行命令

`jexec(8)` 命令允许 `jail` 主机管理员在 `jail` 内部执行命令，而无需费心登录到 `jail`。这有助于保持 `jail` 所有者的隐私感。当 `jail` 所有者 Bert 打电话求助时，我不需要他的 `root` 密码，甚至不需要在他系统上的账户。使用 `jexec` 需要知道 `jail` 的名称或 `JID`。这里，我使用主机的 `root` 账户在我的 `jail` `mariadb` 内部运行 `ps -ax`。

```
###### jexec mariadb ps -ax
PID TT STAT TIME COMMAND
35002 - SsJ 0:00.00 /usr/sbin/syslogd -s
35129 - IsJ 0:00.00 /usr/sbin/sshd
--snip--
```

此命令在 `jail` 内部以 `root` 身份运行。但我可能希望以另一个 `jail` 用户身份运行该命令。使用 `-u` 标志提供该用户名。

```
###### jexec -U xistence mariadb ps
jexec: xistence: no such user
```

嗯，这不太妙。我希望 Bert 来运行我的数据库。让我们为他创建一个用户账户。

```
###### jexec mariadb adduser
Username: xistence
Full name: Bert JW Regeer
Uid (Leave empty for default):
Login group [bert]:
Login group is bert. Invite bert into other groups? []: wheel
--snip--
```

现在这个 `jail` 拥有 Bert 的账户，使用他首选的用户名等设置。我将其添加到 `jail` 内部的 `wheel` 组中。请记住，`jail` 内部的 `root` 访问权限不等于主机上的 `root` 访问权限。这就是 `jail` 的要点所在。

我现在可以以该用户身份在该 `jail` 中运行命令。

```
###### jexec -U xistence mariadb sh
$ 
```

我被关在 `jail` 里了！具体来说，是在 Bert 的 `jail` 牢房里。

然而，这个 `jail` 进程的行为会有些异常。进程会保留其环境。在这种情况下，虽然我以用户 `xistence` 的身份运行，但我保留了在非 `jail` 进程中拥有的所有环境设置。这包括类似 `$SSH_AUTH_SOCK`、我的 IRC 服务器设置等内容。我不希望这些内容出现在我的 `jail` 环境中。如果我以 Bert 的身份登录，我希望成为 Bert。

要在进入 `jail` 之前清除你的环境，请使用 `jexec` 的 `-1` 标志。这模拟了一个干净的登录。

```
###### jexec -lU xistence mariadb sh
```

你是否应该总是在 `jail` 中运行命令前清除环境？不，并非总是如此。这完全取决于你在做什么。

许多命令包含支持在主机上运行但目标指向 `jail` 的功能。务必查阅此类选项的手页。一个很好的例子是 `sysrc(8)`，它允许你使用 `-j` 指定 `jail`。这里，我在 `jail` `mariadb` 上启用 MariaDB。MariaDB 选择继续沿用 MySQL 命名约定，因此它通过 `rc.conf` 选项 `mysql_enable` 进行启用。

```
###### sysrc -j mariadb mysql_enable=YES
mysql_enable:  -> YES
```

此 `jail` 现在已准备好运行 MariaDB。

除了 MariaDB 尚未安装这一点，当然。让我们接下来处理这个问题。

### 安装 Jail 软件包

FreeBSD 的软件包工具允许你从 `jail` 内部或从主机管理软件。如果主机管理员分配给你一个需要配置的 `jail`，你可能希望从 `jail` 内部管理软件包。`jail` 中的软件包与任何其他 FreeBSD 主机上的软件包工作方式完全相同，如第 15 章所述。如果你负责整个系统，包括主机和该主机上的所有 `jail`，你可能希望从主机管理每个 `jail` 的软件包，而不是登录到每个 `jail`。让我们花点时间来看看这一点。

`pkg(8)` 命令的 `-j` 标志允许你指定要管理的 `jail`。你需要提供一个参数，即 `jail` 的名称或 `JID`。`-j` 标志必须放在 `pkg(8)` 子命令之前。这里，我在其专用 `jail` 上安装 MariaDB 服务器：

```
###### pkg -j mariadb install mariadb101-server
Updating FreeBSD repository catalogue...
FreeBSD repository is up to date.
All repositories are up to date.
The following 9 package(s) will be affected (of 0 checked):
--snip--
```

请注意，`pkg(8)` 不会发出它正在 `jail` 内安装软件包的通知。它假设如果你使用 `-j`，你知道自己正在 `jail` 中工作。

当你从主机管理 `jail` 的软件包时，软件包工具不会安装在 `jail` 上。Jail 拥有自己的软件包数据库，存储在 `jail` 内部，但 `jail` 没有直接使用该数据库的方式。

不要在主机上和 `jail` 内部管理软件包之间切换。选择一种方法并坚持使用它。

## 更新 Jails（监狱系统）

假设你的主机上运行着成千上万个 Jails，每个 Jail 都在完美的隔离环境中执行特定的任务。这听起来很美好，直到你需要向所有 Jails 应用安全补丁。如果你是从源代码构建 FreeBSD 的，你需要在每个 Jail 中安装新的 `world`。但如果你运行的是发行版，`freebsd-update(8)`（见第 18 章）可以处理 Jails。

你无法在 Jail *内部* 使用 `freebsd-update(8)`。那些将 Jail 与宿主系统隔离以防止相互干扰的机制，也限制了 `freebsd-update(8)` 所需的部分功能。因此，你需要从宿主机更新 Jail。

每次需要更新系统时，请先更新宿主，然后再更新 Jails。宿主运行的 FreeBSD 版本必须等于或新于任何 Jail。

首先，将 `/etc/freebsd-update.conf` 复制到一个备用文件，例如 `/etc/jail-freebsd-update.conf`。移除所有未安装在 Jail 中的组件。Jails 没有内核，且大多数也没有源代码，因此你最终可能会得到类似以下的条目：

- `Components world`
