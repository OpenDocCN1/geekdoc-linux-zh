
表 A.1 本书所述工具列表（续）

| 工具 | 描述 | 性能管理 | 配置管理 | 诊断管理 | 页码 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| snmpbulkwalk | 增强的 SNMP 检索 | | | | 451 |
| snmpconf | 自动化的 SNMP 配置 | | ✓ | | 454 |
| snmpd | UCD SNMP 代理 | | | | 448 |
| snmpdelta | 格式化 SNMP 数据 | | | | 422 |
| snmpget | 常规 SNMP 检索 | | | | 425 |
| snmpgetnext | 检索多个 SNMP 对象 | | | | 427 |
| snmpnetstat | 从 SNMP 实体检索网络统计信息 | | | | 429 |
| snmpset | 修改 SNMP 配置信息 | | ✓ | | 434 |
| snmpstatus | 检索重要 SNMP 数据 | | | | 437 |
| snmptable | 检索 SNMP 表数据 | | | | 440 |
| snmptest | 测试 SNMP 连接性 | | | | 443 |

表 A.1 本书所述工具列表（续）

| 工具 | 描述 | 性能管理 | 配置管理 | 诊断管理 | 页码 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| snmptrap | 发送 SNMP 陷阱 | | | √ | 445 |
| snmptrapd | 从网络接收 SNMP 陷阱 | | | √ | 446 |
| snmpwalk | 检索一组或整个 MIB 树 | | | √ | 450 |
| tcpdump | 数据包捕获程序 | | | √ | 153 |
| tkined | 用于创建拓扑图和管理网络设备的网络编辑器 | √ | | √ | 568 |
| tkmib | SNMP MIB 浏览器 | | √ | √ | 458 |
| traceroute | 显示路由路径 | √ | | √ | 171 |
| xtraceroute | 显示路由路径信息 | √ | | √ | 239 |

## 安装程序和软件说明

请使用以下安装程序安装本书所述的工具。许多软件包已提供在本书内侧封底的 CD-ROM 上。软件也可以通过互联网获取。由于出版本书后某些工具可能已更新，因此提供了指向替代来源（适用时）的链接。此外，部分工具还以源代码形式提供；因此也包含了构建这些软件包的程序。

表 B.1 包含本书中讨论的所有工具的列表。该表还包括一列，指示该工具是否包含在 CD-ROM 上、其在 CD-ROM 上的目录以及该工具可位于的任何替代互联网来源。此信息提供的原因是某些工具所有者会定期提供更新，并且可以从互联网直接下载更新版本。

## 表 B.1 工具信息目录

| 工具 | 是否在 CD-ROM 上 | CD-ROM 上的目录 | 替代来源 |
| :--- | :--- | :--- | :--- |
| Chesapeake's Subnet Calculator | Y | ccci | http://www.ccci.com/tools/subcalc/index.html |
| arp | N | NA | NA |
| control-panel | N | NA | NA |
| ethereal | Y | ethereal | http://ethereal.zing.org |
| fping | Y | fping | ftp://ftp.stanford.edu/pub/packages/fping/fping2.2b1.tar.gz ftp://sesame.hensa.ac.uk/pub/mirrors/ftp.kernel.org/pub/software/admin/mon/fping2.2b1.tar.gz ftp://www.wooten.net/ftp/pub/unix/att/tcputils/fping.tar.z |
| ifconfig | N | NA | NA |
| ping | N | NA | NA |
| netstat | N | NA | NA |
| nmap | Y | nmap | http://www.insecure.org/nmap |
| ntop | Y | ntop | ftp://ftp.unipi.it/pub/local/ntop |
| mibiisa | Y | sunagent | http://www.sun.com/solstice/products/ent.agents |
| mrtg | Y | mrtg | http://eestaff.ethz.ch/~oetiker/webtools/mrtg/pub/ |
| snmpd | Y | ucd | Part of the UCD package |
| snmpdelta | Y | ucd | Part of the UCD package |
| snmpget | Y | ucd | Part of the UCD package |
| snmpgetnext | Y | ucd | Part of the UCD package |
| snmpgetstat | Y | ucd | Part of the UCD package |
| snmpset | Y | ucd | Part of the UCD package |
| snmpstatus | Y | ucd | Part of the UCD package |
| snmptable | Y | ucd | Part of the UCD package |
| snmptest | Y | ucd | Part of the UCD package |
| snmptranslate | Y | ucd | Part of the UCD package |
| snmptrapd | Y | ucd | Part of the UCD package |
| snmptrapd | Y | ucd | Part of the UCD package |
| snmpwalk | Y | ucd | Part of the UCD package |
| snmpbulkwalk | Y | ucd | http://ftp.ece.ucdavis.edu/pub/snmp/ucd-snmp.tar.gz http://sunsite.cnlab-switch.ch/mirror/ucd-snmp/ucd-snmp.tar.gz http://ftp.win.or.jp/pub/network/ucd-snmp/ucd-snmp.tar.gz |
| snmpconf | Y | snmpconf | http://www.net.cmu.edu/projects/ http://ftp.net.cmu.edu/pub/snmp/snmpconf/snmpconf-V1.1.tar.gz http://ftp.net.cmu.edu/pub/snmp/cmu-snmp-V1.13.tar.gz |
| tkined | Y | scotty | http://wwwhome.cs.utwente.nl/~schoven/scotty/ http://ftp.ibr.cs.tu-bs.de/pub/local/tkined |
| tkmib | Y | ucd | Part of the UCD package |

表 B.1 工具信息目录（续）

| 工具 | 是否在 CD-ROM 上 | CD-ROM 上的目录 | 替代来源 |
| :--- | :--- | :--- | :--- |
| traceroute | N | NA | NA |
| xtraceroute | Y | xtraceroute | http://www.dtek.chalmers.se/~d3august/xt/index.html |

## 使用 RPM 安装软件包

您可以使用 GNOME Red Hat 软件包管理器（RPM）安装程序安装以下软件包：

- Ethereal
- MRTG
- nmap
- ntop
- xtraceroute

CD-ROM 上找到的许多软件包均采用 RPM 软件包格式。因此，您可以使用 Linux 提供的 RPM 安装工具安装这些工具。Linux 上提供两种不同的 RPM 版本，均可用于安装软件工具。第一个名为 *rpm*，是命令行界面。另一个提供 GUI 界面的称为 *gnorpm*。

CD-ROM 包含多个 RPM 软件包，每个软件包的安装程序相同。因此，以下程序中仅显示一个软件包。

### 挂载 CD-ROM

1. 挂载随本书附带的 CD-ROM。将 CD-ROM 放入光驱后，执行以下命令：

```bash
mount -o ro /dev/cdrom /mnt/cdrom
```

该命令将 CD-ROM 挂载在 `/mnt` 目录下。后续程序将使用此目录作为示例。

## 使用命令行 RPM 工具

1. 切换到包含已挂载 CD-ROM 上 RPM 软件包的目录：
   
    rpm --install xtraceroute-0.8.13-1.i386.rpm

如果未遇到错误，则软件包已成功安装。如果软件包已安装，则会显示以下错误消息：

error: package xtraceroute-0.8.13-1.i386.rpm is already installed

## 使用 RPM GUI

1. 以 root 用户身份启动 RPM 安装工具，执行以下命令：
   
    /usr/bin/gnorpm

执行此命令将显示图 B.1 所示的窗口。这是主 gnorpm 安装窗口，可在此安装、查询、验证和删除软件包。您还可以在此执行其他任务，例如搜索特定软件包并升级一个或多个软件包。综合这些功能，使 gnorpm 工具成为网络和系统管理员非常重要的工具。

2. 使用左侧面板检查系统上已安装的软件包。使用此树视图，您可以浏览每个文件夹，从而显示其他文件夹并最终显示单个软件包。如果要删除

![](img/f265c9d1f2610aca197c430cbfcd51f5_661_0.png)

**图 B.1** *GNOME RPM* 主窗口。

一个或多个软件包，只需选择软件包并单击卸载按钮。

![](img/f265c9d1f2610aca197c430cbfcd51f5_661_1.png)

**图 B.2** *安装窗口*。

3. 接下来，单击窗口最左侧的 *Install* 按钮。将显示一个新子窗口，如图 B.2 所示。从 *Operations* 菜单中选择 *Install...* 子菜单也会使此窗口出现。显示的窗口包含一个空面板，因为尚未选择要加载到系统上的软件包。我们现在必须选择要安装的软件包。为此，我们必须单击 *Add* 按钮。这样做时，*Add Package* 对话框窗口将出现，如图 B.3 所示。在此选择要安装的软件包。
