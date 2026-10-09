
- 带有USB端口的打印机

## 软件

- 讲师和学生使用的 Red Hat Enterprise Linux 5 授权副本。
- 讲师和每位学生使用的 Red Hat Enterprise Linux 5 救援 CD 副本。
- 讲师和学生使用的 Debian 5 副本。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_14_0.png)

硬盘的盘符取决于你将其硬盘总线连接到主板上的哪个插槽。如果连接到主主盘插槽，盘符将以 "a" 结尾；对于次主盘插槽，则为 "b"；对于主从盘插槽，则为 "c"；对于次从盘插槽，则为 "d"。对于 IDE 硬盘，盘符以 "hd" 开头，而对于 SATA 驱动器，则从 "sd" 开头。本课程活动的说明是基于连接到次主盘插槽的 SATA 驱动器编写的，因此盘符将为 "sdb"。

## 课堂设置

### 课堂网络连接

1. 为每位学生和讲师设置由两个系统组成的独立网络。
2. 将讲师系统标记为 **srvA** 和 **srvB**。**srvA** 服务器分配 IP 地址 192.168.0.2，**srvB** 服务器分配 IP 地址 192.168.0.3。
3. 将学生系统标记为 **Student X—srvA** 和 **Student X—srvB**，其中 X 是学生编号。为 **Student1—srvA** 和 **Student1—srvB** 分配 IP 地址 192.168.0.4 和 192.168.0.5。对于其他学生，为 **srvA** 分配偶数，为 **srvB** 分配奇数。
4. 在每个系统上安装 Red Hat Enterprise Linux 5.3。
5. 同步每个网络上的系统时间。

### 在 srvA 上安装 Red Hat Enterprise Linux 5.3

要在 **srvA** 上安装 Red Hat Enterprise Linux 5：

1. 将 Red Hat Enterprise Linux CD 1 插入 DVD-RW 驱动器。
2. 在 Red Hat Enterprise Linux 5 页面，要安装或升级现有系统，请按 **Enter** 键。
3. 在欢迎使用 Red Hat Enterprise Linux Server 页面，选择 **Skip**，然后按 **Enter** 键。
4. 在 Red Hat Enterprise 安装页面，单击 **Next**。
5. 在语言选择页面，在语言选择列表框中，验证已选中 **English (English)** 选项，并单击 **Next**。
6. 在键盘配置页面，在键盘选择区域中，验证已选中 **U.S. English**，并单击 **Next**。
7. 在安装号对话框中，输入随 Red Hat Enterprise Linux 5 CD 提供的安装号。
8. 要安装 Red Hat Enterprise Linux 5，选择 **Install Red Hat Enterprise Linux Server**，并单击 **Next**。
9. 在磁盘分区设置页面，从分区布局下拉列表中选择 **Create custom layout**，并单击 **Next**。
10. 删除现有分区。
11. 根据表格对硬盘进行分区，并单击 **Next**。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_14_1.png)

救援 CD 是执行第 16 课活动所必需的。Debian 5 是执行第 7 课活动所必需的。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_14_2.png)

活动将系统称为 **srvA** 和 **srvB**。学生需要使用其各自的系统 **Student X—srvA** 和 **Student X—srvB**。这将适用于本课程的所有活动。

| 类型 | 挂载点 | 大小 |
| --- | --- | --- |
| swap | | RAM 大小的两倍 (1024 MB) |
| ext3 | / | 20000 MB |

12. 在启动加载器配置页面，单击 Next。
13. 在网络配置页面，配置网络参数。
    - 单击 Edit。
    - 在 Enable IPv4 support 部分，在 Edit Interface 对话框中，选择 Manual configuration 选项。
    - 在 IP Address 文本框中，输入 192.168.0.2，在 Prefix(Netmask) 文本框中，输入 255.255.255.0
    - 取消选中 Enable IPv6 support 选项，并单击 OK。
    - 在 manual 选项旁边的文本框中，输入 srvA，并单击 Next。
    - 在 Error With Data 消息框中，两次单击 Continue。
14. 在时区选择页面，在所选城市下拉列表中，验证已选中 America/New_York 选项，并单击 Next。
15. 在设置 root 密码页面，在 Root Password 文本框中，输入 p@ssw0rd，并按 Tab 键。
16. 在 Confirm 文本框中，输入 p@ssw0rd，并单击 Next。
17. 在软件选择页面，在 Include Support 部分，勾选 Software Development 和 Web server 选项。
18. 在 Customize 部分，选择 Customize now 选项，并单击 Next。
19. 在第一个列表框中，选择 Servers 选项，并在相邻的列表框中，勾选 DNS Name Server、FTP Server 和 Network Servers 软件包。
20. 在第一个列表框中，选择 Desktop Environments 选项，并在相邻的列表框中，勾选 KDE (K Desktop Environment) 软件包。
21. 在第一个列表框中，选择 Base System 选项，并在相邻的列表框中，勾选 System Tools 软件包，并单击 Next。
22. 在即将安装页面，单击 Next 以开始安装。
23. 在 Required Install Media 对话框中，单击 Continue 以继续安装。
24. 在 Change CDROM 提示处，插入相应的 RHEL 5 CD。
25. 在 Congratulations 页面，单击 Reboot 以重启系统。
26. 在 Welcome 页面，单击 Forward。
27. 在 License Agreement 页面，验证已选中 Yes, I agree to the License Agreement 选项，并单击 Forward。
28. 在 Firewall 页面，从 Firewall 旋转框中选择 Disabled，并单击 Forward。
29. 在消息框中，单击 Yes。
30. 在 SELinux 页面，从 SELinux Setting 旋转框中选择 Disabled，并单击 Forward。
31. 在消息框中，单击 Yes。
32. 在 **Kdump** 页面，单击 **Forward**。
33. 在 **Date and Time** 页面，设置当前日期和时间，并单击 **Forward**。
34. 在 **Choose Server** 页面，单击 **Forward**。
35. 在 **Set Up Software Updates** 页面，选择 **No, I prefer to register at a later time** 选项，并单击 **Forward**。
36. 在 Red Hat 网络连接对话框中，单击 **No thanks, I’ll connect later**。
37. 在 **Finish Updates Setup** 页面，单击 **Forward**。
38. 在 **Create User** 页面，创建一个名为 *jsmith* 的用户账户，全名为 *Joyce Smith*，密码为 *myp@$$word*。
39. 在确认对话框中，单击 **Continue**。
40. 在 **Sound Card** 页面，单击 **Forward**。
41. 在 **Additional CDs** 页面，单击 **Finish**。
42. 在确认对话框中，单击 **OK** 以重启系统。
43. 在 GUI 登录屏幕，按 **Ctrl+Alt+F1** 切换到第一个终端。在 CLI 中以 *root* 身份登录，密码为 *p@$$word*。
44. 输入 `useradd eric` 并按 **Enter** 键，为 Eric 创建一个新的用户账户。
45. 输入 `passwd eric`，并指定 *myp@$$word* 作为密码。
46. 输入 `useradd robert` 并按 **Enter** 键，为 Robert 创建一个新的用户账户。
47. 输入 `passwd robert`，并指定 *myp@$$word* 作为密码。

## 在 srvA 上安装 Debian Linux 5 作为第二个操作系统（双启动）

要在 srvA 上安装 Debian Linux 5 作为第二个操作系统（双启动）：

1. 将 Debian Linux CD-01 插入 CD-ROM/DVD 驱动器并重启系统。
2. 在 **Installer boot menu** 页面，选择 **Graphical install** 选项并按 **Enter** 键。
3. 在 **Choose language** 页面，在 **Choose a language** 部分，验证已选中 **English**，并单击 **Continue**。
4. 在 **Choose language** 页面，在 **Choose a country, territory or area** 部分，验证已选中 **United States**，并单击 **Continue**。
5. 在 **Select a keyboard layout** 页面，在 **Keymap to use** 部分，验证已选中 **American English**，并单击 **Continue**。
6. 在 **Configure the network** 页面，观察网络自动配置失败的消息显示。单击 **Continue** 以手动配置网络。
7. 在 **Configure the network** 页面，在 **Network configuration method** 部分，选择 **Configure network manually** 选项，并单击 **Continue**。
8. 在 **Configure the network** 页面，在 **IP address** 文本框中，输入 *192.168.0.2* 作为 IP 地址。单击 **Continue**。
9. 在 **Configure the network** 页面，在 **Netmask** 文本框中，验证 *255.255.255.0* 是子网掩码，并单击 **Continue**。
10. 在 **Configure the network** 页面，在 **Gateway** 文本框中，验证 *192.168.0.1* 是网关地址，并单击 **Continue**。
11. 在 **Configure the network** 页面，在 **Name server addresses** 文本框中，验证 *192.168.0.1* 是名称服务器地址，并单击 **Continue**。

