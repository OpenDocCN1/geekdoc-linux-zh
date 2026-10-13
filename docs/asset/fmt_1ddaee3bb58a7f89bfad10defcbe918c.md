
```
[user@server1 ~]$ sudo dnf remove -y cifs-utils
Dependencies resolved.
=================================================
Package         Arch        Version      Repository      Size
=================================================
Removing:
 cifs-utils      x86_64      6.8-2.el8     @BaseOS         189 k
Transaction Summary
=================================================
Remove 1 Package
Free space: 189 k
Running transaction check
Transaction check succeeded.
Running transaction test.
Transaction test succeeded.
Running transaction:
Removing:
Running scriptlet: cifs-utils-6.8-2.el8.x86_64  1/1
Examining:          : cifs-utils-6.8-2.el8.x86_64  1/1
Running scriptlet: cifs-utils-6.8-2.el8.x86_64  1/1
Verifying:         : cifs-utils-6.8-2.el8.x86_64  1/1
Installed products updated.
Removed:
cifs-utils-6.8-2.el8.x86_64
Complete!
```

## 7. 确认删除：

```
[user@server1 ~]$ dnf list installed | grep cifs-utils
[user@server1 ~]$
```

上述无输出确认了包未加载到系统上。

## 确定提供者和搜索包元数据

确定包内容包括对已安装和可用包进行搜索操作。例如，你可以确定特定文件属于哪个包，或者哪个包包含某个字符串。

尝试使用 `--installed` 和 `--available` 选项配合 `group list` 来缩小输出列表。

要列出特定软件包组（如 Base）包含的所有软件包：

```
[user@server ~]$ sudo dnf group info Base
Group: Base
Description: Red Hat Enterprise Linux 的标准安装。
Mandatory Packages:
acl
at
attr
bc
cpcio
crontabs
cyrus-sasl-plain
dndus
ed
file
irptate
irqbalance
kkatch
logrotate
lsofs
```

您可以使用 `group info` 子命令配合 `-v` 选项来获取更多信息。更多详细信息请参考 `dnf` 命令手册页中的 `group list` 和 `group info` 章节。

## 安装和更新软件包组

安装软件包组会为组内包含的所有软件包及其所有依赖包创建必要的目录结构，安装所需的文件，并运行任何安装后步骤。如果软件包组已加载或其部分已存在，该命令将尝试将组内的所有软件包更新到最新可用版本。默认情况下，除非在命令中输入 `-y` 标记，否则 `dnf` 会提示确认（是或否）。

以下示例尝试安装名为 `smart card support` 的软件包组，但如果检测到存在旧版本，将进行更新。您可以使用单引号或双引号括组名。

```
[user1@server1 ~]$ sudo dnf -y groupinstall "smart card support"
Dependencies resolved.
```

| 软件包 | 架构 | 版本 | 仓库 | 容量 |
| :--- | :--- | :--- | :--- | :--- |
| 安装组/模块软件包: | | | | |
| esc | x86_64 | 1.1.2-7.el18 | AppStream | 175 k |
| 安装依赖项: | x86_64 | 0.12.0-4.el18 | BaseOS | 1.2 M |
| psc-lite | x86_64 | 1.8.23-3.el18 | BaseOS | 108 k |
| psc-lite-ccid | x86_64 | 1.4.29-3.el18 | BaseOS | 315 k |
| psc-lite-libs | x86_64 | 1.8.23-3.el18 | BaseOS | 44 k |
| 安装组: | | | | |
| Smart Card Support | | | | |

事务摘要

安装 5 个软件包

总大小: 1.8 M

安装大小: 5.8 M

已更新安装产品。

```
Installed:
esc-1.1.2-7.el18.x86_64             opensc-0.19.0-4.el18.x86_64
pssc-lite-1.8.23-3.el18.x86_64      pssc-lite-ccid-1.4.29-3.el18.x86_64
pssc-lite-libs-1.8.23-3.el18.x86_64
```

完成！

输出显示该命令跨越两个仓库安装了五个软件包，以完成软件包组的安装。

将智能卡支持软件包组更新到最新版本：

```
[user1@server1 ~]$ sudo dnf groupupdate "smart card support" -y
```

如果有访问权限，上述命令将把软件包组内的所有软件包更新到最新版本。更多信息请参考 `dnf` 命令手册页中的 `group install` 和 `group update` 子章节。

## 移除软件包组

移除软件包组会卸载包含的软件包并删除所有关联文件和目录结构。在删除过程中，还会删除任何依赖项。默认情况下，除非在命令行指定了 `-y` 标记，否则 `dnf` 会提示确认（是或否）。

删除已安装的智能卡支持软件包组：

```
user1@server1# sudo dnf -y groupremove 'smart card support'
Dependencies resolved.
==============================================================================
Package                Arch            Version         Repository      Size
==============================================================================
Removing:
esc                   x86_64          1.1.2-7.e18      @AppStream      507 k
Removing unused dependencies:
opensc                 x86_64          0.19.0-4.e18     @BaseOS         3.6 M
pscsc-lite             x86_64          1.8.23-3.e18     @BaseOS         224 k
pscsc-lite-ccid        x86_64          1.4.29-3.e18     @BaseOS         1.4 M
pscsc-lite-libs        x86_64          1.8.23-3.e18     @BaseOS         53 k
Removing Groups:
Smart Card Support
```

事务摘要

================================================================================

移除 5 个软件包

================================================================================

释放空间: 5.8 M

正在执行事务检查

事务检查成功。

已更新安装产品。

```
Removed:
esc-1.1.2-7.e18.x86_64           opensc-0.19.0-4.e18.x86_64
pscsc-lite-1.8.23-3.e18.x86_64   pscsc-lite-ccid-1.4.29-3.e18.x86_64
pscsc-lite-libs-1.8.23-3.e18.x86_64
```

完成！
