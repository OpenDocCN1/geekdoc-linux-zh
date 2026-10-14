

# 网络资源属性

| 是否必需？ | 属性 | 描述 |
|---|---|---|
| ✓ | SUBNET = xxx.xxx.xxx.xxx | xxx.xxx.xxx.xxx 为网络子网。网络子网是 IP 地址与网络掩码的按位与。IP 地址 = 18.32.64.121 & 网络掩码 = 255.255.255.0 子网 = 18.32.64.0 |

表 23-7：CAA 网络资源属性

# 磁带/媒体更换器资源属性

| 是否必需？ | 属性 | 描述 |
|---|---|---|
| ✓ | DEVICE_NAME = device-name | device-name 为磁带或媒体更换器设备特殊文件名。您可以指定完整路径或仅设备特殊文件名。/dev/tape/tape0 | tape0 /dev/changer/mc0 | mc0 |

表 23-8：CAA 磁带和媒体更换器资源属性

## 23.4.4.3 网络资源属性

表 23-7 列出了特定于网络资源类型的唯一一个属性。

## 23.4.4.4 磁带和媒体更换器资源属性

表 23-8 列出了特定于磁带和媒体更换器资源两者共有的唯一一个属性。

## 23.4.5 类型定义文件

从 TruCluster Server 版本 5.1A-IPK 开始，/var/cluster/caa/template 目录中的 TYPE_*.cap 文件已被新文件格式类型定义文件 (*.tdf) 取代。此更改主要为了便于在应用程序资源中添加用户定义属性时的定制。

类型定义文件定义了资源的属性。以下条目定义资源属性。

- attribute - 属性的名称。
- switch - 这是 caa_profile 命令开关，用于为此属性分配值。
- type - 属性的数据类型。有效数据类型包括：boolean、file、internet_address、name_list、name_string、positive_integer、string。
- default - 属性的默认值。
- required - 属性是否必需。

例如，以下是应用程序资源类型定义文件 (application.tdf) 中定义 AUTO_START 属性的摘录。

```
# grep -p AUTO_START application.tdf
! ==============================
attribute: AUTO_START
type: boolean
switch: -o as
default: 0
required: no
```

“AUTO_START” 资源属性不是必需属性。资源的预期值为布尔值，默认值为 0。 “-o as” 开关是传递 AUTO_START 属性值给 caa_profile(8) 命令的命令选项（有关更多信息，请参阅第 23.4.6 节）。

此外，用户定义属性可以添加到应用程序资源类型定义文件。我们将在第 23.5.3.3 节中介绍此主题。

## 23.4.6 创建资源配置文件

资源配置文件可以通过多种方式创建。

- 使用 caa_profile 命令。
- 使用 “sysman caa” 命令（有关示例，请参阅第 23.5.2 节）。
- 使用您喜欢的编辑器创建配置文件。
- 使用上述选项的组合。

本节将探讨第一个选项。

caa_profile 命令可用于从位于 /var/cluster/caa/template 的默认配置文件模板创建资源，或使用 “-I” 选项使用位于其他位置的模板。

## caa_profile(8) 命令的主要选项

| 选项 | 描述 |
|---|---|
| -create | 创建资源配置文件 |
| -delete | 删除资源配置文件 |
| -update | 修改资源配置文件 |
| -template | 创建资源配置文件模板 |
| -print | 打印资源配置文件 |
| -validate | 验证资源配置文件以确定没有拼写错误。 |

表 23-9：CAA 配置文件主要选项

caa_profile 命令有许多、许多选项，但它们在逻辑上按主要、次要和三级选项分类。主要选项如表 23-9 所示。

“-create” 开关有许多附加选项，它们直接对应于第 23.4.4 节中显示的资源属性。我们制作了一张图表来说明这些对应关系（见表 23-10）。

请注意，resource_name 将成为 NAME 资源属性的值，而 “-t” 选项后的字符串将成为 TYPE 资源属性的值。

还需要注意的是，用于指示由 CAA 管理的程序（或应用程序）名称的 “-B” 选项。如果启动应用程序比执行一个程序更复杂，那么编辑生成的脚本（或自行编写）可能更容易，而不使用 “-B” 选项。

# NOTE:

资源在注册之前不会由 CAA 管理或监控。有关更多信息，请参阅第 23.4.11 节。

## 23.4.7 验证资源配置文件

使用 caa_profile 命令或 “sysman caa” 而不是手动编辑配置文件可以帮助您避免资源属性名称中的拼写错误。

要验证资源配置文件，请使用带有 “-validate” 选项的 caa_profile 命令。

```
# caa_profile -validate memberUP
```

