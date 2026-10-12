

已加载插件：langpacks, product-id, subscription-manager
rhel-7-workstation-rpms/x86_64 | 3.4 kB 00:00:00
无需为安全更新软件包；0 个可用软件包

请注意，上述命令以非交互模式运行，因此可用于脚本中以自动检查是否有可用更新。当有安全更新可用时，该命令返回退出值 100；当没有安全更新时，返回 0。遇到错误时，返回 1。

类似地，使用以下命令仅安装与安全相关的更新：

```
[~]# yum update --security
```

使用 **updateinfo** 子命令来显示或处理由仓库提供的有关可用更新的信息。**updateinfo** 子命令本身接受若干命令，其中一些与安全相关用途有关。有关这些命令的概览，请参阅表 3.1“可用于 yum updateinfo 的安全相关命令”。

## 表 3.1. 可用于 yum updateinfo 的安全相关命令

| 命令 | 描述 |
| :--- | :--- |
| `advisory [advisories]` | 显示关于一个或多个公告的信息。用公告编号替换 *advisories*。 |
| `cves` | 显示关于 CVE（*Common Vulnerabilities and Exposures*，通用漏洞披露）信息的子集。 |
| `security` 或 `sec` | 显示所有安全相关信息。 |
| `severity [severity_level ]` 或 `sev [severity_level]` | 显示关于所提供 *severity_level* 的安全相关软件包的信息。 |

## 3.1.2. 更新和安装软件包

在系统中更新软件时，从可信来源下载更新非常重要。攻击者可以轻易地重建一个具有与旨在修复问题的版本相同版本号但包含不同安全漏洞利用的软件包，并将其发布到互联网上。如果发生这种情况，使用验证文件与原始 RPM 是否匹配等安全措施将无法检测到漏洞。因此，仅从可信来源（如 Red Hat）下载 RPM 并检查软件包签名以验证其完整性，这一点至关重要。

有关如何使用 **Yum** 包管理器的详细信息，请参阅《Red Hat Enterprise Linux 7 系统管理员指南》中的 **Yum** 章节。

### 3.1.2.1. 验证签名软件包

所有 Red Hat Enterprise Linux 软件包均使用 Red Hat GPG 密钥进行签名。GPG 代表 **GNU Privacy Guard**，或 **GnuPG**，它是一个用于确保分发文件真实性的免费软件包。如果软件包签名验证失败，该软件包可能已被篡改，因此不可信。

**Yum 包管理器**允许自动验证其安装或升级的所有软件包。此功能默认启用。要在系统中配置此选项，请确保 `/etc/yum.conf` 配置文件中的 `gpgcheck` 配置指令设置为 **1**。

使用以下命令在文件系统上手动验证软件包文件：

```
rpmkeys --checksig package_file.rpm
```

有关 Red Hat 软件包签名实践的更多信息，请参阅 Red Hat Customer Portal 上的产品签名（GPG 密钥）文章。

### 3.1.2.2. 安装签名软件包

要从文件系统安装已验证的软件包（有关如何验证软件包的信息，请参阅第 3.1.2.1 节“验证签名软件包”），请以 **root** 用户身份使用 `yum install` 命令，如下所示：

```
yum install package_file.rpm
```

使用 shell 通配符可同时安装多个软件包。例如，以下命令安装当前目录中的所有 `.rpm` 软件包：

```
yum install *.rpm
```

> **重要**
> 
> 在安装任何安全勘误之前，务必阅读勘误报告中包含的特殊说明并相应执行。有关应用由勘误更新所做的更改的通用说明，请参阅第 3.1.3 节“应用由已安装更新引入的更改”。

## 3.1.3. 应用由已安装更新引入的更改

下载并安装安全勘误和更新后，停止使用旧软件并开始使用新软件非常重要。具体做法取决于已更新的软件类型。以下列表列出了软件的一般类别，并提供了在软件包升级后使用更新版本的说明。

> **注意**
> 
> 通常，重新启动系统是确保使用软件包最新版本的可靠方法；然而，并非总是需要此选项，系统管理员也并非总是可以执行此操作。

### 应用程序

用户空间应用程序是指任何可由用户启动的程序。通常，此类应用程序仅在用户、脚本或自动化任务实用程序启动它们时使用。

一旦此类用户空间应用程序已更新，请停止系统中该应用程序的所有实例，并再次启动该程序以使用更新后的版本。

### 内核

内核是 Red Hat Enterprise Linux 7 操作系统的核心软件组件。它管理对内存、处理器和外围设备的访问，并调度所有任务。

由于其核心角色，不重启计算机就无法重启内核。因此，在系统重启之前，无法使用更新的内核版本。

#### KVM

当更新 qemu-kvm 和 libvirt 软件包时，必须停止所有客户虚拟机，重新加载相关的虚拟化模块（或重启宿主系统），然后重新启动虚拟机。

使用 `lsmod` 命令确定以下模块中哪些已加载：`kvm`、`kvm-intel` 或 `kvm-amd`。然后使用 `modprobe -r` 命令移除受影响的模块，随后使用 `modprobe -a` 命令重新加载它们。例如：

```
~]# lsmod | grep kvm
kvm_intel                143031  0
kvm                      460181  1 kvm_intel
~]# modprobe -r kvm-intel
~]# modprobe -r kvm
~]# modprobe -a kvm kvm-intel
```

#### 共享库

共享库是如 glibc 这样的代码单元，被许多应用程序和服务使用。利用共享库的应用程序通常在初始化时加载共享代码，因此，使用更新库的任何应用程序都必须停止并重新启动。

要确定哪些正在运行的应用程序链接到特定库，请使用 `lsof` 命令：

```
lsof library
```

例如，要确定哪些正在运行的应用程序链接到 `libwrap.so.0` 库，请输入：

```
~]# lsof /lib64/libwrap.so.0
COMMAND     PID USER   FD   TYPE DEVICE SIZE/OFF   NODE NAME
pulseaudi 12363 test mem  REG  253,0    42520 34121785
/usr/lib64/libwrap.so.0.7.6
gnome-set 12365 test mem  REG  253,0    42520 34121785
/usr/lib64/libwrap.so.0.7.6
gnome-she 12454 test mem  REG  253,0    42520 34121785
/usr/lib64/libwrap.so.0.7.6
```

此命令返回使用 TCP wrappers 进行主机访问控制的所有正在运行的程序的列表。因此，当更新 tcp_wrappers 软件包时，必须停止并重新启动列表中列出的任何程序。

#### systemd 服务

systemd 服务是通常在引导过程中启动的持久服务器程序。systemd 服务的示例包括 sshd 或 vsftpd。

由于这些程序通常在机器运行期间一直驻留在内存中，因此在升级其软件包后，必须停止并重新启动每个已更新的 systemd 服务。可以作为 root 用户通过 systemctl 命令完成此操作：

```
systemctl restart service_name
```

用想要重启的服务名称替换 *service_name*，例如 sshd。

### 其他软件

请遵循以下链接资源中列出的说明，以正确更新以下应用程序。

- Red Hat Directory Server – 请参阅相应版本 Red Hat Directory Server 的发行说明，地址为 https://access.redhat.com/site/documentation/en-US/Red_Hat_Directory_Server/。
- Red Hat Enterprise Virtualization Manager – 请参阅相应版本 Red Hat Enterprise Virtualization 的安装指南，地址为 https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Virtualization/。

## 3.2. 使用 Red Hat 客户门户

位于 https://access.redhat.com/ 的 Red Hat Customer Portal 是与 Red Hat 产品相关的官方信息的主要面向客户的资源。您可以使用它查找文档、管理订阅、下载产品和更新、打开支持案例以及了解安全更新。

### 3.2.1. 在客户门户上查看安全公告

要查看与您拥有活动订阅的系统相关的安全公告（勘误），请登录位于 https://access.redhat.com/ 的客户门户，并点击主页面上的“下载产品与更新”按钮。进入“软件与下载中心”页面后，继续点击“勘误”按钮，以查看适用于您注册系统的公告列表。

要浏览所有活动 Red Hat 产品的所有安全更新列表，请使用页面顶部的导航菜单，前往“安全” → “安全更新” → “活动产品”。

点击表格左侧的勘误代码以显示有关单个公告的更详细信息。下一页不仅包含特定勘误的描述，包括其原因、后果和所需修复，还包含该特定勘误更新的所有软件包列表以及应用更新的说明。该页面还包含对相关参考（如相关 CVE）的链接。

### 3.2.2. 导航 CVE 客户门户页面

CVE（Common Vulnerabilities and Exposures，通用漏洞披露）项目由 The MITRE Corporation 维护，它是漏洞和安全暴露的标准化名称列表。要浏览客户门户上与 Red Hat 产品相关的 CVE 列表，请登录位于 https://access.redhat.com/ 的您的帐户，并使用页面顶部的导航菜单导航到“安全” → “资源” → “CVE 数据库”。

点击表格左侧的 CVE 代码以显示有关单个漏洞的更详细信息。下一页不仅包含特定 CVE 的描述，还包含受影响的 Red Hat 产品列表以及指向相关 Red Hat 勘误的链接。

### 3.2.3. 理解问题严重性分类

