

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_216_0.png)

图 7.4. 自定义选定的安全配置

自定义窗口包含与选定安全配置相关的一套完整 XCCDF 元素，以及关于每个元素及其功能的详细信息。您可以通过在该窗口主区域中选中或取消选中相应的复选框来启用或禁用这些元素。自定义窗口还支持撤销和重做功能；您可以点击窗口左上角相应的箭头图标来撤销或重做您的选择。

您还可以更改稍后用于评估的变量。在自定义窗口中找到合适的项，导航至右侧部分，并使用“修改值”字段。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_216_1.png)

图 7.5. 在自定义窗口中设置选定项的值

完成配置自定义后，点击“确认自定义”按钮以确认更改。您的更改现保存在内存中，如果关闭 SCAP Workbench 或进行某些更改（例如选择新的 SCAP 内容或选择其他自定义选项），这些更改将不会持久保存。要保存您的更改，请点击 SCAP Workbench 窗口中的“保存自定义”按钮。此操作允许您将更改作为 XCCDF 自定义文件保存到选定目录中。请注意，此自定义文件可以与其他配置进一步关联使用。

### 7.3.5. 保存 SCAP 内容

SCAP Workbench 还允许您保存用于系统评估的 SCAP 内容。您可以单独保存自定义文件（参见第 7.3.4 节，“自定义安全配置”），或者通过点击“保存内容”组合框并选择“保存到目录”或“保存为 RPM”选项，一次性保存所有安全内容。

通过选择“保存到目录”选项，SCAP Workbench 将 XCCDF 或数据流文件以及自定义文件都保存到指定位置。这可作为备份解决方案使用。

通过选择“保存为 RPM”选项，您可以指示 SCAP Workbench 创建一个包含 XCCDF 或数据流文件和自定义文件的 RPM 包。这对于将安全内容分发给无法进行远程扫描的系统，或仅为传递内容以供进一步处理，都非常有用。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_217_0.png)

图 7.6. 将当前 SCAP 内容保存为 RPM 包

### 7.3.6. 查看扫描结果并生成扫描报告和修复方案

系统扫描完成后，会出现三个新按钮：“清除”、“保存结果”、“生成修复角色”和“显示报告”，取代原来的“扫描”按钮。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_218_0.png)

**警告**

点击**清除**按钮将永久删除扫描结果。

要以 XCCDF、ARF 或 HTML 文件形式存储扫描结果，请点击**保存结果**组合框。选择**HTML 报告**选项以生成人类可读形式的扫描报告。XCCDF 和 ARF（数据流）格式适合进一步的自动化处理。您可以重复选择这三种选项中的任意一种或多种。

如果您希望立即查看扫描结果而不保存，请点击**显示报告**按钮，该按钮会在您的默认网络浏览器中以临时 HTML 文件的形式打开扫描结果。

您可以使用**生成修复角色**弹出菜单将基于结果的修复方案导出到文件。此功能与基于配置的修复角色导出非常相似——区别在于通过系统评估的规则修复方案不会被导出，因此文件可能会更小。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_218_1.png)

**警告**

基于结果的修复方案不支持定制化配置。如果需要导出这些配置，您可以使用**oscap** 命令行工具。

## 7.4. 使用 OSCAP

**oscap** 命令行工具允许用户扫描本地系统、验证安全合规性内容，并基于这些扫描和评估生成报告和指南。此工具作为 OpenSCAP 库的前端，根据其处理的 SCAP 内容类型将其功能分组到模块（子命令）中。

以下部分解释如何安装 **oscap** 并执行最常见的操作。提供示例来说明这些任务。要了解特定子命令的更多信息，请在 **oscap** 命令中使用 **--help** 选项：

```
oscap [options] module module_operation [module_operation_options_and_arguments] --help
```

其中 *module* 表示正在处理的 SCAP 内容类型，*module_operation* 是对 SCAP 内容进行特定操作的子命令。

### 示例 7.4. 获取特定 oscap 操作的帮助

```
~]$ oscap ds sds-split --help
oscap -> ds -> sds-split
```

```
Split given SourceDataStream into separate files

Usage: oscap [options] ds sds-split [options] SDS TARGET_DIRECTORY

SDS - Source data stream that will be split into multiple files.
TARGET_DIRECTORY - Directory of the resulting files.

Options:
--datastream-id <id> - ID of the datastream in the collection to use.
--xccdf-id <id> - ID of XCCDF in the datastream that should be evaluated.
```

要了解所有 oscap 功能及其选项的完整列表，请参阅 oscap(8) 手册页。

### 7.4.1. 安装 oscap

要在您的系统上安装 oscap，请以 root 身份输入以下命令：

```
[~]# yum install openscap-scanner
```

此命令允许您安装 oscap 正常运行所需的所有软件包，包括 openscap 软件包。为了能够编写自己的安全内容，您还应该安装 openscap-engine-sce 软件包，该软件包提供脚本检查引擎（SCE）。SCE 是 SCAP 协议的扩展，允许内容作者使用脚本语言（如 Bash、Python 或 Ruby）编写其安全内容。请注意，openscap-engine-sce 软件包仅在可选频道中可用。参见“启用补充和可选存储库”。

可选地，在安装 oscap 后，您可以检查您的 oscap 版本的能力、它支持哪些规范、特定的 oscap 文件存储在哪里、您可以使用哪些类型的 SCAP 对象以及其他有用信息。要显示此信息，请键入以下命令：

```
[~]$ oscap -V
OpenSCAP command line tool (oscap) 1.0.4
Copyright 2009-2014 Red Hat Inc., Durham, North Carolina.

==== Supported specifications ====
XCCDF Version: 1.2
OVAL Version: 5.10.1
CPE Version: 2.3
CVSS Version: 2.0
CVE Version: 2.0
Asset Identification Version: 1.1
Asset Reporting Format Version: 1.1

==== Capabilities added by auto-loaded plugins ====
SCE Version: 1.0 (from libopenscap_sce.so.8)

==== Paths ====
Schema files: /usr/share/openscap/schemas
Schematron files: /usr/share/openscap/xsl
Default CPE files: /usr/share/openscap/cpe
Probes: /usr/libexec/openscap

===== Inbuilt CPE names =====
Red Hat Enterprise Linux - cpe:/o:redhat:enterprise_linux
Red Hat Enterprise Linux 5 - cpe:/o:redhat:enterprise_linux:5
Red Hat Enterprise Linux 6 - cpe:/o:redhat:enterprise_linux:6
Red Hat Enterprise Linux 7 - cpe:/o:redhat:enterprise_linux:7
Fedora 16 - cpe:/o:fedoraproject:fedora:16
Fedora 17 - cpe:/o:fedoraproject:fedora:17
Fedora 18 - cpe:/o:fedoraproject:fedora:18
Fedora 19 - cpe:/o:fedoraproject:fedora:19
Fedora 20 - cpe:/o:fedoraproject:fedora:20
Fedora 21 - cpe:/o:fedoraproject:fedora:21
Red Hat Enterprise Linux Optional Productivity Applications -
cpe:/a:redhat:rhel_productivity
Red Hat Enterprise Linux Optional Productivity Applications 5 -
cpe:/a:redhat:rhel_productivity:5

===== Supported OVAL objects and associated OpenSCAP probes =====
system_info              probe_system_info
family                   probe_family
filehash                 probe_filehash
environmentvariable      probe_environmentvariable
textfilecontent54        probe_textfilecontent54
textfilecontent          probe_textfilecontent
variable                 probe_variable
xmlfilecontent           probe_xmlfilecontent
environmentvariable58    probe_environmentvariable58
filehash58               probe_filehash58
inetalistenservers       probe_inetalistenservers
rpminfo                  probe_rpminfo
partition                probe_partition
iflisteners              probe_iflisteners
rpmverify                probe_rpmverify
rpmverifyfile            probe_rpmverifyfile
rpmverifypackage         probe_rpmverifypackage
selinuxboolean           probe_selinuxboolean
selinuxsecuritycontext   probe_selinuxsecuritycontext
file                     probe_file
interface                probe_interface
password                 probe_password
process                  probe_process
runlevel                 probe_runlevel
shadow                   probe_shadow
uname                    probe_uname
xinetd                   probe_xinetd
sysctl                   probe_sysctl
process58                probe_process58
fileextendedattribute    probe_fileextendedattribute
routingtable             probe_routingtable
```

在您能够有效地使用 **oscap** 之前，还需要在系统上安装或导入一些安全内容。例如，您可以安装 SCAP 安全指南（SSG）软件包 `scap-security-guide`，其中包含目前 Linux 系统最先进且最完善的安全策略集。要在系统上安装 SCAP 安全指南软件包，请以 root 身份输入以下命令：

```
~]# yum install scap-security-guide
```

