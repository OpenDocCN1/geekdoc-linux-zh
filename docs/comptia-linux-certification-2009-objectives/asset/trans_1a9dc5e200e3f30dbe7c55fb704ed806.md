

## lmhosts 文件

Samba 使用 lmhosts 文件将 NetBIOS 名称解析为 IP 地址。该文件的结构类似于 /etc/hosts 文件，但主机名遵循 NetBIOS 命名约定。lmhosts 文件的默认位置与 smb.conf 文件相同，即 /etc/samba。

## smbclient 命令

smbclient 命令用于通过网络传输文件和查看共享资源的名称。下表列出了 smbclient 命令提供的一些选项。

| 选项 | 用途 |
| :--- | :--- |
| `-N` | 抑制密码提示。 |
| `-L 主机名` | 指定显示来自指定主机的共享。 |
| `-s 路径` | 指定 smb.conf 文件的位置。 |
| `-U 用户名` | 指定 Samba 用户名。 |

它也用作获取文件的工具。获取文件的语法为 smbclient //机器/服务。

## nmblookup 命令

nmblookup 命令用于将 NETBIOS 名称解析为 IP 地址。下表列出了 nmblookup 命令中一些常用的选项。

| 选项 | 用途 |
| :--- | :--- |
| `-T` | 将 IP 地址解析为主机名。 |
| `-s 路径` | 指定 smb.conf 文件的位置。 |
| `-M` | 定位主控浏览器。 |
| `-S` | 显示节点状态。 |

## Samba 配置文件

存储在 /etc/samba 目录中的 smb.conf 文件是 Samba 服务的主要配置文件。初始化脚本从 /etc/init.d/smb 文件运行。smb.conf 文件的结构与 Windows.ini 文件类似。此文件包含每个需要共享的目录或设备的共享定义。典型的共享定义包含共享名称、共享的目录或设备路径，以及允许或拒绝访问该共享的其他选项。每个共享都定义为方括号内的一个部分，共享名称特定于正在共享的资源。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_575_0.png)

```
# Un-comment the following to provide a specific roving profile share
# the default is to use the user's home directory
; [Profiles]
; 	path = /var/lib/samba/profiles
; 	browseable = no
; 	guest ok = yes

# A publicly accessible directory, but read only, except for people in
# the "staff" group
; [public]
; 	comment = Public Stuff
; 	path = /home/samba
; 	public = yes
; 	writable = yes
; 	printable = no
```

![](img/477ccb2f05b6ba1b2d563ea74f18c197_576_0.png)

默认情况下，smb.conf 文件由三个部分组成：global、homes 和 printers。每个部分都包含针对该共享的特定选项。global 部分定义了适用于整个服务器的选项，例如工作组名称、日志大小和安全模式。它定义了所有其他共享通用的默认选项。global 部分中给出的选项可以被其他部分覆盖。homes 部分包含定义用户对主目录中文件访问权限的选项，例如 browseable 和 writable。printers 部分包含定义打印机及其服务共享的选项，例如 path 和 guest ok。

```
[global]
#
# ---------------------- Network Related Options ----------------------
#
# workgroup = NT-Domain-Name or Workgroup-Name, eg: MID-EARTH
# server string is the equivalent of the NT Description field
#
# netbios name can be used to specify a server name not tied to the hostname

[homes]
 	comment = Home Directories
 	browseable = no
 	writable = yes
 	valid users = %S
; 	valid users = MYDOMAIN\%S

[printers]
 	comment = All Printers
 	path = /var/spool/samba
 	browseable = no
 	guest ok = no
 	writable = no
 	printable = yes
```

![](img/477ccb2f05b6ba1b2d563ea74f18c197_576_1.png)

smb.conf 文件中的每个部分都包含针对该共享的特定选项。定义选项的语法为 option = value。一些常用的选项列在表中。

| 选项 | 描述 |
| --- | --- |
| public | 指定共享是否由所有用户访问。设置为 yes 或 no。 |
| browseable | 指定共享是否是浏览列表的一部分。设置为 yes 或 no。 |
| writable | 指定共享文件是只读还是既可读又可写。设置为 yes 或 no。 |
| printable | 指定是否允许共享访问打印机。设置为 yes 或 no。 |
| group | 指定用于连接共享的主组。设置为组名。 |

## Samba 配置工具

可以使用 system-config-samba 和 samba-swat 等各种工具在 GUI 中配置 Samba。然而，建议在 CLI 中手动编辑 smb.conf 文件。

| 工具 | 描述 |
| --- | --- |
| system-config-samba | 用于创建、修改和管理 Samba 共享。通过安装 system-config-samba 包来激活它。 |
| samba-swat | 这是一个 Samba Web 管理工具。它包含一个向导，有助于快速配置 Samba。smb.conf 文件的每个部分都指定为一个单独的 swat 屏幕。通过安装 samba-swat 包来激活 samba-swat 工具。 |

## smb.conf 文件中的全局配置选项

smb.conf 文件中一些常用的全局配置选项列在下表中。

| 选项 | 用途 | 需指定的参数 |
| :--- | :--- | :--- |
| server string = 参数 | 指定服务器的简要描述。 | 字符串 |
| log file = 参数 | 指示存储每个用户日志文件的位置。 | 日志文件路径 |
| encrypt passwords = 参数 | 指示是否应使用加密密码。 | 布尔值 |
| password server = 密码服务器地址 | 指定密码服务器。 | 密码服务器的 FQDN |
| smb passwd file = 参数 | 指定如果安全级别设置为 user 时要使用的密码文件位置。 | 带有完整路径的密码文件名 |
| hosts allow = 参数 | 指定可以访问 Samba 共享的主机。 | 以空格分隔的主机名或 IP 地址 |
| idmap uid = 用户 ID 范围 | 指定用于映射 Windows 和 Linux 系统的 UID 范围。 | UID 范围 |
| idmap gid = 组 ID 范围 | 指定用于映射 Windows 和 Linux 系统的 GID 范围。 | GID 范围 |

## 定义 smb.conf 文件中共享的选项

一些常用的共享定义选项列在下表中。

| 选项 | 用途 | 需指定的参数 |
| :--- | :--- | :--- |
| create mode | 指定为在共享中创建的任何文件设置的权限。 | 代表权限的位 |
| directory mode | 指定为在共享中创建的任何目录设置的权限。 | 代表权限的位 |
| invalid users | 指定没有权限访问共享的用户名。 | 以逗号分隔的用户名或组名 |
| write list | 指定具有共享写权限的组。 | 以逗号分隔的用户名或组名 |
| guest ok | 指定是否允许默认来宾用户登录系统。 | 布尔值 |
| max connections | 指定共享的最大连接数。 | 一个数字 |

## Samba 身份验证机制

Samba 基于在 **smb.conf** 文件中设置的 *security* 选项对用户进行身份验证。*security* 选项可以设置为各种级别。

| **安全级别** | **描述** |
| :--- | :--- |
| 共享级安全 | 可以配置一个共享拥有多个密码。每个密码都可以限制对共享的访问。例如，一个密码可能允许只读访问，而另一个则允许读写访问。拥有有效密码的用户可以访问该共享。 |
| 用户级安全 | 可以配置共享允许特定用户访问。用户可以通过提供用户名和密码来访问共享。Samba 服务器对用户进行身份验证并允许访问共享。 |
| 服务器级安全 | 服务器级安全类似于用户级安全。在服务器级安全中，Samba 通过另一个包含密码详情的服务器对用户进行身份验证。包含密码详情的服务器可以是 Samba 服务器或 Windows NT 主域控制器（PDC）。 |
| 域级安全 | 为了实现域级安全，Samba 必须是 Windows 域的成员。Samba 使用 Windows PDC 根据登录 Windows 域时使用的用户名和密码对用户进行身份验证。用户将基于授予他们的权限访问多个共享。每次用户访问共享时，他们不会每次都进行身份验证。 |
| ADS 级安全 | Active Directory Service 级别（ADS）安全类似于域级安全。然而，ADS 级安全使用依赖于 RPC 的 NT4 风格安全。在使用 ADS 时，Samba 允许用户作为原生 AD 成员加入，使他们能够无需每次都进行身份验证即可访问共享。 |

