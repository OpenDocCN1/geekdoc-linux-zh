
## 表 21.15
### 分区选项
| 选项 | 描述 |
|---|---|
| default | Solaris 安装程序选择磁盘并创建文件系统以安装指定的软件。除 filesys 关键字指定的任何文件系统外，首先选择 rootdisk。如果指定的软件无法安装在 rootdisk 上，则使用额外的磁盘。 |
| existing | Solaris 安装程序使用系统磁盘上现有的文件系统。除了 /, /usr, /usr/openwin, /opt 和 /var 之外的所有文件系统都保留。安装程序使用文件系统超级块中的最后一个挂载点字段来确定切片代表哪个文件系统挂载点。当您使用分区指定 filesys 类文件关键字时，必须指定 existing。 |
| explicit | Solaris 安装程序使用磁盘并创建 filesys 关键字指定的文件系统。如果您仅使用 filesys 关键字指定根 (/) 文件系统，则所有 Solaris 软件都将安装在根文件系统中。当您使用 explicit 类文件值时，必须使用 filesys 类文件关键字来指定要使用的磁盘以及要创建的文件系统。 |

## root_device
root_device 指定系统的根磁盘。

以下是语法：
```
root_device slice
```
以下是示例：
```
root_device c0t3d0s2
```

## system_type
system_type 定义正在安装的系统类型。如果您在类文件中未指定 system_type，则默认设置为 standalone。

以下是语法：
```
system_type [standalone | server]
```
以下是示例：
```
system_type server
```

## usedisk
usedisk 指定一个或多个磁盘，您希望 Solaris 安装程序在分区指定为 default 时使用。默认情况下，安装程序使用系统上所有可操作的磁盘。disk_name 必须以 c?t?d? 或 c?d? 的形式指定，例如 c0t0d0。如果您在类文件中指定 usedisk 类文件关键字，则 Solaris 安装程序仅使用您指定的磁盘。

以下是语法：
```
usedisk disk_name [disk_name]
```
以下是示例：
```
usedisk c0t0d0 c0t1d0
```

> NOTE 您不能在同一个类文件中同时指定 usedisk 关键字和 dontuse 关键字。

## 测试类文件
创建类文件后，您可以使用 pfinstall 命令对其进行测试。测试类文件有时称为“试运行”安装。通过查看 pfinstall 生成的安装输出，您可以快速确定类文件是否会按预期执行。例如，您可以在实际执行升级之前确定系统是否有足够的磁盘空间升级到新版本的 Solaris。

要为特定 Solaris 版本测试类文件，您必须在同一版本的 Solaris 环境中对其进行测试。例如，如果您想为 Solaris 8 测试类文件，则必须在运行 Solaris 8 的系统上运行 pfinstall 命令。

要测试类文件，请更改为包含类文件的 JumpStart 目录并输入
```
/usr/sbin/install.d/pfinstall -d
```
或
```
/usr/sbin/install.d/pfinstall -D
```

> **CAUTION**
如果没有 -d 或 -D 选项，pfinstall 实际上会使用指定的类文件在系统上安装 Solaris 软件，并且系统上的数据将被覆盖。

以下是 pfinstall 的语法：
```
/usr/sbin/install.d/pfinstall [-D | -d] disk_config \
[-c path] profile
```
pfinstall 选项在表 21.16 中描述。

## 表 21.16
### pfinstall 选项
| 选项 | 描述 |
|---|---|
| -D | 指示 pfinstall 使用当前系统的磁盘配置来测试类文件。 |
| -d <disk_config> | 指示 pfinstall 使用磁盘配置文件 <disk_config> 来测试类文件。如果 <disk_config> 文件不在运行 pfinstall 的目录中，则必须指定路径。此选项不能与升级类文件（install-type 升级）一起使用。您必须始终使用 -D 选项针对系统的磁盘配置测试升级类文件。磁盘配置文件表示磁盘的结构。它描述了磁盘的每扇区字节数、标志和切片。有关如何创建 <disk_config> 文件的示例，请参阅本表之后的示例。 |
| -c path | 指定 Solaris CD 映像的路径。如果 Solaris CD 未挂载在 /cdrom 上，则需要此选项。例如，如果系统使用 Volume Manager 挂载 Solaris CD，则使用此选项。 |
| profile | 指定要测试的类文件的名称。如果类文件不在运行 pfinstall 的目录中，则必须指定路径。 |

> **NOTE**
c?t?d?s2 指定 SCSI 磁盘的特定目标，而 c?d?s2 指定非 SCSI 磁盘。

您可以通过发出以下命令创建 <disk_config> 文件：
```
prtvtoc /dev/rdsk/<device_name> <disk_config>
```
/dev/rdsk/<device_name> 是系统磁盘的设备名称。
<device_name> 必须采用 c?t?d?s2 或 c?d?s2 的形式。
<disk_config> 是磁盘配置文件的名称。

以下是示例：
```
prtvtoc /dev/rdsk/c0t3d0s2 >test
```
此示例创建的文件名为 "test"，它将是您的 <disk_config> 文件，其内容如下所示：
```
* /dev/rdsk/c0t3d0s2 partition map
*
* Dimensions:
*     512 bytes/sector
*     126 sectors/track
*     4 tracks/cylinder
*     504 sectors/cylinder
*     4106 cylinders
*     4104 accessible cylinders
*
* Flags:
*     1: unmountable
*     10: read-only
*
*
*               First  Sector Last
* Partition  Tag  Flags  Sector Count  Sector    Mount Directory
        0     2    00      0    268632  268631    /
        1     3    01  268632  193032  461663
        2     5    00      0  2068416 2068415
        3     0    00  461664  152712  614375    export
        4     0    00  614376  141624  755999    export/swap   /
        6     4    00  756000  1312416 2068415  /usr
```

> NOTE 如果您想在多个磁盘上测试安装 Solaris 软件，请将单个磁盘配置文件连接起来并将输出保存到新文件。

以下示例在运行 pfinstall 的 Solaris 8 系统上，将 ultra_class 类文件与磁盘配置进行测试。ultra_class 类文件位于 /jumpstart 目录中，并且由于使用了 Volume Management，因此指定了 Solaris CD 映像的路径。

此外，如果您想为具有特定系统内存大小的系统测试类文件，请按如下方式将 SYS_MEMSIZE 设置为特定内存大小（以 MB 为单位）：
```
SYS_MEMSIZE=memory_size
export SYS_MEMSIZE
cd /jumpstart
/usr/sbin/install.d/pfinstall -D -c /cdrom/cdrom0/s0 ultra_class
```
系统测试类文件并显示数页结果。请查找以下消息，表示测试成功：
```
Installation complete
Test run complete. Exit status 0.
```

## sysidcfg 文件
当 JumpStart 客户端首次启动时，启动软件首先尝试从名为 sysidcfg 的文件获取系统识别信息（例如系统的主机名、IP地址、区域设置、时区和 root 密码），然后从名称服务数据库获取。如果您未使用名称服务，您将使用此文件在安装的初始阶段回答系统识别问题。如果您使用名称服务，您可能需要查看下一节标题为“在名称服务环境中设置 JumpStart”。

您将使用 sysidcfg 文件在安装的初始阶段回答系统识别问题。如果 JumpStart 服务器提供此信息，客户端将绕过 Solaris 8 安装过程中的初始系统识别部分。如果没有 sysidcfg 文件，客户端将显示适当的交互式对话框以请求系统识别信息。您必须为每个需要不同配置信息的系统创建唯一的 sysidcfg 文件。

sysidcfg 文件可以位于共享 NFS 目录或 UFS 文件系统上的根 (/) 目录中。它也可以位于软盘上的 PCFS 文件系统上。每个目录或软盘上只能有一个 sysidcfg 文件。sysidcfg 文件的位置由用于创建 JumpStart 客户端信息文件的 add_install_client 脚本的 -p 参数指定。

创建 sysidcfg 文件要求系统管理员在 sysidcfg 文件中指定一组关键字以预配置系统。sysidcfg 文件中使用的关键字有两种类型：独立和从属。以下是说明独立和从属关键字的示例：
```
name_service=NIS {domain_name=pyramid.com \
name_server=server(192.168.0.1)}
```
在此示例中，name_service 是独立关键字，而 domain_name 和 name_server 是从属关键字。

为了帮助解释 sysidcfg 关键字，我将它们分组到类别中并详细描述每个关键字。

> NOTE

将所有从属关键字用大括号 {} 括起来以将其与关联的独立关键字绑定。值可以 optionally 用单 ' 或双引号 " 括起来。
