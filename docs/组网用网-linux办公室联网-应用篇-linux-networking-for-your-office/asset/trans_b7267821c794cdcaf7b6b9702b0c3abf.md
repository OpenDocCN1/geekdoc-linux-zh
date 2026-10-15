

第一种方法是打开命令提示符后发出 net use 命令。例如，键入 net use m: \\speaker\rodsmith 会将共享 \\speaker\rodsmith 映射到驱动器字母 M:。

分配驱动器字母的第二种方法是按照以下步骤操作：

- 1. 在任意打开的文件浏览器窗口中，确保工具栏可见，如果不可见，请选择 View，Toolbar 以显示它。
- 2. 在工具栏中单击 Map Network Drive 图标（见图 11.5）。Windows 会响应并显示图 11.8 所示的 Map Network Drive 对话框。

![](img/5d4d3092919d1d16884788127447cc6d_305_0.png)

图 11.8
Windows 的 Map Network Drive 对话框因 Windows 版本而异。这里显示的是 Windows NT 4.0 中的对话框；Windows 98 中的相应对话框则更简单。

- 3. 在 Path 字段中输入共享名称，如 \\speaker\rodsmith。在 Windows NT 4.0 中，你也可以使用对话框下部的浏览器来选择共享。
- 4. 选择要分配给该共享的驱动器字母。
- 5. 单击 OK。Windows 会在你指定的字母下挂载该共享。

## 从 Windows 程序访问 Samba 共享

如果你正在使用 Windows 程序并意识到需要访问一个共享目录，通常可以在不将共享作为驱动器字母挂载的情况下进行访问。Windows 程序中的典型文件对话框允许你从桌面中选择 Network Neighborhood 作为可用选项之一，如图 11.9 所示。你可以从那里向下浏览到你的 Linux 服务器并打开或保存文件。或者，你也可以经常在对话框的文件名字段中输入文件的完整路径，如 \\speaker\rodsmith\a-file.txt。

![](img/5d4d3092919d1d16884788127447cc6d_306_0.png)

图 11.9
你可以通过多次单击 Up One Level 图标或在 Look in 列表中定位 Network Neighborhood 来访问网络共享。

## Linux 作为 SMB 客户端

与 Windows 计算机的文件共享可以双向进行——可以从 Linux 访问 Windows 共享。事实上，有两种主要方法可以做到这一点：你可以使用一种快速简便的界面，或者将 Windows 共享像本地驱动器一样挂载。你可以使用这两种方法来访问实际 Windows 计算机或运行 Samba 的 Linux 或 UNIX 计算机上的 Windows 导出。由于 Samba 非常出色地模拟了 Windows 网络，因此在 Linux 客户端侧没有操作上的差异。

### 使用 smbclient

smbclient 程序为共享的 Windows 资源提供类似 FTP 的界面。一般来说，你可以通过键入其名称，后跟你打算使用的资源来开始使用 smbclient，如以下示例所示：

```
smbclient //nessus/shared
```

NOTE

> 在 Linux 中，你使用斜杠（/）字符而不是 Windows 中使用的反斜杠（\）。虽然你可以在 Linux 中使用反斜杠字符，但需要使用两倍的数量——机器名称前使用四个，反斜杠在机器名称和资源之间使用两个。

程序随后会提示你输入密码，如果你输入的密码服务器接受，你将被提示符迎接。你可以输入多个类似 FTP 的命令，包括以下内容：

- ls 或 dir—显示目录列表。
- cd—更改服务器上的新目录。
- lcd—更改本地机器上的新目录。
- get 和 mget—分别从服务器传输单个或多个文件。
- put 和 mput—分别向服务器传输单个或多个文件。
- ? 或 help—显示可用命令。
- quit—退出 smbclient。

还有许多其他 smbclient 命令，以及用于更改其行为的命令行选项。你可以查阅 smbclient 手册页以获取更多详细信息。

## 在 Linux 中挂载 Windows 卷

虽然 smbclient 对于偶尔的传输可能很方便，但它远不如实际挂载共享那样灵活。因此，很幸运 Linux 在内核中实现了对 SMB/CIFS 的支持，并且拥有允许你像挂载本地硬盘或 NFS 导出一样挂载 SMB 共享的实用程序。

### 将支持编译到内核中

如果你想挂载 Windows 或 Samba 共享，必须采取的第一步是确保内核中有适当的支持。在 Network File Systems 选项下，你应确保已选择 SMB 文件系统支持，作为模块或编译到内核文件中。如果你只计划挂载 Windows 95 共享，你还应选择 SMB Win95 bug work-around 选项。如果计划连接 Windows 98、Windows NT 或混合机器，则不应选择此最后选项。

### 使用 smbmount 命令

在最简单的形式下，你可以按如下方式使用 smbmount：

```
smbmount //nessus/shared -c /mnt/nessus
```
