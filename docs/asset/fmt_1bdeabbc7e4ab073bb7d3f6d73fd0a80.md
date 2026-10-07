
`server` 是服务器的主机名或 IP 地址。`name` 是服务器上打印机的名称。

# 总结

CUPS 支持许多类型的客户端配置，包括非 CUPS 客户端。当设置了两个或多个带有打印机的服务器时，基本的 CUPS 客户端配置提供了远程打印机的自动负载均衡和故障保护。

# 图 7.3
IPP 对象之间的关系。

![](img/b159ac7fe2135643dc37ccfeef6d3980_151_0.png)

这些对象的每个关系和操作都可以由有限状态机驱动，使得 IPP 在各种硬件上都极易实现。

## 扩展

IPP 支持从 HTTP 传输层到低层 IPP 协议本身的灵活扩展机制。可以为属性、身份验证、加密、文档格式、通知、操作和值类型添加扩展，而不会破坏与 IPP 标准的兼容性。这种扩展机制允许 IPP 成为一个一个活跃的、不断增长的标准，同时不会牺牲与旧实现的兼容性，使其成为比古老的 LPD 更好的长期网络打印解决方案。

## 参考文献

IPP 由 IETF 标准的几篇“意见征求”（RFC）论文以及来自 PWG 的几篇标准论文进行了描述。表 7.1 描述了当前的 IETF 规范：

## 表 7.1 IETF IPP 规范

| 文档 | 描述 |
| --- | --- |
| RFC 2568 互联网打印协议模型和协议结构的原理 | 描述了为什么 IPP 采用这样的设计 |
| RFC 2567 互联网打印协议的设计目标 | 描述了互联网打印协议的最终目标 |

## 表 7.1 续表

| 文档 | 描述 |
| --- | --- |
| RFC 2569 LPD 与 IPP 协议之间的映射 | 描述了如何将 IPP 映射到 LPD，反之亦然 |
| RFC 2911 IPP/1.1: 模型与语义 | 描述了 IPP 的所有打印机和作业对象的操作及属性 |
| RFC 2910 IPP/1.1: 编码与 IPP/1.1: 实现指南 | 描述了低层 IPP 协议 |
| IPP: IPP 作业和打印机管理操作 | 描述了用于打印机和作业管理的 IPP 扩展 |
| IPP: 作业和打印机组操作 | 描述了用于控制打印机和作业的 IPP 扩展 |
| IPP: 作业进度属性 | 描述了用于详细监控作业状态的新型作业属性 |
| IPP: 集合属性语法 | 描述了一种被某些扩展使用的新集合值类型 |
| IPP: IPP 事件通知规范 | 描述了 IPP 通知机制和订阅对象 |
| 用于事件通知的协议/1.0 的 inod 递送方法 | 描述了 inod（广播）通知方案 |
| IPP: ippget 事件通知递送方法 | 描述了 ippget（轮询）通知方案 |
| IPP: mailto 通知递送方法 | 描述了 mailto（电子邮件）通知方案 |

PWG 还有几项被 PWG 成员认可的额外标准，以及关于在使用蓝牙协议的无线设备上使用 IPP 的实验性文档。

您可以在以下网站找到当前的 IPP 文档：

http://www.pwg.org/ipp/

## 总结

IPP 是 RFC 1179 中描述的 LPD 协议的替代方案。IPP 的设计是一个相当易于实现的协议，同时提供了许多高级打印功能。IPP 扩展机制允许 IPP 能够增长以支持新技术，同时保持与现有的 IPP 实现的兼容性。

## 第 8 章

## IPP 请求的构造

本章描述了互联网打印协议的低层格式，包括请求或响应中的每个值是如何编码的，以及数据如何在客户端和服务器之间交换。

## 剖析 IPP 请求

每个 IPP 请求都由以下部分组成：

- 一个 HTTP 请求
- 一个 IPP 请求消息
- 可选的额外（文档）数据
- 一个 HTTP 响应
- 一个 IPP 响应消息

后续章节描述了这些每个部分。

## HTTP 请求

HTTP 请求是一个包含类型为 `application/ipp` 数据的 POST 请求。每个 POST 包含一个 IPP 请求消息，并可能包含 Print-Job 请求或 Send-Document 请求的文档数据。图 8.1 显示了数据流。

![](img/b159ac7fe2135643dc37ccfeef6d3980_154_0.png)

由于 IPP 要求完全符合 HTTP/1.1 标准，IPP 请求可以使用 `Content-length` 字段一次性发送，也可以使用分块传输（chunking）增量发送。POST 的结果也是类型为 `application/ipp` 的数据，由 IPP 响应消息组成。

请求和响应都使用通用格式，以固定长度的头部开始，随后是一系列属性。IPP 消息中的数据是字节对齐的，因此在您的程序中，通常必须从适当对齐的数据结构中读取和写入数据。

## 请求头部

请求头部由 8 字节二进制数据组成，如图 8.2 所示。

| IPP 主版本 | IPP 小版本 | 操作代码 |
| --- | --- | --- |
| 请求 ID | | |

图 8.2

IPP 请求头部由 8 字节二进制数据组成。

前两个字节包含 IPP 版本号，`01 00` 代表 IPP/1.0，或者 `01 01` 代表 IPP/1.1。通常情况下，您应该发送 IPP/1.1 请求，除非服务器响应了 `server-error-version-not-supported`。

第 3-4 字节包含操作代码，这是一个网络（大端序）字节序的 16 位整数。表 8.1 列出了当前定义的代码。

## 表 8.1 IPP 操作代码

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x0002 | Print-Job | 打印单个文件 |
| 0x0003 | Print-URI | 打印单个 URI |
| 0x0004 | Validate-Job | 验证作业 |
| 0x0005 | Create-Job | 创建作业 |
| 0x0006 | Send-Document | 向作业中添加文件 |
| 0x0007 | Send-URI | 向作业中添加 URI |
| 0x0008 | Cancel-Job | 取消作业 |
| 0x0009 | Get-Job-Attributes | 获取作业属性 |
| 0x000A | Get-Jobs | 获取作业列表 |
| 0x000B | Get-Printer-Attributes | 获取打印机属性 |
| 0x000C | Hold-Job | 保持作业 |
| 0x000D | Release-Job | 释放作业 |
| 0x000E | Restart-Job | 重启作业 |
| 0x0010 | Pause-Printer | 暂停打印 |
| 0x0011 | Resume-Printer | 恢复打印 |
| 0x0012 | Purge-Job | 清除作业 |
| 0x0013 | Set-Printer | 设置打印机 |
| 0x0014 | Set-Job | 设置作业 |
| 0x0015 | Get-Printer-Supported | 获取打印机支持的值 |

## 第二部分 打印协议

## 表 8.1 续表

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x0016 | Create-Printer-Subscription | 创建打印机订阅 |
| 0x0017 | Create-Job-Subscription | 创建作业订阅 |
| 0x0018 | Get-Subscription-Attributes | 获取订阅属性 |
| 0x0019 | Get-Subscriptions | 获取订阅列表 |
| 0x001A | Renew-Subscription | 续订订阅 |
| 0x001B | Cancel-Subscription | 取消订阅 |
| 0x001C | Get-Notifications | 使用 ippget 获取通知 |
| 0x001D | Send-Notifications | 使用 ippsend 获取通知 |
| 0x0021 | Get-Printer-Support-Files | 获取打印机支持的文件 |
| 0x0022 | Enable-Printer | 允许向打印机提交作业 |
| 0x0023 | Disable-Printer | 禁止向打印机提交作业 |
| 0x0024 | Pause-After-Current-Job | 在完成当前作业后暂停打印 |
| 0x0025 | Hold-New-Jobs | 保持所有新作业 |
| 0x0026 | Release-Held-Jobs | 释放（启动）任何保持的作业 |
| 0x0027 | Deactivate-Printer | 停止打印机并允许进行更改 |
| 0x0028 | Activate-Printer | 启动打印机并允许进行更改 |
| 0x0029 | Restart-Printer | 重启打印机，重启任何被 Deactivate 停止的作业 |
| 0x002A | Shutdown-Printer | 关闭打印机电源 |
| 0x002B | Startup-Printer | 打开打印机电源 |
| 0x002C | Reprocess-Job | 重新打印已完成的作业 |
| 0x002D | Cancel-Current-Job | 取消打印机上的当前作业 |
| 0x002E | Suspend-Current-Job | 暂停打印机上的当前作业 |
| 0x002F | Resume-Job | 重启打印机上的当前作业 |
| 0x0030 | Promote-Job | 在队列中优先于其他作业打印 |
| 0x0031 | Schedule-Job-After | 在另一个作业之后打印 |
| 0x0401 | CUPS-Get-Default | 获取默认打印机 |
| 0x0402 | CUPS-Get-Printers | 获取打印机列表 |
| 0x0403 | CUPS-Add-Printer | 在服务器上添加或修改打印机 |
| 0x0404 | CUPS-Delete-Printer | 从服务器上删除打印机 |
| 0x0405 | CUPS-Get-Classes | 获取打印类列表 |
| 0x0406 | CUPS-Add-Class | 在服务器上添加或修改类 |
| 0x0407 | CUPS-Delete-Class | 从服务器上删除类 |
| 0x0408 | CUPS-Accept-Jobs | 允许向打印机或打印类提交新作业（类似于新的 Enable-Printer 操作） |

## 表 8.1 续

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x4009 | CUPS-Reject-Jobs | 拒绝发送到打印机或打印机类的新打印作业（类似于新的 Disable-Printer 操作） |
| 0x400A | CUPS-Set-Default | 设置默认打印机 |
| 0x400B | CUPS-Get-Devices | 获取可用打印机设备列表 |
| 0x400C | CUPS-Get-PPDS | 获取可用的打印机驱动程序列表 |
| 0x400D | CUPS-Move-Job | 将打印作业移动到另一个打印机或打印机类 |

字节 5–8 包含请求 ID，这是一个网络字节序（大端序）的 32 位整数。请求 ID 由客户端生成并由服务器返回，以便客户端确定哪个响应对应哪一个请求。

# 什么是大端和小小端？

大端和小小端是指大于 1 字节的数字或指针值中的字节顺序。通过大多数网络协议发送的多字节数字采用大端序，因此“网络字节序”术语等同于大端序。

大端序数字以最高字节（高位）存储：一个 32 位整数值 1234 在内存中存储为字节 0, 0, 4 和 2¹⁰。

小端序数字以最低有效字节（低位）存储：一个 32 位整数值 1234 在内存中存储为字节 2¹⁰, 4, 0 和 0。

大端和小小端的术语源自 Swift 语言中的《格列夫游记》，这借用了丹尼·科恩（Danny Cohen）著名的论文《论圣战与和平的诉求》。

## IPP 组和属性

IPP 组紧跟在请求头之后。每个组或属性都以一个字节的值标签开头。某些值标签引入属性组，而另一些则表示属性值的开始。属性标签之后是属性名称和属性值本身（参见第 8.3 节）。

请求以 Get-Jobs 请求的标准 8 字节头开始。接下来是一个开始操作属性的组标签 (01) 和一个开始字符集值的字符集标签 (47)。字符集标签之后是属性长度 (18) 和名称字符串 ("attributes-charset")。在值字符串 ("utf-8") 之后，该属性完成。请求中的所有属性都重复此过程，并并使用属性结束标签 (03) 结束。

# 互联网打印协议

| 01 01 | IPP/1.1 版本号 |
| 00 0A | Get-Jobs |
| 00 00 01 | 请求 ID #1 |
| 01 | 操作组标签 |
| 47 | 字符集 |
| 00 12 | 名称 = 18 |
| "attributes-charset" | 值长度 = 5 |
| 00 05 | 自然语言 |
| "utf-8" | 名称长度 = 27 |
| 48 | |
| 00 1B | 值长度 = 2 |
| "attributes-natural-language" | |
| 00 02 | uri |
| "en" | 名称长度 = 11 |
| 45 | |
| 00 0B | 值长度 = 13 |
| "printer-uri" | |
| 00 0D | |
| "ipp://foo/bar" | 属性结束标签 |
| 03 | |

图 8.3
请求中的 IPP 属性数据。

# 组

IPP 目前定义了表 8.2 所示的七种组标签。每个组标签用于该组的第一个属性一次；如果该组中未提供属性，则省略该组标签。属性结束标签是一个特殊的组标签，用作 IPP 消息的最后一个标签。

除了属性结束标签外，IPP 请求中的所有标签必须以升序发送（与表 8.2 所示的顺序相同）。

## 表 8.2 IPP 组标签

| 标签 | 名称 | 描述 |
| --- | --- | --- |
| 0x01 | operation-attributes-tag | 操作属性组 |
| 0x02 | job-attributes-tag | 作业属性组 |
| 0x03 | end-of-attributes-tag | IPP 消息的结束标签 |
| 0x04 | printer-attributes-tag | 打印机属性组 |
| 0x05 | unsupported-attributes-tag | IPP 服务器返回的不支持属性的组 |

## 表 8.2 续

| 标签 | 名称 | 描述 |
| --- | --- | --- |
| 0x06 | subscription-attributes-tag | 订阅属性组（创建订阅时使用） |
| 0x07 | event-notification-attributes-tag | 事件属性组（用于报告来自订阅的事件） |

# 属性

在每个属性组内部是属性本身。每个属性都以一个字节的标签开头（参见表 8.3），随后是网络字节序（大端序）的 16 位名称长度、名称中的字符、网络字节序（大端序）的 16 位长度以及数据值。

## 表 8.3 IPP 值标签

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x16 | delete-attribute | 删除命名的属性（仅限 IPP 请求） |
| 0x21 | integer | 网络字节序（大端序）的 32 位符号整数。 |
| 0x22 | boolean | 一个字节整数，0 表示假值，1 表示真值 |
| 0x23 | enum | 网络字节序（大端序）的 32 位符号整数枚举。 |
| 0x30 | octetString | 最多 32767 字节的任意字符串。 |
| 0x31 | dateTime | 11 字节 RFC 1903 格式的日期和时间。 |
| 0x32 | resolution | 9 分辨率值，由两个网络字节序（大端序）的 32 位符号整数组成，代表水平和垂直分辨率。 |
| 0x33 | rangeInteger | 两个网络字节序（大端序）的 32 位符号整数。 |
| 0x34 | begCollection | 集合的开始。 |
| 0x35 | textWithLanguage | 带有语言的文本。值 3 表示英寸，值 4 表示厘米。 |
| 0x36 | nameWithLanguage | 带有语言的名称。网络字节序（大端序）的长度，文本字符串。 |
| 0x37 | endCollection | 集合的结束。 |

## 表 8.3 续

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x41 | textWithoutLanguage | 默认文本。 |
| 0x42 | nameWithoutLanguage | 默认名称。 |
| 0x43 | keyword | 关键字。 |
| 0x44 | uri | URI。 |
| 0x45 | uriScheme | URI 方案。 |
| 0x46 | charset | 字符集。 |
| 0x47 | naturalLanguage | 自然语言。 |
| 0x48 | defaultLanguage | 默认语言。 |
| 0x49 | mimeType | MIME 类型。 |
| 0x4A | member | 成员。 |

## 数组

IPP 支持值数组；第一个值是元素数量。图 8.4 显示了数组值。

## 响应

IPP 响应的格式与 IPP 请求完全相同，只是头部中的操作代码替换为状态码。

## 状态码

状态码是一个网络字节序（大端序）的 16 位整数，定义请求的成功失败。大多数错误包含定义特定错误的属性（例如 printer-reasons 属性）。表 8.4 显示了可能的状态码。

| 代码 | 描述 |
| --- | --- |
| 0x0000 | 正常。 |
| 0x0001 | 忽略了某些属性。 |
| 0x0002 | 正常，但某些属性之间冲突。 |
| 0x0003 | 正常，但未创建订阅。 |
| 0x0004 | 正常，但接收者无法处理所有事件。 |
| 0x0005 | 正常，但事件数量超过打印机发送能力。 |
| 0x0006 | 正常，但接收者想要取消订阅。 |
| 0x0300 | redirection-other-site 将 get 重定向到不同的服务器。 |
| 0x0400 | 客户端请求包含无效数据。 |
| 0x0401 | 禁止客户端执行该操作。 |
| 0x0402 | 客户端未身份验证，需要验证后才能允许操作。 |
| 0x0403 | 客户端无权限执行该操作。 |
| 0x0404 | 操作无法成功。 |
| 0x0405 | 客户端请求未及时收到。 |
| 0x0406 | 客户端请求涉及的对象不存在。 |
| 0x0407 | 请求的对象已不可用。 |
| 0x0408 | 客户端包含额外数据过大。 |
| 0x0409 | 客户端请求包含的属性值过大。 |

图 8.4
数组值。

# 表 8.4 续

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x040A | client-error-document-not-supported | 不支持文档格式。 |
| 0x040B | client-error-attributes-values-not-supported | 请求包含不支持的属性或值。 |
| 0x040C | client-error-uri-scheme-supported | URI 属性中的 URI 方案不支持。 |
| 0x040D | client-error-charset-not-supported | 客户端请求使用了不支持的字符集。 |
| 0x040E | client-error-conflicting-attributes | 客户端请求包含冲突的属性。 |
| 0x040F | client-error-compression-not-supported | 客户端请求使用了不支持的压缩类型。 |
| 0x0410 | client-error-compression-error | 压缩数据包含错误。 |
| 0x0411 | client-error-document-format-error | 文档数据包含错误。 |
| 0x0412 | client-error-document-access-error | 无法访问远程文档。 |
| 0x0413 | client-error-attributes-not-settable | 客户端请求中指定的属性无法更改。 |
| 0x0414 | client-error-ignored-all-subscriptions | 服务器在 Create-Job、Print-Job、Print-URI 或 Reprocess-Job 操作中无法创建订阅。 |
| 0x0415 | client-errors-too-many-subscriptions | 服务器无法再创建订阅订阅。 |
| 0x0416 | client-error-ignored-all-notifications | 通知接收接收者无法收集任何事件。 |
| 0x0417 | client-error-print-support-file-not | 找不到打印机支持文件（驱动程序）。 |
| 0x0500 | server-error-internal-error | 服务器发生内部错误。 |
| 0x0501 | server-error-operation-not-supported | 服务器不支持请求的操作。 |
| 0x0502 | server-error-service-unavailable | 由于临时状况无法执行请求的操作。 |
| 0x0503 | server-error-version-not-supported | 请求头中的 IPP 版本号不支持。 |
| 0x0504 | server-error-device-error | 打印机对象无法打印任务。 |
| 0x0505 | server-error-temporary-error | 由于临时服务器错误无法执行请求的操作。 |

# 表 8.4 续

| 代码 | 名称 | 描述 |
|---|---|---|
| 0x0506 | server-error-accepting-jobs | 打印机对象此时不接受任务。 |
| 0x0507 | server-error-busy | 由于负载过高，服务器暂时不可用。 |
| 0x0508 | server-error-job-canceled | 打印任务在从客户端接收所有文档数据之前已取消。 |
| 0x0509 | server-error-multiple-document-not-supported | 服务器不支持在打印任务中包含多个文档。 |
| 0x050A | server-error-printer-deactivated | 打印机处于离线状态或已关机。 |

# 值标签

当 IPP 请求中的属性无法被服务器使用时，响应将使用特殊的值标签包含这些属性。这些属性可以在“不支持组”（unsupported-attributes-tag）中找到，不同的值标签有助于指示属性为何被拒绝。表 8.5 显示了在响应中使用的额外值标签。

# 表 8.5 响应中的 IPP 值标签

| 代码 | 名称 | 描述 |
|---|---|---|
| 0x10 | unsupported | 属性名不支持。 |
| 0x12 | unknown | 命名属性的值当前尚未知。 |
| 0x13 | no-value | 命名属性没有关联的值。 |
| 0x15 | not-settable | 无法设置命名属性的值。 |
| 0x17 | admin-define | 值由管理员定义且无法更改。 |

# 包含多个对象的响应

Get-Jobs、Get-Notifications、Get-Subscriptions、CUPS-Classes、Get-Pinters 操作的 IPP 响应可能包含多个对象的属性，这些属性会多次引入相同的组标签。然而，对象属性内的组标签仍按升序发送。请参见图 8.5 关于 Get-Jobs 操作的示例。

# 互联网打印协议

| 01 01 | IPP/1.1 版本号 |
| 00 00 | successful-ok |
| 00 00 00 01 | 请求 ID #1 |
| 01 | operation-group-tag |
| 47 | charset |
| 00 12 | name length = 18 |
| "attributes-charset" | |
| 00 05 | value length = 5 |
| "utf-8" | naturalLanguage |
| 00 1B | name length = 27 |
| "attributes-charset-language" | |
| 00 02 | value length = 2 |
| "en" | operation-group-tag |
| 45 | uri |
| 00 07 | name length = 7 |
| "job-uri" |
| 00 14 | value length = 20 |
| "ipp://printer/jobs/1" | |
| 21 | integer |
| 00 06 | name length = 6 |
| "job-id" | |
| 00 04 | value length = 4 |
| 00 00 | value = 1 |
| 23 | enum |
| 00 09 | name length = 9 |
| "job-state" | |
| 00 04 | value length = 4 |
| 00 05 | value = 3 |
| 02 | attributes-tag |
| 45 | uri |
| 00 07 | name length = 7 |
| "job-uri" | |
| 00 14 | value length = 20 |
| "ipp://printer/jobs/2" | |
| 21 | integer |
| 00 06 | name length = 6 |
| "job-id" | |
| 00 04 | value length = 4 |
| 00 00 | value = 2 |
| 23 | enum |
| 00 09 | name length = 9 |
| "job-state" | |
| 00 04 | value length = 4 |
| 00 00 | value = 1 |
| 02 | attributes-tag |
| 45 | attributes-tag

一个 IPP 请求的结构

```
