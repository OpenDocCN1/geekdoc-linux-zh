
你现在可以使用 `--configure --user=nagios --group=nagios` 编译 Nagios，然后执行 `make`，最后通过 `make install` 安装带有所有管理文件和脚本的主界面。为了方便配置，使用 `sudo make install-config=/usr/local/etc` 目录。同样，输入 `sudo make install-command-mode=/system` 为所有可用选项的外部命令设置正确的权限。例如，现在有了 nagios 脚本。但在 Ubuntu 上，你必须手动创建一个如下内容的服务：`etc/systemd/system/nagios.service`

```ini
[Unit]
Description=Nagios
After=network.target
[Install]
WantedBy=multi-user.target
[Service]
Type=simple
User=nagios
Group=nagios
ExecStart=/usr/local/bin/nagios -cfg=/usr/local/etc/nagios/nagios.cfg
```

保存文件并启用服务：
```
$ systemctl enable /etc/systemd/system/nagios.service
$ systemctl start nagios
```
Nagios 现在已在你下方运行。

## 插件服务

Nagios 服务器拥有广泛的插件架构，你可以用它来监控 DHCP、HTTP 等更多服务。为了监控监控服务，要安装 Nagios Plugins，请访问下载页面（`https://nagios-plugins.org/downloads/`）并复制当前稳定版本的下载链接：

```
wget wget https://www.nagios-plugins.org/download/nagios-plugins-2.1.3.tar.gz
tar xvf nagios-plugins-2.1.3.tar.gz
```

![](img/97fdf078658cf34e6c480f18f1f2014d_89_0.png)

90 | The Hacker's Manual

# Nagios

进入新创建的目录，然后使用以下命令配置、编译并安装插件：
```
$ cd nagios-plugins-2.1.3/
$ configure --with-nagios-user=nagios --with-group=nagios --with-opt
$ make install
```

在移动之前，你应该调整默认配置，以指定用于存储 Nagios 监控的网络中其他计算机配置的目录。

使用以下命令打开主 nagios 配置文件：`nano /usr/local/nagios/etc/nagios.cfg` 并删除 `#` 符号以取消以下行的注释：
`cddir = /usr/local/nagios/etc`

保存并退出更改后的文件。你还想为 Nagios 指定一个电子邮件地址，以便在它发现所监控计算机出现问题时发送通知。虽然这完全是可选的，但拥有多个 Nagios 主机本身就是一个项目。在本教程中，我们将使用一个简单的脚本让 Nagios 向 Gmail 发送通知，你也可以通过以下命令打开联系文件：`sudo nano /usr/local/nagios/etc/objects/contacts.cfg` 并将默认地址替换为你自己的电子邮件地址。

## 进入仪表板

流程的最后一步是为 Web 仪表板配置环境。通过以下命令重新编译引擎和 Nagios 组件：`sudo apt update && sudo apt make all`
现在，可以通过复制示例配置文件在 Apache 内部完成设置虚拟主机：`sudo cp sample-config.cfg /usr/local/nagios/etc/nagios.cfg`。在编辑它以反映你的实际主机设置之前，为该文件赋予正确的访问权限：`chmod 644 /usr/local/nagios/etc/nagios.cfg`。你还需要更新管理界面的认证详细信息。命令 `sudo chown nagios:nagios /usr/local/nagios/etc/nagios.cfg` 将创建一个名为 nagiosadmin 的用户：

如果你已经安装了 Nagios，你可以添加 Linux 主机来监控它们之上的各种服务和属性。在监控 Windows 机器之前，编辑 Nagios 核心配置文件以取消以下行的注释：
`cfg_file = /usr/local/nagios/etc/objects/windows.cfg`

这让 Nagios 可以检测此主机中的 Windows 主机对象。下载最新版本的 Windows 监控客户端。双击下载的可执行文件并运行安装程序。在某些 Windows 安装中，你必须进入控制面板 > 管理工具 > 服务并双-

![](img/97fdf078658cf34e6c480f18f1f2014d_90_0.png)

在提交之前，检查配置的预检…………并检查包括所有主机和服务在内的所有组件的定义

> 始终记住在通过重启服务提交更改之前，检查 Nagios 配置并检查包括所有主机和服务在内的所有组件的定义。

提示你设置密码。仅此而已。现在重启 Nagios 和 Nagios 服务：

```bash
$ sudo service apache restart
$ systemctl restart nagios
```

然后在计算机上打开任何浏览器，通过输入你设置的计算机的域名或 IP 地址后加上 `/nagios` 来访问管理界面。通过 Nagios@192.168.1.304 访问 Nagios 管理界面 192.168.1.304。系统将提示输入你创建的 Nagios 管理凭据。

验证后，你将进入管理控制台，其中加载了大量信息。起初观察时，你会发现它的逻辑非常清晰且易于操作。从左侧导航栏上的 Hosts（主机）开始。如果你还没有配置任何监控的主机，仪表板页面将显示列表名称：localhost（安装并运行主机的机器）。

## 业务开放

你想要监控的客户端计算机在 Nagios 中被称为主机。添加主机时，可以通过物理方式或通过 SSH 进行配置，然后使用命令安装 Nagios 插件和 NRPE：`sudo apt install nagios-plugins nagios-nrpe-server`。NRPE 是 Nagios 远程执行器，允许你远程访问 Linux 服务器上的 Nagios 主机，以便你可以监控

# 监控 Windows 主机

如果你已经安装了 Nagios，你可以添加 Linux 主机来监控它们之上的各种服务和属性。在监控 Windows 机器之前，编辑 Nagios 核心配置文件以取消以下行的注释：
`cfg_file = /usr/local/nagios/etc/objects/windows.cfg`

在 NC 服务器上检测事件。切换到 OS 标签页并切换 Nagios 服务与桌面交互。当服务在 Windows 机器上运行时，切换到运行的 Nagios 主机并在服务内部编辑 Windows 主机。

```bash
$ sudo nano /usr/local/nagios/etc/windows.cfg
win10_host
```

```bash
define host {
  use = windows-server
  host_name = win10_host
  alias = Windows 10 Box
  address = 192.168.2.101
}
```

```bash
define service {
  use = generic-service
  host_name = win10_host
  service_Description = Uptime
  check_command = check_UPTIME
}
```

```bash
define service {
  use = generic-service
  host_name = win10_host
  service_Description = CPU load
  check_command = check_CPPLOAD!5,80
}
```

这些定义定义了 Windows 主机在网络中的位置，以及其运行时间和 CPU 负载。

黑客手册 | 91

## 软件

使用上述配置，Nagios 将仅监控主机在线或离线。你必须手动添加想要监控的其他服务块。例如，以下是间隔 ping 主机的方法：

```bash
define service {
  use = generic-service
  host_name = ubuntu_host
  service_description    PING
  check_command = check_ping!100.25,75%,5000,60
}
```

同样，以下是检查磁盘的方法：
```bash
```
