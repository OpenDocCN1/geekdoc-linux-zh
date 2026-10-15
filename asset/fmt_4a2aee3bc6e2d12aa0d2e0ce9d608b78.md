
最后的一点：NIS 对影子密码（`Shadow passwords`）的支持并不良好。Linux 通常使用影子密码来增加密码安全性。由于它们没有为 NIS 提供任何额外的安全性，最好不要在 NIS 中使用影子密码。请参阅用户手册了解有关影子密码的详细信息以及你的发行版是否使用了它们。

Windows 不能作为 NIS 服务器，但 `NISGina` 是适用于 Windows NT 的可用 NIS 客户端。`GINA`（图形化识别与认证）是 Windows NT 的登录屏幕。`NISGina` 将 Windows NT 中的 `msgnina.dll` 替换为它自己的版本登录程序 `nisgina.dll`。在设置 `NISGina` 时要非常小心。如果设置错误，将把你锁在电脑之外并导致电脑无法使用！（参见 http://www.ldv.ei.tum.de/software/nisgina/）。

首先，下载并解压文件。`NISGina` 的最新版本使用 `Install Shield` 自动安装。以下是手动安装的说明。

假设 Windows NT 安装在 `/winnt` 目录（默认目录），以管理员身份登录，并将 `*.dll` 和 `*.exe` 文件复制到 `/winnt/system32` 目录。首先，通过输入以下命令安装 `portmap`：

```
installservice portmap \winnt\system32\portmapservice.exe
```

你应该会收到服务已成功安装的消息。创建目录 `\winnt\var\run` 和 `\winnt\var\yp`。接下来，启动 `portmap` 服务：

```
net start portmap
```

安装 `ypbind` 并指定它将使用 `portmap` 服务：

```
installservice ypbind portmap \winnt\System32\ypbindservice.exe
```

现在，需要修改几个注册表项。最简单的方法是使用 `NisConfig.exe`，我们稍早将其复制到了 `\winnt\system32` 目录。某些版本会在控制面板上显示图标。启动此程序后，进入 NIS 标签页（见下图 16.2）。

![](img/a1ad58e4259f15e8b2826ecf57a28362_188_0.png)

设置 NIS 域、密码映射（`Password Map`）和组映射（`Group Map`）。你一次只能配置一个 NIS 域。一旦设置了 NIS 域，启动 `ypbind`：

```
net start ypbind
```

接下来，我们将使用熟悉的 NIS 工具测试 CIS：`ypwhich.exe`、`ypcat.exe` 和 `ypmatch.exe`。这些文件稍早已复制到 `/wind/system32` 目录。`ypwhich` 将返回 NIS 服务器的主机名或 IP 地址。如果没有返回，请检查 NIS 服务器是否正常工作以及 NIS 域是否正确。`ypcat <password map>` 将显示 NIS 密码文件。如果没有显示，请确保密码映射正确。例如，如果密码映射为 `passwd.byname`，则命令为：

```
ypcat passwd.byname
```

`xp_port 2f8. Add 10.0.0.1, port 805`

`mmcune:x:500:Mike McCune:/home/mmcune:/bin/bash`

其余部分为了简洁已删除。
