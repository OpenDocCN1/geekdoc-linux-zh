
- 3. 在 Mac OS X 客户端中，选择屏幕顶部 Finder 栏中的 `Go`，然后选择连接到服务器。连接到服务器窗口出现。
- 4. 在 Mac OS X 客户端中，将共享目录的地址输入地址框。例如，要连接到名为 `jukebox.linuxtoys.net` 的计算机上的共享 NFS（`nfs://`）目录 `/var/music`，您可以输入地址：`nfs://jukebox.linuxtoys.net/var/music`，如图 26-5 所示。

如果一切正常运行，代表服务器的图标应出现在您的 Mac OS X 桌面上。打开该图标以查看共享目录的内容。您可以像在 Mac 上一样使用共享文件和目录（如果服务器上的权限允许您这样做）。完成后将图标拖到废纸篓中。

> **注意：** 如果您无法连接到共享目录，请更仔细地重新执行第 18 章中的 NFS 过程。特别是，请确保服务器上的防火墙端口已打开，并且用户/主机权限已设置为允许您所需的访问级别。

![](img/27a85d56d393921ced6412ae6e8336bf_992_0.png)

### 从命令行连接 NFS

您可能完全无法控制 Linux NFS 服务器的配置方式。因此，如果未设置不安全选项，您将无法从 Mac 的“连接到服务器”窗口挂载 NFS 目录。一个可能的解决方法是手动从 Mac OS X 挂载 NFS 目录并使用安全端口。方法如下：

- 1. 在 Mac OS X 计算机上，按如下方式访问 root 用户帐户：
  - a. 选择文件夹图标后，单击 `Go` → `Applications`。应用程序文件夹出现。
  - b. 打开实用工具文件夹，然后打开 `Netinfo Manager` 实用程序。
  - c. 单击 `Netinfo Manager` 窗口上的锁图标以将其解锁。
  - d. 单击 `安全` → `启用 root 用户`。（如果出现 Netinfo 错误，单击确定。）
  - e. 输入并验证新的 root 用户密码，然后单击验证。（记住该密码！）
  - f. 单击打开的锁图标以关闭它并防止进一步更改。
- 2. 在 Mac OS X 计算机上，单击终端图标打开 shell 并以 root 身份登录：

```
# su -
Password: ******
```

- 3. 创建一个可供想要在 Mac 上使用共享 NFS 目录的用户帐户访问的目录。例如，对于用户 `chris`，您可能键入：

```bash
# mkdir /Users/chris/music
# chown chris /Users/chris/music
```

- 4. 将 NFS 共享目录挂载到您刚刚创建的目录上。例如：

```bash
# mount -o "-P" jukebox.linuxtoys.net:/var/music /Users/chris/music
```
