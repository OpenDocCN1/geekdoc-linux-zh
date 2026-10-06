
## NFS 服务器配置

4. 从 YaST 控制中心，选择“网络服务 > NFS 服务器”在你的计算机上配置 NFS 服务器。

出现“NFS 服务器配置”对话框。

5. 选择“启动 NFS 服务器”，然后选择“下一步”继续。

出现“导出其他目录 (Directories to Export to the others)”对话框。

6. 将 `/export/data` 目录添加到导出列表中：

   - a. 选择“添加目录”。

   出现对话框，请求要导出的目录。

   - b. 输入 `/export/data/`；然后选择 OK。

   出现带有输入通配符和选项字段的对话框。

   - c. 输入以下内容：

     - * 主机通配符：*
     - * 选项：`rw,no_root_squash,sync`（确保你将 "ro" 替换为 "rw"`）

   - d. 选择 OK 继续。

目录已添加到列表中。

7. 选择 Finish 将更改保存到系统。

8. 在终端窗口，输入以下内容验证文件系统是否已导出：

```
showmount -e localhost
```

9. 输入以下内容查看 YaST 在 `/etc/exports` 文件中创建的条目：

```
cat /etc/exports
```

这些都是你在 YaST 中设置的配置。

10. 与伙伴配合，通过以下方法直接从伙伴的服务器访问 `/export/data` 目录：

   - a. 输入以下命令在你的服务器上创建挂载点 `/mnt/share`：

     ```
     mkdir -p /mnt/share
     ```

   - b. 执行以下任一操作挂载伙伴的目录：

     - * 按回车键
     - * 输入 `mount -t nfs partner_IP:/export/data /mnt/share`

     或者

     - * 使用 YaST NFS 客户端模块挂载目录，输入：

11. 通过 `mount` 验证伙伴的目录是否已挂载：

12. 按 Alt + F2 并输入 `kdesu konqueror` 以超级用户模式启动 Konqueror；然后选择“运行”。

- 13. 输入密码 `novel` 并选择 OK。

- 14. 输入以下 URL 查看你的 NFS 导出：

`nfs://localhost`

- 16. （可选）如果你提前完成，可以尝试更改 `/etc/exports` 文件中的条目，以便你或你的伙伴可以向文件系统写入，且只有你们其中一人可以读取。

- 17. 完成后，关闭所有已打开的窗口和对话框。

# Samba (CIFS)

Samba 是一个软件包，它在 Linux 上实现了以下微软网络协议：

- * 消息块 (SMB)。SMB 是一种用于在网络计算机之间共享资源的协议。SMB 可以在多种协议上实现，包括 TCP/IP、NetBEUI（通常称为 NetBIOS）或 IPX/SPX。

> 欲了解更多关于 SMB 的信息，请访问 www.samba.org/cifs/docs/what-is-smb.html。

注意

- * 通用互联网文件系统 (CIFS)。CIFS 是在原生 TCP/IP 之上的 SMB 实现，不需要 NetBIOS。

CIFS 是一种客户端/服务器协议，用于 Windows 操作系统。它也实现在许多其他平台（如 DOS、NetWare、UNIX、Linux 和 VMSTM）。

安装 Samba 后，Linux 计算机可以充当以下角色：

- * 微软 Windows 服务器。Samba 允许服务器为用户提供 Windows 文件和打印服务。
- * 微软 Windows 客户端。Samba 允许工作站访问并使用 Windows 文件和打印服务，无论这些服务源自 Windows 服务器还是安装了 Samba 的 Linux 服务器。

要在你的 SUSE Linux Enterprise 上上配置 Samba，你需要了解以下内容：

- Samba 特性和版本
- Linux 上的 Samba 客户端支持

# 配置网络文件系统

- 启动和停止 Samba 服务
- 使用 YaST 配置 Samba 服务器
- 使用 YaST 配置 Samba 客户端
- 监控和测试 Samba

欲了解更多关于 Samba 的信息，输入 `man samba`。浏览目录 `/usr/share/doc/samba/`。如果没有安装文档，使用 YaST 安装模块。

# Samba 特性和版本

SLES 9 包含了 Samba 3 版本，具有以下新功能：

- 改进的 Unicode 支持
- 改进的内部认证机制
- 对 Windows XP 的支持
- 能够作为 Active Directory 成员服务器设置
- 采用 Samba 域

# Linux 客户端支持

所有常见的操作系统（如 Mac X、Windows 和 OS/2）都支持 SMB 协议。为了让 SMB 协议运行，必须安装 TCP/IP 协议。Samba 为不同的 UNIX 版本提供了客户端。Samba 共享目录及其子目录通过名称导出，并可以通过该名称访问。

# 第 10 管理网络服务：DNS 以及文件和打印服务

共享名称可以设置为任何名称——不需要是导出名称。

打印机也分配了一个名称。客户端可以通过该名称访问打印机。

# 启动和停止

启动 Samba 所需的服务，输入：

```
rcnmbd start && rcmbd start
```

停止 Samba 服务，输入：

```
rcnmbd stop && rcmbd stop
```

**Samba 配置文件** Samba 的主配置文件是 `/etc/samba/smb.conf`。

该文件分为两个逻辑部分：

- `[global]` 部分。包含集中和全局设置
- `[share]` 部分。包含单独的文件和打印共享

通过使用两个逻辑部分，你可以单独设置共享，也可以使用 `[global]` 部分中的全局设置。

以下内容帮助你理解 `smb.conf` 文件的配置：

- `[global]` 配置
- `[cdrom]` 和 `[homes]` 共享配置示例
- 共享密码保护

你可以在 `/usr/share/doc/packages/samba/examples/smb.conf.SUSE` 中找到一个注释过的示例配置。

你可以手动配置，也可以使用 YaST Samba 服务器。

![](img/39399c9366aee7ad257a7d2d6505f1a1_511_0.png)

> 配置

`[global]` 部分的以下参数需要根据你的网络设置（手动或通过 YaST）进行调整，以便其他机器可以通过 SMB 访问你的 Samba 服务器。

- `workgroup = TUX-NET`。此行将 Samba 服务器分配到工作组。将 TUX-NET 替换为你网络环境中的适当工作组。
- `netbiosname = MYNAME`。你的 Samba 服务器按其 DNS 名称显示，除非该名称已分配给网络中的其他计算机。如果 DNS 名称不可用，使用 `netbiosname=MYNAME` 设置服务器名称。

# 配置网络文件系统

有关此参数的更多信息，请参阅 `man smb.conf`。

- `os level = 2`。此参数触发您的 Samba 服务器是否尝试成为其工作组的 LMB（本地主主浏览器）。

选择一个非常低的值，以保护现有的 Windows 网络免受配置不当的 Samba 服务器引起的任何干扰。

- 有关此重要主题的更多信息，请参阅文件 `/usr/share/doc/packages/samba/htmldocs/howto/NetworkBrowsing.html`。
- `wins support` 和 `wins server`。要将您的 Samba 服务器集成到具有活动 WINS 服务器的现有 Windows 网络中，请启用 `wins server` 选项并将其值设置为该 WINS 服务器的 IP 地址。

如果您的 Windows 计算机连接到不同的子网并需要相互感知，则需要设置一个 WINS 服务器。

要将 Samba 服务器转换为 WINS 服务器，请将 `wins support` 选项设置为 `Yes`（`wins support = Yes`）。确保网络上只有一个 Samba 服务器启用了此设置。

在 `smb.conf` 文件中，绝不能同时启用 `wins server` 和 `wins support` 选项。

## [cdrom] 和 [homes] 共享配置示例

以下示例说明了如何通过配置 `smb.conf` 文件中的共享，使 CD-ROM 驱动器和用户目录（homes）供 SMB 客户端使用。

- `[cdrom]`。以下行使 Linux 服务器上的 CD-ROM 驱动器对客户端可用：

```
comment = Linux CD-ROM
path = /media/cdrom
locking = No
```

您可以配置以下内容：

- `[cdrom]`。这是网络上所有 SMB 客户端可见的共享名称。
- `comment`。使用此项添加描述共享的额外注释。
- `path`。这是导出 cdrom 目录的路径（例如 `path = /media/cdrom`）。

## 492 第 10 管理网络服务：DNS 以及文件和打印服务

通过非常严格的默认配置，此类共享仅对此系统上的现有用户可用。

如果此共享应对所有人可用，请在配置中添加 `guest = yes` 行。此设置赋予网络上的任何人读取权限。

您需要非常小心地处理此参数，特别是在 `[global]` 节中使用它时。

- `[homes]`。如果用户拥有 Linux 文件服务器的有效帐户和密码以及自己的家目录，她就可以通过 `[homes]` 共享连接到它。

以下是配置过的 `[homes]` 共享示例：

```
comment = Home Directories
valid users = %S
browseable = No
read only = No
create mask = 0640
directory mask = 750
inherit permissions = Yes
```

配置以下内容：

- `[homes]`。只要没有其他共享使用连接到 SMB 服务器的用户的共享名称，就会使用 `[homes]` 共享指令动态生成共享。

生成的共享名称与用户名完全相同。

- `valid users = %S`，一旦成功建立，`%S` 就会替换为共享的实际名称。

对于 `[homes]` 共享，这始终与用户名相同。因此，对用户共享的访问权限被专门地限制为该用户本人。

- `browseable = No`。此设置使共享在网络环境中是不可见的。
- `read only = No`。默认情况下，Samba 通过此参数禁止对任何导出共享的写入访问。

要使共享变为可写，请将值设置为 `read only = No`，这等同于 `writeable = Yes`。

## 配置网络文件系统 493

- `create mask = 0640`。基于 Windows NT 的系统不理解 UNIX 权限的“概念”，因此它们在创建文件时无法分配权限。

此参数定义了分配给新创建文件的访问权限。这仅适用于可写共享。

在此示例中，所有者具有读写权限，所有者主主组的成员具有读取权限。

> 参数 `valid users = %S` 即使组具有读取权限，也会防止读取访问。如果您希望组具有读取或写入权限，则需要禁用 `valid users = %S` 这一行。

## 密码保护

SMB 协议源于 DOS 环境，并直接考虑安全问题。

每个共享都可以用密码保护。SMB 有三种可能的权限检查方式：

- 共享级安全（`security = share`）。密码被固定地分配给共享。知道此密码的人都可以访问该共享。
- 用户级安全（`security = user`）。所有用户必须使用自己的密码在服务器上注册。注册后，服务器可以根据用户名授予单个导出共享的访问权限。
- 服务器级安全（`security = server`）。对于其客户端，Samba 假装工作在用户级模式。然而，它将所有密码查询传递给另一个用户级模式服务器，由该服务器处理身份验证。此设置需要额外的参数（`password server =`）。

设置共享、用户和服务器级安全适用于整个服务器。无法在服务器配置中同时提供使用共享级安全的单个共享和使用用户级安全的其他共享。但是，您可以为系统上的每个配置 IP 地址运行一个单独的 Samba 服务器。

> 有关密码安全的更多信息，请检查 Samba HOWTO 集合。

## 第 10 管理网络服务：DNS 以及文件和打印服务

## 使用 YaST 配置 Samba 服务器

要使用 YaST 配置 Samba 服务器，请执行以下操作：

1. 从 KDE 开始，通过以下操作之一启动 YaST 模块：

   * 选择 YaST 图标，输入 root 密码，选择 Network > Samba Server。
   * 打开终端并输入 `yast2-server`。

   出现类似于图 10-9 的屏幕。

2. 从下拉列表中选择网络上可用的工作组或域，或输入名称。

3. 点击 Next 继续。

## 配置网络文件系统 495

出现类似于图 10-10 的屏幕。

4. 为您的 Samba 服务器选择域控制器类型；然后点击 Next。

通常情况下，您可能希望选择主域控制器（Primary Domain Controller）以使用本地定义的用户和密码进行安全。

## 496 第 10 管理网络服务：DNS 以及文件和打印服务

出现图 10-11 所示的对话框。

对话框上的四个标签页允许您为 Samba 服务器配置启动、共享、身份和信任域。

5. 通过选择 On 配置系统服务在开机时启动。

6. 通过选择 Shares 显示配置的共享列表。

## 配置网络文件系统 497

出现图 10-12 所示的对话框。

您可以通过添加（Add）、编辑（Edit）或删除（Delete）共享来管理可用共享列表。

您还可以通过选择 Toggle Status 来启用或禁用选定的共享。Disabled 表示该共享在启动服务器时不会被激活。

可以通过选择 Identity 显示配置服务器身份的选项。

## 498 第 10 管理网络服务：DNS 以及文件和打印服务

出现图 10-13 所示的对话框。

您可以更改安装期间配置的基础设置（选择工作组或域名称以及域控制器）。

您还可以将主机配置为 WINS 服务器，或输入网络上 WINS 服务器的 IP 地址。如果您输入星号（*），YaST 将自动查找 WINS 服务器。

此外，您可以在 NetBIOS Host Name 字段中输入名称，确定是否在网络中使用备用主机名。

8. 通过选择 Trusted Domains 显示信任域列表。

出现图 10-14 所示的对话框。

![](img/39399c9366aee7ad257a7d2d6505f1a1_520_0.png)

图 10-14

可以通过添加（Add）或删除（Delete）域名来管理主机可以信任的域名列表。

请记住，添加受信任域名意味着你采用了该域的相应设置。

- 当你完成 Samba 服务器配置时，选择“完成”保存设置。
- （可选）如果你是从桌面启动 YaST 的，请关闭 YaST 控制中心。

## 使用 YaST 配置 Samba 客户端

要使用 YaST 配置 Samba 客户端，请执行以下操作：

- 通过以下任之一启动 YaST Samba 客户端模块：
- 从桌面，选择“应用程序 > 系统 > YaST”启动 YaST 控制中心；输入 root 密码并点击确定；然后选择：

  网络服务 > Samba 客户端

或

- 从终端窗口，输入 `su -` 和 root 密码，然后输入 `yast2 samba-client`。

出现一个与图 10-15 类似的屏幕。

![](img/39399c9366aee7ad257a7d2d6505f1a1_521_0.png)

图 10-15

- 2. 输入 Samba 客户端成员的工作组名称或 NT 域，并通过“浏览”查找并选择可用的工作组或域。
- 3. 选择“Linux 认证也使用 SMB 信息”，允许对 NT 服务器进行密码验证。
- 4. 完成后，选择“完成”保存 Samba 客户端设置。
- 5. （可选）如果你是从桌面启动 YaST 的，请关闭 YaST 控制中心。

## 监控和测试 Samba

配置 Samba 后，你需要了解以下内容来监控和测试你的配置：

- 诊断工具
- 如何启动和测试 Samba
- 使用 smclient 访问 SMB 共享
- 将 SMB 共享挂载到 Linux 系统

### 诊断工具

以下是你可以用于检查 Samba 配置的命令：

- `/usr/bin/testparam`。你可以输入此命令对 `/etc/samba/smb.conf` 文件进行语法检查。

将显示所有设置参数的列表。然而，只有最后部分的输出（光标在此处中断）对你对配置的初始检查很重要。

查找以下内容：

Loaded services file OK.

如果你看到此消息，说明到为止一切正常。如果你按下回车键，将显示一个长列表。只有在你进行高级调试时才需要评估此列表。

如果服务存在语法错误，`testparam` 通常会立即显示此。与早期版本相比，`/etc/samba/smb.conf` 文件已变得不易出现语法错误。

然而，你应该避免在同一行上编写选项和注释。如果选项行包含错误表达式（例如 `security = purchase`），Samba 将回退到默认的 `security = user`。

虽然这种方式更可靠，但在实践中很容易被忽略。

- `/usr/bin/nmblook`。你可以输入此命令显示主机的本地或远程名称，无论运行 NetBIOS 的什么种操作系统（微软对应的命令是 `nbtstat`）。

你可以通过 `nmblook -help` 查看此命令提供的各种功能。

命令 `nmblook` 在使用选项 `-A` 和 `-S` 时较为冗长。当你使用选项 `-S` 时，`nmblook` 首先显示查询主机的 IP 号，然后显示它们注册的名称，包括所有别名。
