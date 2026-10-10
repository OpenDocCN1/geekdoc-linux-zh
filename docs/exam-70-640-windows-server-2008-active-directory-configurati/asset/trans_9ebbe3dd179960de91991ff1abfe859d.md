

## 提升域和林的功能级别

随着您的组织通过收购竞争对手而迅速增长，可以安全地假设并非所有新收购的公司都在运行 Windows Server 2008。决定如何将网络结构整合到您的企业架构中将是一个挑战，因为许多网络运行着各种混合的操作系统。Windows Server 2008 系列提供了几项新的增强功能，以帮助使过渡过程更容易。请注意提升域和林功能级别的关键事实和以下要求：

-   这是一项单向操作。如果不完整重新安装域或林，就无法逆转提升域和林功能级别的操作。
-   每个域都可以独立处理，从而允许采取分阶段的方式来增加功能。这允许公司有充足的过渡时间来升级每个站点或域。某些站点在迁移之前可能需要购买新硬件或升级现有基础设施。
-   在林中的所有域都提升到至少相应的**域功能级别**之前，无法提升林功能级别。
-   您必须作为**域管理员**组成员登录，以提升域功能级别。
-   您必须作为**企业管理员**组成员登录，以提升林功能级别。

> **注意**
> 您可以使用“Active Directory 域和信任关系”来提升域或林的功能。

### 提升域功能级别

**准备就绪。** 在开始这些步骤之前，您必须作为域管理员组成员登录。

-   从“管理工具”文件夹中打开 **Active Directory 域和信任关系**。
-   右键单击您希望提升的域，并选择**提升域功能级别**，如图 2-14 所示。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_78_0.png)

-   从“选择一个可用的域功能级别”中选择您希望达到的级别，然后单击**提升**。您将看到图 2-15 中所示的对话框，该对话框解释了此过程的不可逆性质。单击**确定**以确认此警告并提升域的功能级别，然后再次单击**确定**以确认更改已完成。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_78_1.png)

**暂停。** 您已提升域功能级别。

### 提升林功能级别

在上一个练习中，您已将 Active Directory 域的域功能级别提升至 Windows Server 2008 功能级别。接下来，您将提升林功能级别。

**准备就绪。** 在开始这些步骤之前，您必须作为企业管理员组成员登录。

-   从“管理工具”文件夹中打开 **Active Directory 域和信任关系**。
-   在控制台树中右键单击 **Active Directory 域和信任关系** 图标，并选择**提升林功能级别**。
-   如果您的所有域尚未全部提升至至少 Windows Server 2008 级别，您将收到一条错误信息，指出目前无法提升林功能级别。如果所有域都满足 Windows Server 2008 的域功能标准，您可以单击**提升**以继续。
-   会显示一条警告消息，解释此过程的不可逆性质。单击**确定**以确认此警告并提升林的功能级别，然后再次单击**确定**以确认更改已完成。

**暂停。** 您已提升林功能级别。

在上一个练习中，您将您的林的功能级别提升至 Windows Server 2008。

## 向林根域添加第二台域控制器

> 在规划 Active Directory 基础架构时，应为每个域添加第二台域控制器以实现故障容错。这提供了某种冗余，以防其中一台域控制器发生故障。此外，由于林中的第一台域控制器持有所有 FSMO 角色，因此添加第二台域控制器可以让您将部分工作卸载到另一台域控制器。

### 向林根域添加第二台域控制器

**准备就绪。** 您必须在现有的 Active Directory 域上拥有管理员凭据才能添加第二台域控制器；服务器计算机应配置为使用静态 IP 地址。

-   安装服务器操作系统。您可以将服务器配置为工作组成员，或作为现有域内的成员服务器。
-   确保新的域控制器能够解析它要加入的域内的 SRV 记录。实现此目的最简单的方法是配置新服务器使用现有域内 DNS 服务器的 IP 地址。如果新服务器正在运行 DNS 服务器服务，您可以配置新服务器使用 Active Directory 环境中现有 DNS 服务器的 DNS 转发器、辅助区域或存根区域（新服务器将加入该环境）。
-   将此 Active Directory 域服务角色添加到该服务器，并将其配置为现有域中的附加域控制器。这是 Active Directory 安装向导中“选择部署配置”页面上的第一个子选项，如图 2-16 所示。向导将提示您提供以下信息，以便向现有域添加第二台域控制器：
    -   您希望加入的域的 DNS 名称（如果服务器尚未配置为成员服务器）
    -   域的管理凭据
    -   新域控制器应放置的 Active Directory 站点名称
    -   将服务器配置为 DNS 服务器、全局目录和/或只读域控制器
    -   Active Directory 数据库、日志文件和 SYSVOL 文件夹的位置
    -   DSRM 密码
    -   选择通过网络从现有域控制器复制数据库，或选择“从介质安装”功能，该功能允许您使用现有域控制器的系统状态备份来创建新的域控制器
-   必要时将单个操作主机角色转移到该服务器。

**暂停。** 已添加第二台域控制器。

在上一个练习中，您向现有的 Active Directory 域添加了一台域控制器。

> **交叉引用**
> 有关将一个服务器上的 FSMO 角色转移到另一个服务器的过程，请参见第 4 课。

#### 图 2-16

添加第二台域控制器

![](img/a8ee53dbf1310726255b6fbb9f296fb2_80_0.png)

## 在 Server Core 上安装 Active Directory

Windows Server 2008 的一个主要新功能是*Server Core*，这是一种特殊的安装选项，创建一个最小化环境，仅用于运行特定的服务和角色。Server Core 几乎完全在没有图形用户界面（GUI）的情况下运行，这意味着必须专门从命令行对其进行管理。就 Active Directory 而言，Server Core 提供了一种有用的方法，可以部署具有极小安全足迹的域控制器，从而改善分支机构或其他远程环境中域控制器的安全性。

当您登录到 Server Core 计算机时，您会看到一个单独的命令行窗口，如图 2-17 所示。由于 Server Core 不支持许多图形实用程序（包括服务器管理器和 Active Directory 安装向导），因此您需要使用**无人参与安装**从命令行运行 dcpromo，该安装使用一个特殊格式化的文本文件来指定必要的安装选项。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_81_0.png)

### 在 Server Core 上安装 Active Directory

**准备就绪。** 您必须在现有的 Active Directory 域上拥有管理员凭据才能安装 Active Directory on Server Core；服务器计算机应配置为使用静态 IP 地址。

-   在 Server Core 命令提示符窗口中键入 **`notepad`**，然后按**`Enter`**键。
-   当记事本窗口打开时，键入以下内容：

```
; DCPROMO unattend file
; Usage:
[DcInstall]
; Replica DC promotion
ReplicaOrNewDomain=Replica
ReplicaDomainDNSName=lucernepublishing.com
SiteName=Default-First-Site-Name
InstallDNS=Yes
ConfirmGc=Yes
UserDomain=lucernepublishing.com
Username=lucernepublishing.com\\administrator
Password=Password1
DatabasePath=C:\\Windows\\NTDS
LogPath=C:\\Windows\\NTDS
SafeModeAdminPassword=MySafeModePassword
RebootOnCompletion=Yes
TransferNRolesIfNecessary=No
```

-   将该文本文件保存为 `C:\` 根目录下的 *unattend.txt*。
-   从 Server Core 控制台输入以下命令：

```
dcpromo /unattend:c:\unattend.txt
```

**暂停。** 已添加第二台运行 Windows Server 2008 Server Core 的域控制器。通过通读 unattend.txt 文件中列出的值，您可以看到目标域控制器将如何配置。您可以通过...
