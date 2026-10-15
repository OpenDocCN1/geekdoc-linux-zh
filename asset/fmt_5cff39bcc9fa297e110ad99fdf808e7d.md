
# 移除包和依赖项

在你输入 `y` 后，`yum` 会下载并安装软件包，并继续告知它正在做什么。

```
Resolving Dependencies
--> Populating transaction set with selected
packages. Please wait.
--> Downloading header for xmms to pack into
transaction set.
mms-1.2.10-9.i386.rpm 100% |================| 24 kB 00:00
--> Restarting Dependency Resolution with new
changes.

--> Downloading header for gtk+ to pack into
transaction set.
gtk2B-1.2.10-33.i386.rpm 100% |====================| 23 kB
00:00

Dependencies Resolved

| Package | Arch Version | Repository | Size |
|---|---|---|---|
| Installing: | i386 1:1.2.10-9 | base | 1.9 M |
| Installing for dependencies: | | | |
| libogg | i386 2:1.1.2-1 | base | 16 k |
| libvorbis | i386 1:1.1.0-0 | base | 185 k |

Total download size: 3.3 M
Is this ok [y/N]:
```

```
Downloading Packages:
...
(5/6): libogg-1.1.2-1 100% |=======| 16 kB
00:00
(6/6): libvorbis-1.1.0-1 100% |=======| 185 kB
00:00
Running Transaction Base
Running Transaction
  Installing: libogg         ######## [1/6]
  Installing: libvorbis ######## [2/6]
...
Installed: xmms.i386 1:1.2.10-9
Dependency Installed: gdk-pixbuf.i386
=0.22.0-17 gtk+-i386 2.10-33 libogg.i386
=2:1.1.2-1 libvorbis.i386 1:1.1.0-1
-mikmod.i386 0:3.1.6-32.EL4
Complete!
```

呼！`XMMS` 终于安装并可以使用了。现在如果你决定不喜欢 `XMMS`，看看如何把它移除。

`yum` 的优点之一：它的命令语法非常易用。想安装包？`yum install`。想移除？`yum remove`。所以，如果你厌倦了 `XMMS`，只需运行此命令：

```
# yum remove xmms
Setting up Remove Process
Resolving Dependencies

--> Package xmms.i386 1:1.2.10-9 set to be erased

Dependencies Resolved

Package Arch Version Repository Size
Removing:
 xmms i386 1:1.2.10-9  installed  5.2 M

Is this ok [y/N]:
Running Transaction Base

Running Transaction

Removing : xmms ############################ [1/1]

Removed: xmms.i386 1:1.2.10-9

Complete!
```

现在 `XMMS` 消失了。注意，由 `yum` 安装的依赖项（见上一节“为基于 RPM 的发行版安装软件包和依赖项”）并没有随着 `xmms` 包一起被移除。`XMMS` 运行需要这些依赖项，但它们仍然可以在你的电脑上工作。

# 升级软件包和依赖项

使用不同的程序，因此 `yum` 允许它们保留（这也是 `apt` 的默认行为，你很快就会在“为 Debian 移除软件包和依赖项”中看到）。

## 为基于 RPM 的发行版升级软件包和依赖项

```
yum update
```

你的 Linux 系统包含成百甚至数千个软件包，而且某个软件包的更新层不断。要手动跟踪每个软件每一个新版本并安装更新对你来说将是一项全职工作，而 `yum` 让这个过程变得简单。一个简单的 `yum update` 命令会告诉 `yum` 检查它正在跟踪的软件是否有任何升级。如果有新的软件包，`yum` 会向你显示哪些可用包，并请求你许可继续更新。

```
# yum update

Setting Update Process

Setting up repositories

update 100% |========================= 951 B 00:00

base 100% |========================= 1.1 kB 00:00

Resolving Dependencies

--> Populating transaction set with selected

packages. Please wait.

--> Downloading header for cups-libs to pack into

ttransaction set.

cups-libs-1.1.22-0.rc1.9. 100% |=======| 22 kB
-->00:00
--> Package cups-libs.i386 1:1.1.22-0.rc1.9.10
-->to be updated

--> Running transaction check
Dependencies Resolved

| Package | Arch | Version | Repository | Size |
| :--- | :--- | :--- | :--- | :--- |
| openssl | i386 | 0.9.7a-43.4 | update | 1.1 M |
| pam | i386 | 0.77-66.13 | update | 1.8 M |
| perl | i386 | 3:5.8-24.RHEL4 | update | 11 M |
| udev | i386 | 0.39-10.10.EL43 | update | 830 k |
| wget | i386 | 1.1.20-0.40E | update | 567 k |

Transaction Summary

Install 1 Package(s)
Update 11 Package(s)
Remove 0 Package(s)
Total download size: 30 M
Is this ok [y/N]:
```

如果你在此时按下 `y`，你就是允许 `yum` 下载并安装 12 个软件包。在大量的输出之后，`yum` 完成了它的工作，你的计算机现在已经是最新状态了。想体验最前沿的技术？每天运行 `yum update`。如果你并不追求使用最新、最强大的功能，可以增加运行的时间间隔运行 `yum update`，但要确保定期运行它。软件的安全更新一直在发布，保持更新是一个好主意。

## 为基于 RPM 的发行版查找可下载的软件包

```
yum search [string]
yum list available
```

现在你已经知道如何使用 `yum` 安装和删除软件，但你最初是如何找到软件的呢？假设你对 `GIMP`（即 GNU 图像处理程序）感兴趣。你想知道是否有与 `GIMP` 相关的软件包可以使用 `yum` 进行安装。你可以尝试使用 `yum search gimp`，但并不是一个好主意。该命令会在所有软件包名称、描述、摘要，甚至打包者名称列表中搜索你的匹配项。你最终会得到一个像比尔·盖斯的银行账单一样长的列表。

更好的选择是查询 `yum` 可用的软件包列表（这通常会产生另一个疯狂的长列表），然后将结果通过给 `grep` 搜索你的术语。

```
$ yum list available | grep gimp
gimp.i386             1:2.0.5-5      base
gimp-devel.i386      1:2.0.5-5      base
gimp-help.noarch      2:0.1.0.3      base
gimp-print.i386      4:2.7-2        base
```

出现了十一个结果——这就可以操作的了。如果你真的想执行完整的搜索，请使用 `yum search`；否则，使用 `yum list available` 配合 `grep`。大多数情况下，后者才是你真正想要的，而且处理起来更方便。
