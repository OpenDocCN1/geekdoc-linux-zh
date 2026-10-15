

## 文件共享

## 第三部分

如果看到除了 grep 之外的进程，则说明 atalk 正在运行。你可以通过输入以下命令进一步检查功能

```
cat /proc/net/atalk_iface
```

该命令显示 atalkd 已附加到的设备信息。例如，在我的系统上，该命令报告如下：

```
eth0                 F500:DA  0000-FFFF  0
lo                   0000:00  0000-0000  0
```

这意味着 atalkd 使用地址 F500:DA 为 eth0 提供服务（网络地址 62720，节点地址 218，以十六进制表示），并监听 0 到 FFFE（65534）之间的网络。守护进程也已附加到 lo，即回环接口。

对 atalkd 基本功能进行最终测试的方法是使用 aecho 命令，它是 AppleTalk 的 TCP/IP ping 等价物——它向指定主机发送 AppleTalk Echo 请求，等待回复，并打印一些基本统计信息。你可以指定目标计算机的 AppleTalk 名称或其地址（网络和节点，用句点分隔，如 41201.173）。以下是我在网络上执行命令 aecho teela 的结果：

```
14 bytes from 41201.173: aep_seq=0, time=0. ms
14 bytes from 41201.173: aep_seq=1, time=0. ms
14 bytes from 41201.173: aep_seq=2, time=0. ms
14 bytes from 41201.173: aep_seq=3, time=0. ms

---41201.173 AEP Statistics---
4 packets sent, 4 packets received, 0% packet loss
round-trip (ms)  min/avg/max = 0/0/0
```

我在发送四个数据包后通过按 Ctrl+C 终止了此测试。

> **注意**
> 
> 你可以使用真正的 Macintosh 或另一台启用了 Netatalk 的计算机作为 aecho 命令的目标。不过，在配置过程的这个阶段，你不能对自己的计算机使用 aecho。

此时，我建议终止 atalkd，因为在下一节中你将学习如何通过单个命令同时启动它、afpd 和 papd。

## afpd 守护进程

让 atalkd 运行是好的，但单独使用它本质上是无用的。要配置 Netatalk 执行任何实际工作，你还必须配置并启动 afpd。

## 配置 afpd

你通过四个文件配置 afpd，所有文件均位于 /etc/atalk 目录中：

- config—设置整体配置选项。
- afpd.conf—控制与身份验证和数据传输最相关的选项。这些选项中的大多数可以在 config 文件中设置。
- AppleVolumes.default—指定你想要导出的目录。
- AppleVolumes.system—指定用于原生 Linux 文件的 Macintosh 创建者和类型代码。

## 创建 config 文件

/etc/atalk/config 文件包含在本图书 CD-ROM 上的特定 RPM 发行版中，并被 Netatalk 启动脚本使用。Netatalk 的另一个发行版可能不使用此文件。它包含提供 AppleTalk 服务的重要配置参数。你通过给出选项名称、等号和值来在此文件中设置选项。你可以在此文件中设置的重要选项包括以下内容：

- AFPD_MAX_CLIENTS—此选项是服务器允许的最大客户端计算机数量。默认值为 5。
- ATALK_NAME—此选项是你在 AppleTalk 网络上的计算机名称。默认设置尝试基于你的 Internet 机器名称，并通常有效。在某些情况下你可能需要指定其他名称。
- AFPD_NOCLR—你将此参数设置为 -c 以禁用明文登录。本书 CD-ROM 包含的 Netatalk 版本不支持加密登录，因此你应将此行注释掉。如果你想启用加密登录，你需要获取 Netatalk 的源代码和一个 DES 库，然后自行编译程序的自定义版本。
- AFPD_NOGUEST—你将此参数设置为 -g 以禁用访客（无密码）登录。默认设置允许访客登录。
- AFPD_GUEST—此选项指定访客用户的名称。默认值为 nobody，这会给访客用户非常严格的权限。
- PAPD_RUN—此选项指定启动脚本是否运行 papd 以提供打印机服务，取值为 yes 或 no。

