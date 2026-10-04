

# 134 第4 章 • 攻击与防御 Windows XP 专业

## 表 4.5 本地安全选项

| 选项 | 最小值 | 推荐值 |
|---|---|--|
| 限制本地账户空密码仅用于控制台登录 | 启用 | 启用 |
| 重命名管理员 | Administrator | (Renamed_Administrator_Account) |
| 重命名访客账户 | Guest | (Renamed_Guest_Account) |
| 审计全局系统对象的访问 | 禁用 | 启用 |
| 审计备份和恢复权限的使用 | 禁用 | 启用 |
| 如果无法记录安全审核则立即关闭系统 | 禁用 | 启用 |
| 允许在不登录的情况下卸下设备 | 启用 | 启用 |
| 允许格式化和弹出移动式介质 | 验证的用户 | 验证的用户 |
| 防止用户安装打印机驱动程序 | 禁用 | 启用
| 限制 CD-ROM 访问仅限本地登录用户 | 禁用 | 禁用 |
| 限制软盘访问仅限本地登录用户 | 禁用 | 禁用 |
| 未签名驱动程序的安装行为 | 允许安装 | 不允许安装 |
| 域控制器：允许服务器操作员计划任务 | 启用 | 启用 |
| LDAP 服务器签名要求 | 无 | 无 *这是一个特定于基础设施的要求，仅在环境内部使用时才定义。 |
| 拒绝计算机账户密码更改 | 启用 | 启用 |
| 对安全通道数据数字加密或签名（始终） | 禁用 | 启用 |
| 数字加密安全通道数据（可能时） | 启用 | 启用 |
| 对通道数据数字签名（可能时） | 启用 | 启用 |
| 禁用计算机账户密码更改 | 禁用 | 禁用 |
| 计算机账户密码最大有效期 | 60 天 | 30 天 |
| 要求强会话密钥（Windows 2000 或更高版本） | 禁用 | 启用 |
| 不显示最后用户名 | 启用 | 启用 |
| 不要求 CTRL+ALT+DEL | 禁用 | 禁用 |
| 尝试登录的用户的消息 | 无 | 您应该为所有尝试身份验证系统的用户确定一个要显示的消息。示例消息：“为了保护系统不受未经授权的使用并确保系统正常运行，此系统上的活动可能会被监控和记录，并可能接受审核。使用此系统意味着同意潜在的监控和记录。禁止任何未经授权的访问或尝试未经授权使用此自动化系统，可能面临刑事和民事处罚。您应该为所有尝试身份验证系统的用户确定一个要显示的消息。示例消息：‘注意：正在登录 XYZ 计算机’” |
| 缓存之前的登录次数（以防域控制器不可用时） | 10 次登录 | 1 次登录 |
| 在过期前提示用户更改密码 | 14 天 | 7 天 |
| 需要域控制器认证以解锁工作站 | 禁用 | 禁用 |
| 智能卡删除行为 | 不采取操作 | 锁定工作站 |
| 对通信数字签名（始终） | 禁用 | 禁用 |
| 对通信数字签名（如果服务器同意） | 启用 | 启用 |
| 向第三方 SMB 服务器发送未加密的密码 | 禁用 | 禁用 |
| 挂起会话所需的空闲时间 | 120 分钟 | 30 分钟 |

## Microsoft 网络客户端

### ### 表 4.5 本地安全选项

| 选项 | 最小值 | 推荐值 |
|---|---|--|
| **Microsoft 网络服务器** | | |
| 对通信数字签名（始终） | 禁用 | 禁用 |
| 对通信数字签名（如果客户端同意） | 启用 | 启用 |
| 登录时间过期时断开客户端 | 启用 | 启用 |
| **网络访问** | | |
| 允许匿名 SID/名称翻译 | 禁用 | 禁用 |
| 网络访问：不允许匿名枚举 SAM 账户 | 启用 | 启用 |
| 不允许匿名枚举 SAM 账户和共享 | 启用 | 启用 |
| 不允许存储网络身份验证的凭据或 .NET 通行证 | 启用 | 启用 |
| 让“Everyone”权限允许匿名用户 | 禁用 | 禁用 |
| 网络访问：可以匿名访问的命名管道 | 无 | 无 |
| 远程访问的注册表路径 | System\CurrentSet\Control\ProductOptions\System\CurrentControlSet\Control\Print\Printers\System\CurrentControlSet\ | System\CurrentSet\Services\Eventlog\System\CurrentControlSet\Control\TerminalServer\Software\Microsoft\OLAP Server\ServerApplications |
| System\CurrentControlSet\Services\Eventlog\Software\Microsoft\OLAP Server,\Software\Microsoft\WindowsNT\CurrentVersionSystem\CurrentControlSet\Control\ContentIndexSystem\CurrentControlSet\Control\TerminalServerSystem\CurrentControlSet\Control\TerminalServer\UserConfigSystem\CurrentControlSet\Control\TerminalServer\DefaultUserConfiguration | 禁用 | 禁用 |
| 可以匿名访问的共享 | 禁用 | 禁用 |
| 本地账户的共享和安全模型 | 经典 – 本地用户身份验证自身 | 经典 – 本地用户身份验证自身 |
| 网络安全 | | |
| 更改密码时不存储 LAN Manager 哈希值 | 启用 | 启用 |
| 登录时间过期时强制注销 | 启用 | 启用 |
| LAN Manager 认证级别 | 发送 LM & NTLM – 如果协商使用 NTLmv2 会话安全 | 发送 LM & NTLM – 如果协商使用 NTLmv2 会话安全 |
| LDAP 客户端签名要求 | 协商签名 | 协商签名 |
| 基于 NTLM SSP 的客户端（包括 RPC）的最小会话安全 | 要求消息机密性 | 要求 NTLmv2 会话安全 |
| 基于 NTLM SSP 的服务器（包括安全 RPC）的最小会话安全 | 要求消息机密性 | 要求 NTLmv2 会话安全 |

## 恢复控制台

| 允许管理员登录 | 禁用 | 禁用 |
| 允许对所有驱动器和文件夹进行软盘复制和访问 | 禁用 | 禁用 |

## 机

| 允许在不登录的情况下关闭系统 | 启用 | 启用 |
| 清除虚拟分页文件 | 启用 | 启用 |

## 系统加密

| 使用符合 FIPS 的算法进行加密、哈希和签名 | 禁用 | 启用 |

## 系统对象

| 管理员组成员创建对象的默认所有者 | 对象创建者 | 对象创建者 |
| 要求非 Windows 子系统不区分大小写 | 启用 | 启用 |
| 增强内部系统对象的默认权限（例如：符号链接） | 启用 | 启用 |

![](img/729efc56f204a2ebffb8295c3a2dfdfb_163_0.png)

由于软件限制策略的学习曲线陡峭、整体复杂性高且非多选择性配置，我们专门分配了一个章节用于配置您的策略。欲需更多信息，请参阅本章节后后的“软件限制策略”部分。

## 安全系统文件和目录权限

系统文件和目录结构是您在加固过程中必须保护的关键配置之一。通常情况下，只需要对几个系统目录设置额外的、修改的或验证权限。接下来的章节将向您展示如何设置这些或其他目录以存储敏感或不可信的信息。管理目录应均配置为允许管理员组完全控制权限。不应允许未经验证的用户访问这些文件夹，系统账户应仅允许读取和执行权限，其他系统用户应仅具有执行应用程序的能力。

## 管理目录

Windows XP 专业版的默认安装在分配系统目录权限方面是足够的；但应对以下目录进行配置，允许管理员和系统组完全控制：

- /Windows/System32
- /Windows/System
- /Windows/Temp
- /Windows/Assembly
- /Windows/Drivers
- /Windows/Repair
- /Documents and Settings/Administrator（如果您已经更改了管理员账户名称，此文件夹将反映该更改）

