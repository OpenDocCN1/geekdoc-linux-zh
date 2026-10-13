
```
Transaction Summary
```
Install 60 Packages
=====================
Total download size: 17 M
Installed size: 50 M
Is this ok [y/N]: y
... omitted ...
Installing               : perl-Exporter-5.72-396.el8.noarch  1/60
Installing               : perl-libs-4.5.26-316.el8.x86_64  2/60
Installing               : perl-Carp-1.42-396.el8.noarch  3/60
... omitted ...
Verifying               : dwz-0.12-9.el8.x86_64           2/60
Verifying               : efi-srm-macros-3-2.el8.noarch  2/60
Verifying               : gdb-devel-8.2-5.el8.x86_64  3/60
... omitted ...
Installed:
redhat-rpm-config-115-1.el8.noarch
rpm-build-4.14.2-9.el8.x86_64
rpm-devtools-8.10-7.el8.noarch
... omitted ...
```
完成！

# 7. 探索 yum 的历史和撤销操作

### 7.1. 使用 `yum history` 命令显示最近的 yum 历史

```
[root@servera ~] yum history
ID  | Command line               | Date and time       | Action(s)  | Altered
---|-----------------------------|-------------------|------------|---------
6 | group install RPM Develo | 2019-02-26 17:11 | Install    | 61
5 | install -y guile          | 2019-02-26 17:05 | Install    | 4
4 | -y install @base firewall  | 2019-02-04 11:27 | Install    | 127
3 | -C remove firewall | 2019-01-16 13:12 | Removed | 11 
2 | -C remove linux-firmw | 2019-01-16 13:12 | Removed | 1
1 | | 2019-01-16 13:05 | Install | 447
```

### 7.2. 使用 `yum history undo` 命令确认上一次事务是组安装

```
[root@servera ~] yum history info 6
Transaction ID : 6
Begin time : Tue 26 Feb 2019 05:11:25 PM EST
Begin rpmdb : 563:bf46c4c156982a7e208795400482694072f5ebb
End time : Tue 26 Feb 2019 05:11:33 PM EST (8 seconds)
End rpmdb : 623:bf25b4b2c47ac51d90ae674fib8e497e66636203
User : Student2b4<student>
Return-Code : Success
Releaser : 8
Command Line : group RPM Development Tools
Packages Altered:
Install dwz-01.12-9.el.x86_64 @rhel-8.0-for-x86_64-appstream-rpm
Install efi-sprm-macos-3.2.el18.noarch @rhel-8.0-for-x86_64-appstream-rpm
...output omitted.
```

### 7.3. 使用 `yum history undo` 命令移除安装 guile 包时安装的一整组软件包

```
[root@servera ~] yum history undo 5
```

- 8. 退出服务器系统

```
[root@servera ~] exit
logout
[student@servera ~] exit
Connection to server closed.
[student@workstation ~]
```

# 结束

在工作站上，运行 `lab-yum finish` 完成本次练习。

```
[student@workstation ~]$ lab-yum finish
```

本引导性练习结束。

# 启用 YUM 仓库

## 目标

完成本节后，你将能够启用和禁用对 Red Hat 或第三方仓库的使用。

## 启用 RED HAT 仓库

将服务器注册到订阅管理服务可以获得根据关联订阅访问软件仓库的权限。要查看所有可用仓库：

```
[user@host ~] reposolist all
Loaded plugins: langpacks
rhel-8-server-debug-rpms/x86_64 Red Hat Linux 8 (Debug RPMs) disabled
rhel-8-server-rpms/x86_64 Red Hat Linux 8 enabled
rhel-8-server-source-rpms/x86_64 Red Hat Linux 8 (Source RPMs) disabled
```

`yum-config-manager` 命令用于启用或禁用仓库。要启用仓库，该命令将 `enabled` 参数设置为 `1`。例如，以下命令启用了 `rhel-8-server-debug-rpms` 仓库：

```
[user@host ~]$ yum-config-manager --enable rhel-8-server-debug-rpms
Loaded plugins: langpacks
repo: rhel-8-server-debug-rpms enabled = True
width = 0
base_dir = /var/lib/yum/repos/
```

Red Hat 通过第三方仓库提供其部分软件，可以通过 `yum` 命令从网站、FTP 服务器或本地文件系统访问这些仓库。例如，要启用对第三方仓库的支持，你必须在 `/etc/yum.repos.d/` 目录下创建一个文件。仓库配置文件必须以 `.repo` 扩展结尾。仓库定义包含仓库的 URL、名称、是否使用 GPG 检查软件包签名，以及指向信任 GPG 密钥的 URL。

## 创建 Yum 仓库

使用 `yum-config-manager` 创建 Yum 仓库。以下命令创建了一个名为 `/etc/yum.repos.d/dl.fedoraproject.org.pub_86_64/` 的文件，输出所示：

```
[user@host ~]$ yum-config-manager --add-repo http://dl.fedoraproject.org/pub_86_64/
Loaded plugins: langpacks
adding repo: http://dl.fedoraproject.org/pub_86_64/
repo: dl.fedoraproject.org.pub_86_64
name=Fedora Project 86_64
baseurl=http://dl.fedoraproject.org/pub_86_64/
enabled=1
gpgcheck=1
```

要定义一个仓库但默认不搜索，将 `enabled` 参数设置为 `0`。仓库可以通过 `yum-config-manager` 持久启用或禁用，也可以通过 `yum` 命令选项临时启用或禁用。修改 `/etc/yum.repos.d/epel.repo` 文件以提供自定义值以及 GPG 密钥的位置。管理员应该从外部源下载密钥，例如：

```
[epel]
name=Extra Packages for Enterprise Linux
baseurl=http://dl.fedoraproject.org/pub/el8/
enabled=0
gpgcheck=1
```
