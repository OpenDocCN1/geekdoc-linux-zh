
也修改你的 services 文件 (/etc/services)。找到 vmware-authd 条目并更改你想要使用的端口号。

```
vmware-authd 902/tcp
```

接下来，你需要重启 xinetd 守护进程：

```
/etc/init.d/xinetd restart
```

## 37.3 设置 VMware 管理界面的会话长度并禁用登录

管理界面会话的默认超时设置是 60 分钟。此超时值可以通过修改管理界面配置文件来更改。

### Windows

在文件 C:\Program Files\VMware\VMware Management Interface\htdocs\init.pl 中更改 vmware_SESSION_LENGTH 的设置

```
$ENV{vmware_SESSION_LENGTH} = 60;
```

### Linux

对于 Linux，你需要运行管理实用程序的配置脚本。这将提示你输入想要的分钟数。

```
/usr/bin/vmware-config-mui.pl
```

对于 Windows 和 Linux，你也可以通过将超时值指定为 0 来禁用对管理界面的访问。登录屏幕将显示一条消息以警告用户登录被禁止：VMware Management Interface 已关闭且不允许登录。

当你在配置文件中指定 -1 时，会话将永远不会超时。

## 37.4 访问 VMware GSX Server 日志文件

如果你在 VMware GSX Server 环境中遇到任何问题，日志文件是开始调查的好地方。本段仅为你指出正确的日志文件位置。

### Virtual machine log file

每个虚拟机都会保留自己的日志，记录正在发生的事情。它创建在虚拟机的配置目录中，即 .vmx 文件所在的位置。

### Virtual machine event log file

对于 GSX Server 主机上运行的每个虚拟机，都使用一个日志文件来存储有关该机器事件和问题的信息。最基本的信息是它已开机或关机。此信息也在管理界面中 VM 属性的“用户和事件”选项卡中显示。机器的日志文件存储在以下路径：

对于 Windows：

```
C:\Program Files\VMware\
    VMware GSX Server\vmserverdRoot\eventlog
```

对于 Linux：

```
/var/log/vmware
```

### VMware virtual machine Console log file

用于访问虚拟机控制台的客户端应用程序也会存储一个日志文件。它存储在用户的 TEMP 目录中。你可以了解活动日志文件和位置。最简单的方法是在 VMware 虚拟机控制台帮助菜单的“关于”信息中查看此信息。

### VMware Management Interface log file

用于管理你的 VMware GSX Server 的 Web 服务器也保留一个日志文件。在 Windows 主机上，它称为 mui.log，存储在 C:\Program Files\VMware\VMware Management Interface 中。在 Linux 上，日志文件称为 error_log，存储在 /var/log/vmware-mui 中。

### VMware Authorization Service Log File

授权服务的日志记录默认未启用。你必须在配置文件中添加以下行以启用日志记录：

```
vmauthd.logEnabled = true
log.vmauthdFileName = "vmauthd.log"
```

对于 Windows，配置文件称为 config.ini，位于以下位置：C:\Documents and Settings\All Users\Application Data\VMware\VMware GSX Server。在 Linux 主机上，文件称为 config，存储在 /etc/vmware 目录中。

修改此设置后，你需要重启 VMware 授权服务。对于 Windows，你可以从“管理工具”中的“服务控制中心”执行此操作。对于 Linux，重启 xinetd 守护进程：

```
/etc/init.d/xinetd restart
```

### VMware Registration Service log file

所有 VMware GSX Server 的一般活动都记录在名为 vmware-serverd.log 的文件中。它存储在以下目录中：

对于 Windows：

```
C:\Windows\Temp
```

对于 Linux：

```
/var/log/vmware
```

### Installation log files

在安装 VMware 软件期间，会创建安装日志。对于 Windows，文件称为 VMInst.log。它保存在执行安装的用户 TEMP 目录中。一个示例是 `C:\Documents and Settings\Administrator\Local Settings\Temp`。在 Linux 主机上，日志文件称为 locations，存储在 `/etc/vmware` 中。

## 37.5 使用 VMware GSX Server 脚本命令

VMware 创建了一个非常全面的脚本 API，可用于 VMware GSX Server 和 ESX Server。API 可以在基于 COM 的语言（如 Visual Basic）或 Perl 脚本语言中使用。

对于喜欢编程的管理员以及想要创建软件来管理 VMware 环境的第三方开发人员来说，脚本 API 非常有价值。但对于普通管理员来说，从批处理文件或 shell 脚本运行的简单任务很可能就足够了。为此目的，VMware 包含了 vmware-cmd 实用程序，可在 Windows 和 Linux 上用于自动化任务。

注意：脚本 API 至今仍可使用，但也有 Virtual Infrastructure Software Developer's Kit 可用。有了这套 Web 服务，你可以做同样的事情，甚至更多。

可以执行的操作范围从启动和停止虚拟机到更改配置参数和连接可移动设备。

### Suspending virtual machines

脚本可用于的实际场景之一是，当你关闭主机时希望挂起虚拟机而不是让它们关闭；在主机重新启动后需要再次启动整个客户机操作系统。以下是一个简单的脚本，它会挂起虚拟机然后重启机器：

```
#script to reboot the server
#first suspends the virtual machines and then reboots
vmware-cmd /data1/vmware/nw65/nw65.vmx suspend
vmware-cmd /data1/vmware/suse10/suse10.vmx suspend
vmware-cmd /data1/vmware/sles9/sles9.vmx suspend
#maybe do some other stuff;-)
reboot
```

此示例脚本演示了该实用程序的语法。vmware-cmd 命令后面跟着配置文件路径和名称，并以要执行的操作结尾。

### Preparing for a backup

在第 35.5 节中，我解释了备份正在运行虚拟机的 VMware GSX Server 主机是个坏主意。此外，我建议停止虚拟机，并在备份后重新启动它们。以下脚本扩展了我为重启主机而创建的脚本。在此脚本中，我不会手动列出虚拟机，而是使用 vmware-cmd -l 命令列出所有已列出的虚拟机：

```
for vm in $(vmware-cmd -l); do
  vmware-cmd $vm suspend
done
```

如果你运行此脚本并且虚拟机已处于挂起状态或电源关闭状态，实用程序将生成错误消息，说明机器处于错误状态。因此，如果你有空闲时间和脚本技能，你可以使用 vmware-cmd getstate 命令检查虚拟机状态来扩展它。

### Command reference

在本节末尾，我想为你提供 vmware-cmd 实用程序可用的完整选项集。要处理虚拟机操作，请使用以下语法：

```
vmware-cmd <options> <vm-cfg-path> <vm-action> <arguments>
```

要处理基于服务器的操作，请在命令中添加 -s 参数。

```
vmware-cmd -s <options> <server-action> <arguments>
```

表 37.1：vmware-cmd 命令的选项。

| 选项 | 描述 |
|---|---|
| -H <host> | 指定替代主机（如果设置，则必须同时设置 -U 和 -P） |
| -O <port> | 指定替代端口 |
| -U <username> | 指定用户 |
| -P <password> | 指定密码 |
| -h | 更详细的帮助 |
| -q | 安静 - 最小输出 |
| -v | 详细 |

表 37.2：vmware-cmd 实用程序的服务器操作。

| 选项 | 描述 |
|---|---|
| -l | 列出已注册的 VM |
| -s register <config file path> | 注册 VM |
| -s unregister <config file path> | 注销 VM |
| -s getresource <variable> | 检索服务器资源 |
| -s setresource <variable> <value> | 设置服务器资源 |

