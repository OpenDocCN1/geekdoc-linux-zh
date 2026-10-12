
在一段时间内，你可能在该窗口中不会看到任何结果。请记住，你正在下载数百兆的软件包、补丁等等更多内容。如果你想监控下载进度，请监控`/var/lib/YaST2/you/mnt/i386/update`目录的变化。例如，通过`SUSE-CORE`通道下载的`SUSE Linux Enterprise Server`版本`9`的`1586`个`RPM`包可以在`SUSE-CORE/9/rpm/i386`子目录中找到。因此，你可以通过以下命令监控下载：

```bash
cd /var/lib/YaST2/you/mnt/i386/update
ls -ltr SUSE-CORE/9/rpm/i386
```

自然，在你为更新服务器下载了软件包后，你会希望让它保持最新。选择“设置自动同步”（`Setup automatic synchronization`）选项。这将打开“YOU 服务器自动同步设置”窗口，允许你将更新配置为每日`cron`任务。结果存储在`/etc/cron.d/yast2-you-server`中。位于`/var/lib/YaST2/you`目录下的此同步文件脚本可以随时运行。我这个版本的脚本包含以下命令，它会与`SUSE-SLES`和`SUSE-CORE`仓库同步更新，以及`SUSE Linux Professional 9.2`更新镜像的镜像：

```bash
#!/bin/sh
/usr/bin/online_update -g "SUSE SLES" -v 9 -a i386 -u http://dbd.suse.de/download/
/usr/bin/online_update -g "SUSE CORE" -v 9 -a i386 -u http://dbd.suse.de/Download/
/usr/bin/online_update -g "SUSE LINUX" -v 9.2 -a i386 -u http://dbd.suse.de/
```

## 3.2 为局域网配置 YaST 补丁管理

如果这无效，你可以在本地挂载共享目录，并使用上一节介绍的技术。

1. 现在，你可以使用上一节介绍的技术更新你的系统。
2. 进程完成后，请考虑配置自动更新。返回 YaST 在线更新。选择“配置全自动更新”。

为 SUSE Linux Professional 配置更新服务器有两种方法。你可以在 SUSE Linux Enterprise Server 上使用 YaST 在线更新服务器来配置镜像。或者，你可以使用 `rsync` 命令来配置镜像。`rsync` 的一个相对优势是它是可定制的；如果你为普通 PC 使用 YaST 在线更新服务器，你最终将获得 32 位和 64 位系统的更新。

无论在哪种情况下，你都需要选择一个镜像。你可以在`http://www.novell.com/products/linuxprofessional/downloads/ftp/int_mirrors.html`找到一份当前的（但不是完全的）列表。在选择镜像之前，请在您选择的浏览器中检查它。你在列表中看到的镜像可能会重定向到不同的 URL。例如，我使用的镜像`http.suse.oregonstate.edu`会自动重定向到`http://suse.osol.org`。

### 3.2.1 使用 YaST 在线更新服务器创建本地镜像

如果你有一台 SUSE Linux Enterprise Server，你可以使用 YaST 在线更新服务器为网络上的 SUSE Linux Professional 计算机创建一个镜像。首先，选择镜像。

> **注意**
>
> 本节假设你正在维护 SUSE Linux Professional 9.2 版本的更新。如果你正在为不同版本的 SUSE Linux Professional 维护更新，请相应替换版本号。

#### 选择镜像

你在本章的前面已经看到过此服务器是如何运作的。要在 GUI 中打开 YaST，点击主菜单 -> 系统 -> 控制中心 (YaST)。在左侧窗格中选择“软件”，并选择“YOU 服务器配置”。在 YaST 在线更新服务器配置窗口中，选择“添加”。这将打开一个与图 3-12 所示类似的窗口。

在这个未命名的窗口中，你需要输入四个参数：

- `ProductName`（产品名称）——`SUSE Linux` 即可。
- `Version`（版本）——输入发行版的版本号，例如 `9.2`；这将成为在`/var/lib/YaST2/you/mnt/i386/update`目录下镜像所在的子目录。
- `Architecture`（架构）——指定你发行版的架构，例如 `i386`。
- `Synchronization URL`（同步 URL）——输入你选择的 SUSE 镜像。在我的情况下，我输入了`http://suse.oosual/suse/`。根据镜像的可用性，可能需要一些时间和报错。
- `Authentication`（身份验证）——在许多情况下，与 SUSE Linux Professional 相关的 SUSE 镜像支持匿名身份验证。

#### 同步

输入你选择的参数后，点击确定。回到 YaST 在线更新服务器配置窗口中，选择“立即同步”。YaST 在线更新服务器将处理此菜单中配置的任何产品。根据你更新的时间，你可能会下载几个 GB 的。此过程可能需要一些时间。

如果出现问题，你将看到如“同步失败”的消息。你选择的镜像可能不可用。如果成功，你将在`/var/lib/YaST2/you/mnt/i386/update`目录下找到`RPM`和补丁。在我的情况下（我为 SUSE Linux Professional 9.2 创建了更新服务器），它们位于以下子目录：

- `9.2/patches`——包含你的 SUSE Linux 客户端上 YaST 在线更新可用的补丁列表。
- `9.2/scripts`——包含任何更新脚本，这些脚本可以帮助你安装特殊组件。
- `9.2/rpm`——包含 `i586`、`i686` 和 `north` 子目录下的 `RPM`。

#### YaST 在线更新服务器故障排除

如果你遇到问题，可以对 YaST 在线更新服务器进行故障排除。退出服务器。检查`/var/log/YaST2/y2log`中关联日志文件的当前版本。如果你无法从日志文件中找出问题，还有更多可以做的操作。

默认情况下，YaST 在线更新服务器的设置存储在`/var/lib/YaST2/you`目录下的`user_settings`文件。如果你配置了身份验证设置，用户名和密码存储在同一目录的`password`文件中。为了下一步的故障排除，请移动这些文件。以下命令将它们移动到你的`/root`主目录目录（默认权限不允许你作为普通用户移动这些文件）：

```bash
mv /var/lib/YaST2/you/you_server_settings -
mv /var/lib/YaST2/password ~
```

如果你之前使用 YaST 在线更新服务器向系统下载过包，它们仍然在那里。

> **注意**
>
> 默认情况下，`/var/lib/YaST2/password`文件是“世界可读的”；换句话说，关联 `644` 权限。该文件可以明文显示你的密码。你可以更改此文件的权限，使其仅文件所有者可见，而不影响 YaST 在线更新服务器的性能。

返回 YaST。重新打开 YaST 在线更新服务器。

## 3.2.2 使用 rsync 创建本地镜像

`rsync` 的一个相对优势是它是可定制的；如果你为普通 PC 使用 YaST 在线更新服务器，你最终将获得 32 位和 64 位系统的更新。

无论在何种情况下，你都需要选择一个镜像。你可以在`http://www.novell.com/products/linuxprofessional/downloads/ftp/int_mirrors.html`找到一份当前的（但不是完全的）列表。在选择镜像之前，请在您选择的浏览器中检查它。你在列表中看到的镜像可能会重定向到不同的 URL。例如，我使用的镜像`http.suse.oregonstate.edu`会自动重定向到`http://suse.osol.org`。

如果你有一台 SUSE Linux Enterprise Server，你可以使用 YaST 在线更新服务器为网络上的 SUSE Linux Professional 计算机创建一个镜像。首先，选择镜像。

> **注意**
>
> 本节假设你正在维护 SUSE Linux Professional 9.2 版本的更新。如果你正在为不同版本的 SUSE Linux Professional 维护更新，请相应替换版本号。

#### 选择镜像

你在本章的前面已经看到过此服务器是如何运作的。要在 GUI 中打开 YaST，点击主菜单 -> 系统 -> 控制中心 (YaST)。在左侧窗格中选择“软件”，并选择“YOU 服务器配置”。在 YaST 在线更新服务器配置窗口中，选择“添加”。这将打开一个与图 3-12 类似的窗口。

在这个未命名的窗口中，你需要输入四个参数：

- `ProductName`（产品名称）——`SUSE Linux` 即可。
