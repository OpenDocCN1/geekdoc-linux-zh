

954

nisdefaults

```
castle@ nischttl -L 12h linkname
cast@ nischttl 3600 '[],hobbies'
```

## 环境变量

NIS_PATH 如果此变量已设置且 NIS+ 名称不是完全限定的，则搜索每个指定的目录直到找到对象为止（参见 nisdefaults(1)）。

## 退出状态

- 0 成功。
- 1 失败。

## 属性

参见 attributes(5) 以获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可性 | SUNwnisu |

## 参见

nis+(1), nischgrp(1), nischmod(1), nischown(1), nisdefaults(1), nis_objects(3NSL), attributes(5)

## nisdefaults — 显示 NIS+ 默认值

### 概要

```
/usr/bin/nisdefaults [-adghprst]
```

### 描述

使用 nisdefaults 命令打印调用 NIS+ 本地名函数返回的默认值（参见 nis_local_names(3NSL)）。当您指定选项时，所有默认值将以详细格式打印。带有选项时，仅以适用于 shell 脚本的简明格式显示该选项的信息。

### 选项

- -a 以简明格式打印所有默认值。
- -d 打印默认域名。
- -g 打印默认组名。
- -h 打印默认主机名。
- -p 打印默认主体名（principal name）。
- -r 打印创建新对象时的默认访问权限。
- -s 打印默认目录搜索路径。
- -t 打印默认生存时间（time-to-live）值。
- -v 以详细格式打印默认值。此选项会在输出前加上标识字符串。

## 示例

以下示例打印了 foo.bar.domain 机器 castle 上根进程的 NIS+ 默认值。

```
castle% nisdefaults
Principal Name : castle.foo.bar
Domain Name : foo.bar
Host Name : castle.foo.bar
Group Name : 
Access Rights : ----rmcddr---r----
Time to live : 12:00:00
Search Path : foo.bar.
```

以下示例在 shell 脚本中将变量设置为默认域名。
`DOMAIN=nisdefaults -d`

以下示例以详细格式打印默认的生存时间。
```
castle% nisdefaults -tv
Time to live : 12:00:00
```

以下示例以简明格式打印生存时间。

```
castle% nisdefaults -t
43200
```

## 环境变量

多个环境变量影响与进程关联的默认值。

```
NIS_DEFAULTS
```

> 指定一个默认字符串来覆盖 NIS+ 标准默认值。该默认字符串是一系列由冒号分隔的令牌（tokens）。这些令牌表示用于通用对象属性的默认值。所有合法的令牌描述见下文。

- ttl=time 为创建的对象设置默认的生存时间。按照 nischttl(1) 命令定义的格式指定时间值。默认值为 12 小时。
- owner=ownername 指定 NIS+ 主体 ownername 应该拥有被创建的对象。该值的默认值是执行命令的主体。
- group=groupname 指定组 groupname 应该是被创建对象的所有者。默认值为空。
- access=rights 指定授予被创建对象的访问权限集。按照 nischmod(1) 命令定义的格式指定权限值。默认值为 --rmcmdr--

```
NIS_GROUP
```

本地 NIS+ 组的名称。如果名称不是完全限定的，则在其后追加默认域名。

覆盖默认的 NIS+ 目录搜索路径。指定一个由冒号分隔的有序目录列表。美元符号 ($) 被视为特殊字符。在目录名后追加默认域名。将 s 替换为位于默认域名和全局根目录之间且至少两个层深的目录列表。默认的 NIS+ 目录搜索路径为。

```
NIS_PATH
```

更多详情请参阅 nis+(1) 中的“名称扩展”小节。

## 属性

参见 attributes(5)以获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可性 | SUN+minisu |

## 参见

nis+(1), nis_local_names(3NSL), attributes (5)

## niserror — 显示 NIS+ 错误消息

### 概要

```
/usr/bin/niserror error-num
```

### 描述

使用 niserror 命令在标准输出上打印状态值 error-num 相关的 NIS+ 错误。此命令用于 shell 脚本，将返回的 NIS+ 错误代码转换为文本消息。

## 示例

以下示例打印与错误代码 20 相关的错误。

```
castle% niserror 20
Not Found, no such name
castle%
```

以下示例打印与错误代码 21 相关的错误。

```
castle% niserror 21
Name/entry isn't unique
castle%
```

## 属性

参见 attributes(5)以获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可性 | SUN|

## 参见

nis+(1), nis_error(3NSL), attributes(5)

## nisgrep — 搜索 NIS+ 表

### 概要

```
/usr/bin/nisgrep [-AchMov] [-s sep] keypat tablename
/usr/bin/nisgrep [-AchMov] [-s sep] colname=keypat... tablename
```

### 描述

参见 nismatch(1)。

## nisgrpadm — NIS+ 组管理命令

### 概要

```
/usr/bin/nisgrpadm -a [-r |-t [-s] group principal
/usr/bin/nisgrpadm -d -1 [-M] [-s] group
/usr/bin/nisgrpadm -c [-D defaults] [-M] [-s] group
```

### 描述

使用 nisgrpadm 命令管理 NIS+ 组及其成员列表。nisgrpadm 可以创建、销毁或列出 NIS+ 组，并用于管理组成员列表。它可以从组中添加或删除主体，或测试主体是否为该组成员。

NIS+ 组的名称在语法上与 NIS+ 对象的名称相似，但它们占据独立的命名空间。名为 a.b.c.d. 的组被表示为名为 a.groups. 的 NIS+ 组对象；这里描述的函数都期望组名。

组成员有三种：

- 显式成员（explicit）就是一个 NIS+ 主体名，例如 wickedwitch.west。
- 隐式成员（implicit），写为 *.oz.，意味着给定域名内的所有主体都属于该成员。不允许其他形式的通配符：wickedwitch.* 是无效的。
- 递归成员（recursive），写为 @group.oz.，指向另一个组；属于该组的所有主体都被认为属于此地。

您可以通过在名称前加减号 (-)将任何名称变为负的。组包含显式、隐式、递归、负显式、负隐式和负递归成员。

如果一个主体属于组的至少一个非负成员且不属于任何负成员，则被认为属于该组。

> 注意主体名称必须是完全限定的，而组在所有操作之外都可以省略。

### 选项

- -a 将指定的 NIS+ 主体添加到组。主体名应该是完全限定的。
- -c 在 NIS+ 命名空间中创建组。NIS+ 组名应该是完全限定的。
- -d 从命名空间中删除组。
- -D 在创建对象时指定一组不同的默认值。默认字符串是一系列分隔的令牌，表示用于通用对象属性的默认值。所有合法的令牌描述见下文。

- ttl=time 为此命令创建的对象设置默认的生存时间。按照 nischttl(1) 命令定义的格式指定时间值。默认值为 12 小时。
- owner=ownername 指定 NIS+ 主体 ownername 拥有被创建的对象。通常，该值与执行命令的主体相同。
- group=groupname 指定组 groupname 应该是被创建对象的所有者。默认值为空。
- access=rights 指定授予给定对象的访问权限集。按照 nischmod(1) 命令定义的格式指定权限值。默认值为 ----rmcdmr---r---
- -1 列出指定组的成员列表。（参见 -M）。

