
> 46 注意，变量不是 `$DECONF_PRIORITY`，而是 `$DEBIAN_PRIORITY`！

## 5.8 debconf: Debian 软件包的配置

### 5.8.3 debconf 前端（front-ends）

将用户交互与软件包软件配置分离的一个主要优势是可以使用不同的前端来提问。使用哪种前端的决定由系统管理员做出的。对于软件包维护者来说，选择哪种前端没有区别；`postinst` 文件会查询 debconf 数据库以获取缓存信息，无论使用何种前端从用户处收集数据。

除了标准的蓝底白字文本模式对话框外，debconf 还可以通过 KDE 或 Gnome 窗口、控制台文本模式、文本编辑器或网络浏览器获取信息。此外，debconf 还可以为全自动安装抑制所有形式的交互。

呈现的界面以及选项集在所有前端中都是相同的，非交互式前端除外。图 5.11 中的对话框前端提问 debconf 问题的方式与下方的 readline 前端相同所示：

![](img/cb2919de23e4chend0d6a7dcecaea10c9_222_0.png)

> 图 5.11
> debconf 的对话框前端。

## 配置 debconf

使用 debconf 进行配置的软件包具有共同的外观。你可以选择使用的用户界面类型。

对话框前端是一个全屏基于字符的界面，而 readline 前端使用更传统的纯文本界面，gnome 和 kde 前端都是现代 X 界面，适用于各自的桌面（但可以在任何 X 环境中使用）。编辑器前端允许你使用喜爱的文本编辑器进行配置。非交互式前端永远不会向你提问任何问题。

- 1. Dialog（对话框）
- 2. Readline
- 3. Gnome
- 4. Kde
- 5. Editor（编辑器）
- 6. Noninteractive（非交互式）

应该使用什么界面来配置软件包？2

因此，使用哪种前端实际上取决于喜好。在配置 debconf 软件包期间，你可以选择一个默认前端，随后可以通过适当设置环境变量 `$DEBIAN_FRONTEND` 来覆盖它 47。

对于无人值安装，非交互前端确保过程不会暂停并等待用户输入。相反，所有之前未回答的问题将使用默认值。理想情况下，数据库应该预先填充高或关键优先级的答案，因为这些问题没有合理的默认值。或者，可以使用远程数据库（第 5.8.6 节）。

除了提问，debconf 还可以向用户显示消息。如果使用非交互前端，这些消息将通过电子邮件发送给 root 用户。

## 5.8.4 重新配置软件包

响应 debconf 查询的选项和设置并不是最终的。事实上，重新运行 debconf 为问题提供不同的答案是非常简单的。以前，重新配置软件包的标准方法是重新安装。然而，由于 debconf 记得它展示过哪些问题并且不再再次显示（除非被要求），重新安装最终将使用相同的 debconf 参数。显然，使用 debconf 数据库（或至少是相关记录）可以解决问题，专门为此目的设计的工具 `dpkg-reconfigure` 也是如此。

`dpkg-reconfigure` 软件包名称并告诉 debconf 再次询问所有问题，无论它们之前是否被回答过；`--unknown` 选项会导致跳过已经见过的问题。例如，以下指令了 `dpkg-reconfigure`：

```bash
# dpkg-reconfigure --frontend=readline
应该使用什么界面来配置软件包？2
```

## 5.8 debconf: Debian 软件包配置

```bash
db_get hinfo/autoupdateversebase
verb=$RET
temp='tempfile -p hinfo -m 0755'
cat <<EOF >$temp
n!/bin/sh -e
if [ -x /usr/sbin/hinfo-update ]; then
  su hinfo -s /usr/bin/sh -c '/usr/sbin/hinfo-update $verb'
fi
EOF
ucf -s /usr/share/hinfo /etc/cron.$au/hinfo
chmod u+x /etc/cron.$au/hinfo
rm $temp
[...]
esac;
[...]
```

简而言之，这个 `postinst`（安装后）脚本读取了自动更新的周期，并使用 `case` 语句根据用户的选择采取相应的步骤。如果选择每天、每周或每月更新，它会在临时文件中创建升级脚本，并使用 `ucf` 将其放置到位，以确保管理员的设置不会在未经意愿的情况下被覆盖。

通过将所有配置本地化在软件包脚本中，关于如何将用户的选择转换为有效配置的所有知识都包含在 `hinfo` 软件包中，`debconf` 不需要了解任何关于 `hinfo`、`cron` 甚至不需要知道前者使用了后者的信息。与配置仪表板和控制面板相反，`debconf` 的方法可以在不修改 `debconf` 核心的情况下处理无限数量的配置方案。

## 5.8.6 使用远程数据库后端

`debconf` 数据库是一个平面文件缓存数据库（位于 `/var/cache/debconf` 下）。尽管这种数据库后端有许多缺点（如性能和大小），但它非常适合作为单机机器的用户界面和响应缓存。尽管如此，如果 `debconf` 不允许根据不同的需求使用不同的后端，那么它就不是 `debconf` 了；在编写本文时，`debconf` 除了可以使用轻级目录访问协议（LDAP）后端外，还可以使用三种数据库方法之一：单个文件（File，默认值）、目录层次结构（DirTree）或基于每个包一个文件（PackageDir）。LDAP 后端虽然处于实验阶段，但它允许使用安全套接层（SSL）以及只读属性的设置。

有多个原因让你可能想要使用远程 `debconf` 数据库。最常见的原因可能是你想在安装新系统时使用现有 Debian 系统的设置。最简单的方法是

![](img/cb2919de23e4ceed0d6a7dcecaea10c9_226_0.png)

使用 `Pipe` 驱动程序和 SSH 隧道传输来自另一台机器的平面数据库 `config.dat` 内容（或者提前将其复制并使用本地版本的管道，而不是使用 SSH 隧道）。我将向你展示如何瞬间完成操作。

`debconf` 提供了为此目的合并多个数据库的功能。可以临时告知 `debconf` 使用两个环境变量 `$DECONF_DB_OVERRIDE` 和 `$DECONF_DB_FALLBACK` 从另一个源拉取参数。如果设置了第一个变量，`debconf` 会在查看本地缓存之前咨询引用的数据库。同样，`$DECONF_DB_FALLBACK` 可用于指定当远程数据未存储在本地缓存时的查询源。

源以驱动程序的形式以及特定驱动程序所需的任何参数指定。驱动程序是访问数据库的简单方法，`debconf` 带有许多驱动程序，这些驱动程序在 `debconf.conf (5)` 中描述。以下是可用驱动程序：

### File

使 `debconf` 使用平面文件作为数据库。例如：`File{/tmp/my-debconf-db}`。

### Pipe

配置 `debconf` 从标准文件描述符 `stdin`（或 `stdout`）读取（并写入）。这些可以通过参数指向其他地方。

### Stack

可以堆叠不同的源，然后按照指定的顺序对它们进行查询。帮助页面（`debconf.conf (5)`）给出了该驱动程序的有用示例。

### LDAP

告诉 `debconf` 通过 LDAP 获取值。例如：`LDAP{server:localhost,basedn:dc=debconf}`

如果你想让 APT 执行到下一个版本的升级，同时从远程机器而非用户那里获取所有未知设置，你可以像这样使用 `Pipe` 传输：

```bash
# export DECONF_DB_FALLBACK=Pipe
# export DEBIAN_FRONTEND=noninteractive
# ssh remote cat /var/cache/debconf/config.dat \
apt-get dist-upgrade
```

APT 将继续下载所有新软件包，并在预配置阶段将参数模板向 `debconf` 注册。所有尚未存储在本地 `debconf` 数据库中的参数将从 `stdin` 读取，假设它是平面格式的 `debconf` 数据库。非交互前端确保升级过程中没有中断。

或者，你可能想更改各种机器上许多软件包的配置。完成此任务的一种方法是准备一台具有所需配置的机器，然后覆盖剩余机器上的 `debconf` 设置。例如，要在同一台机器上强制对 `postfix` 和 `apache` 使用相同的配置（为了演示，使用 `File` 驱动程序而非 `Pipe`），需要在每个目标上执行以下操作：

```bash
# scp remte:/var/cache/debconf/config.dat /tmp/remote-config.dat
```
