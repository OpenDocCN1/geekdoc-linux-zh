

## 分析服务器并确保其安全

## 红帽企业版 Linux 

![](img/59afb92e10b67a9cecc358a2c65e93b5_583_0.png)

```
$ student@servera-lab...~$ ls -l /var/log
audit
df.log-20190310
df.log-20190310
df.log-20190310
df.log-20190310
df.rpm-20190310
chrony-20190310
cloud-init.log-20190310
cloud-init.log
kernel.log-20190310
secure.log-20190310
samba.log-20190310
spooler.log-20190310
messages-20190310
lastlog
hawkey
gmu.au
README
tmp
```

图 16.12：非特权终端会故障排除

## 创建诊断报告

诊断报告是红帽 Linux 系统配置数据、系统信息和诊断信息的集合。完成后的报告中收集的数据包括系统日志和调试信息，可用于排除故障。

以特权用户身份登录 Web 控制台。点击左侧导航栏中的**诊断报告**（Diagnostic Reports），打开创建这些报告的页面。点击**创建报告**Create Report）按钮生成新的诊断报告。

![](img/59afb92e10b67a9cecc358a2c65e93b5_583_1.png)

图 16.13：诊断报告

报告完成后，界面将显示“完成!”（Done!）。点击**下载报告”（Download report）按钮保存报告。

## 第 1 章 | 分析服务器并获取支持

![](img/59afb92e10b67a9cecc358a2c65e93b5_584_0.png)

图 16.14：已完成的报告

点击“保存文件”（Save File）完成该过程。

![](img/59afb92e10b67a9cecc358a2c65e93b5_584_1.png)

图 16.15：保存诊断报告

完成后的报告将保存到访问 Web 控制台的系统的 Downloads 目录。在本例中，该系统是 workstation（工作站）。

![](img/59afb92e10b67a9cecc358a2c65e93b5_584_2.png)

图 16.16：访问已完成的报告

## 使用 Web 控制台管理系统服务

作为 Web 控制台的特权用户，你可以停止、启动、启用和重启系统服务。此外，你可以配置网络接口、配置防火墙规则、管理账户等。以下图像显示了使用 Web 控制台管理工具的常见示例。

RH124-RHEL8.0-en-1-20190507

## 系统电源选项

Web 控制台允许你重启或关闭系统。以特权用户身份登录 Web 控制台。点击左侧栏中的“系统”（System）访问系统电源选项。

从“电源选项”（Power Options）下拉菜单中选择所需的选项来重启（Restart）或关闭（Shut Down）系统。

![](img/59afb92e10b67a9cecc358a2c65e93b5_585_0.png)

## 控制运行中的服务

你可以使用 Web 控制台中的图形化工具启动、启用、禁用和停止服务。点击左侧导航栏中的“服务”（Services）访问 Web 控制台服务的首页。点击服务首页右上角的“服务”按钮。服务按已启用（Enabled）、已禁用（Disabled）和静态（Static）部分显示。滚动页面以选择你想管理的服务。

在下例中，顺着 chron.service 行操作打开服务管理页面。

![](img/59afb92e10b67a9cecc358a2c65e93b5_585_1.png)

点击管理界面右侧的相应按钮来停止、重启或禁用服务。在本例中，该服务正在运行，因此“启动”按钮不显示。点击任何高亮链接或滚动查看服务管理部分下方显示的“日志”（Logs），可以获取与服务相关的更多信息。

## 第 15 章 | 分析服务器并获取支持

![](img/59afb92e10b67a9cecc358a2c65e93b5_586_0.png)

## 配置网络接口和防火墙

要防火墙规则和网络接口，点击左侧导航栏中的“网络”（Networking）。以下示例显示了如何收集网络接口信息以及如何管理它们。

![](img/59afb92e10b67a9cecc358a2c65e93b5_586_1.png)

图 16.20：网络：初始视图

点击“接口”（Interfaces）部分中所需的接口名称以访问管理页面。在本例中，选择了 ens3 接口。

RH124-RHEL8.0-en-1-20190507

## 第 19 章 | 分析服务器并获取支持

| 名称 | IP 地址 | 发送 | 接收 |
| :--- | :--- | :--- | :--- |
| ens3 | 172.250.10/24 | 8.48 Kbps | 4.75 Kbps |

图 16.21：网络：接口

管理页顶部显示所选设备的网络活动。向下滚动查看设置和管理选项。

![](img/59afb92e10b67a9cecc358a2c65e93b5_587_0.png)

图 16.22：网络：接口

要修改或添加接口配置，点击高亮链接。在本例中，IPv4 链接显示了 ens3 接口的 IP 地址和掩码 `172.250.10/24`。要为 ens3 网络接口添加额外的 IP 地址，点击链接。

## 第 1 章 | 分析服务器并获取支持

| ens3 Red Hat, Inc. Virtio device virtio_net 状态 ON | 负载 自动 |
| :--- | :--- | :--- |
| IPv4 地址 | 172.250.10/24 | |
| DNS | 172.250.254 | |
| 搜索域 | lab.example.com, example.com | |
| IPv6 | 自动 | |
| MTU | 自动 | |

图 16.23：网络：ens3 配置

在“手动”（Manual）列表右侧点击 + 添加额外的 IP 地址。在相应字段输入 IP 地址和网络掩码。点击“应用”（Apply）激活新设置。

![](img/59afb92e10b67a9cecc358a2c65e93b5_588_0.png)

图 16.24：为现有接口添加 IP 地址

显示会自动切换回接口管理页面，你可以在那里确认新的 IP 地址。

RH124-RHEL8.0-en-1-20190507

## 第 19 章 | 分析服务器并获取支持

![](img/59afb92e10b67a9cecc358a2c65e93b5_589_0.png)

图 16.25：确认新的 IP 地址

## 管理用户账户

作为特权用户，你可以在 Web 控制台中创建用户账户。点击左侧导航栏中的“账户”（Accounts）查看现有账户。点击“创建新账户”（Create New Account）打开账户管理页面。

![](img/59afb92e10b67a9cecc358a2c65e93b5_589_1.png)

图 16.26：现有用户账户

输入新账户的信息，然后点击“创建”（Create）完成操作。

## 创建账户

| 全名 | 新用户 |
| :--- | :--- |
| 用户名 | nuser |
| 密码 | ******** |
| 确认 | ******** |

![](img/59afb92e10b67a9cecc358a2c65e93b5_590_0.png)

显示会自动切换回账户管理页面，你可以在那里确认新用户账户。

![](img/59afb92e10b67a9cecc358a2c65e93b5_590_1.png)

## 参考

cockpit(1)、cockpit-ws(8) 和 cockpit.conf(5) 手页

有关更多信息，请参阅*红帽企业版 Linux 8.0 Beta* 使用 Cockpit 管理系统的指南中的**使用 Cockpit Web 界面管理系统**https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8-beta/html/managing_systems_using_the_cockpit_web_interface/

## 引导练习

## 分析管理远程服务器

在此练习中，你启用并访问服务器上的 Web 控制台以对其管理、诊断并解决问题。

## 结果

你应该能够使用 Web 控制台监控基本系统功能、检查日志文件、创建用户账户并访问终端。

## 开始之前

在工作站上使用 student 作为密码登录 student 用户。

从工作站运行 `lab support-cockpit start` 命令。该命令运行一个脚本来确定主机 servera 和 serverb 是否在网络上可达。

```
[student@workstation -] $ lab support-cockpit start
```

- 1. 使用 ssh 命令以 student 用户登录 servera。系统配置为使用 SSH 密钥验证，因此登录 servera 不需要密码。

```
[student@workstation -] $ ssh student@servera
激活 web 控制台: systemctl enable --now cockpit.socket[student@servera -]$
```

- 2. 系统上已安装 Web 控制台，但尚未激活。启用并启动 cockpit 服务。

- 2.1. 使用 `systemctl enable --now cockpit.socket` 命令启用 Web 控制台。

```
[student@servera -] sudo systemctl enable --now cockpit.socket
[sudo] password for student: student
Created symlink /etc/systemd/system/sockets.target.wants/cockpit.socket -> /usr/lib/systemd/system/cockpit.socket.
```

- 3. 在工作站上，打开 Firefox 并以 student 用户身份和密码登录 servera.lab.example.com 系统上的 Web 控制台界面。

- 3.1. 打开 Firefox 并访问 https://servera.lab.example.com:9090 地址。

- 3.2. 通过将其添加为异常来接受自签名证书。

