

SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly

前面的示例在 cron 环境中设置了一些默认值，并在几个指定的时间执行 run-parts。具体来说，/etc/cron.hourly 文件会在每个小时的一分钟后执行。run-parts 只是处理指定目录并执行其中所有命令的程序。

## Available Modules

与 Webmin 模块选择页面类似，此页面允许您选择哪些模块对用户可用。例如，如果您不希望用户拥有任何直接的文件系统访问权限，您可以禁用命令 Shell、文件管理器和 SSH/Telnet 登录。SSH 配置和登录脚本随后就变得无用了，因此也可以将其禁用。

## When to Use Usermin

很可能已经很清楚 Usermin 和 Webmin 在许多方面惊人地相似，而 Usermin 几乎没有 Webmin 所没有的功能。那么，为什么要用它呢？为什么不直接让每个人都访问 Webmin，从而简化每个人的生活呢？如果不分析系统部署的环境，就无法完全回答这个问题。在某些情况下，Usermin 将毫无用处，同时还需要额外的资源来安装和运行它。但在其他情况下，Usermin 可以成为管理员工具箱中的宝贵补充。

当服务器被大量无特权用户使用，并且需要简化这些用户的管理时，Usermin 最有用。在 Usermin 之前，可以授予用户访问 Webmin 以读取邮件、更改密码并执行一些普通用户功能，并且该功能仍然存在。可以通过构建复杂的 ACL 和组并仔细为这些新用户配置仅这些权限，使用 Webmin 实现相同的目的。然而，这给管理员错误留下了一些余地，而这可能产生戏剧性的后果。另一方面，Usermin 不会留下任何错误空间。Usermin 用户拥有的权限仅限于登录用户的权限，不多也不少。用户不会意外获得额外的权限，因此无需仔细选择可用模块来确保安全和易用性（因为，坦白说，许多用户可能会因太多复杂的选项而感到相当困惑）。

Usermin 的另一个良好用途是为经常旅行的用户提供一种轻松的方法来阅读邮件并从自己的主目录检索文件。通过为本地机器提供 Web 界面（并且通过网络文件服务器，可能提供用户所有的数据），远程办公人员可以从世界任何地方的任何 Web 启用设备上完成所有这些操作。换句话说，用户可以从网吧、贸易展览会的互联网亭或无线网络设备登录到本地网络。这样做不需要在客户端系统上安装专用软件。

Usermin 在共享托管环境中的另一个有趣用途是允许用户查看自己的目录、通过 Web 浏览器上传文件、编辑其 shell 帐户的许多基本功能、阅读邮件等等。实现一些不错的额外功能，例如运行 Web 日志分析工具并允许用户从 Usermin 内查看结果，并不会很困难。

## 5

## GENERAL SYSTEM CONFIGURATION

![](img/d84604054810a13cacfdac212ebee2f7_78_0.png)

Webmin 选项卡栏上的第二个类别是 System。点击它将允许您编辑诸如：启动和关闭行为、磁盘配额、文件系统、手动页面、NFS 导出、进程、Cron 作业、系统日志等系统功能。图 5-1 显示了 Linux 系统上可用的选项（具体来说，是运行 Red Hat Linux 的服务器）。

![](img/d84604054810a13cacfdac212ebee2f7_79_0.png)

Figure 5-1: System category

## Bootup and Shutdown

点击 Bootup and Shutdown 会带您进入启动选项页面。在 Red Hat 系统的情况下，它提供了对 /etc/rc.d/init.d 中找到的所有 init 脚本的访问。同样，在 Solaris 系统上，脚本位于 /etc/init.d。点击任何脚本名称将提供编辑、启动、停止和删除 init 脚本的能力。通常，每个 init 脚本都提供启动、停止和重启系统服务（如 Sendmail、named 和 Apache）的功能，以及执行诸如设置网络设备和路由表等基本系统初始化。如果它没有 init 脚本，将新服务或命令添加到系统启动例程的一种简单方法是将其添加到 /etc/rc.d/rc.local 或 /etc/rc.local。

在此页面上您还会看到 Reboot 和 Shutdown 按钮。它们在确认屏幕后会执行您所假设的功能。

## Disk and Network Filesystems

磁盘和网络文件系统页面提供了 /etc/fstab 中列出的文件系统的详细视图。从此页面您可以编辑挂载点、创建新的挂载点、卸载和挂载分区，并为特定挂载点添加执行和 setuid 限制以提高安全性（图 5-2）。此模块配置 /etc/fstab 文件。

![](img/d84604054810a13cacfdac212ebee2f7_80_0.png)

Figure 5-2: Mounted filesystems

要编辑其中一个列出的文件系统，只需点击它即可。从那里您可以挂载和卸载文件系统并调整多个文件系统选项。可用选项可能会根据操作系统和媒体而有所不同。Linux 和 Solaris 有很大差异，因此将分别记录。Irix 和 FreeBSD 与 Linux 几乎相同，因此没有单独的章节。

## Linux Native Filesystem Mount Details

在编辑挂载页面的上表中，Webmin 为所有文件系统提供访问多个通用选项（图 5-3）。

![](img/d84604054810a13cacfdac212ebee2f7_80_1.png)

Figure 5-3: Linux Native Filesystem Mount Details

### Mounted As

这是文件系统将在系统目录层次结构中所在的位置的挂载点。挂载点是一个目录，像使用 mkdir 命令创建的任何其他目录一样创建。挂载文件系统时，操作系统会检查此值以决定文件系统的内容应位于层次结构中的何处。某些挂载点，如 /usr 和 /，对操作系统具有特定含义，不得更改。虽然其他一些挂载点因长期存在的 UNIX 传统而得名，例如 /home 和 /usr/local。尽管如此，大多数挂载点可以根据您的环境以任何方式命名；只要在偏离历史认可的名称时小心即可。

### Save mount?

提供是否保存当前挂载点的选项。通常，在创建新挂载点或修改旧挂载点时，您希望在启动时保存并挂载。然而，如果媒体是可移动媒体，如软盘或 CD-ROM，您可能会选择仅保存挂载。最后，如果您只是创建临时文件系统，例如将 ISO 映像作为文件系统挂载，您将不需要保存挂载点。

### Mount now?

允许您选择是否立即挂载或卸载文件系统。如果选择 Mount，Webmin 将在您点击创建或保存按钮时尝试挂载文件系统。同样，选择 Unmount 将尝试卸载已挂载的文件系统。如果文件系统正被任何程序使用，操作系统将拒绝卸载文件系统。

### Check filesystem at boot

选择文件系统是否将在系统启动时使用 fsck 检查，以及如果检查，检查应获得什么优先级。请注意，某些文件系统类型，如日志文件系统 ReiserFS 和 XFS，通常不需要检查。此外，只读文件系统，如 CD-ROM，应不予检查。在 Linux 下，ext3 文件系统即使 fstab 条目在此处指定了优先级，也会在启动时悄悄跳过 fsck，除非用户在不干净关闭后的启动期间手动另行指定。由于它是日志文件系统，因此这种行为是合理的，但可能不会立即从文档中显而易见。

### Linux Native Filesystem

允许您选择将与挂载点关联的设备。一些现代 Linux 发行版对此使用标记设备，而其他发行版则直接标识设备。下拉菜单提供对所有已知磁盘设备的访问。您也可以通过点击 Other devices 单选按钮，在文本输入字段中直接输入设备或 ISO 文件名。

## Linux Advanced Mount Options

此页面上的下表显示了 Linux 文件系统的高级挂载选项，并指示当前启用了哪些选项（图 5-4）。

![](img/d84604054810a13cacfdac212ebee2f7_81_0.png)

Figure 5-4: Advanced Mount Options

