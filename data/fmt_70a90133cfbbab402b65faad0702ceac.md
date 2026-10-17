
```bash
[user1@server1 ~]$ sudo dnf -y groupremove 'system tools'
Dependencies resolved.
==============================================================
Package                 Arch            Version         Repository
==============================================================
Removing:
NetworkManager-libreswan  x86_64   1.20-3.el18      AppStream
libreswan                x86_64   3.27-9.el18      AppStream
map                      x86_64   2.70-4.el18      AppStream
tigercnu                  x86_64   1.9-0.el18      AppStream
cifs-utils               x86_64   6.8-2.el18       AppStream
openldap-clients         x86_64   2.46-9.el18      AppStream
samba-client             x86_64   4.9.1.el.18     AppStream
seterial                  x86_64   2.17-4.el18      AppStream
tntx                      x86_64   2.7-1.el18       AppStream
delta                    x86_64   1.10-4.el18      AppStream
Removing unused dependencies:
ldns                     x86_64   1.7.0-20.el18   AppStream
fix                      x86_64   1.2.3-4.el18      AppStream
mesa-libGL                x86_64   9.0-15.el18      AppStream
nss-tools                 x86_64   3.41.0-5.el18   AppStream
tigercnu-icons            noarch           1.9-9.el18      AppStream
Removing Groups:
system Tools
```

标签开始后中断了，且没有结尾的闭合标签）。不过，根据你之前提供的上下文和要求，我已将你给出的部分内容（从 `bash` 命令开始到 `Complete!` 结束）进行了翻译。

**如果你有后续的内容需要翻译，请继续提供完整的英文文本，我将立即为你完成翻译。**

以下是针对你提供的文本片段的译文：

[content]

```bash
[user1@server ~]$ sudo dnf remove -system tools -y
依赖关系解析完成。

正在移除未使用的依赖：

| libdtk | x86_64 | 1.3.4-5.e18 | @AppStream | 1.6 M |
| nmap | x86_64 | 1.7.0-20.e18 | @AppStream | 428 k |
| mesa-libGLU | x86_64 | 9.0.0-15.e18 | | 477 k |
| nss-tools | x86_64 | 3.4.1-0.e18 | @AppStream | 3.6 M |
| tigernvc-icons | noarch | 1.9.0-9.e18 | | 33 k |

正在移除组：
系统工具

事务摘要

移除 15 个软件包

可用空间：39 M

已更新已安装产品。

已移除：
NetworkManager-libreswan-1.2.10-3.e18.x86_64 cifs-utils-6.8-2.e18.x86_64
libreswan-3.2-9.e18.x86_64 nmap-2:70-4.e18.x86_64
openldap-clients-2.4.6-9.e18.x86_64 samba-client-4.9-1.e18.x86_64
seterial-2.17-45.e18.x86_64 tigernvc-1.9.0-9.e18.x86_64
tau-2:7.1-45.e18.x86_64 xdelta-3.1-0.e18.x86_64
flitk-1.3.4-5.e18.x86_64 idn2-1.7.0-20.e18.x86_64
mesa-libGLU-9.0.0-15.e18.x86_64
nss-tools-3.4.1-0.e18.x86_64
tigernvc-icons-1.9.0-9.e18.x86_64

完成！

# 6. 确认移除：

```bash

[user1@server ~]$ dnf group list listed

已安装的环境组：

带 GUI 的服务器

已安装的组：

容器管理

无头界面管理

```

软件包组未在上述输出列表中，这证实了它已被移除。

## 模块管理

模块是 RHEL 8 中引入的新概念，yum/dnf 命令也经过修改以处理模块。可以通过在命令中指定模块子命令来对模块执行许多操作。以下小节将通过示例详细说明如何使用此工具列出、启用、安装、查询、移除和禁用模块。

### 列出可用和已安装的模块

`dnf` 命令可以列出从一个或两个仓库可供安装的模块，以及系统中已经安装的模块。

要列出来自所有已配置仓库的可用模块及其流（stream）、配置文件（profile）和摘要信息：

```bash
[user1@~$] dnf module list
最后元数据过期检查：2019年9月22日周二 晚上11:17:09 EDT， 01:14:50。

AppStream               Summary

Name            Stream      Profiles

389-ds          1.4         common [d]   389 目录服务器 (base)

ant             1.1 [d]      common [d]   Java 构建工具

container-tools  1.0         common [d]   容器运行时常用的工具和依赖项

container-tools  rhel8 [d]common [d]   容器运行时常用的工具和依赖项

freeradius      3.0 [d]      server [d]  高性能且高度可配置的 RADIUS 服务器

提示：[d]默认,[e]启用,[x]禁用,[i]已安装
```

你可以通过在上述命令后添加 `--repo AppStream` 将输出限制为来自特定仓库（如 AppStream）的可用模块列表。Stream 和 Profiles 列下以及输出最后最后一行的字母 d、e、x 和 i 表示它们的状态，分别为：默认 (d)、启用 (e)、禁用 (x) 或已安装 (i)。

要列出特定模块（如 perl）的所有流并显示其状态：

```bash
[user1@server1 ~]$ dnf module list perl
AppStream
Name      Stream            Summary
perl      5.24      common [d], minimal    实用提取与报告语言
perl      5.26      [d][e]     common [d], minimal    实用提取与报告语言
提示：[d]默认, [e]启用, [x]禁用, [i]已安装
```

上述输出显示，AppStream 仓库为 perl 模块提供了两个流（5.24 和 5.26），且当前默认和启用的版本是后者。

要修改上述内容并仅列出 perl 模块指定的流（5.24）：

```bash
[user1@server1 ~]$ dnf module list perl:5.24
AppStream
Name      Stream            Summary
perl      5.24      common [d], minimal    实用提取与报告语言
提示：[d]默认, [e]启用, [x]禁用, [i]已安装
```

列出所有启用的模块：

```bash
[user1@server1 ~]$ dnf module list --enabled
AppStream
Name                 Stream            Summary
```
