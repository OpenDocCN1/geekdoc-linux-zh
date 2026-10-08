
![](img/75f39fc91296b889c0653851accdfd46_1269_0.png)

**图 18-8** *SFU 挂载选项*

我们将使用默认值 64,000 字节的 *读缓冲区大小*。我倾向于保持这个数字较大，因为它是 NFS 读取期间使用的数据包中的数据部分。通常，越大越好。*写缓冲区大小* 也是同样的道理。*初始超时* 指定了在重试之前等待服务器响应的时间量。*重试次数* 指定了在完全放弃操作之前尝试访问服务器的次数。我还将 *挂载类型* 设置为 *Soft*（软挂载），而不是 *Hard*（硬挂载），并启用 *缓存*。

*文件访问* 允许您指定建立 NFS 挂载的用户权限。这些是您在使用文件时习惯看到的权限，如图 18-9 所示。

![](img/75f39fc91296b889c0653851accdfd46_1270_0.png)

**图 18-9** **SFU 文件访问**

默认情况下，*用户* 将对文件拥有无限制访问权限，而 *组* 和 *其他* 用户只有读取 (R) 和执行 (X) 权限。这些是常见的权限分配设置。

通过选择图 18-2 所示的 *认证* 窗口中的 *确定* 按钮，我们可以轻松建立 NFS 连接。此时会出现一个对话框，要求您确认用户名及其他信息，如图 18-10 所示。

![](img/75f39fc91296b889c0653851accdfd46_1271_0.png)

**图 18-10** **NFS 登录成功**

用户名、UID 和主 GID 对应于 UNIX NFS 服务器上的相应内容。如果我们查看 UNIX NFS 服务器系统上的 passwd 文件并查找用户 hp，我们将看到以下条目：

```
hp:EkyXw/N.EwFNw:104:20::/home/hp:/sbin/sh
```

此 **passwd** 条目中的信息与 NFS 登录窗口中显示的内容相对应。

登录完成后，我们可以在 Windows 系统上使用资源管理器查看 UNIX NFS 服务器上导出的文件系统。图 18-11 显示了 *Manhattan* 局域网，并选中了一个特定系统。

![](img/75f39fc91296b889c0653851accdfd46_1272_0.png)

**图 18-11** **查看 NFS 挂载的文件系统**

选中了 `/home/hp`，右侧的资源管理器窗口显示了 `\home\hp` 目录中的文件。我们有权操纵 `hp` 目录中的文件。我们可以通过选择一个文件（例如 .cshrc）并查看其属性来检查这一点。图 18-12 显示了 *属性* 窗口。

![](img/75f39fc91296b889c0653851accdfd46_1273_0.png)

**图 18-12** **SFU *属性***

此窗口中的 *只读* 复选框未被勾选；因此，我们对该文件拥有完全访问权限。

# Telnet 客户端

SFU 中还加载了一个 Telnet 客户端。从 SFU 菜单中选择 *Telnet - Telnet 客户端* 会产生如图 18-13 所示的 Telnet 窗口。

![](img/75f39fc91296b889c0653851accdfd46_1274_0.png)

**图 18-13** **SFU Telnet 客户端**

我在此 Telnet 窗口中创建了 **/home/hp** 内容的一个长列表。

![](img/75f39fc91296b889c0653851accdfd46_1274_1.png)

# Telnet 服务器

![](img/75f39fc91296b889c0653851accdfd46_1275_0.png)

SFU 中还加载了一个 Telnet 服务器。这意味着您可以从 UNIX 系统或任何带有 Telnet 客户端的系统连接到装有 SFU Telnet 服务器的 Windows NT 系统。图 18-14 显示了从 UNIX 系统访问 Windows Telnet 服务器。

![](img/75f39fc91296b889c0653851accdfd46_1275_1.png)

![](img/75f39fc91296b889c0653851accdfd46_1275_2.png)

在图 18-14 中，我从我的 UNIX 系统到 Windows 系统发起了一个 Telnet 会话。在收到来自 Microsoft Telnet 服务器的欢迎信息后，我可以像在 Windows 系统提示符下直接操作一样发出命令，例如图中的 **dir**。

SFU 的 Telnet 服务器功能提供了从 UNIX 到 Windows 的直接访问方式，这在混合环境中非常有帮助。

许多可以在 Windows 系统上通过此 Telnet 连接或直接在 Windows 系统上运行的 UNIX 实用程序进一步增强了此功能。下一节“UNIX 实用程序”将介绍这些实用程序。

# UNIX 实用程序

SFU 的一个高度期望的功能是通过 *Unix Utilities - Unix Command Shell* 调用的 UNIX 命令 Shell。图 18-15 显示了一个打开的窗口，其中列出了 UNIX 实用程序。

![](img/75f39fc91296b889c0653851accdfd46_1276_0.png)

图 18-15 中列出的实用程序在 SFU 中的工作方式与它们在 UNIX 中的工作方式完全相同。您还可以通过从其他系统建立的 Telnet 会话访问这些 UNIX 实用程序。为了让您了解这些实用程序是如何工作的，让我们发出几条命令，如图 18-16 所示。

![](img/75f39fc91296b889c0653851accdfd46_1277_0.png)

![](img/75f39fc91296b889c0653851accdfd46_1277_1.png)

![](img/75f39fc91296b889c0653851accdfd46_1277_2.png)

**图 18-16** **SFU 使用某些 UNIX 实用程序的示例**

![](img/75f39fc91296b889c0653851accdfd46_1277_3.png)

此窗口表明，当我们调用 *Unix Utilities* 时，我们在 Windows 系统上位于 `C:/SFU/Shell` 目录。我们通过发出 `cd /` 命令将目录更改为 `C:/`，这与我们在 UNIX 系统上的操作方式相同。`pwd` 确认我们位于 `C:/` 级别。然后我们发出 `ls` 命令查看 `C:/` 中的文件。

让我们再发出两个 *Unix Utilities* 命令，以便更好地了解这些实用程序在 Windows 中的性能，如图 18-17 所示。

```
C:\> Unix Command Shell
$ ls | grep -i s
CONFIG.SYS
FIRSTBOOT.TXT
IE401SP1
Internet Explorer 4.01 SP1 Setup
MOUSE
Multimedia Files
MSISF3
Program Files
SETUP
SFU
IT4S
ITHS
topools
pagefile.sys
$ ls | grep -i s | wc
    14    20   166
```

**图 18-17** **SFU 使用某些 UNIX 实用程序的示例**

![](img/75f39fc91296b889c0653851accdfd46_1278_0.png)

在此窗口中，我们发出了一条 **ls** 命令和一条 **grep** 命令，该命令忽略大小写 (-i) 并搜索 *s*。包含大写和小写 *s* 的文件被列了出来。然后我们将相同的输出通过管道传递给 **wc** 以获取单词计数。

![](img/75f39fc91296b889c0653851accdfd46_1278_1.png)

# NFS 服务器

Windows 系统不仅可以作为 NFS 客户端，还可以使用 SFU 作为 NFS 服务器。运行 NFS 的系统可以挂载 Windows 系统上的导出文件系统。

在 *Server for NFS Configuration*（NFS 服务器配置）中，您可以配置 NFS 服务器设置的所有方面。大多数配置类别的默认值适合进行初始测试，我们将在这里执行此操作。您可能希望稍后进行额外配置以调整您的 NFS 服务器。

在我们的示例中，我创建了一个 *共享名称*，如图 18-18 所示。

![](img/75f39fc91296b889c0653851accdfd46_1279_0.png)

**图 18-18** **SFU 共享名称**

通过从菜单中选择 **Server for NFS Configuration**，然后选择 *Share Options*（共享选项），我输入了图 18-18 中显示的 *共享名称* **C:\temp**。

我们可以查看 *Mount Information*（挂载信息）以查看我们导出了哪些文件系统，如图 18-19 所示。

![](img/75f39fc91296b889c0653851accdfd46_1280_0.png)

**图 18-19** **SFU 挂载信息**

我们的文件系统 **C:\temp** 确实出现在导出列表中，且对访问者没有限制。
既然已经建立了此 *共享名称*，我们可以使用 NFS 服务器配置的所有其他类别的默认值，并在 UNIX 系统上挂载 **C:\temp**。要挂载 **C:\temp**，您需要在 UNIX 系统上发出以下命令：

![](img/75f39fc91296b889c0653851accdfd46_1281_0.png)

```
# mount 19.32.23.112:C:\temp /ntmount
```

此命令在大多数 UNIX 系统上都能工作。我们首先指定了挂载命令，通常是以 root 身份发出的。接下来是包含我们要挂载的文件系统的 Windows 系统的名称；在这种情况下，我使用了 IP 地址而不是系统名称。系统名称或 IP 地址后跟一个冒号 (:)。接下来是我们要挂载的文件系统名称，如它在 Windows 系统上显示的那样，即 **C:\temp**。最后是 UNIX 系统下我们要挂载 **C:\temp** 的目录名称，即 `/ntmount`。您还可以为 **mount** 命令添加各种选项，但在我们的示例中我们将使用所有默认值。

让我们现在检查指定的 NFS 挂载是否确实在 UNIX 系统上建立。以下示例显示了在 UNIX 系统上发出 **bdf** 命令（这与书中前面介绍的 **df** 命令有些相似）以查看挂载是否已建立，然后 **cd** 到 **ntmount** 目录，最后列出该目录中的文件：

![](img/75f39fc91296b889c0653851accdfd46_1281_1.png)

```
# bdf
Filesystem      kbytes    used    avail %used Mounted on
/dev/vg00/1vol3  151552   53165   92162   37%   /
/dev/vg00/1vol1   47829   14324   28722   33%   /stand
/dev/vg00/1vol8  163840   87595   71039   55%   /var
/dev/vg00/1vol7  339968  314984  23189   93%   /usr
/dev/vg00/1vol6  102400   62284   37607   62%   /tmp
/dev/vg00/1vol5  1048576  656649  367439  64%   /opt
```
