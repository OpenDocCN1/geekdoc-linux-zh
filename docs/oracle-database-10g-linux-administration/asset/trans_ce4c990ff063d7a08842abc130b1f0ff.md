
对于私有网络，互连必须支持用户数据报协议（UDP），使用支持 TCP/IP 的高速网络适配器和交换机（推荐千兆以太网或更好）。

> **NOTE**  
> *UDP* 是 RAC 的默认互连协议，而 TCP 是 Oracle CRS 的互连协议。

## 设置 Linux 内核

配置内核的第一步是确定将使用的内核。请前往 Oracle MetaLink 以识别最新的认证内核版本。
在您识别并安装正确的内核后，您需要将其配置为 Oracle 10g RAC。第一步是验证是否满足 Oracle 10g RAC 的软件要求。

### 检查软件要求

您必须具有以下其中一种操作系统版本：

#### Oracle 10g R1

- Red Hat Enterprise Linux AS/ES 2.1 or 3.0 (x86)
- UnitedLinux 1.0, service pack 3 or higher (x86)

#### Oracle 10g R2

- Red Hat AS/ES 3.0 or 4.0
- SuSE Linux Enterprise Server 9.0

RAC 所需的操作系统软件包与独立 Oracle 安装所需的一样。此信息已在第 5 章中提供。

### Oracle 集群文件系统（OCFS）版本 1.0.9–12 或更高

- ocfs-support
- ocfs-tools
- ocfs-kernel_version

![](img/9479df2d00f5e62b87366b125224950f_223_0.png)

**NOTE**
*只有在您想使用集群文件系统存放数据库文件时才需要 OCFS。如果您想使用自动存储管理或原始设备进行数据库文件存储，则无需安装 OCFS。*

为确保系统满足这些要求，请执行以下步骤：

- 1. 要确定安装了哪个发行版和版本的 Red Hat Linux，请输入以下命令：
  ```
  cat /etc/issue
  ```
  or
  ```
  uname -r
  ```
- 2. 仅在 SLES 8 系统上，使用前一命令的输出来确定是否安装了 Service Pack 3。版本必须至少为 2.4.21-138-default。此命令显示内核版本和类型。如果内核版本小于 2.4.21-138，请联系您的 SLES 供应商以获取有关升级到 Service Pack 3 的信息。
- 3. 要确定是否已安装所需的软件包，请输入类似以下命令：
  ```
  rpm -q package_name
  ```
  如果某个软件包未安装，请从您的 Linux 发行版介质中安装它。
- 4. 要验证 OCFS 是否已安装在您的系统上，请输入以下命令：
  ```
  rpm -qa | grep ocfs
  ```
  如果您想将 Oracle 数据库文件安装在 OCFS 文件系统上且软件包未安装，请从 OCFS 网站 http://oss.oracle.com/projects/ocfs/ 下载它们。

### 检查所需补丁

根据您打算安装的产品，验证是否已安装任何必要的补丁。始终检查最新的 Oracle 文档以获取更新的要求列表。

**NOTE**
Oracle Universal Installer 会检查您的系统以验证其是否满足所列要求。为确保这些检查通过，请在启动安装程序之前验证要求，或以预安装模式运行安装程序，使用 runInstaller `-executeSysPrereqs` 命令并安装任何缺失的操作系统补丁或软件包。

## 设置内核参数和 shell 限制值

Oracle 在 Linux 上开箱即用即可运行良好。然而，在安装 Oracle RAC 之前，我们需要确保某些内核参数达到最低水平。

**NOTE**
以下各节中显示的内核参数和 shell 限制值仅为推荐值。对于生产数据库系统，Oracle 建议您调整这些值以优化系统性能。您必须在所有集群节点上设置内核参数和 shell 限制。

### 更改内核参数

Linux 上 RAC 部署最重要的项目之一是内核参数更改。

使用任何文本编辑器，创建或编辑 `/etc/sysctl.conf` 文件并添加或编辑类似以下的行：

```
kernel.shmall = 2097152
kernel.shmmax = 2147483648
kernel.shmmni = 4096
kernel.sem = 250 32000 100 142
fs.file-max = 131072
net.ipv4.ip_local_port_range = 1024 65000
```

一旦您在 `/etc/sysctl.conf` 文件中指定了值，它们将在系统重新启动时仍然保留。

## Oracle Database 10g Linux 管理

输入以下命令以更改内核参数的当前值：

```
sysctl -p
```

查看此命令的输出以验证值是否正确。如果值不正确，请编辑 /etc/sysctl.conf 文件，然后再次输入此命令。仅在 SLES 上，输入以下命令以使系统在重新启动时读取 /etc/sysctl.conf 文件：

```
/sbin/chkconfig boot.sysctl on
```

在所有其他集群节点上重复此过程。

## 为 Oracle 用户设置 Shell 限制

为了提高软件性能，您必须增加 oracle 用户的 shell 限制。这在第 5 章中已涵盖，对于 RAC 与独立 Oracle 系统没有区别；因此此处不再重复。

## 设置 Linux 系统

Oracle 账户的创建与在独立 Oracle 系统中的创建类似，但必须在 RAC 集群中的所有系统上完全相同地创建账户至关重要。集群中所有节点上的组和用户 ID 必须相同。此外，必须正确设置 ssh 或 rsh。

### 账户创建

根据这是首次在该系统上安装 Oracle 软件以及您正在安装的产品，您可能需要创建多个 Linux 组和一个 Linux 用户。如果您正在安装 Oracle 数据库，则需要以下 Linux 组和用户。

**OSDBA 组（dba）** 您必须在系统上首次安装 Oracle 数据库软件时创建此组。它标识具有数据库管理权限（SYSDBA 权限）的 Linux 用户。此组的默认名称为 dba。如果您想指定除默认 dba 组之外的组名，则必须选择自定义安装类型来安装软件，或以非此组成员的用户身份启动安装程序。在这种情况下，安装程序会提示您指定此组的名称。

**OSOPER 组（oper）** 这是一个可选组。如果您希望一组单独的 Linux 用户具有有限的数据库管理权限（SYSOPER 权限），请创建此组。默认情况下，OSDBA 组的成员也具有 SYSOPER 权限。如果您想指定除默认 dba 组之外的单独 OSOPER 组，则必须选择自定义安装类型来安装软件，或以非 dba 组成员的用户身份启动安装程序。在这种情况下，安装程序会提示您指定此组的名称。此组通常选择的名称为 oper。

以下 Linux 组和用户对所有安装都是必需的。

**Oracle 库存组（oinstall）** 您必须在系统上首次安装 Oracle 软件时创建此组。此组通常选择的名称为 oinstall。此组拥有 Oracle 库存，即系统中安装的所有 Oracle 软件的目录。

> NOTE 如果系统上已安装 Oracle 软件，则现有的 Oracle 库存组必须是您用来安装新 Oracle 软件的 Linux 用户的主要组。以下各节描述如何识别现有的 Oracle 库存组。

**Oracle 软件所有者用户（oracle）** 您必须在系统上首次安装 Oracle 软件时创建此用户。此用户拥有安装期间安装的所有软件。此用户通常选择的名称为 oracle。此用户必须以 Oracle 库存组作为其主要组。它还必须以 OSDBA 和 OSOPER 组作为次要组。

系统上所有 Oracle 软件安装都需要一个单一的 Oracle 库存组。在首次安装 Oracle 软件后，您必须对该系统上的所有后续 Oracle 软件安装使用相同的 Oracle 库存组。但是，您可以选择为单独的安装创建不同的 Oracle 软件所有者用户、OSDBA 组和 OSOPER 组（oracle、dba 和 oper 除外）。通过为不同安装使用不同的组，您可以确保这些不同组的成员仅对相关数据库具有 DBA 权限，而不是对系统上的所有数据库具有权限。

当您首次在系统上安装 Oracle 软件时，安装程序会创建 oracle$$.loc 文件。此文件标识 Oracle 库存组的名称和 Oracle 库存目录的路径。要确定是否存在名为 oracle 的 Oracle 软件所有者用户，请输入以下命令：

```
id oracle
```

如果 oracle 用户存在，则此命令的输出类似于以下内容：

```
uid=440 (oracle) gid=200 (oinstall) groups=201 (dba), 202 (oper)
```
