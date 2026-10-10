
# 利用工业级监控的力量来监控网络

监控网络是一项复杂的任务，但可能非常繁琐。如果我们所有人都能像架构师一样在舒适的家里管理自己的网络，那不是很好吗？想象一下一个管理员在凌晨 3 点从帮助台打来电话要求你处理。

Nagios 现在正在运行并正常工作。

## 插件服务

Nagios 服务器拥有广泛的插件架构，可以使用它来监控 FTP、HTTP 等服务。要监控监控服务器本身，你必须安装 Nagios 插件，去下载包（`https://www.nagios.org/plugins/`）并复制当前稳定下载链接。

切换到新创建的目录，然后使用以下命令配置、编译并安装插件：

```bash
$ nagios-plugins-2.1.3/
$ configure --with-nagios-user=nagios --ngroup=nagios --with-openssl
$ make
$ sudo make
```

在移动之前，您应该调整 Nagios 配置，以指定用于存储您想要 Nagios 监控的网络中其他计算机配置的目录。

使用 `nano /usr/local/etc/nagios/etc` 打开 nagios 主配置文件，向下滚动并删除 `#` 符号以取消以下行的注释：

```bash
cfg_dir=/usr/local/etc/nagios/etc
```

保存并退出带有指定目录的文件。您还想包含一个电子邮件地址，以便 Nagios 在检测到其监控的任何一台计算机时发送通知。这是可选的，但拥有多个主机是一个好主意。在后面的章节中，我们将使用一个特定的电子邮件地址，首先比假设 Nagios 通过电子邮件发送通知，使用 `nano /usr/local/etc/nagios/objects/contacts.conf` 打开配置文件，并将条目替换为您的电子邮件地址。

## 进入仪表板

流程的最后一步是为基于 Web 的仪表板配置环境。通过 `sudo make && sudo make check && sudo make install` 编译引擎和 Nagios 插件。

现在，通过 `sudo cp main/sample/httpd.conf /etc/sites-available/nagios.conf` 配置 apache 服务器配置，将 Nagios 设置为 Web 主机 Apache。在安装之前，使用 `sudo chmod 644 /etc/sites-available/nagios.conf` 赋予 apache 正确的访问权限，然后运行 `sudo apache restart`。您还需要为管理界面创建身份验证信息。使用命令 `sudo chown -R nagios:nagios /usr/local/etc/nagios/admin`；创建一个名为 `nagiosadmin` 的用户：

## 监控 Windows

如果您在 Linux 上安装了 Windows 主机，您可以使用 Nagios 监控各种服务及其属性。在监控 Windows 机器之前，编辑 Nagios 核心配置文件以包含 Windows 插件行：`cfg_file=/usr/local/etc/nagios/objects/windows.conf`。

这允许 Nagios 检测 Windows 主机的对象。下载最新版本的 Windows 监控客户端。双击可执行文件并通过设置向程序运行它进行安装。在某些 Windows 安装中，您必须前往“控制面板 | 管理工具 > 服务”，并点击提示设置其密码。操作仅此而已。现在重启 Nagios 和 Nagios 服务：

```bash
$ sudo service apache2
```

```bash
$ systemctl start nagios
```

始终记住检查 Nagios 配置（包含所有主机和服务的定义），通过重启服务器来提交更改。

![](img/d2d879b5f295fad9b17e4fc9976250c7_98_0.png)

然后可以在网络中的任何一台计算机上打开浏览器，通过您设置的计算机的域名或 IP 地址访问 nagios 管理界面。Nagios 服务的地址为 192.168.1.30。您可以通过 Nagios 访问 192.168.1.30 处的管理界面。系统将提示您输入创建的 `nagiosadmin` 凭据。

身份验证后，您将进入加载了信息的 Nagios 管理控制台。以逻辑方式展示所有主机非常简单，且操作非常直观。如果您在左侧还没有配置任何主机，请在导航栏或监控（monitoring）处开始添加主机。页面列表将向您显示：运行和正在安装的主机位置。

## 业务启动

您想要监控的客户端在 Nagios 中被称为主机（hosts）。要通过物理方式或 SSH 配置一个主机，请使用 `apt install plugins-nagios-nrpe-server` 安装 Nagios 插件和 NRPE。NRPE 是 Nagios 远程执行器，它允许您在可以监控的 Linux 机器上远程执行 Nagios 服务。

| definition service | |
| :--- | :--- |
| use | generic-service |
| host_name | win10_host |
| serviceDescription | |
| check_command | check_ntUPTIME |

当服务宕机时，切换机器到运行的 Nagios 服务，在服务内部定义 Windows 主机——

| definition service | |
| :--- | :--- |
| use | generic-service |
| host_name | win10_host |
| serviceDescription | |
| check_command | check_ntCPU! |

| definition host | |
| :--- | :--- |
| host_name | windows-server |
| alias | Windows 10 Box |
| address | 192.168.2.107 |

这些定义了 Windows 主机在网络中的位置，并定义了运行时间和 CPU 负载服务。

# 软件
