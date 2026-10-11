
## 第 IV 部分：为团队上传文件

执行以下操作：

1. 选择 **Logout** 链接。
2. 使用 KWrite，在 /home/student 目录下创建一个名为 **agenda.txt** 的文本文件。
3. 以 **srife**（团队所有者）身份登录到 Virtual Office。
   您必须以团队所有者的身份登录，才能为团队上传文件。
4. 在左侧选择 **Efficiency Project**。
5. 在右侧 **Files** 下方，选择 **Upload**。
6. 选择 **Browse**。
7. 浏览并选择 /home/student/agenda.txt；然后选择 **Open**。
8. 在窗口底部选择 **Notify All Members**；然后选择 **Upload**。
9. 选择 **Close**。
   屏幕刷新，agenda.txt 显示为可用文件。
10. 选择 **Logout** 链接。
11. 以 **cgrayson** 身份登录。
12. 在左侧选择 **Efficiency Project**。
    注意，agenda.txt 可供 Chris Grayson 下载。

## 第 V 部分：为团队会议创建提醒消息

执行以下操作：

1. 选择 **Logout** 链接。
2. 以 **srife**（团队所有者）身份登录。
3. 在左侧选择 **Efficiency Project**。
4. 在右侧 **Discussion** 下方，选择 **New Message**。
5. 在主题字段中，输入 **Team Meeting Reminder**。
6. 在消息字段中，输入 **Don't forget the team meeting tomorrow**。
7. 标记 **Notify All Members**；然后选择 **Post**。
8. 选择 **Logout** 链接。
9. 以 **cgrayson** 身份登录。
10. 在左侧框架中，选择 **Efficiency Project**。
11. 在右侧的 Discussion 下方，选择 **Team Meeting Reminder** 消息。
12. 尝试使用 Virtual Office 的其他功能。
13. 完成后，关闭网页浏览器。

（练习结束）

## 总结

| 目标 | 摘要 |
| :--- | :--- |
| 1. 描述 Virtual Office | Virtual Office 是一个 Web 访问门户，允许远程用户与工作组团队进行协作和信息共享。<br><br> Virtual Office 通过允许用户自行设置和管理许多网络、信息共享和数据备份过程，优化了用户的自助服务概念。<br><br> Virtual Office 还允许用户创建自己的功能团队，称为 Virtual Teams，以便进行交互式实时协作。<br><br> 加入虚拟团队的人员可以访问共享文档、讨论帖、书签和团队日历。团队的所有成员都可以访问团队信息和服务。 |
| **1. 描述 Virtual Office（续）** | - 使用 Virtual Office，用户可以<br>- 定位并设置打印机<br>- 设置和维护密码<br>- 备份信息<br>- 与其他用户和组进行实时通信<br>- 发布个人 Web 页面，以便向其他用户提供信息<br>- 使用任何启用 Web 的设备从任何位置访问重要信息<br>- 将 Web 页面加入书签 |
| 2. 安装 Virtual Office | 安装 Novell Nterprise Linux Services (NNLS) 时，您可以将 Virtual Office 作为可选组件进行安装。当您选择 Virtual Office 时，NNLS 安装脚本将安装服务器所需的所有组件。<br><br> 由于 Virtual Office 主页提供对其他已随 NNLS 安装的产品进行 Web 访问，如果您希望从 Virtual Office 访问以下产品，则需要在安装期间选择这些产品：<br>- eGuide<br>- iFolder<br>- iPrint<br>- NetMail<br><br> Virtual Office 主页仅显示您所选产品的快捷按钮。 |
| 3. 配置 Virtual Office | 在 iManager 中，您可以配置以下服务：<br>- Company Info Service<br>- NetStorage<br>- iPrint<br>- eGuide<br>- ZENworks<br>- Bookmarks<br>- Groupwise 配置<br>- Lotus Notes 配置<br>- Microsoft Exchange 配置<br>- NetMail 配置<br>- IMAP/POP3 服务器配置<br>- 公共 Web 页面<br>- 更改密码<br><br> 您可以使用 Virtual Office 主页配置许多 Virtual Office 服务。要打开虚拟办公室主页，请打开浏览器窗口并输入 http://server_IP_or_DNS/vo。<br><br> 您从此位置配置以下服务：<br>- 书签<br>- 更改密码<br>- 公共 Web 页面<br>- 虚拟团队<br>- 虚拟团队服务 |

## 第 10 部分 为 Novell CLE 实习做准备

强调这些场景有助于学生为 NNLS 服务部分的实习做准备。

这些场景不包括可能作为测试 LPI 1 级认证目标一部分的 Linux 管理员任务。

在学生开始场景 1 之前，您需要向他们提供一个干净的 SuSE\* SLES 8 安装环境。

在本部分中，您将完成以下场景，以帮助您为 CLE 实习做准备：

- 场景 1：安装 NNLS（必需）
- 场景 2：业务需求文档 1
- 场景 3：业务需求文档 2
- 场景 4：业务需求文档 3

初始场景是必需的。然后，您可以根据时间选择剩余场景中的一个或两个来配置 NNLS 产品。

场景 2、3 和 4 为您提供了一个业务需求列表，您需要作为 Digital Airlines 办公室的网络管理员来满足这些需求。

虽然一些需求在所有 3 个场景中都是相同的，但其他需求可能会改变测试或配置 NNLS 服务以满足相同需求的方式。

![](img/d63035f3fce0eaaf97203dde900affb7_284_0.png)

> 在课堂环境中，在您开始场景 1 之前，您的讲师将提供干净的 SuSE\* SLES 8 安装环境。

### 场景 1：安装 NNLS（必需）

Digital Airlines 目前正在使用 NetWare® 上的 eDirectory™ 和其他 Nterprise™ 服务向客户和员工提供网络服务。

然而，随着 NNLS 的可用，CTO 已决定开始将多项 Nterprise 服务（如 iFolder® 和 iPrint）迁移到 Linux 服务器。

您最近收到了一份文档，概述了在办公室交付 Nterprise 服务于 Linux 上的业务需求，以及这些服务的时间表。

为了满足这些需求和时间表，您需要立即开始创建并测试一个满足业务需求的 NNLS 实验室环境配置。

您决定从一个安装了 NNLS 的单个 Linux 服务器开始。

执行以下操作：

- 安装 Mozilla 1.5，并使用课堂上分配给您的参数为您的服务器准备 NNLS 安装环境（您的 *container*、**10.0.0.x**、**DAx**）。
  遵循您在第 1 和第 2 部分中遵循的相同说明。
- 使用课堂上分配给您的默认值安装 NNLS 的所有组件（*您的* **container**、**10.0.0.x**、**DAx**）。
  遵循您在第 2 部分中遵循的相同说明。
- 将您在第 3 部分中导入的相同 LDIF 文件导入到您的树中。
- 运行您的 eDirectory 树的健康检查，以确保没有错误。

### 场景 2：业务需求文档 1

在安装了 NNLS 1.0 并导入了 LDIF 文件后，您在实验室环境中实施并测试以下业务需求：

- 您必须能够订阅 3015 频道并安装 NNLS 的任何更新。所有 NNLS 服务的 man 页必须能从终端会话窗口中的 shell 提示符访问。您必须能够导入和导出 eDirectory 的 CSV 文件，并备份输出目录中的任何 CSV 文件。

![](img/d63035f3fce0eaaf97203dde900affb7_286_0.png)

> 使用与第 5 部分中相同的 Delimited Text 驱动器的基本配置。

为了满足此要求：

- 硬盘上 sample.csv 文件中的所有员工必须导入到您 eDirectory 树中的 **tempwork.your container** 容器中。*您的 container* 中 WPU5ERS 组的所有成员必须导出到硬盘上的 **pilots.csv** 文件。要备份输出目录中的 CSV 文件，创建一个名为 **backupcsv** 的脚本，该脚本将当前输出目录中的所有 CSV 文件打包成一个 tarball，并将其移动到 /tmp/csvbackup 目录。确保 /tmp/csvbackup 目录具有与 /tmp 目录相同的权限。创建一个 cron 作业，每周星期五下午 5:00 执行一次 backupcsv 脚本。

