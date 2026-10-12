
```
 Package                Arch          Version               Repository        Size
================================================================================
更新：
 selinux-policy-targeted    noarch          3.6.32-46.fc12            updates           1.9 M
 xorg-x11-drv-evdev         1.0.0-2.fc12            updates           29 k
 xorg-x11-drv-keyboard       1.4.0-2.fc12            updates           17 k
 xorg-x11-drv-synaptics      1.1.99-7.20090907.fc12  updates           60 k

 事务摘要
================================================================================
 安装       0 个软件包
 升级       4 个软件包

总下载大小：2.0 M
是否继续 [y/N]：y
正在下载软件包：
设置并读取 Presto 增量元数据
正在处理增量元数据
增量下载大小：1.5 M
(1/4): selinux-policy-targeted-3.6.32-41.fc12.3.6.32-46..  | 1.5 MB   00:02
(2/4): xorg-x11-drv-evdev-2.3.0-1.fc12.2.3.0-4.fc12.i686    11 kB   00:00
(3/4): xorg-x11-drv-keyboard-1.3.99-1.1.fc12.1.4.0-2.fc1  10 kB   00:00
(4/4): xorg-x11-drv-synaptics-1.1.99-7.20090907.fc12.1.2  37 kB   00:00
完成来自 deltarpm 的 rpm 重建
<增量重建>                                          | 2.0 MB   00:04
Presto 将更新大小减少了 24%（从 2.0 M 减少到 1.5 M）。
运行 rpm_check_db
运行事务测试
事务测试完成
事务测试成功
运行事务
  正在更新   : xorg-x11-drv-evdev-2.3.0-4.fc12.i686                     1/4
  正在更新   : xorg-x11-drv-synaptics-1.2.0-2.fc12.i686                2/4
  正在更新   : selinux-policy-targeted-3.6.32-46.fc12.noarch           3/4
  正在更新   : xorg-x11-drv-keyboard-1.4.0-2.fc12.i686                 4/4
  正在清理    : xorg-x11-drv-evdev-2.3.0-1.fc12.i686                    5/8
  正在清理    : xorg-x11-drv-synaptics-1.1.99-7.20090907.fc12.i686      6/8
  正在清理    : selinux-policy-targeted-3.6.32-41.fc12.noarch           7/8
  正在清理    : xorg-x11-drv-keyboard-1.3.99-1.1.fc12.i686              8/8

已更新：
  selinux-policy-targeted.noarch 0:3.6.32-46.fc12
  xorg-x11-drv-evdev.i686 0:2.3.0-4.fc12
  xorg-x11-drv-keyboard.i686 0:1.4.0-2.fc12
  xorg-x11-drv-synaptics.i686 0:1.2.0-2.fc12

完成！
```

![](img/f28adb66a7398a382f0505e0ba74a872_541_0.png)

### 可选

某些软件包仅应安装，不应升级。参数 `installonlypkgs` 用于标识这些软件包。与内核相关的软件包默认属于 `installonlypkgs`。参数 `tokeep` 指定 `yum` 保留的 `installonlypkgs` 软件包版本数量。

通过指定软件包名称并在命令 `update` 后跟上这些名称，您可以更新单个软件包。

### 安装软件包

若要连同其依赖的软件包一起安装新软件包，请输入命令 `yum install`，后跟软件包名称。在 `yum` 确定需要执行的操作后，它会请求确认。下一个示例安装 `tcsh` 软件包：

```
# yum install tcsh
Loaded plugins: presto, refresh-packagekit
Setting up Install Process
Resolving Dependencies
---> Running transaction check
---> Package tcsh.i686 0:6.17-3.fc12 set to be updated
---> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package        Arch    Version          Repository        Size
================================================================================
Installing:
 tcsh           i686    6.17-3.fc12      fedora            375 k

Transaction Summary
================================================================================
Install 1 Package(s)
Upgrade 0 Package(s)

Total download size: 375 k
Is this ok [y/N]: y
Downloading Packages:
Setting up and reading Presto delta metadata
fedora/prestdelta | 1.3 kB 00:00
Processing delta metadata
Package(s) data still to download: 375 k
tcsh-6.17-3.fc12.i686.rpm | 375 kB 00:00
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
Installing : tcsh-6.17-3.fc12.i686 1/1

Installed:
  tcsh.i686 0:6.17-3.fc12

Complete!
```

您也可以使用 `yum` 移除软件包，语法类似。以下示例移除 `tcsh` 软件包：
