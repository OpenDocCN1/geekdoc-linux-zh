# 从 RedHat 迁移到 SUSE Linux Enterprise Server 10 管理手册











![](img/d3c94bc7006978796634313176d5ffa7_0_0.png)

![](img/d3c94bc7006978796634313176d5ffa7_0_1.png)
















# 引言

















* 练习 8-5 检查网络配置 . . . 8-9



# 引言

本手册旨在帮助您练习与从 RedHat 迁移到 SUSE Linux Enterprise Server 10（课程 3068）目标相关的技能。

通过涵盖 SUSE Linux Enterprise Server 10 的特定管理细节，本课程为参加 Novell Certified Linux Professional 10 (Novell CLP 10)认证实践考试做准备——前提是您已经拥有 SUSE Linux Enterprise Server 10 基础（课程 3071）、SUSE Linux Enterprise Server 10 管理（课程 3072）以及 SUSE Linux Enterprise Server 10 高级管理（课程 3073）课程中的通用 Linux 知识。

从 RedHat 迁移到 SUSE Linux Enterprise Server 10 课程 DVD 包含一个 SUSE Linux Enterprise Server 10 安装镜像，可以在可以在外配合《从 RedHat 迁移到 SUSE Linux Enterprise Server 10 训练手册》来练习参加 Novell CLP 10 实践考试所需的技能。

还提供了一个未安装操作系统的 VMware 镜像。您可以使用它按照第 1 节练习中的描述安装 SUSE Linux Enterprise Server 10。

设置自学环境的说明位于学生 DVD 的目录中。

![](img/d3c94bc7006978796634313176d5ffa7_4_0.png)





# 练习约定

在进行练习时，你将看到一些约定，这些约定指示了你需要输入的针对你特定服务器的信息。

以下是最常见的约定：

- *斜体/粗体文本*。这指的是你特定的情况，例如你服务器的主机。
- 例如，如果你的服务器主机名为 DA50，而你看到以下内容：

  `hostname.digitalairirlines.com`
  你应该输入
  `DA50.digitalairirlines.com`
- **10.0.0.xx**。这是分配给你的 SUSE Linux Enterprise Server 10 服务器的 IP 地址。

  例如，如果你的 IP 地址是 10.0.0.50，而你看到以下内容：

  `10.0.0.xx`
  你应该输入
  `10.0.0.50`
- **选择（Select）**。练习步骤中使用 *select*（选择）一词表示各种操作，包括点击界面上的按钮和选择菜单项。
- **输入（Enter）和输入（Type）**。*enter*（输入）和 *type*（输入）这两个词具有不同的含义。
  *enter* 意味着在字段或命令行中输入文本，并在必要时按下 Enter 键。*type* 意味着输入文本但不按下 Enter 键。

  如果你被指示要 *type*（输入）一个值，请确保你不要按下 Enter 键，否则你可能会启动一个你尚未准备好启动的进程。


在本练习册的范围内，你将学习如何执行以下操作：

- 在 1-2 页执行“安装 SUSE Linux Enterprise Server 10”

在此练习中，你将安装 SUSE Linux Enterprise Server 10。


在此练习中，你将安装 SUSE Linux Enterprise Server 10。请参考以下规范作为指南：

- 一个 1 GB 的交换空间（swap）分区。
- 一个 6 GB 的 / 分区（硬盘上应留有空间以便在后续练习中添加分区）。
- 使用默认软件模式，添加 C/C++ 编译器和工具模式。
- root 密码：novell
- （由于 novell 在生产环境中显然不适合作为 root 密码，你可以使用其他的；但本手册中的练习将 novell 作为 root 密码。）
- 使用固定 IP 地址；教师将告知你使用哪一个：
  - IP 地址：
  - 网络掩掩码：255.255.255.0
  - 主机名：
    - 域名：digital airlines.com
    - 域名服务器：10.0.0.254
  - 默认网关：10.0.0.254
- （如果你是在自学中进行此练习且网络中没有其他学生，请使用 10.0.0.10 作为 IP 地址，使用 da10 作为主机名。）
- 使用本地认证；创建用户账户 geeko，密码：novell。
- 跳过在线更新

## 完成此练习的详细步骤：

- 第一部分：从安装介质启动
- 第二部分：为你的硬盘配置分区
- 第三部分：配置已安装的服务器

# 第一部分：从安装介质启动

要从安装介质启动，请执行以下操作：

1. 开启电脑。
2. 将 SUSE Linux Enterprise Server 10 DVD 插入 DVD 驱动器。
3. （可选）如果你的电脑没有从驱动器启动，通过选择 **Reset（重置）** 按钮或按下 **Ctrl+Alt+Del** 重启电脑。
4. 当 GRUB 安装界面出现时，使用方向键选择 **Installation（安装）** 并按下 **Enter**。
5. 在语言选择对话框中，选择*你的语言*；然后选择 **Accept（接受）**。

调整 BIOS 设置，使 DVD 驱动器成为第一个启动设备并重启电脑。

> 虽然你可以选择任何可用语言，但本手册中的练习是用美式英语编写的。

6. 当 YaST 显示 **Novell Software Agreement（许可协议）**时，选择 **Yes, I Agree to the License Agreement（是的，我同意许可协议）**，然后点击 Next。
7. 当安装模式对话框出现时，选择 **New Installation（新安装）**；然后选择 **Next**。
8. 在 **Clock and Time Zone（时和时区）**对话框中选择你的时区。如果需要，选择 UTC 并将时间调整为当前时间。

完成后，选择 Next。出现一个 Installation Settings（安装设置）建议对话框。

9. 选择 Keyboard Layout（键盘布局）：选择你的键盘布局；选择 Accept。

你将返回 Installation Proposal（安装建议）对话框。

# 第二部分：为你的硬盘配置分区

1. 通过选择 Partitioning（分区）来更改分区设置。

2. 选择 Create Custom Partition Setup（创建自定义分区设置）；然后选择 **Next**。

3. 选择 Custom Partitioning -- for experts（自定义分区——专家级）；然后选择 **Next**。

4. 删除现有分区：

   a. 在 Expert Partitioner（专家分区器）对话框中，检查分区列表中是否存在任何现有分区。
   b. 如果存在分区，选择对应分区的硬盘项（如 hda 或 hdc）。
   c. 通过选择 Delete（删除）删除所选硬盘上的所有现有分区。
   d. 当被要求确认删除时，选择 Yes（是）。
   e. （可选）如果系统中有多个包含分区的硬盘，重复步骤 b、c、d，直到列表中只剩下硬盘项。

5. 创建交换分区（swap partition）：
   a. 从分区列表中选择硬盘项；然后选择 **Create（创建）**。
   如果有多个硬盘，选择较大的磁盘。
   b. 选择 Primary partition（主分区）；然后选择 OK。
   c. 在尺寸设置的 End（结束）字段中输入 `+1GB`。
   d. 从 File（文件）文件系统下拉列表中选择 Swap（交换分区）。
   e. 通过选择 OK 添加交换分区。

6. 创建根分区（root partition）：

   a. 选择你创建交换分区时使用的同一个硬盘；选择 **Create（创建）**。
   b. 选择 **Primary partition（主分区）**；然后选择 **OK**。
   c. 在尺寸设置的 End（结束）字段中输入 **+6GB**。
   d. 确保设置了以下选项：
      - 在 File file system（文件系统）下拉列表中应选择 **Reiser**。
      - 在 Mount Point（挂载点）下拉列表中应选择 **/**。
   e. 通过选择 **OK** 添加根分区。

7. 通过选择 **Finish（完成）**确认分区设置并返回安装建议。

8. 在 Installation Settings Overview（安装设置概览）中，选择 **Accept（接受）**。

9. 在确认对话框中，选择 **Install（安装）**。
10. （可选）如果你使用的是 CD，YaST 会在安装过程中要求更换 CD，当第一张 CD 上的软件完成后，服务器可能会重启。

插入所需的 CD 并选择 **OK**。

# 第三部分：配置已安装的服务器和域名对话框，

1. 当显示 **Hostname（主机名）**时，在 **Hostname** 字段中输入*主机名*，并在 **Domain Name（域名）** 字段中输入 digital airlines.com。

2. 取消 Hostname by DHCP（通过 DHCP 设置主机名）前面的选择；然后选择 **Next**。

3. 现在系统 **Administrator（管理员）**“root”**Password（密码）**对话框。在 **Password for root（root 用户密码）** **User** 和 **Confirm Password（确认密码）** 字段中输入*novell*。

4. 选择 **Next** 继续。

提示你密码过于简单。

5. 选择 Yes 继续。

提示你正在使用小写字母。

6. 选择 Yes 继续。

7. 在 Network Configuration（网络配置）建议中，选择 Firewall（防火墙）启用。项目将变为 Firewall is disabled（防火墙已禁用）。

8. 从 Network Configuration建议中选择 Network Interfaces（网络接口）。

9. 选择第一个检测到的网卡并 Edit。

10. 选择 Static Address Setup（静态地址设置）。

11. 在 IP Address 字段中输入你的 IP 地址。

12. 在 Subnet Mask（子网掩码）字段中输入 255.255.255.0。

13. 配置主机和名称服务器：
   a. 选择 Hostname and Name Server（主机名和名称服务器）。
   b. 你的主机名应该已经正确填写；如果没有，输入你的主机名和域名 digital airlines.com。
   c. 如果选择了 Update Name Servers and Search List by DHCP（通过 DHCP 更新名称服务器和搜索列表），请点击它取消选择。
   d. 在 Network Server 1（网络服务器1）字段中输入名称服务器 10.0.0.254。
   e. 选择 OK 返回网络设置对话框。

14. 配置路由（routing）：
   a. 选择 Routing（路由）。
   b. 在 Default Gateway（默认网关）字段中输入 10.0.0.254。
   c. 选择 OK 返回网络设置对话框。

15. 选择 Next 返回 Network Configuration（网络配置）对话框。

16. 选择 Next 继续安装；然后再次选择 Next。





- 17. 在“测试 Internet 连接”对话框中，选择**否，跳过此测试**；然后选择**下一步**。

- 18. 在**服务配置**对话框中，选择**下一步**以接受默认设置。

- 19. 在“用户身份验证方法”中，选择**本地 (/etc/passwd)**；然后选择**下一步**。

- 20. 添加一个用户：
    - a. 用户全名：**Geeko Novell**
    - b. 用户登录名：**geeko**
    - c. 密码：**novell**
    - d. 确认密码：**novell**
    - e. 选择**下一步**创建用户；在弹出“密码太简单”和“全全小写密码”的对话框中选择**是**。

- 21. 在**发行说明**对话框中，选择**下一步**。

- 22. 在**硬件配置**对话框中，检查**显卡**下建议的设置。对于不正确的设置，选择相应的项目并在弹出的对话框中进行更正。

- 23. 设置无误后，在硬件配置对话框中选择**下一步**。

- 24. 选择**完成**完成安装过程。

（练习结束）

# 第 2 部分 YaST

在本教程的章节中，你将学习如何执行以下操作：

- 2-2 页的“了解 YaST”
  在本练习中，你学习如何使用 YaST 的不同用户界面以及如何启动某些 YaST 模块。
- 2-5 页的“安装软件”
  在本练习中，你将安装 SUSE Linux Enterprise Server 10 安装介质上提供的另一个软件包包。
- 2-7 页的“使用 YaST 管理用户账户”
  在本练习中，你将使用 YaST 用户管理模块创建和删除用户账户。
- 2-9 页的“配置密码安全设置”
  在本练习中，你将练习更改安全设置。

## 练习 2-1

## 了解 YaST

在本练习中，你将学习如何使用 YaST 的不同用户界面以及如何启动某些 YaST 模块。在第一部分中，你将启动 YaST 的图形用户界面。在第二部分中，你将使用 YaST 系统日志模块查看文件 /proc/version。在第三部分中，你将设置时间。在第四部分和第五部分中，使用 YaST 的 ncurses 用户界面重复第一、第二部分的操作。

要使用 YaST，请执行以下操作：

- 第一部分：启动 YaST
- 第二部分：查看系统日志文件内容
- 第三部分：更改日期
- 第四部分：启动 YaST 的 ncurses 界面
- 第五部分：查看系统日志文件内容
- 第六部分：退出 YaST

### 第一部分：启动 YaST

要启动 YaST，请执行以下操作：

- 1. 从 GNOME 桌面打开主菜单。
2. 选择“更多应用程序”。
3. 在过滤文本框中输入 `ya`。
4. 选择 YaST 图标启动 YaST。
5. 在弹出的对话框中输入 root 密码 novel；然后选择“继续”或按回车键。
出现 YaST 控制中心。

### 第二部分：查看系统日志文件内容

要查看系统日志文件的内容，请执行以下操作：

- 1. 选择“杂项 > 查看系统日志”。
- 2. 从顶部下拉列表中选择 `/proc/version`。
3. 选择“确定”关闭日志窗口。

### 第三部分：更改日期

要更改日期时间，请执行以下操作：

- 1. 选择“系统 > 日期和时间”。
2. 选择“更改”。
3. 输入当前时间（如 08:00:00）和当前日期（如 27/04/2006）。
4. 选择“应用”。
5. 选择“接受”。

### 第四部分：启动 YaST 的 ncurses 界面

要启动 YaST 的 ncurses 界面，请执行以下操作：

- 1. 按 Ctrl+Alt+F1 切换到第一个虚拟终端。
2. 使用密码 novel 以 root 身份登录。
3. 输入 `yast -l` 查看可用的 YaST 模块列表。
4. 输入 `yast` 启动 YaST 的 ncurses 界面。

### 第五部分：查看系统日志文件内容

要查看系统日志文件的内容，请执行以下操作：

- 1. 一直向下方向键，直到左侧框架高亮显示“杂项”并按回车。
- 2. 一直向下方向键，直到右侧框架高亮显示“查看系统日志”并按回车。
- 3. 一直向下方向键，直到选中 `/proc/version` 并按回车。
- 4. 双击 Tab 键高亮“确定”并按回车。

### 第六部分：退出 YaST

要退出 YaST，请执行以下操作：

- 1. 按 Alt+Q 选择“退出”。
- 2. 输入 exit 注登录。
- 3. 按 Ctrl+Alt+F7 切换回图形界面。
- 4. 关闭 YaST 窗口。

（练习结束）


在本练习中，你将安装 SUSE Linux Enterprise Server 10 安装介质上提供的另一个软件包。它名为 `locate`，在后续章节中会需要用到。

要安装新软件，请执行以下操作：

- 第一部分：启动 YaST
- 第二部分：查找软件包
- 第三部分：安装软件包并完成

### 第一部分：启动 YaST

要启动 YaST，请执行以下操作：

- 1. 从 GNOME 桌面打开主菜单。
2. 选择“更多应用程序”。
3. 在过滤文本框中输入 `ya`。
4. 选择 YaST 图标启动 YaST。
5. 在弹出的对话框中输入 root 密码 novel；然后选择“继续”或按回车键。
6. 出现 YaST 控制中心。

### 第二部分：查找软件包

要查找软件包，请执行以下操作：

- 1. 从 YaST 控制中心，选择“软件 > 软件管理”。
2. 从过滤下拉列表中选择“搜索”。
3. 在搜索框中输入 `locate`；选择“搜索”。

### 第三部分：安装软件包并完成

要安装软件包并完成，请执行以下操作：

- 1. 从窗口右侧选择软件包 `findutitls-locate`。
- 2. 选择“接受”。
- 3. （条件性的）如果提示，插入 SUSE Linux Enterprise Server 10 DVD；然后选择“确定”。
- 4. 当询问是否安装或删除软件包时，选择“否”。
- 5. 选择“关闭”关闭 YaST 控制中心。
- 6. （条件性的）如果是从 DVD 安装的，请从驱动器移除 DVD。

（练习结束）


在本练习中，你将使用 YaST 用户管理模块创建和删除用户账户。在第一部分中，你为用户“Tux Penguin”创建一个名为“tux”的新账户，密码为“novell”。在第二部分中，你以 tux 身份登录。在第三部分中，你打开文件 /etc/passwd 并查找 geeko 和 tux 的条目。在第四部分中，你以 geeko 身份登录并删除 tux 的账户。

使用 YaST 管理用户账户，请执行以下操作：

- 第一部分：使用 YaST 创建用户账户
- 第二部分：以用户登录
- 第三部分：查看 passwd 文件

### 第一部分：使用 YaST 创建用户账户

要使用 YaST 创建用户账户，请执行以下操作：

- 1. 从 GNOME 桌面选择“应用程序 > 系统 > YaST”；输入密码 novel 并选择“继续”。
2. 从 YaST 控制中心，选择“安全和用户 > 用户管理”。
3. 选择“添加”添加新用户。
4. 输入以下信息：
   - 用户全名：Tux Penguin
   - 用户名：tux
   - 密码：novel
   - 确认密码：novel
5. 完成后，选择“接受”。
6. 选择“是”确认密码警告。
7. 选择“完成”保存新设置。
8. 关闭 YaST 窗口。


要以新用户身份登录，请执行以下操作：

- 1. 从底部面板开始通过选择**桌面 > 注销**进行注销。
2. 在注销对话框中，选择**确定**。
X Window 重启并出现 GUI 登录界面。
3. 在“用户名”字段中输入 **tux** 并按**回车**。
4. 在“密码”字段中输入 **novell** 并按**回车**。
5. 关闭或取消任何显示的对话框。

### 第三部分：查看 passwd 文件

要查看 passwd 文件，请执行以下操作：

- 1. 双击桌面上的 **tux 的主目录** 图标启动 Nautilus 文件管理器。
   显示 tux 主目录的内容。
2. 浏览到目录 **/home.**。
   注意这里有用户 tux 和 geeko 的目录。
3. 浏览到目录 **/etc.**。
4. 选择文件 **passwd.**。
   注意文件末尾用户 tux 和 geeko 的条目。
5. 关闭所有窗口。

（练习结束）




## 练习 2-4 配置密码安全设置

在此练习中，你将练习更改不同的安全设置。将按下 Ctrl+Alt+Del 键时的默认行为更改为停止机器。还将加密方式从 blowfish 更改为 MD5。使用 YaST 本地安全模块完成上述操作。

## 完成此练习的详细步骤：

1. 打开终端窗口。
2. 通过输入 `grep ctraltldel /etc/inittab` 检查文件 `/etc/inittab` 中 Ctrl+Alt+Del 键的设置。
注意当前的设置：
3. 启动 YaST 并选择 安全与用户 (Security and Users) > 本地安全 (Local Security)。
出现“本地安全配置”对话框。
4. 确保选择了自定义设置 (Custom Settings)；然后选择“下一步 (Next)”。出现“密码设置 (Password Settings)”对话框。
5. 从密码加密方法 (Password Encryption Method)”下拉列表中选择 MD5。
6. 选择“下一步 (Next)”继续。
出现“启动设置 (Boot Settings)”对话框。
7. 从“Ctrl + Alt + Del 的解释 (Interpretation of Ctrl + Alt + Del)”下拉列表中选择 停止 (Halt)。
8. 选择“下一步 (Next)”继续。
出现“登录设置 (Login Settings)”对话框。
9. 选择“下一步 (Next)”接受默认设置。
出现“添加用户 (Adding User)”对话框。

10. 选择“下一步 (Next)”接受默认设置。
出现“杂设置 (Miscellaneous Settings)”对话框。

11. 选择“完成 (Finish)”接受默认设置并为系统配置新设置。

12. 要测试更改，必须通过重启系统或在终端窗口中（以 root 身份）输入 `init q`（重新加载 /etc/init 文件）来激活新配置。
    a. 从终端窗口执行 `su -` 切换到 root（密码为 novel），
    b. 输入 `init q` 重新加载文件 `/etc/initabb`。

13. 通过输入 `grep ctrlaltd /etc/initabb` 验证 Ctrl+Alt+Del 设置已更改。
注意此设置现在是“shutdown -h”，而不是你在第 2 步中记录的内容。

14. 按 Ctrl+Alt+F2 测试此设置；然后按 Ctrl+Alt+Del。
系统将关机而不是重启。

15. 开启电脑并以 geeko 身份登录 Gnome 桌面。
16. （可选）使用 YaST 安全设置模块将 Ctrl+Alt+Del 的默认恢复为重启。

（练习结束）

WB 2-10 严禁复制本手册的全部或部分内容或分发此类副本。版本 1\如需报告疑似抄袭，请拨打 1-800-PIRATES。

## 第 3 节 网络配置

在本工作簿中，你将学习如何执行以下操作：

- 3-2 页的“从 YaST 管理网络配置信息”
在此练习中，你将所有网络配置信息更改为静态值。

- 3-6 页的“手动配置网络连接”
在此练习中，你将学习如何手动配置网络。


到目前为止，你的系统通过 DHCP 获取所有网络配置信息。在此练习中，你将所有重要信息更改为静态值。

使用 `ip` 命令找出你当前正在使用的 IP 地址。同时记录你当前的主机名。然后使用你找到的值将网络配置更改为静态 IP 地址。使用 10.0.0.254 作为默认网关以及服务器地址。

要从 YaST 管理网络配置信息，请执行以下操作：

- 第一部分：获取你的 IP 号和主机名
- 第二部分：启动 YaST 网络配置模块
- 第三部分：输入静态 IP 地址和子网掩码
- 第四部分：更改你的主机名
- 第五部分：输入 DNS 服务器
- 第六部分：输入默认网关
- 第七部分：激活新设置并完成

## 第一部分：获取你的 IP 号和主机名

获取你的 IP 号和主机名，请执行以下操作：

1. 从 GNOME 桌面打开主菜单。
2. 选择 更多应用程序 (More Applications)。
3. 在过滤文本框中输入 `term`。
4. 选择 Gnome Terminal 图标启动终端仿真。
5. 输入 `/sbin/ip address show` 以为你的 SUSE Linux Enterprise Server 10 服务器记录以下信息：
    * IP 地址：
    * 主机名：
6. 关闭终端窗口。

## 第二部分：启动 YaST 网络配置模块

启动 YaST 网络配置模块，请执行以下操作：

1. 从 GNOME 桌面打开主菜单。
2. 选择 更多应用程序 (More Applications)。
3. 在过滤文本框中输入 `ya`。
4. 选择 YaST 图标启动 YaST。
5. 在出现的对话框中输入 root 密码 `novel`；然后选择 继续 (Continue) 或按回车。
出现 YaST 控制中心。
6. 通过选择 网络设备 (Network Devices) > 网卡 (Network Card) 启动网卡模块。

## 第三部分：输入静态 IP 地址和子网掩码

输入静态 IP 地址和子网掩码，请执行以下操作：

1. 确保带有 ifup 的传统方法 (Traditional Method with ifup) 并选择“下一步 (Next)”。
你的网卡列在上方表中。
2. 确保选中了你的网卡；然后选择“编辑 (Edit)”。
3. 确保“地址 (Address)”选项卡已激活。
4. 通过选择“静态地址设置 (Static address setup)”切换设置。
5. 在“IP 地址 (IP Address)”字段中，输入第一部分中的 IP 地址。
6. 在“子网掩码 (Subnet mask)”字段中，输入 `255.255.255.0`。

## 第四部分：更改你的主机名

更改你的主机名，请执行以下操作：

1. 选择 主机和名称服务器 (Host name and name server)。
2. （条件）如果出现对话框指示 resolv.conf 文件已被临时修改，选择 修改 (Modify) 继续。
3. 在“主机名 (Hostname)”字段中，输入第一部分中的主机名。
4. 在“域名 (Domain Name)”字段中，输入 `digitalairlines.com`。

## 第五部分：输入 DNS 服务器

输入 DNS 服务器，请执行以下操作：

1. 在“名称服务器 1 (Name Server 1)”中，输入你的 DNS 服务器 IP 地址 (10.0.0.254)。
2. 如果其他名称服务器文本字段中有值，请将其删除。
3. 在“域搜索 (Domain Search)”字段中，输入 `digitalairlines.com`。
4. 如果其他域搜索文本字段中有值，请将其删除。
5. 选择 确定 (OK)。

## 第六部分：输入默认网关

输入默认网关，请执行以下操作：

1. 选择 路由 (Routing)。
2. 在“默认网关 (Default Gateway)”字段中，输入你的互联网网关 IP 地址 (10.0.0.254)。
3. 选择 确定 (OK)。

## 第七部分：激活新设置并完成

激活新设置并完成，请执行以下操作：

1. 选择 下一步 (Next)。
2. 选择 下一步 (Next)。
3. 关闭 YaST 控制中心。
4. 测试你的网络连接，启动 浏览器 Firefox 并尝试访问 http://www.novell.com。

（练习结束）
## 练习 3-2 手动配置网络连接

此练习目的是让你熟悉手动配置网络。

在第一部分，使用命令 `ip` Find IP 地址、路由、mac 地址的当前设置，以及位于 `/etc/sysconfig/hardware/` 存储网卡硬件配置的文件以及该文件中的配置选项。

在第二部分，使用 YaST 删除当前的网络配置。

在第三部分，使用 `ip` 命令手动设置网络。由于只使用了 `ip` 命令，此配置是永久的。

在第四部分，使用编辑器重建第一部分记录的 `/etc/sysconfig/hardware/` 文件，以及文件 `/etc/sysconfig/network/ifcfg-eth-id-address` 和 `/etc/sysconfig/network/routes`。重启电脑并测试重启后网络是否设置。

## 完成此练习的详细步骤：

- 第一部分：记录当前网络配置
- 第二部分：使用 YaST 删除当前网络设置
- 第三部分：手动配置网络
- 第四部分：保存网络连接到接口和硬件配置


记录当前网络配置，请执行以下操作：

1. 在图形桌面上，打开终端窗口并 `su -` 切换到 root（密码为 novel）。
2. 输入 `ip address show eth0`（取决于设置，你可能需要使用 eth1 代替 eth0）。
3. 找到以 `inet` 开头的行，记录该行显示的 IP 地址和子网掩码：
    - IP 地址：
    - 子网掩码：
4. 输入 `ip route show`。
5. 找到以 `default` 开头的行，记录网关的网关 IP 地址：
    - 网关 IP 地址：
6. 输入 `ip link show eth0`。
7. 找到以 `link/ether` 开头的行，记录网卡的 MAC 地址：
    - MAC 地址：
8. 输入以下命令切换到 `/etc/sysconfig/hardware` 目录：

```
cd /etc/sysconfig/hardware
```
9. 输入 `ls -al`，然后寻找以下文件之一（取决于你的硬件配置）：
    - hwcfg-id-PCI_address
    - 或者
    - hwcfg-bus-pci-PCI_address
10. 记录文件名称：





注意：如果存在多个符合上述模式的文件，请在终端窗口中输入 `lspci`。输出显示了计算机中 PCI 硬件组件的 PCI 地址。

11. 输入以下命令之一显示文件内容：

- `cat hwcfg-id-PCI_address`
或
- `cat hwcfg-bus-pci-PCI_address`

12. 记录以下参数：

- MODULE=
- MODULE_OPTIONS=
- STARTMODE=

你将在第四部分中使用这些参数和 `hwcfg` 文件名来创建文件。

### 第二部分：使用 YaST 删除当前网络设置

要使用 YaST 删除当前网络设置，请执行以下操作：

1. 启动 YaST，并选择网络设备（Network Devices） > 网卡（Network Card）。
2. 选择带有 `ifup` 的传统方法（Traditional Method）。
3. 选择网卡；然后选择删除（Delete）。
4. 选择下一步（Next）。
5. 在终端窗口（以 root 身份），输入 `rm /etc/sysconfig/network/routes`。
6. 输入 `ping 10.0.0.254` 验证网络连接已不再工作。
7. 输入 `ip address show`。

注意设备 `eth0` 已不再处于状态或不再列在列表中。

### 第三部分：手动配置网络

要手动配置网络，请执行以下操作：

1. 要再次初始化设备 `eth0`，在终端窗口中输入：
`hwup bus-pci-PCI_address`

你在第一部分第 10 步中记录了 PCI 地址。该命令看起来类似于：
`hwup bus-pci-000\02\00.0`

2. 输入以下命令：
`ip address add_IP_address/24 brd + dev eth0`

3. 要激活网络设备，输入 `ip link eth0 up`。
4. 要设置默认路由，输入以下内容：
`ip route add default via gateway_IP_address`

5. 输入 `ping www.novell.com.` 验证网络连接是否恢复工作。

### 第四部分：将网络连接保存到接口和硬件配置文件

要将网络连接保存到接口和硬件配置文件，请执行以下操作：

1. 在终端窗口中，切换到目录 `/etc/sysconfig/network`。
2. 输入以下内容创建网络配置模板的副本：
`ifcfg.template ifcfg-eth-id-MAC_address`
3. 使用 vi 编辑器打开副本（`ifcfg-eth-id-MAC_address`）。
4. 找到以下选项并输入指定的值：
- STARTMODE='auto'
- BOOTPROTO='static'
- IPADDR='your_IP_address/24'
- NETMASK='255.255.255.0'
- BROADCAST='10.0.0.255'
5. 保存文件并退出 vi (:wq)。
6. 切换到目录 `/etc/sysconfig/hardware`。
7. 使用 vi 创建以下文件之一：
- `hwcfg-id-PCI_address`
或
- `hwcfg-bus-pci-PCI_address`

8. 输入你在练习第一部分最后一步中记录的参数。
9. 完成后，保存文件并退出编辑器。
10. 切换到目录 `/etc/sysconfig/network`。
11. 使用 vi 创建一个名为 `routes` 的新文件。
12. 在文件中添加以下行：
```
default default_gateway_IP_address - -
```
13. 保存文件并退出 vi。
14. 重启系统 (`init 6`) 并以 `geeko` 登录，密码为 `nov`。
15. 在终端窗口（以 root 身份），输入以下命令验证网络配置是否正确加载：
```
ip address show eth0
ip route show
```
16. 输入 `ping www.novell.com.` 验证网络连接是否正常。





/dev/hda5 /apps ext2 acl,user_xattr 1 2

此条目确保系统在启动时，新的文件系统会被挂载。

- 8. 目录 /srv 的当前内容不再可见，因为它被用分区 /dev/hda6（或 /dev/sda6，取决于你的硬件）的挂载点。要将内容复制到新分区，请执行以下操作：
a. 通过输入以下命令卸载 /dev/hda6（或 /dev/sda6，取决于你的硬件）：
umount /srv
b. 通过输入命令将分区 /dev/hda6（或 /dev/sda6，取决于你的硬件）挂载到 /mnt 下：
mount /dev/hda6 /mnt
c. 将 /srv 的内容移动到 /mnt：
mv /srv/* /mnt
d. 卸载 /mnt 并使用 /etc/fstab 中的条目重新挂载 /dev/hda6（或 /dev/sda6，取决于你的硬件）：
mount /mnt
mount -a
e. 通过输入 ls /srv/ 验证你移动的文件是否可以再次在 /srv 下使用。

## 第二部分：使用 fdisk 手动分区

要使用 fdisk 进行手动分区，请执行以下操作：

- 1. 在命令行，通过输入 fdisk /dev/hda 启动服务器上第一块 IDE 硬盘的 fdisk 工具（如果你的电脑使用 SATA 或 SCSI 磁盘，请输入 fdisk /dev/sda）。根据磁盘上磁道的数量，系统会显示一条磁道数超过 1024 的消息，这在某些情况下可能会导致问题。
- 2. 通过输入 p 在 fdisk 中查看当前分区表。

注意有 5 个分区（hda1, hda2, hda3, hda5 和 hda6）。

- 3. 通过执行以下操作在扩展分区中创建一个 500MB 的 Win95 FAT32 逻辑分区：
a. 输入 n 创建新分区。
b. 输入 l（小写 L）表示逻辑分区。
c. 输入回车键接受默认的第一个磁道。
d. 输入 +500M 指定分区大小。
e. 输入 t 将分区类型更改为 Win95 FAT32（代表类型，从提供的范围中选择最大的分区号，然后输入 b 代表 Win95/FAT32）。
f. 输入 p 验证新分区配置。
注意表中添加了一个新的 hda7 分区。

- 4. 通过执行以下操作创建 2 个具有（默认）分区类型的逻辑分区：
a. 输入 n 创建新分区；输入 l（小写 L）；然后输入回车键接受默认的第一个磁道。
b. 输入 +1G 指定分区大小。
c. 输入 n 创建新分区；输入 l（小写 L）；然后输入回车键接受默认的第一个磁道。
d. 输入 +2G 指定分区大小。
e. 输入 p 验证新分区配置。
注意分区表中添加了 2 个新分区。

- 5. 输入 w 将新分区表写入硬盘并退出 fdisk。

- 6. 通过输入以下命令查看内核使用的当前分区表：
cat /proc/partitions

- 7. 为了能够访问新分区，内核必须更新存储在内存中的分区表。执行以下操作之一：
- 输入 reboot 重启系统。
- 输入 partprobe 让内核更新其分区表。

- 8. 通过输入 /proc/partitions 再次查看内核使用的分区表。

## 第三部分：从命令行管理文件系统

要从命令行管理文件系统，请执行以下操作：

- 1. 从 GNOME 桌面打开终端窗口；然后使用 su - 切换到 root（密码为 novel）。

- a. 通过输入以下命令在 /dev/sda7 上创建一个新的 FAT32 文件系统并将其标记为 "data1”（确保在命令中指定设备时没有拼写错误；不会有警告消息，命令将立即执行）：
mkfs.msdos -n data1 /dev/sda7

类似 mkfs.msdos 2.11 (12 Mar 2005) 的消息确认了文件系统的创建。

- b. 通过输入以下命令在 /dev/sda8 上创建一个带有详细输出的新型 ext2 文件系统（确保在命令中指定设备时没有拼写错误；不会有警告消息，命令将立即执行）：
mkfs -t ext2 -v /dev/sda8

注意通过添加 -v 选项，你获得了关于新文件系统的详尽信息。

- c. 通过输入以下命令在 /dev/sda9 上创建一个仅 65 MB 的 Reiser 文件系统：
kreiserfs /dev/sda9

# 从 RedHat 迁移到 SUSE

- 3. 在 /export 下创建目录 data1、data2 和 data3。
- 4. 通过输入 ls /export 验证目录是否已创建。
- 5. 以 root 身份，使用你选择的编辑器（例如 vi），向此处添加条目：
a. 打开文件 /fstab。
b. 在 fstab 的末尾添加以下内容：
```
/dev/sda7 fat defaults 0 0
/dev/sda8 ext2 defaults 0 0
/dev/sda9 reiserfs defaults 0 0
```
（注意：fstab 的 OCR 乱码，上述内容是根据上下文重建的）。

-c. 完成后，按下 :wq 保存 /fstab。
- 6. 输入以下命令查看分区表：
```
cat /proc/partitions
```
- 7. 通过输入 mount -a 管理文件系统。





+   i. 输入 `dumpe2fs /dev/hda8 | less` 验证文件系统状态是否洁净。

+   j. 编辑 `/etc/fstab` 将文件系统类型从 ext2 改为 ext3，如下所示：
/dev/hda8 /export/data2 ext3 defaults 1 2
保存文件。

+   k. 从命令行，输入 `mount -a` 重新读取 `/etc/fstab` 并将分区挂载为 ext3 文件系统。

+   l. 输入 `mount` 验证更改。

+   m. 输入 `umount /export/data2` 再次卸载分区 `/dev/hda8`。

+   n. 输入以下命令将分区手动挂载为 ext2 文件系统：
mount -t ext2 /dev/hda8 /export/data2

+   o. 输入 `mount -t ext2` 验证文件系统是否在没有日志的情况下挂载（作为 ext2 文件系统）。
如你所见，ext3 与 ext2 是向后兼容的。

+   输入以下 3 条命令，重新挂载 `/dev/hda8` 为 ext3 文件系统并验证更改：
mount /export/data2
mount -a
mount

+   2. 修改分区 /dev/hda9：
   a. 输入 `df -h` 查看分区 `/dev/hda9` 的大小。
   b. 卸载 `/dev/hda9`
   umount /export/data3.
   c. 在分区卸载状态下，输入以下命令为 `/export/data3` 文件系统添加标签：
   reiserstone -l /export/data3 /dev/hda9
   d. 输入 `resize_reiserfs /dev/hda9` 调整分区大小以占用整个分区。

当未指定大小时，文件系统将调整大小以使用分区上的所有可用空间。在文件系统挂载时，也可以增加 ReiserFS 的大小。

+   e. 输入 `mount -a` 重新挂载分区。

+   f. 输入 `df -h` 查看分区大小。
大小不再是 625 MB，但取决于你的分区大小，应该是 1 GB 或更多。

+   g. 输入 `umount /export/data3` 卸载分区以对其文件系统检查。

+   h. 输入以下命令对 /dev/hda9 文件系统进行检查：

```
reiserfsck -y /dev/hda9
```

+   i. 输入 `mount -a` 重新挂载所有文件系统。

（练习结束）


在本练习中，你将学习如何使用 YaST 管理 LVM（逻辑卷管理器）。

在练习的第一部分，使用 YaST 创建两个大小均为 1 GB 的物理卷 (PV)。将它们添加到名为 projects 的卷组 (VG) 中。在卷组内添加两个名为 pilot (750MB) 和 production (750MB) 的逻辑卷，分别挂载到 /projects/pilot 和 /projects/production。

在练习的第二部分，将逻辑卷 production 的大小增加到卷组内可用的最大空间。

## 完成此练习的详细步骤：

+   - 第一部分：创建 LVM 物理卷、卷组和逻辑卷
-- 第二部分：调整 LVM 卷的大小

# 第一部分：创建 LVM 物理卷、卷组和逻辑卷

要创建 LVM 物理卷、卷组和逻辑卷，请执行以下操作：

+   1. 启动 YaST，输入 root 密码 (novell)，选择 System（系统） > Partitioner（分区）。
   选择 Yes 确认警告消息。
   出现专家分区器（Expert Partitioner）对话框。

+   2. 通过以下步骤创建一个新的 LVM 分区：
   a. 选择 Create（创建）。
   b. 选择 Do not format（不格式化）；然后选择或输入以下：
      文件系统 ID：0x8E Linux LVM
- 结束（区道）：+1GB
   c. 选择 OK 保存分区定义。

+   3. 重复步骤 2 创建另一个 1GB 的 LVM 分区。

你现在应该有两个 1GB 的 LVM 分区。

+   4. 选择 LVM 按钮，并在创建卷组（Create Volume Group）对话框中输入以下：

+   - 卷组名称：projects
+   - 物理区段大小：4M

+   5. 选择 OK 继续。

+   6. 选择每个物理卷（如 /dev/hda10）并选择 Add Volume（添加卷），将每个 Linux LVM 物理卷添加到 projects 卷组。然后选择 Next（下一步）。

出现逻辑卷管理器逻辑卷对话框。

+   7. 在 projects 卷组内添加逻辑卷 pilot：

+   a. 选择 Add（添加）。

出现创建逻辑卷（Create Logical Volume）对话框。

+   b. 输入或选择以下：

+   - 格式（文件系统）：Reiser
+   - 逻辑卷名称：pilot
+   - 大小：750 MB
+   - 挂载点：/projects/pilot
   c. 选择 OK 保存逻辑卷定义。

+   8. 在 projects 卷组内添加逻辑卷 production：

+   a. 选择 Add（添加）。

出现创建逻辑卷（Create Logical Volume）对话框。

+   b. 输入或选择以下：

+   - 格式（文件系统）：Reiser
+   - 逻辑卷名称：production
+   - 大小：750 MB
+   - 挂载点：/projects/production
   c. 选择 OK 保存逻辑卷定义。

+   9. 选择 Next（下一步）保存更改。

你返回专家分区器。

+   10. 在专家分区器中选择 Apply（应用）。

出现一条消息；选择 Finish（完成）接受更改。

+   11. 从终端窗口，执行 `su -` 变为 root（密码 novel）。

+   12. 输入以下内容查看新的 LVM 文件系统：
df -h

注意这些新文件系统的大小。

+   13. 输入 `cat /etc/fstab` 查看设备名称和挂载位置。

# 第二部分：调整 LVM 卷的大小

要调整 LVM 卷的大小，请执行以下操作：

+   1. 从 YaST 控制中心选择 System > LVM。

出现 LVM 对话框。

+   2. 在逻辑卷列表中选择 /dev/projects/production：
然后选择 Edit（编辑）。

出现编辑逻辑卷（Edit Logical Volume）对话框。

注意卷的大小。

+   3. 选择 max（最大）按钮。

注意大小变为了可用的最大空间。

+   4. 选择 OK 继续。

+   5. 选择 Finish 保存更改；然后选择 OK 确认通知。

+   6. 从终端窗口，输入 `df -h` 查看 production 的新大小。

+   7. 关闭所有打开的窗口。

（练习结束）

# 第 5 节 管理系统初始化

在工作集的本节，你将学习如何执行：

+   - 在 5-2 学习“管理引导程序”
在本练习中，你将练习启动到 shell 并修改 /boot/grub/menu.lst。
- 在 5-4 学习“管理运行级别 (Runlevels)”
在本练习中，你将练习配置运行级别。

# 练习 5-1

# 管理引导程序

在本练习中，你将练习启动到 shell 并修改 /boot/grub/menu.lst。

在启动提示符输入 `init=/bin/bash`，修改 /boot/grub/menu.lst 以便在修改内核参数之前需要密码，并测试新的 GRUB 配置。

## 完成此练习的详细步骤：

+   1. 从终端窗口，执行 `su` 变为 root（密码 novel）。

+   2. 输入 `init 6` 重启。

+   3. 当显示启动菜单时，按空格键停止计时。

+   4. 在启动选项字段输入 `init=/bin/bash`；然后回车。

+   5. 当 bash 提示符出现时，输入以下命令重新挂载根分区为读写：
mount -o remount,rw /

+   6. 使用 vi 编辑 /boot/grub/menu.lst。

在以 gfxmenu 开头的行前面加上注释符号 (#)。在其下方添加以下行：

password secret

+   7. （可选）为了避免在文件中出现明文密码，可以使用 MD5 哈希。你可以在 vi 中通过以下命令创建并包含它：

按下 Escape

输入

```
:r -e "secret\n" | grub-mdcrypt
```
并回车。

文件中会出现 grub-mdcrypt 的输出，包括密码的 MD5 哈希。

删除 grub-mdcrypt 输出中除哈希行。如果文件中还有 password secret 行，也将其删除。

在哈希行的开头写入 `password --md5`，使该行看起来如下：

```
password --md5 $1$t9kdK1$juAcBOwQFV3Cl7b.v0
```
注意：你的哈希值将与不同。

按下 Esc 并输入 :wq 保存文件。

+   8. 再次挂载根文件系统为只读：
mount -o remount,ro /

如果在下一步重启电脑时文件系统是读写的，则在再次启动时需要进行文件系统检查。

+   9. 重启电脑。

由于你关闭了图形菜单，你会发现现在的启动界面有所不同。

+   10. 如果你想编辑内核命令行，按 p 然后输入在步骤 6 或 7 中使用的密码。简短的帮助文本会告知可用选项。

+   11. 按 b 启动电脑。
12. 撤销 /boot/grub/menu.lst 中的更改：

+   a. 登录 geeko，打开终端窗口，su - 变为 root（密码 novel）

+   b. 使用 vi 打开 /boot/grub/menu.lst，在以 password 开头的行前面加上注释。按下 Esc 并输入 :wq 保存文件并关闭 vi。





## 练习 5-2 管理运行级别 (Runlevels)

在本练习中，你将练习配置运行级别。本练习分为四个部分。

第一部分，使用 `runlevel` 命令查看当前运行级别，并使用 `init` 命令切换到运行级别 3，然后返回运行级别 5。

第二部分，激活 `at` 服务 atd。该服务允许在未来的时间点调度命令。

第三部分，重启电脑并启动到运行级别 3 而不是默认的运行级别 5。登录并切换到运行级别 5。

第四部分，使用 YaST 运行级别编辑器激活 `rsync` 守护进程。

## 完成此练习的详细步骤：

- 第一部分：查看和更改当前运行级别
- 第二部分：激活 atd 服务
- 第三部分：在启动时设置运行级别
- 第四部分：使用 YaST 启用 rsyncd

### 第一部分：查看和更改当前运行级别

要查看并更改当前运行级别，请执行以下操作：

1. 打开终端窗口并使用 `su -` 切换到 root（密码为 `novel`）。
2. 通过输入 `runlevel` 检查之前的和当前的运行级别。
   列出运行级别：

| 表 5-1 | 之前的 | 当前的 |
|---|---|---|

注意，之前的运行级别显示为 N，这意味着没有设置之前的运行级别。

3. 通过输入 **init 3.** 切换到运行级别 3。

图形化环境已终止，你将处于终端登录提示符处。

4. 使用密码 **novell.** 登录 **root**。

5. 通过输入 **runlevel.** 检查之前的和当前的运行级别。

列出运行级别：

| 表 5-2 | 之前的 | 当前的 |
|---|---|---|

6. 通过输入 **init 5.** 切换到运行级别 5。

出现 GUI 登录界面。

7. 使用密码 **novell.** 登录 **geeko**。

### 第二部分：激活 at 服务 atd

要激活服务 at atd，请执行以下操作：

1. 从终端窗口，使用密码 **novell.** `su` 切换到 root (**su -**），密码为 **novell.**。

2. 通过输入 **chkconfig atd -l.** 查看 atd 的当前运行级别配置。

注意所有运行级别的配置均为关闭状态（off）。

3. 通过输入 **inserv -d atd.** 将服务安装到其预定义的运行级别。

4. 通过输入 **chkconfig atd -l.** 检查修改后的运行级别配置。

注意默认配置将运行级别 2、3 和 5 设置为开启（on）。

5. 通过输入 `cd /etc/rc.d/rc3.d` 切换到目录 /etc/rc.d/rc3.d。

6. 通过输入 `ls -l *atd` 列出目录中的 atd 文件。注意有两个 atd 链接——一个用于启动 atd 服务，另一个用于杀死 atd 服务。

7. 通过输入 `rcatd` 启动服务。

8. 通过输入 `rcatd status` 验证服务是否正在运行。

9. 按 `Ctrl+Alt+F1` 切换到虚拟终端 1；然后登录为 `root`。

10. 通过输入 `init 1` 切换到运行级别 1。

11. 输入 root 密码 `novell`。

12. 通过输入 `rcatd status` 检查服务是否运行。该服务列为未未使用（unused），因为它没有被配置在运行级别 1 下启动。

13. 通过输入 `init 5` 切回你之前的运行级别 (5)。出现 GUI 登录界面。

14. 使用密码 `novell` 登录 `geeko`。

15. 打开终端窗口并 `su - 切换到 root`（密码为 `novell`）。

16. 现在使用 `chkconfig` 代替 `inserv` 来配置系统服务。从命令行中，通过输入 `chkconfig off` 将服务从系统启动运行级别中移除。

17. 通过输入 `chkconfig atd -l` 查看 at 的当前运行级别配置。

注意服务在所有运行级别上都是关闭的。

18. 通过输入 `chkconfig atd on` 重新启用服务在默认运行级别下启动。

### 第三部分：在启动时设置运行级别

要在启动时设置运行级别，请执行以下操作：

1. 从终端窗口，使用密码 `novel` `su` 切换到 root (su -)。
2. 通过输入 `init 6` 重启。
3. 当启动菜单显示时，按空格键停止计时器。
4. 在“Boot Options”字段中输入 3；然后按回车键启动 Linux 系统到运行级别 3。
5. 当登录提示符出现时，使用密码 `novel` 登录为 root。
6. 通过输入 `runlevel` 显示当前运行级别。
7. 通过输入 `init 5` 切换到运行级别 5。
8. 按 `Ctrl+Alt+F1` 切回虚拟终端。
9. 通过输入 `exit` 退出 root 登录。
10. 按 `Ctrl+Alt+F7` 切回图形用户界面。
11. 使用密码 `novel` 登录 `geeko`。

### 第四部分：使用 YaST 启用 rsyncd

要使用 YaST 启用 rsyncd，请执行以下操作：

1. 从图形桌面启动 YaST。
   出现 YaST 控制中心。
2. 选择 System（系统）> System Services (Runlevel)（系统服务（运行级别））。
   出现编辑器对话框。
3. 通过选择 Expert Mode（专家模式）切换到更详细的视图（带有附加选项）。
4. 滚动服务列表并选择 rsyncd。

5. 在列表下方，通过选择 **3** 和 5 配置此服务在运行级别 3 和 5 下启动。
6. 从 Set/Reset（设置/重置）下拉列表中选择 **Enable the service（启用服务）。
7. 从 Start/Stop/Refresh（启动/停止/刷新）下拉列表中选择 **Start now.**（现在启动）启动 rsyncd 服务。

出现状态消息，表示服务已成功启动。

8. 通过选择 **OK.**（确定）关闭消息。
9. 从 Start/Stop/Refresh（启动/停止/刷新）下拉列表中选择 **Stop now.**（现在停止）停止 rsyncd 服务。

出现状态消息，表示服务已成功停止。

10. 通过选择 **OK.**（确定）关闭消息。
11. 通过选择 Finish（完成）保存更改；然后选择 Yes（是）。
12. 关闭 YaST 控制中心和终端窗口。

（练习结束）

# 第 6 部分 配置邮件和 Web 服务

在工作集的本章节中，你将学习如何执行以下操作：

- 6-2 节的“在局域网上发送邮件”
在本练习中，你将在局域网上发送邮件。你配置 Postfix 并测试你的配置。
- 6-4 节的“在互联网上使用 Postfix”
在本练习中，你将配置 Postfix 向互联网发送电子邮件。
- 6-6 节的“使用查找表”
在本项练习中，你将使用 Postfix 查找表。
- 6-9 节的“安装 Apache”
在本练习中，你将在你的系统上安装 apache 组件。
- 6-10 节的“测试 Apache 安装”
在本练习中，你将检查 apache 的安装是否成功。
- 6-11 节的“配置虚拟主机”
在本练习中，你将为会计部门配置一个虚拟主机。

## 练习 6-1

### 在局域网上发送邮件

在本练习中，你将编辑 Postfix 配置文件 /etc/postfix/main.cf。你配置 Postfix 在你的局域网上发送邮件。普通用户的发送者域名名应进行伪装。通过向 root 发送邮件来测试你的配置。

执行以下操作：

- 第一部分 - 编辑 /etc/postfix/main.cf
- 第二部分 - 测试配置

### 第一部分 - 编辑 /etc/postfix/main.cf

1. 打开终端窗口并输入 su- 获取 root 权限。
2. 在提示时，输入 root 密码 `novel`。
3. 通过输入 `rcpostfix stop` 停止 postfix 守护进程。
4. 使用文本编辑器打开 /etc/postfix/main.cf。
5. 滚动到文件末尾设置。
6. 为了仅从局域网接收邮件，编辑以下选项：

- inet_interfaces = your_IP-Address, 127.0.0.1
- mynetworks_style = subnet（可能已设置）
- smtpd_recipient_restrictions = permit_mynetworks, reject（在同一行）

7. 为了重写发送者地址并删除主机名，编辑以下选项：

- masquerade_exceptions = root（可能已设置）
- masquerade_domains = digital airlines.com





- 8. 要向中继主机 da1 递送外部邮件，编辑以下选项：

```
relayhost = 10.0.0.254
```

- 9. 保存文件并关闭编辑器。

- 10. 输入以下启动 Postfix：

```
rcpostfix start
```

### 第二部分 - 测试配置

- 1. 要生成测试邮件，请执行以下操作：
  a. 输入 `exit` 退出 root 用户登录。
  b. 输入 `mail root@hostname.digitalairairlines.com`。

- 2. 输入主题和正文，并执行以下操作完成邮件：
  a. 按回车键。
  b. 输入 `.`（点）。
  c. 按回车键。

- 3. 输入 `su -` 再次获取 root 权限。

- 4. 提示时，输入 root 密码 novel。

- 5. 输入 `mail`。

- 6. 输入你撰写的邮件对应的数字。

- 7. 输入 `q` 退出。

（练习结束）

## 练习 6-2 在互联网上使用 Postfix

在本次练习中，你将配置 Postfix 向互联网发送邮件。仅允许接受来自本地邮件的邮件；任何未发送至本地域的邮件都将被拒绝。

请执行以下操作：

- 1. 打开终端窗口并输入 `su -` 获取 root 权限。
- 2. 提示时，输入 root 密码 novel。
- 3. 输入以下命令停止 postfix 守护进程：
```
rcpostfix stop
```
- 4. 使用你喜喜欢的文本编辑器打开 `/etc/postfix/main.cf` 文件。
- 5. 要配置 Postfix 接受来自本地网络的邮件以及发送到 digitalairlines.com 域中任何接收者的邮件，请编辑或添加以下：
  - myhostname = hostname.digitalairlines.com
  - mydomain = digitalairlines.com
  - mydestination = $hostname,$omain （同一行）
  - smtpd_recipient_restrictions = permit_mynworks, reject_unauth 前三行定义了主机和域名。最后一行告诉 Postfix，只要邮件是来自 `mynworks` 中的主机就接受，并拒绝任何未发送至 `mydestination` 中定义的域之一的邮件。
- 6. 保存文件并关闭编辑器。
- 7. 输入 `rcpostfix start` 启动 Postfix。

（要测试配置，你必须从本地网络之外的 IP 地址访问 Postfix，并尝试向 airlines.com 以外的域名发送邮件。Postfix 不应接受此邮件。）

（练习结束）

## 练习 6-3 使用查找表

在本次练习中，你将使用 Postfix 查找表。

在第一部分，你创建了一个密码为 novel 的新用户。
在第二部分，你修改查找表，使新用户的邮件以发送者地址 master@airlines.com 发出。
在第三部分，测试你的配置。

请执行以下操作：

- 1. 打开终端窗口并输入 `su -` 获取 root 权限。
- 2. 提示时，输入 root 密码 novel。
- 3. 要创建新用户，输入 `useradd -G users -m master`。
- 4. 通过输入两次 `passwd master` 为用户设置密码。
- 5. 输入 `su - master` 以用户身份登录。
- 6. 要给 root 用户写邮件，输入 `mail@localhost`。
- 7. 输入主题和一些正文；然后完成邮件：
  a. 按回车键。
  b. 输入 `.`（点）。
  c. 按回车键。
- 8. 输入 `exit` 获取 root 权限。
- 9. 输入 `mail`。
- 10. 输入你撰写的邮件对应的数字。
- 11. 在下方的空间记录发送者地址：
- 12. 输入 `q` 退出。

- 第二部分 - 更改 sender_canonical 表
- 1. 输入 `rcpostfix stop`。
- 2. 使用你喜喜欢的文本编辑器打开 `/etc/postfix/sender_canonical`。
- 3. 要更改用户的发送地址，输入（同一行）`master@airlines.com master@airlines.com`。
- 4. 保存文件并关闭编辑器。
- 5. 输入 `postmap :/etc/postfix/sender_canonical`。
- 6. 输入 `rcpostfix start` 启动 Postfix。

- 第三部分 - 测试配置
- 1. 输入 `su - master` 以用户身份登录。
- 2. 要给 root 用户写邮件，输入 `mail@localhost`。
- 3. 输入主题和一些正文；然后完成邮件：
  a. 按回车键。
  b. 输入 `.`（点）。
  c. 按回车键。
- 4. 输入 `exit` 获取 root 权限。
- 5. 输入 `mail`。
- 6. 输入你撰写的邮件对应的数字。
- 7. 在下方的空间记录发送者地址：
- 8. 输入 `q` 退出。

（练习结束）

## 练习 6-4 安装 Apache

在本次练习中，你将在系统上安装 apache 组件。

请执行以下操作：

- 1. 启动 YaST。
- 2. 从 YaST 控制中心，选择 Software（软件）> Software Management（软件管理）。
- 3. 从过滤器下拉菜单中选择 Search（搜索）。
- 4. 在 Search 字段中输入 `apache`；然后选择 Search。
- 5. 在右侧，选择以下软件包：
  - apache2
  - apache2-example-pages
  - apache2-prefork
- 6. 选择 Accept（接受）。
- 7. （可选）如果 YaST 显示软件包依赖关系，通过选择 Continue（继续）进行确认。
- 8. 提示时，向驱动器插入所需的 SUSE Linux Enterprise Server 10 CD。
- 9. 安装完成后，关闭 YaST 控制中心并移除 CD。
- 10. 打开终端窗口并 `su` 到 root。
- 11. 要现在系统启动时启动 Apache，输入以下内容：
```
insserv apache2
```
- 12. 要启动 Apache 守护进程，输入以下：
```
rcapache2 start
```

（练习结束）

## 练习 6-5 测试 Apache 安装

在本次练习中，你将检查 apache 是否成功安装。

请执行以下操作：

- 1. 启动 Firefox。
- 2. 在网络浏览器的地址栏中，请输入以下内容：
```http://localhost```
如果出现了 Apache 示例页面，说明 Web 服务器已正确安装并启动。
- 3. （可选）如果你在显示页面时遇到问题，你需要重命名文件 `/srv/www/htdocs/index.html.en` 为 `/srv/www/htdocs/index.html`。

（练习结束）

## 练习 6-6 配置虚拟主机

在本次练习中，你将为部门配置虚拟主机。

请执行以下操作：

- 1. 在终端窗口（以 root 身份），通过以下命令创建虚拟主机目录：
`mkdir /srv/www/accounting`
- 2. 在新目录中创建一个 `index.html` 文件，内容如下：
```html
<html>
<head>
<title>Accounting Intranet</title>
</head>
<body>
<h1>Accounting Intranet</h1>
建设中。
</body>
</html>
```
- 3. 输入以下命令进入 `/etc/apache2/vhosts.d/` ：
`cd /etc/apache2/vhosts.d/`
- 4. 输入以下命令拷贝虚拟主机模板：
`cp vhost.template accounting.conf`
- 5. 使用文本编辑器打开 `accounting.conf` 文件并进行以下更改：

```
<VirtualHost accounting.da.com:80>
ServerName accounting.da.com
DocumentRoot /srv/www/accounting
ErrorLog /var/log/apache2/accounting.da.com-error_log
CustomLog /var/log/apache2/accounting.da.com-access_log combined
UseCanonicalName On
ScriptAlias "cgi-bin/" "/srv/www/cgi-bin"
<Directory>
AllowOverride None
Options +ExecCGI -Includes
Order allow,deny
Allow from all
</Directory>
<Directory "/srv/www/accounting/">
AllowOverride None
Options Indexes FollowSymLinks
Order allow,deny
Allow from all
</Directory>
```

- 6. 为了测试目的，在 `/etc/hosts` 文件的 `127.0.0.1` 行后添加 `accounting.da.com`：
127.0.0.1 localhost accounting.da.com
- 7. 输入以下命令测试配置文件的语法：
apache2ctl configtest
- 8. 输入以下命令重载 Apache：
rcapache2 reload

此文件也可以在你的 3073 课程 CD 的 `/section_2` 目录中找到。




- 9. 从 Konqueror 浏览器通过输入以下内容访问虚拟主机：

**http://accounting.da.com**

将显示会计内部网首页页。

- 10. 关闭 Konqueror 浏览器。

**(练习结束)**

## 第 7 节 AppArmor

在本练习册中，你将学习如何执行以下操作：

- 7-2 上的“AppArmor”
  在此练习中，你将为 Firefox 浏览器创建、测试并改进配置文件。

## 练习 7-1

### AppArmor

在本练习中，你将为 Firefox 浏览器创建、测试并改进配置文件。此练习分为四个部分。

在第一部分，为 Firefox 浏览器创建一个配置文件。在使用 Firefox 为初始配置生成日志条目时，只需浏览网页；不要用 Firefox 访问本地文件。

在第二部分，使用 Firefox 访问本地文件，例如 `/usr/share/doc/packages/apparmor-docs/apparmor.7.html`。AppArmor 应该阻止你查看该文件。将配置更改为允许。你可以为此使用 YaST、genprof 或 complain logprof。

在第三部分，安装 Java 4_2 浏览器插件 `java-1_4_2-sun-plugin`。重启 Firefox 并使用它访问包含 Java applet 的页面。

http://java.sun.com/products/plugin/1.4/demos/plugin/applets.html 链接到各种演示。Firefox 将无法显示它们。再次更改配置以能够运行 Java applet。使用一种不同于上述第二部分所用的方法来实现此。

在第四部分，将你生成的配置与 `/etc/apparmor/profiles/extras/` 中的 Firefox 配置文件进行比较。找出你的配置与这些配置相比是更严格了还是更宽松。

## 完成此练习的详细步骤

- 第一部分：为 Firefox 浏览器创建配置
- 第二部分：修改 Firefox 配置文件以允许对本地文件系统的读取访问
- 第三部分：使用浏览器插件
- 第四部分：将你创建的配置与来自 SLES 10 的进行比较

### 第一部分：为 Firefox 浏览器创建配置

执行以下操作：

- 1. 启动 Yast，输入 root 密码 (novell)。
- 2. 选择 Novell AppArmor > 添加配置向导 (Add Profile Wizard)。
- 3. 在提示“应用程序到配置 (Application to Profile)”处，输入 firefox。
- 4. 按 Alt+F2  Firefox，输入 firefox 并选择运行。查看一些网页。再次关闭 Firefox。
- 5. 在 YaST AppArmor 配置向导对话框中，选择扫描系统日志中的 AppArmor 事件。
- 6. 现在你创建配置并需要回答几个问题。注意，应用程序 Firefox 非常复杂，并访问系统上的多个可执行文件和文件。
  a. 为 `/bin/basename` 和其他执行的程序选择继承 (Inherit)。
  b. 对于文件和目录，选择合适的选项，例如 `#include`、文件名、目录或带有占位符的路径，并选择允许 (Allow)。当返回到 AppArmor 配置向导对话框时，选择完成 (Finish)。
通过使用 `cat` 查看 `/sys/kernel/security/apparmor/profiles` 来确保 Firefox 配置处于强制执行模式 (enforce mode)。必须有一个项 `/usr/lib/firefox/firefox.sh (enforce)`。如果没有，执行 `enforce firefox`。

### 第二部分：修改 Firefox 配置文件以允许对本地文件系统的读取访问

执行以下操作：

- 1. 打开终端窗口并 `su - root`（密码 novel）。
- 2. 输入 `tail -f /var/log/audit/audit.log`。
- 3. 按 Alt+F2  Firefox，输入 firefox 并选择运行。查看文件 `/usr/share/doc/packages/apparmor-docs/apparmor.7.html`（你不应该能这样做）。
- 4. 在终端窗口中查看日志文件。你应该看到一条拒绝 (reject) 消息。
- 5. 按 Ctrl+c 停止查看日志文件。
- 6. 在终端窗口中输入 `complain firefox`。
- 7. 在 Firefox 中再次尝试访问 `/usr/share/doc/packages/apparmor-docs/apparmor.7.html`。你现在应该能够访问该文件。
- 8. 启动 Yast，输入 root 密码 (novel)。
- 9. 选择 Novell AppArmor > 更新配置向导 (Update Profile Wizard)。
- 10. 你看到与第一部分相同的界面，可以在其中选择允许 (Allow)、继承 (Inherit)、拒绝 (Deny) 等。确保你正在更新 Firefox 配置，而不是其他配置。稍后或晚些时候你应该看到一个路径 `/usr/share/doc/packages/apparmor-docs/apparmor.7.html` 的项，通过连续点击三次 Glob 按钮，你可以创建一个建议 `/usr/share/doc/**`。通过选择允许 (Allow) 来允许它。
- 11. 当日志文件中的所有条目处理完毕后，选择完成 (Finish)。
- 12. 在终端窗口中输入 `firefox` 将 Firefox 配置放回强制执行模式。
- 13. 在 Firefox 中尝试访问 `/usr/share/doc/` 下的文件，例如 `/usr/share/doc/packages/`。你应该能够访问它们。然而，访问文件系统中的其他地方应该是不允许的。
- 14. 关闭 Firefox。
- 15. 关闭 YaST。

### 第三部分：使用浏览器插件

执行以下操作：

- 1. 打开终端窗口并 `su - root`（密码 novel）。
- 2. 输入 `tail -f /var/log/audit/audit.log`。
- 3. 按 Alt+F2  Firefox，输入 firefox 并选择运行。查看文件 `/usr/share/doc/packages/apparmor-docs/apparmor.7.html`（你不应该能这样做）。
- 4. 在终端窗口中查看日志文件。你应该看到一条拒绝 (reject) 消息。
- 5. 按 Ctrl+c 停止查看日志文件。
- 6. 在终端窗口中输入 `complain firefox`。
- 7. 在 Firefox 中再次尝试访问 `/usr/share/doc/packages/apparmor-docs/apparmor.7.html`。你现在应该能够访问该文件。
- 8. 启动 Yast，输入 root 密码 (novel)。
- 9. 选择 Novell AppArmor > 更新配置向导 (Update Profile Wizard)。
- 10. 你看到与第一部分相同的界面，可以在其中选择允许 (Allow)、继承 (Inherit)、拒绝 (Deny) 等。确保你正在更新 Firefox 配置，而不是其他配置。稍后或晚些时候你应该看到一个路径 `/usr/share/doc/packages/apparmor-docs/apparmor.7.html` 的项，通过连续点击三次 Glob 按钮，你可以创建一个建议 `/usr/share/doc/**`。通过选择允许 (Allow) 来允许它。
- 11. 当日志文件中的所有条目处理完毕后，选择完成 (Finish)。
- 12. 在终端窗口中输入 `firefox` 将 Firefox 配置放回强制执行模式。
- 13. 在 Firefox 中尝试访问 `/usr/share/doc/` 下的文件，例如 `/usr/share/doc/packages/`。你应该能够访问它们。然而，访问文件系统中的其他地方应该是不允许的。
- 14. 关闭 Firefox。
- 15. 关闭 YaST。

### 第四部分：将你创建的配置与来自 SLES 10 的进行比较

执行以下操作：

- 1. 打开终端窗口并 `su - root`（密码 novel）。
- 2. 输入 `tail -f /var/log/audit/audit.log`。
- 3. 按 Alt+F2  Firefox，输入 firefox 并选择运行。查看文件 `/usr/share/doc/packages/apparmor-docs/apparmor.7.html`（你不应该能这样做）。
- 4. 在终端窗口中查看日志文件。你应该看到一条拒绝 (reject) 消息。
- 5. 按 Ctrl+c 停止查看日志文件。
- 6. 在终端窗口中输入 `complain firefox`。
- 7. 在 Firefox 中再次尝试访问 `/usr/share/doc/packages/apparmor-docs/apparmor.7.html`。你现在应该能够访问该文件。
- 8. 启动 Yast，输入 root 密码 (novel)。
- 9. 选择 Novell AppArmor > 更新配置向导。
- 10. 你看到与第一部分相同的界面，可以在其中选择允许 (Allow)、继承 (Inherit)、拒绝 (Deny) 等。确保你正在更新 Firefox 配置，而不是其他配置。稍后或晚些时候你应该看到一个路径 `/usr/share/doc/packages/apparmor-docs/apparmor.7.html` 的项，通过连续点击三次 Glob 按钮，你可以创建一个建议 `/usr/share/doc/**`。通过选择允许 (Allow) 来允许它。
- 11. 当日志文件中的所有条目处理完毕后，选择完成 (Finish)。
- 12. 在终端窗口中输入 `firefox` 将 Firefox 配置放回强制执行模式。
- 13. 在 Firefox 中尝试访问 `/usr/share/doc/` 下的文件，例如 `/usr/share/doc/packages/`。你应该能够访问它们。然而，访问文件系统中的其他地方应该是不允许的。
- 14. 关闭 Firefox。
- 15. 关闭 YaST。

*(注：由于原文中存在大量重复的步骤，此处已按要求翻译并保持格式一致。)*




- 5. 关闭文件。

- 6. 输入命令：
insnserv -r SuSEfirewall2_setup
以及
inserv -r SuSEfirewall2_init

- 7. 关闭终端窗口。

## 第三部分：重启并测试 Xen。

- 1. 重启你的系统。

- 2. 在启动菜单中，选择 Xen 条目并按回车。

- 3. 系统启动后，使用用户 geeko 和密码 novel 登录。

- 4. 打开终端窗口并使用 su - 切换到 root 用户。

- 5. 输入命令 xm list。

- 6. 在输出中，你应该能看到一个状态为运行（running）域（Domain-0）。

（练习结束）

- 20. 选择 Next（按 Alt+P）。
- 21. 输入 novel 作为 root 密码。选择 Next（按 Alt+N）。
- 22. 接受密码过于简单。
- 23. 选择 Alt-n 继续。
- 24. 选择 No，跳过此测试（按 Alt+O）。
- 25. 选择 Next（Alt+N）。
- 26. 选择 Next（Alt+N）。
- 27. 选择 Next（Alt+N）。
- 28. 创建用户 geeko，密码为 novel。
- 29. 选择 Next（Alt+N）。
- 30. 接受密码过于简单。
- 31. 选择 Next（Alt+N）。
- 32. 选择 Next（Alt+N）。
- 33. 选择 Finish（Alt+F）。
- 34. 测试你是否可以使用用户 root 和密码 novel 登录新域。
- 35. 请不要关闭终端窗口，我们将在下一个练习中使用它。

（练习结束）

## 练习 8-3 更改客户域的内存分配

在本练习中，你将学习如何通过更改域配置文件来改变客户域的内存分配。

以下假设你仍然保留着在之前的练习中配置的客户域的打开终端窗口。

执行以下操作：

- 1. 打开终端窗口并使用 su - 切换到 root 用户。
- 2. 输入命令 xm list。
- 3. 记录域 vm1 的内存分配情况。
- 4. 切换到 Xen 域终端并输入 halt 停止系统。等待系统停止。
- 5. 返回到 root 终端并使用命令 xm list 验证域 vm1 已不再运行。
- 6. 使用文本编辑器打开 /etc/xen/vm/vm1 文件。
- 7. 查找内存参数（memory）并将值改为 172。
- 8. 保存并关闭文件。
- 9. 输入以下命令启动域：

```
xm create -c -f /etc/xen/vm/vm1
```

- 10. 等待系统启动并看到登录提示符。
- 11. 按组合键 Ctrl-] 剥离域终端并返回到 root 终端。
- 12. 使用命令 xm list 确定域 vm1 的内存分配。它 应该是 172MB。
- 13. 同样记录域 vm1 的 ID。
- 14. 使用命令 sxm console <noted_id> 连接到 vm1 的终端。

（练习结束）

## 练习 8-4

## 自动化域启动

在本练习中，你将学习如何在系统启动时自动启动域。

执行以下操作：

- 1. 打开终端窗口并使用 su - 切换到 root 用户。
- 2. 将 vm1 配置文件移动到 auto 目录：
mv /etc/xen/vm/vm1 /etc/xen/auto/
- 3. 使用命令 xm shutdown vm1 关 vm1。
- 4. 等待一会儿并使用命令 xm list 检查域是否已关闭。当域 vm1 不再显示时，继续下一步。
- 5. 输入 reboot 重启系统。
- 6. 在启动提示符处，选择 Xen 条目。
- 7. 系统启动后，使用用户 geeko 和密码 novel 登录图形界面。
- 8. 打开终端窗口并使用 su - 切换到 root 用户。
- 9. 输入命令 xm list。
- 10. 域 vm1 应该已经自动启动并并列在 xm 的输出中。

（练习结束）

## 练习 8-5 检查网络配置

此练习假设你有一个运行域 0 和另一个 Xen 域的 Xen 系统。

执行以下操作：

- 1. 打开终端窗口并使用 su - 切换到 root 用户。
- 2. 输入命令 xm list 确保域 vm1 正在运行。
- 3. 在 xm 命令的输出中，记录域 vm1 的 ID。
- 4. 使用命令 brctl show 查看网桥配置。
- 5. 你应该看到网桥 xenbr0 的配置。接口 peth0（物理接口）、vif0.0（域 0 的虚拟接口）和虚拟接口 vifx.0（x 是域 vm1 的 ID）应该添加到网桥。
- 6. 使用命令 xm shutdown vm1 关闭域。
- 7. 等待一会儿并使用命令 xm list 检查域是否已关闭。当域 vm1 不再显示时，继续下一步。
- 8. 再次输入命令 brctl show。注意域 vm1 的接口已从网桥中移除。
- 9. 使用：xm create -f /etc/xen/xen/vm1 重启域。

- 记录 vm1 的 ID 并通过 brctl show 检查域 vm1 的接口是否已重新添加。

（练习结束）

## 第 9  iSCSI

在教程的这一部分，你将学习执行以下操作：

- 在 9-2 中“设置 iSCSI 目标和 iSCSI 启动器”
在本练习中，你将设置 iSCSI。

## 练习 9-1

## 设置 iSCSI 目标和 iSCSI 启动器

在本练习中，你将学习如何设置 iSCSI 目标以及如何使用 iSCSI 启动器访问该目标。

第一部分，在你的机器上设置 iSCSI 目标。

第二部分，设置访问自己机器上 iSCSI 目标的 iSCSI 启动器。

第三部分，你将与另一位同学合作。在你们其中一台机器上设置 iSCSI 启动器，连接到 iSCSI 目标，而不是第二部分中配置的 localhost。

### 第一部分：在你的机器上设置 iSCSI 目标

- 1. 使用命令安装所需的包：
   yast -iscsitarget open-iscsi
- 2. 创建一个大小为 1GB 的空文件作为后端存储：
   dd if=/dev/zero of=/srv/iscsi/ocfs2_disk.img bs=1M
   count=1024
- 3. 通过启动 YaST 打开 YaST iSCSI 模块
- 4. 在 Service（服务）选项卡中，选择 Booting（启动）。
- 5. 在 Targets（目标）选项卡中，选择 Next（下一步）。
- 6. 在验证对话框中，选择 Next。
- 7. 在验证窗口中，选择 Next。
- 8. 选择 Finish（完成）关闭窗口。
- 9. 在终端中，检查...（注意：此部分的 OCR 文本被截或在后面的页面继续）


你将在下一个练习中使用此设备。

（练习结束）

# 1 允许纸质打印-禁止分发

严禁复制本手册的全部或部分内容或分发此类副本。如怀疑有抄袭行为，请拨打 1-800-PIRATES。

## 第 10 节 集群文件系统

在本工作手册的本节中，你将学习如何执行以下操作：

-   在 10-2 节“设置 OCFS2”

在本次练习中，你将设置 OCFS2。

从 RedHat 迁移到 SUSE Linux Enterprise 10 / 工作手册

## 练习 10-1 设置 OCFS2

本次练习基于之前第 9-2 页的“设置 iSCSI Target 和 iSCSI 启动器”练习。

你将在本次练习中继续与第三部分中的伙伴进行操作。

本次练习的目的是让你熟悉生产环境中的 OCFS2，在生产环境中，你可能需要某些故障转移能力（例如通过使用 DRBD 和 Heartbeat）；本课程未涵盖此内容。

在本次练习中，你将在上一个练习配置的 iSCSI 设备之上设置 OCFS2。

- 1. 在两台计算机上，使用以下命令安装所需的包：
   yast -i ocsfs-tools ocfs2console

```
yast -i ocsfs-tools ocfs2console
```

- 2. 在两台计算机上，创建一个内容如下的 `/etc/ocfs2/cluster.conf` 文件：

```
cluster:
  name = mycluster
  node_count = 2
node:
  name = daxx.digitalairirlines.com
  cluster = mycluster
  number = 0
  ip_address = 10.0.0.xx
  ip_port = 7777
node:
  name = dayy.digitalairirlines.com
  cluster = mycluster
  number = 1
  ip_address = 10.0.0.yy
  ip_port = 7777
```

将 xx 替换为运行 iSCSI target 的机器编号，将 yy 替换为另一台机器的编号。

# 1 允许纸质打印-禁止分发

严禁复制本手册的全部或部分内容或分发副本。如怀疑有抄袭行为，请拨打 1-800-PIRATES。

WB 10-2

版本 1

- 3. 在两台计算机上，使用命令配置 OCFS2 集群服务：
`/etc/init.d/o2cb configure`
恰当地回答问题。

- 4. 在提供 iSCSI target 的机器上，使用命令创建 OCFS2 文件系统：
`mkfs.ocfs2 -b 4k -C 128k -N 4 -L mycluster /dev/sd.x`
将 sdx 替换为正确的设备。

- 5. 创建目录 `/ocfs-cluster-fs`

- 6. 在两台机器上，在 `/etc/fstab` 中为文件系统创建一个条目，在现有条目中添加类似如下行：
`/dev/sdb /ocfs-cluster-fs ocfs2 defaults 0 0`

- 7. 在两台机器上，通过输入 `ocfs2 start` 挂载文件系统。
使用 `mount` 命令检查文件系统是否已挂载。

- 8. 在其中一台机器的 `/ocfs-cluster-fs` 中创建一个文件；该文件应该在另一个系统中可见的。

（练习结束）

# 1 允许纸质打印-禁止分发

严禁复制本手册的全部或部分内容或分发副本。
如怀疑有抄袭行为，请拨打 1-800-PIRATES。

WB 10-4

版本 1
