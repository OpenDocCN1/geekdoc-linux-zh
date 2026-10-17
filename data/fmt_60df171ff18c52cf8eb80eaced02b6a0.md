
SuSE 会随着新版本的发布不断升级其软件包。新软件包可能包含重要的错误和安全修复。SuSE 将这些新版本准备为 RPM 软件包，可在你的系统上完美安装。它们还提供源 RPM，如果你想自行编译软件包。源 RPM 很好，因为 SuSE 对其进行了微调，使其在他们的发行版上表现最佳。

那么，你如何知道系统是否有新的更新软件包集？好吧，你可以通过许多方式找到。你可以先检查 SuSE 网站 `http://www.suse.com`。按照以下步骤操作：

- 1. 在此地址启动浏览器。
- 2. 点击 `Updates`。你将被带到一个按发行版版本组织可用更新的页面。
- 3. 点击你的版本。你将被带到另一个页面，列出你发行版的所有可用新更新以及每个更新的相当详细的描述。软件包按系列列出。

## 从硬盘安装新软件包

现在你知道有新的更新软件包，可以立即开始安装。很简单；只需按照以下步骤操作：

- 1. 点击软件包名称（如果你使用的是 Netscape Navigator，请按住 Shift 键）开始将它们下载到你的硬盘。
- 2. 当你硬盘上有了想要的所有软件包时，你可以使用两种方法之一安装它们——YaST 或手动。两者都很容易执行。让我们从手动方法开始。

### 手动安装软件包

要手动安装软件包，你只需发出 `rpm` 命令即可。例如，假设你将所有软件包下载到名为 `/tmp/updates` 的目录。按照以下步骤操作：

- 1. 以 root 身份登录。
- 2. 如果你不想在执行升级时有用户登录，请关闭网络。
- 3. 将当前路径更改为包含要安装的 RPM 的目录：
- 4. 然后，使用以下 `rpm` 命令一次性安装它们全部：

```
# cd /tmp/updates
```

```
# rpm -Uvh *
```

如果 `rpm` 找到其中一个软件包的旧版本，它将升级它；如果没有，它将安装新软件包。`rpm` 将遍历所有新软件包并安装它们。

### 使用 YaST 安装软件包

如果你不想使用手动方法，你始终可以使用 YaST 安装新软件包。按照以下步骤操作：

- 1. 运行 YaST，选择 Choose/Install Packages。
- 2. 现在你进入安装菜单，选择 Install packages，如图 7.1 所示。

FIGURE 7.1

YaST installation menu.

![](img/659f91d9da7b29976c0625e2e9628511_159_0.png)

3. 告诉 SuSE 从哪里获取你的软件包。在 Source: (None) 字段，按 Enter 获取 YaST 可用的安装源列表，如图 7.2 所示。

FIGURE 7.2

Installation sources YaST can use.

![](img/659f91d9da7b29976c0625e2e9628511_159_1.png)

+   4. 选择目录，并输入包含新 RPM 的目录的路径，在本例中为 `/tmp/updates`。YaST 将加载该目录中找到的所有 RPM 的名称。
+   5. 要安装 RPM，只需使用空格键在其名称旁标记一个 X 即可。
+   6. 按 F10 开始安装 RPM。

## 使用 Internet 更新 SuSE

在前两种方法中，你将 RPM 下载到硬盘，然后使用 RPM 或 YaST 开始安装它们。如果你拥有快速的 Internet 连接，可以轻松使用 YaST 一次性下载并安装 RPM。思路是让 YaST 连接到 SuSE FTP 站点并从那里下载和安装 RPM。请按照以下步骤操作：

+   1. 运行 YaST 并选择 选择/安装软件包。
+   2. 在 源 字段中，按 Enter。选择 FTP——注意 YaST 已在地址字段中填入 FTP 站点的正确 URL。你当然可以更改，但在本例中，这样就可以了。按 Enter。
+   3. YaST 尝试连接到 FTP 站点，如果成功，它将列出可用的目录（见图 7.3）。列表按系列组织，就像 SuSE 安装 CD 一样。

FIGURE 7.3

使用 YaST 从 FTP 安装：

![](img/659f91d9da7b29976c0625e2e9628511_160_0.png)

+   4. 按 Enter 查看每个系列的内容。
+   5. 使用空格键标记你想要安装的软件包，如图 7.4 所示。

FIGURE 7.4

通过在文件上标记 X 来选择要安装的文件。

![](img/659f91d9da7b29976c0625e2e9628511_160_1.png)

6. 按 F10 安装软件包。

请注意，如果你退出一个系列去查看另一个系列，YaST 不会记住你的选择。你必须按 F10 并在当前系列中安装所有想要的软件包，然后才能切换到另一个系列。

## 升级你的 X Window System

X Window System，正如我们所知，是负责为 Linux 提供图形界面的主要应用程序。X Windows 是与你的图形硬件交互的层，使 GUI 应用程序能够使用它。

升级你的 X Windows 是一个重要问题。有多个原因需要升级它。如果你将系统作为服务器运行，安全性就成为首要关注点，例如 X Windows 的新版本可能包含安全漏洞修复。

另一个原因可能是你安装了新的显卡，而你当前版本的 X Windows 不支持它，但较新版本支持。最后，你可能只是为了获得更好的性能而升级。

你如何得知是否有新版本可用于 X Windows？首先要查看的地方是 X Windows 的主页，`http://www.xfree86.org`。每当有新版本的 X Windows 可用时，你一定会在该网站上找到公告和下载链接。

另一个你可能有的问题是如何知道是否需要升级？或者如何知道新版本是否支持我的新卡？这些问题的答案都在随每个新版本发布的发行说明中。公告本身通常包含新版本的主要亮点。例如，X Windows 的当前版本 3.3.5 是这样宣布的：

```
XFree86-3.3.5
[August 1999]
XFree86-3.3.5 is now available!
This is a full release, that completes the missing pieces from the somewhat less optimal 3.3.4 release in July 1999. If you are having problems with a prior release, please try XFree86-3.3.5 first before asking for help.
Highlights of the new release include
DC/ux iX86 support was added
QNX support was added
Linux/x86-only S3 Savage4 driver was added (provided from S3)
Fixes for SIS 530/620 (provided from SIS)
Fix Mach64 server to support Rage LT and LT Pro
PAM support
Misc bug fixes for several drivers
Misc fixes for security problems and other bugs
```

你很容易就能看到此版本中的新功能和新增内容，但你可能想阅读发行说明以获取完整信息。

### 从 SuSE 获取 X Windows 的最新版本

升级 X Windows 的最简单方法是直接从 SuSE 获取最新的 RPM。你应该能找到几乎无需费力即可在系统上运行的二进制文件。要检查 SuSE 是否有新的 RPM，请按照以下步骤操作：

+   1. 访问 `http://www.suse.com` 并点击 更新。
+   2. 当 更新 页面加载后，找到你的发行版版本并点击它。
+   3. 检查他们是否发布了 X Windows 新版本的 RPM。如果发布了，那么你就可以轻松使用 YaST 下载并安装它们。

你可以使用上一节中的完全相同程序来更新你的 X Windows。使用 SuSE 的 FTP 站点更新 X Windows 是更新 SuSE 的一部分。

### 获取 X Windows 并安装它

偶尔 SuSE 可能需要一些时间才能在其 FTP 站点上提供 X Windows 新版本的 RPM。在这种情况下，你需要直接从 XFree86 站点下载。

你所要做的就是下载适当的二进制文件并将其解包到正确的位置。就这么简单就能升级你的 X Windows。关键是选择要获取的正确软件包。这取决于你希望通过升级 X Windows 获得什么。如果你是为了获得新卡的支持而升级，你只需下载适用于该卡的服务器即可。如果你是为了修复错误而升级，那么你应该获取全部内容。在大多数情况下，最好获取整个版本以确保一切正常工作。

在开始下载 X Windows 的最新版本之前，你需要知道要获取哪些文件。发行说明中有一个关于安装 XFree86 的部分，其中包含有关升级 X Windows 所需文件的说明。这些文件如下：
