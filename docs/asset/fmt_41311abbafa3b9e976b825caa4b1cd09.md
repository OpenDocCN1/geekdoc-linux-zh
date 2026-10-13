
| `local_diskette` | 指定升级系统上的本地软盘。`<path>` 是本地软盘，例如 `/dev/diskd0`。软盘必须经过格式化。 |

| `local_filesystem` | 指定升级系统上的本地文件系统。`<path>` 可以是磁盘分区的块设备路径，也可以是 `/etc/fstab` 文件挂载的文件系统的绝对路径。`<path>` 的示例包括 `/dev/disk/cn0s7` 和 `/home`。 |

# 第 21 章 JUMPSTART 781

| 关键字 | 说明 |

| :--- | :--- |

| `remote_filesystem` | 指定远程系统上的 NFS 文件系统。`<path>` 必须包含远程系统（主机）名称或 IP 地址以及指向 NFS 文件系统的绝对 `<path>`。该 NFS 文件系统必须具有读/写权限。示例 `<path>` 为 `sparcl1:/home`。 |

| `remote_system` | 定义远程系统上的一个目录，该目录可以通过远程 shell (`sh`) 访问。正在升级的系统必须通过远程系统的文件访问远程系统。`<path>` 必须包含远程系统的名称以及目录的绝对路径。如果用户不存在，则尝试以 root 身份登录。示例 `<path>` 为 `balkins@sparcl:/home`。 |

以下是一些示例：

- `backup_media local_tape /dev/rmtmt0`
- `backup_media local_diskette /dev/rdiskette0`
- `backup_media local_filesystem /dev/dsk/ct3d0s7`
- `backup_media local_filesystem /export`
- `backup_media remote_filesystem sparcl1:/export/temp`
- `backup_media remote_system balkins@sparcl1:/export/temp`

只有在需要磁盘空间重新分配时，才必须配合升级选项使用 `backup_media`。

## boot_device

`boot_device` 指定安装程序安装根文件系统的设备，从而决定了系统的启动设备。EEPROM 值还允许您在更改当前启动设备时更新系统的 EEPROM，以便系统能够从新的启动设备自动启动。

以下是 `boot_device` 的语法：

```
boot_device <device> <eeprom>
```

`device` 和 `eeprom` 的值见表 21.6。

### 表 21.6 设备关键字

| 关键字 | 说明 |

| --- | --- |

| `<device>` | 通过指定磁盘切片（例如 `c01d00`）来指定启动设备。可以是关键字 `existing`，将根文件系统放置在现有的启动设备上；也可以是 `any`，让安装程序选择放置根文件系统的位置。 |

| `<eeprom>` | 指定是否要将 EEPROM 更新为指定的启动设备。`eeprom` 指定值更新，告诉安装程序将系统 EEPROM 更新为指定的启动设备；或者 `preserve`，保持系统中的启动设备值不变。示例为 `boot_device c01d00` |

安装程序在 `c01d00` 上安装根文件系统，并更新 EEPROM 以从新的启动设备自动启动。

## client_arch

`client_arch` 表示 OS 服务器支持除自身以外的平台组。如果您未指定 `client_arch`，任何使用该 OS 服务器的无盘客户端或 Solstice AutoClient 必须与服务器具有相同的平台组。`client_arch` 只有在 `system_type` 指定为 `server` 时可以使用。您必须指定希望服务器支持的每个平台组。

以下是 `client_arch` 的语法：

```
client_arch karch_value [karch_value...]
```

`karch_value` 的值包括 `sun4d`、`sun4c`、`sun4u` 和 `i86pc`。

示例下：

```
client_arch sun4m
```

## client_root

`client_root` 定义了为每个客户端分配的根空间（单位：MB）。如果您在服务器配置文件中未指定 `client_root`，安装软件将为每个客户端自动分配 15MB 的根空间。客户端根区域的大小与 `num_clients` 关键字结合使用，以确定为 `/export/root` 文件系统预留空间。

语法如下：

```
client_root <root_size>
```

`root_size` 以 MB 为单位。

示例：

```
client_root 20
```

## client_swap

`client_swap` 定义了为每个磁盘客户端分配的交换空间（单位：MB）。如果您未指定 `client_swap`，将分配 32MB 的交换空间。物理内存加交换空间至少为 32MB。如果类文件没有显式指定交换空间，Solaris 安装程序将根据系统确定交换文件可以的大小。

语法如下：

```
client_root <root_size>
```

`root_size` 以 MB 为单位。

示例：

```
client_root 20
```

## cluster

`cluster` 表示 OS 服务器支持除自身以外的平台组。如果您未指定 `client_arch`，任何使用该 OS 服务器的无盘客户端或 Solstice AutoClient 必须与服务器具有相同的平台组。`client_arch` 只有在 `system_type` 指定为 `server` 时可以使用。您必须指定希望服务器支持的每个平台组。

# 第 21 章 JUMPSTART 787

### 表 21.10

#### <SIZE> 值

| 值 | 描述 |

| --- | --- |

| `num` | 文件系统的大小，单位为 MB。 |

| `existing` | 现有文件系统的当前大小。 |

| `auto` | 文件系统的大小根据所选软件自动确定。 |

| `all` | 指定分区使用整个磁盘作为文件系统。当指定此值时，指定的磁盘上将无法保留其他文件系统。 |

| `free` | 磁盘上剩余的未使用空间用于文件系统。 |

| `<start>:<size>` | 文件系统被分区。`<start>` 是分区开始的柱面数，`<size>` 是该分区的柱面数。 |

当分区被划分为 `any` 或 `exists` 时，`file_system` 是可选字段。如果未指定 `file_system`，默认设置为 `unnamed`，但你无法使用 `optional_parameters` 值。

表 21.11 中列出的值可用于 `file_system`。

### 表 21.11

#### FILE_SYSTEM 值

| 值 | 描述 |

| --- | --- |

| `<mount_pt_name>` | 文件系统的挂载点名称，例如 `/opt`。 |

| `<swap>` | 指定分区用作交换分区（swap）。 |

| `<overlap>` | 指定分区定义为整个磁盘的表示。只有当 `<size>` 为 `existing`、`all` 或 `start:size` 时，才能指定 `overlap`。 |

| `<unnamed>` | 指定分区定义为原始分区（raw slice），因此分区没有挂载点名称。如果未指定 `file_system`，默认设置为 `unnamed`。 |

| `<ignore>` | Solaris 安装程序不使用或识别指定的分区。这可以在安装期间忽略磁盘上的某个文件系统，以便 Solaris 安装程序在同一块磁盘上创建相同名称的新文件系统。`ignore` 仅在指定 `existing` 分区时可用。 |

在下面的示例中，swap 的大小被设置为 64MB，并安装在 `c0t3d0s1` 上：

| `filesys` | `c0t3d0s1 64 swap` |

在下一个示例中，`/usr` 基于所选软件，当你指定任何值时，安装程序将决定将其放在哪个磁盘上：

| `filesys` | `any auto /usr` |

`optional_parameters` 字段可以是表 21.12 中列出的选项之一。

### 表 21.12

#### OPTIONAL_PARAMETERS 选项

| 选项 | 描述 |

| --- | --- |

| `preserve` | 保留指定分区上的文件系统。当 size 为 `existing` 且分区为 `c0t/d0s?` 时，可以指定 `preserve`。 |

| `mount_options` | 添加到指定的 `mount_pt_name` 的 `/etc/vfstab` 条目中的一个或多个挂载选项。 |

## install_type

`install_type` 指定在系统上执行初始安装选项还是升级选项。`install_type` 必须是每个配置文件中的第一个类文件关键字。

语法如下：

```
install_type [initial_install | upgrade]
```
