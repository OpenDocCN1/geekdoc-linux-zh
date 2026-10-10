
当指定 `e` 参数时，错误消息将显示在标准输出和日志文件中，并在显示错误消息后停止 make_net_recovery 的执行。

### -s ignite-UX 服务器
指定 Ignite-UX 服务器的主机名。客户机系统的配置文件、默认值文件和内容文件将从 Ignite-UX 服务器的 /var/opt/ignite/clients/[[ox][LLA]]/recovery 目录中读取。make_net_recovery 工具将通过 NFS 挂载每个客户机的目录来访问此信息。

### -v
在创建系统恢复归档时显示详细进度消息。包括哪些卷组/磁盘将被包含在系统恢复归档中等信息。

### -x include=file|dir
将文件或目录包含在恢复归档中，但不跨越任何挂载点。

### -x inc cross=file|dir
将文件或目录包含在恢复归档中，并跨越挂载点以访问已挂载的目录或包含在已挂载目录中的文件。

### -x inc entree=/dev/dsk/<name> |vg_name
包含指定磁盘或卷组中的所有文件系统。在指定整盘（非 LVM）文件系统时，请使用 /dev/dsk/<name> 格式的设备文件。如果您希望将属于该 LVM 卷组的所有文件系统都包含在归档中，请使用卷组名称（例如 vg01）。

### -x exclude=file|dir
将文件或目录从归档中排除。当指定目录时，该目录下的任何文件都将不会存储在归档中。

## XToolkit 选项

make_net_recovery 命令支持标准 X Toolkit 选项的一个子集，以在指定 -i 选项时控制 GUI 的外观。支持的选项包括：-bg、-background、-fg、-foreground、-display、-name、-xrm 和 -synchronous。有关这些选项的定义，请参阅 X(1) 手册页。

## 归档的包含与排除

归档的内容可以通过内容文件进行控制。内容文件的完整路径为 /var/opt/ignite/clients/[[ox]][[LLA]]/recovery。归档标识符指定了文件、目录、整个磁盘和卷组的包含情况。关键字标识符还指示 make_net_recovery 在创建系统恢复归档时是否遵循挂载点。内容文件包含以下关键字标识符：

- include <文件名 | 目录>
  包含指定的文件名或目录以及所有子目录和关联文件。不会跨越挂载点，也不会跟随符号链接。
- inc_cross <文件名 | 目录>
  包含指定的文件名或目录以及所有子目录和子目录中包含的文件。会跨越本地挂载点，但不会跟随符号链接。
- inc_entire <卷组 | 磁盘>
  包含指定的整个卷组（例如 "vg00"）或磁盘（块设备 - 例如 "/dev/dsk/c1td5D0"）。如果磁盘是卷组的一部分，请勿指定该磁盘。
- exclude <文件名 | 目录>
  排除指定的文件名或目录以及所有子目录和子目录中包含的文件。

make_net_recovery 读取内容文件以生成用于创建系统恢复归档的文件列表。内容文件可以手动修改，也可以通过以交互模式运行 make_net_recovery 来修改。修改内容文件时，请记住以下几点：

- 不能排除任何基本文件或目录。对基本文件或目录的排除将被忽略。
- 排除优先于包含。同时被包含和被排除的任何内容都将从归档中排除。
- 默认文件中包含和排除的顺序并不重要。

## 使用以前归档创建的设置

默认文件存储了通过与 make_net_recovery GUI 交互指定的输入。选项会保留，直到通过与 GUI 交互生成下一个归档为止。命令行选项将覆盖默认文件中的设置。默认文件在 Ignite-UX 服务器上的完整路径为 /var/opt/ignite/clients/xxx/LUA//recovery/defaults。该目录通过 NFS 从客户机访问。

```
##### 默认文件 #####

RECOVERY_MULTI_IN-
RECOVERY_DESCRIPTION="recovery_archive"
SAVE_NUM_ARCHIVES=2
```

## 使用恢复归档

要使用网络恢复归档恢复故障系统：

- 如果正在替换客户机系统，或者自上次使用 make_net_recovery 以来 LAN 卡已更改，您应在开始恢复之前手动重命名旧的客户机目录。不这样做会导致创建新目录，您将无法看到在旧客户机目录下创建的恢复归档。要重命名客户机目录，请获取新的 LIA 地址（您可以在信息菜单中使用 LeadAddress 608-POW 命令），然后使用 mv 命令。例如：
  `mv /cd/L08108305461A XXX006GBCO43AB7`
- 如果您已经启动了新系统，在重命名旧目录之前需要移除新客户机。请小心不要移除包含恢复信息的旧目录。
- 使用网络引导、使用 make_boot_tape 创建的磁带，或者如果系统仍在运行则使用 bootsys 命令来启动系统。
- 不要与 ISL 交互
- 选择：[ 安装 HP-UX ]
- 从 Ignite-UX GUI：选择客户机的图标
- 选择 *安装/新安装*
- 选择要使用的恢复配置

## 导出归档目录

用于存储归档的目录必须从归档服务器导出到每个客户机。从存储归档的系统导出归档目录使 make_net_recovery 能够创建并通过 NFS 访问归档。归档服务器默认为 Ignite-UX 服务器，但可以使用 -a 选项更改为不同的远程服务器，甚至是本地客户机，如果您希望将归档作为客户机常规备份的一部分进行捕获。但是，请注意，如果归档存储在客户机本身，一旦需要使用它们进行恢复，必须将它们放到远程服务器上。

出于安全原因，最好将每个特定于客户机的归档目录仅导出给该单个客户机。如果恢复归档创建是从 Ignite GUI 发起的，无论 Ignite-UX 服务器在何处，且归档服务器与 Ignite-UX 服务器相同，/etc/exports 文件将自动编辑，以便将归档存储在期望的位置。否则，如果在客户机上直接运行 make_net_recovery，则需要在归档服务器上执行以下步骤。

- 在归档服务器上，为每个客户机创建一个目录，用于存放该客户机文件的归档。重要的是该目录的所有者必须是 *bin* 用户。请将以下命令中的 **client** 替换为客户机的主机名。如果使用 make_net_recovery 的 -a 选项来指定归档的替代位置，则需要使用那个路径而不是下面显示的默认路径。

```sh
mkdir -p /var/opt/ignite/recovery/archives/<client>
chown bin:bin /var/opt/ignite/recovery/archives/<client>
```

- 编辑 /etc/exports 为每个客户机添加条目。请将示例中的 <client> 替换为客户机的主机名：

```sh
/var/opt/ignite/recovery/archives/<client> -anow=2,access=<client>
```

- 运行 exportsfs 命令以使对 exports 文件的编辑生效：

```sh
/usr/sbin/exportsfs -av
```

## 网络功能

make_net_recovery 在客户机上建立两个 NFS 挂载点。Ignite-UX 服务器上的 /var/opt/ignite/clients 目录挂载到客户机系统，用于存储描述客户机配置和恢复归档位置配置文件。第二个挂载点指向 archive_server/archive_dir（参见 -a 选项），用于存储客户机系统的恢复归档。在系统恢复归档成功或不成功后，这些 NFS 挂载点将被卸载。

归档目录的 NFS 挂载可以按客户机为基础导出。每个客户机使用单独的归档目录。这允许您仅将每个目录 NFS 导出给拥有该归档的单个客户机，从而提供安全性。

如果客户机系统没有最新版本的 Ignite-UX 工具，Ignite-UX GUI 将使用 suinstall\[M\] 安装“恢复包”，其中包含执行恢复所需的所有必要文件。

## 返回值

make_net_recovery 在成功完成时返回 0。当发生警告时，返回 2。否则，当发生故障时返回 1。

## 示例

通过与 Ignite-UX 服务器上的 Ignite-UX GUI 交互来创建系统恢复归档：

```sh
export DISPLAY=hostname:0
ignite
```

从客户机创建系统恢复归档，使用上次调用 Ignite-UX GUI 时的设置。使用 Ignite-UX 服务器上的选项文件（位于默认位置 /var/opt/ignite/clients/OxDIA/recovery 中的 /server/）。

```sh
make_net_recovery -s myserver
```

创建包含 vg00 卷组中所有文件系统文件的系统恢复归档：

