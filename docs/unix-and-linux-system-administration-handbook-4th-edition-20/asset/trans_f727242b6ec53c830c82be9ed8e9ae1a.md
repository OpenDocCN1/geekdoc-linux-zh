

# 第10 章 备份

与其对应的 Autochanger（自动换带器）资源。名称（Name）还可以帮助您记住该资源描述的是哪部分设备。

AlwaysOpen 参数告诉 Bacula 除非管理员显式请求卸载（unmount），否则保持设备处于打开状态。此选项可以节省时间并减少磁带磨损，因为避免了回绕和定位作业作业。

```
Device {
Name = TL4000-Drive0
Media Type = LTO-3
Archive Device = /dev/nst0
AutomaticMount = yes
AlwaysOpen = yes
RemovableMedia = yes
RandomAccess = no
Autochanger = yes
}
```

# 自动换带器资源

可选的 Autochanger 资源定义仅在您幸运地拥有磁带库时才需要。它将存储设备与自动换带器关联，并指定让换带库交换磁带的命令。

```
Autochanger {
Name = TL4000
Device = TL4000-Drive0,TL4000-Drive1
Changer Command = "/etc/bacula/mtx-changer %c %o %s %a %d"
Changer Device = /dev/changer
}
```

# bconsole.conf：控制台配置

控制台与目录（director）通信以调度作业、检查作业状态或恢复数据。bconsole.conf 告诉控制台如何与目录通信。此文件中的参数必须与配置文件 (bacula-dir.conf) 中 Director 资源中提供的参数对应，Address 参数除外。

# 控制台配置文件，bconsole.conf

```
Director {
Name = bull-dir
DIRPort = 9101
Address = bull
Password = "zHpScUnHN9"
}
```

# 安装和配置文件守护进程 (file daemon)

安装在备份客户端上的文件守护进程在执行备份和恢复时与 Bacula 守护进程通信。在每台要使用 Bacula 备份的计算机上都必须安装并配置文件守护进程。

# 将媒体添加到池（pools）中

Bacula 以二进制形式提供于许多平台，包括 Windows 和 Linux 发行版。在 UNIX 系统上，您可以通过运行 `./configure --enable-client-only` 随后执行 `make` 和 `make install` 从原始源码树安装文件守护进程。您可以在配置时为许多文件选项硬编码默认值，但如果将它们列在 `bacula-fd.conf` 文件中，维护会更容易。默认情况下，二进制文件安装在 `/sbin`，配置文件在 `/etc/bacula`。

安装文件守护进程后，通过编辑 `bacula-fd.conf` 来进行配置，该文件分为三部分。第一部分由 Director 资源组成，它告诉文件守护进程为哪个目录调度备份。Director 资源还包含一个 Password 参数，该参数必须与目录配置文件中 Client 资源列出的密码完全一致。

bacula-fd.conf 的第二部分是 FileDaemon 资源，它命名客户端，并指定了文件守护进程监听目录守护进程命令的端口。

最后一个组件是 Messages 资源（请参阅第 323 页），它定义了如何处理本地消息。

# 启动 Bacula 守护进程

在安装了服务器守护进程并配置了测试客户端后，下一步是运行服务器目录下的启动脚本（`/bacula start`）来启动守护进程。此命令也用于每个客户端以启动客户端的文件守护进程。

bacula 启动脚本应在系统启动时运行。根据您的系统和安装方法，这可能会自动完成或手动完成。参见第 3 章“启动与关机”，获取有关如何在您的示例系统在启动时启动服务的更多信息。

一旦守护进程运行，您就可以使用控制台程序（安装目录下的 `bconsole`）来检查它们的状态、将媒体添加到池中并执行备份和恢复作业。只要 bconsole 已正确安装和配置，您就可以运行它。

```
$ /bconsole
```
Connecting to Director bull:9101
...
（注：此处后续为示例交互输出，通常根据要求保留或或进行语境性翻译，此处已完成上述正文本的完整翻译）

