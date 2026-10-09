

## 第 2 课 实验 1
### 管理用户和组设置

![](img/477ccb2f05b6ba1b2d563ea74f18c197_927_0.png)

您可以在学生数据文件的 Managing_Users_and_Groups\Solution 文件夹中的 Lesson 2 Lab 1 solution.html 文件中找到本活动的建议解决方案。

**场景：**
一名合同工迈克（Mike）加入了您的组织。您需要根据以下详细信息为他创建一个用户账户：

- 用户名：contractor01
- 密码：myp@$$w0rd
- 用户账户的有效截止日期：2011 年 11 月 16 日
- 设置为默认主目录的目录：/home/oncontract/contractor01
- 密码应在多少天后过期：60 天
- 密码过期前多少天发出警告：7 天
- 新用户需要加入的组：Contract

- 1. 创建用户账户 contractor01，并配置用户配置文件。
- 2. 修改密码过期设置。
- 3. 创建组 Contract，并将用户 contractor01 添加到该组中。

## 第 3 课 实验 1
### 管理分区

![](img/477ccb2f05b6ba1b2d563ea74f18c197_928_0.png)

您可以在学生数据文件的 Managing_Partitions\Solution 文件夹中的 Lesson 3 Lab 1 solution.html 文件中找到本活动的建议解决方案。

**场景：**
作为系统管理员，您需要为新员工设置系统。您被要求配置他们的硬盘，并将磁盘上用户可访问的区域与包含系统和软件信息的敏感区域分开。您还必须用文件系统填充分区，并确保分区的易于识别。用户的需求如下：

usr 分区大小：1024 MB

root 分区大小：1024 MB

您还被要求创建一个标记为“公司策略”的文件系统，并将其放置在 usr 分区中。

- 1. 创建分区。
- 2. 在扩展分区内创建两个逻辑分区。
- 3. 为逻辑分区设置 ext2 文件系统。
- 4. 验证新分区具有 ext2 文件系统。
- 5. 为新创建的分区添加标签。
- 6. 为分区应用标签。
- 7. 验证已应用到分区的标签。
- 8. 使用其标签挂载分区。

## 第 3 课 实验 2
### 组织 Linux 中的文件

![](img/477ccb2f05b6ba1b2d563ea74f18c197_929_0.png)

您可以在学生数据文件的 Managing_Partitions\Solution 文件夹中的 Lesson 3 Lab 2 solution.html 文件中找到本活动的建议解决方案。

**数据文件：**
Software_Rules.txt, Hardware_Inventory.txt

**开始前：**
确保所需的数据文件已复制到 /root 目录中。

**场景：**
作为您组织的初级管理员，您需要执行以下任务：

- 将 Software_Rules.txt 文件从 /root 目录移动到 /home 目录。
- 将 Hardware_Inventory.txt 文件从 /root 目录复制到 /home 目录。
- 检查 Hardware_Inventory.txt 文件是否包含内容列表已在 2009 年 1 月更新的信息。
- 从 /root 目录中删除 Hardware_Inventory.txt 文件。
- 设置 Nautilus 浏览器以 Spatial 模式打开。

- 1. 将 Software_Rules.txt 文件移动到 /home 目录。
- 2. 将 Hardware_Inventory.txt 文件复制到 /home 目录。
- 3. 从 /root 目录中删除 Hardware_Inventory.txt 文件。
- 4. 将 Nautilus 浏览器的视图从 Browser 模式更改为 Spatial 模式。

## 第 4 课 实验 1
### 查找文件

![](img/477ccb2f05b6ba1b2d563ea74f18c197_930_0.png)

您可以在学生数据文件的 Managing_Files\Solution 文件夹中的 **Lesson 4 Lab 1 solution.html** 文件中找到本活动的建议解决方案。

**场景：**
您在多用户系统上工作，想要搜索您拥有的文件，这些文件位于系统中的不同目录中。您定期备份系统上的重要文件和目录。您还想定位那些超过两年的无用文件和目录，以便稍后能够删除它们。

- 1. 打开 GNOME 搜索工具并搜索由 root 用户拥有的文件。
- 2. 细化搜索以仅包括由 root 用户拥有的空文件。
- 3. 细化搜索以仅包括由 root 用户拥有且超过 730 天的空文件。

## 第 4 课 实验 2
### 管理 Linux 中的文件

![](img/477ccb2f05b6ba1b2d563ea74f18c197_931_0.png)

您可以在学生数据文件的 Managing_Files\Solution 文件夹中的 Lesson 4 Lab 2 solution.html 文件中找到本活动的建议解决方案。

**数据文件：**
Leave_Log.txt, Hardware_Report_09.txt, Empclaimfeb.txt, Empclaimjan.txt, Policies.txt

**开始前：**
确保所需的数据文件已复制到 /root 目录中。

**场景：**
您想要清理 Linux 系统中未使用的文件。在清理之前，您决定归档重要的工作相关文件，并在根目录中创建指向这些文件的链接。

- 1. 从您的主目录中删除 Leave_Log.txt 文件。
- 2. 在主目录中创建 Empclaimfeb.txt、Empclaimjan.txt 和 Policies.txt 文件的 zip 归档。
- 3. 在 / 目录中为 Hardware_Report_09.txt 文件创建一个硬链接。

## 第 5 课 实验 1
### 修改文件权限和所有权

![](img/477ccb2f05b6ba1b2d563ea74f18c197_932_0.png)

您可以在学生数据文件的 Linux_Permissions\Solution 文件夹中的 Lesson 5 Lab 1 solution.html 文件中找到本活动的建议解决方案。

**数据文件：**
*Leave_Log.txt, Stationery_List.txt*

**开始前：**
确保所需的数据文件已复制到 /root 目录中。

**场景：**
作为一名初级系统管理员，您负责管理管理团队成员的用户权限。在这个角色中，您需要执行以下任务：

- 1. 对系统中现有用户和组的数量进行审计。
- 2. 更改某些文件的权限。

- 1. 查看您 Linux 系统上的用户和组。
- 2. 修改 Leave_Log.txt 文件的权限，使其对所有用户只读。
- 3. 使用字符方法修改权限并验证更改。
- 4. 使用 Nautilus 浏览器修改 Stationery_List.txt 文件的权限，使其可被所有用户写入。
- 5. 使用属性对话框修改 Stationery_List.txt 文件的权限。

## 第 6 课 实验 1
### 配置系统设置

![](img/477ccb2f05b6ba1b2d563ea74f18c197_933_0.png)

您可以在学生数据文件的 Printing_Files/Solution 文件夹中的 Lesson 6 Lab 1 solution.html 文件中找到本活动的建议解决方案。

**数据文件：**
Onsite_Training_Policy.txt

**开始前：**
1. 如有必要，将 USB 打印机连接到系统。确保已下载必要的驱动程序并且打印机已准备好使用。
2. 将所需的数据文件复制到 /root 目录。

**场景：**
您已被调往现场进行培训。您想为运行 Linux 操作系统的笔记本电脑配置一台打印机。您还想应用文本格式并打印培训策略文档。

- 1. 在 srvB 上配置通用 Postscript 打印机。
- 2. 选择要配置的打印机的制造商和型号。
- 3. 检查 **printer2** 是否已添加到 **Local Printers**（本地打印机）列表中，并将其设为系统的默认打印机。
- 4. 对 Onsite_Training_Policy.txt 应用文本格式以每页打印 30 行。
- 5. 指定标题“The Onsite Training Policy”并为文档应用双倍行距后预览文档。

## 第 7 课 实验 1
### 管理软件包

![](img/477ccb2f05b6ba1b2d563ea74f18c197_934_0.png)

您可以在学生数据文件的 Managing_Packages\Solution 文件夹中的 Lesson 7 Lab 1 solution.html 文件中找到本活动的建议解决方案。

**开始前：**
1. 确保所有五个 RHEL 5.3 安装光盘均可用。
2. 在 srvA 上执行步骤。要在 srvB 上执行此实验，您需要配置 yum 软件包管理器以禁用 gpgcheck。

**场景：**
您被分配了管理网络上几台系统的任务。您需要使用 php 软件包更新所有系统。您决定设置一个中央仓库。

- 1. 从所有五个设置光盘中复制安装文件到 /setup 目录。
- 2. 将 /setup 目录定义为私有仓库。
- 3. 使用 YUM 软件包管理器安装 php 软件包。

