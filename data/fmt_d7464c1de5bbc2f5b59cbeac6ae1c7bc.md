
```
# yum install p7zip
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
* base: mirror.ufscar.br
* epel: mirror.glob0.com
* extras: mirror.ufscar.br
* updates: mirror.ufscar.br
Resolving Dependencies
---> Running transaction check
---> Package p7zip.x86_64 0:16.02-10.el7 will be installed
---> Finished Dependency Resolution

Dependencies Resolved

=============================================================
 Package          Arch           Version            Repository   Size
=============================================================
Installing:
p7zip             x86_64         16.02-10.el7       epel          604 k

Transaction Summary
=============================================================
Install  1 Package

Total download size: 604 k
Installed size: 1.7 M
Is this ok [y/d/N]:
```

若要升级已安装的软件包，请使用 `yum update` `PACKAGENAME`，其中 `PACKAGENAME` 是你想要升级的软件包名称。例如：

```
# yum update wget
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
* base: mirror.ufscar.br
* epel: mirror.glob0.com
* extras: mirror.ufscar.br
* updates: mirror.ufscar.br
Resolving Dependencies
---> Running transaction check
---> Package wget.x86_64 0:1.14-18.el7 will be updated
---> Package wget.x86_64 0:1.14-18.el7_6.1 will be an update
---> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package          Arch          Version            Repository        Size
================================================================================
Updating:
 wget             x86_64       1.14-18.el7_6.1    updates            547 k

Transaction Summary
================================================================================
Upgrade  1 Package

Total download size: 547 k
Is this ok [y/d/N]:
```

如果你省略了软件包名称，你可以更新系统中所有有可用更新的软件包。

若要检查特定软件包是否有可用更新，请使用 `yum` `check-update` `PACKAGENAME`。与之前一样，如果你省略软件包名称，`yum` 将检查系统中所有已安装软件包的更新。

若要删除已安装的软件包，请使用 `yum` `remove` `PACKAGENAME`，其中 `PACKAGENAME` 是你希望删除的软件包名称。

### 查找提供特定文件的软件包

在一个先前的示例中，我们展示了尝试安装 `gimp` 图像编辑器的过程，但由于依赖关系未满足而失败。然而，`rpm` 只显示缺少哪些文件，并未列出提供这些文件的软件包名称。

例如，其中一个缺失的依赖项是 `libgimpui-2.0.so.0`。要查看是哪个软件包提供了它，可以使用 `yum` `whatprovides`，后接你要搜索的文件名称：

```
# yum whatprovides libgimpui-2.0.so.0
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
* base: mirror.ufscar.br
* epel: mirror.globo.com
* extras: mirror.ufscar.br
* updates: mirror.ufscar.br
2:gimp-libs-2.8.22-1.el7.i686 : GIMP libraries
Repo : base
Matched from:
Provides : libgimpui-2.0.so.0
```

答案是 `gimp-libs-2.8.22-1.el7.i686`。然后你可以使用命令 `yum install gimp-libs` 安装该软件包。

这也适用于系统中已存在的文件。例如，如果你想知道文件 `/etc/hosts` 来自哪里，你可以使用：

```
# yum whatprovides /etc/hosts
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
* base: mirror.ufscar.br
* epel: mirror.globo.com
* extras: mirror.ufscar.br
* updates: mirror.ufscar.br
setup-2.8.71-10.el7.noarch : A set of system configuration and setup files
Repo : base
Matched from:
Filename : /etc/hosts
```

答案是 `setup-2.8.71-10.el7.noarch`。

## 获取软件包信息

若要获取软件包的信息，如版本、架构、描述、大小等，请使用 `yum info` `PACKAGENAME`，其中 `PACKAGENAME` 是你想要获取信息的软件包名称：

```
# yum info firefox
Last metadata expiration check: 0:24:16 ago on Sat 21 Sep 2019 02:39:43 PM -03.
Installed Packages
Name : firefox
Version : 69.0.1
Release : 3.fc30
Architecture : x86_64
Size : 268 M
Source : firefox-69.0.1-3.fc30.src.rpm
Repository : @System

From repo: updates
Summary: Mozilla Firefox Web browser
URL: https://www.mozilla.org/firefox/
License: MPLv1.1 or GPLv2+ or LGPLv2+
Description: Mozilla Firefox is an open-source web browser, designed for standards compliance, performance and portability.
```

## 管理软件仓库

对于 `yum` 而言，“repos” 仓库列在目录 `/etc/yum.repos.d/` 中。每个仓库由一个 `.repo` 文件表示，例如 `CentOS-Base.repo`。

此外，用户可以在上述目录中添加 `.repo` 文件，或在 `/etc/yum.conf` 的末尾添加，以添加额外的外部仓库。然而，添加或管理仓库的推荐方式是使用 `yum-config-manager` 工具。

若要添加仓库，请使用 `--add-repo` 参数，后接 `.repo` 文件的 URL。
