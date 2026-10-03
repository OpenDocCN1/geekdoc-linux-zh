
## 表 21.6
### BOOT_DEVICE 关键字
| 关键字 | 描述 |
|---|---|
| `<device>` | 通过指定磁盘切片（如 c0t1d0s0）来指定启动设备。它可以是关键字 existing，将根文件系统放在现有的启动设备上，或关键字 any，让安装程序选择放置根文件系统的位置。 |
| `<eeprom>` | 指定是否要将系统的 EEPROM 更新为指定的启动设备。`<eeprom>` 指定值 update，指示安装程序将系统的 EEPROM 更新为指定的启动设备，或 preserve，保留系统 EEPROM 中启动设备值不变。一个示例是 boot_device c0t1d0s0 update。 |

安装程序将根文件系统安装在 c0t1d0s0 上，并更新 EEPROM 以便从新的启动设备自动启动。

## client_arch
client_arch 指示 OS 服务器支持与其自身不同的平台组。如果未指定 client_arch，使用 OS 服务器的任何无盘客户端或 Solstice AutoClient 系统必须与服务器具有相同的平台组。client_arch 只能在 system_type 指定为 server 时使用。您必须指定希望 OS 服务器支持的每个平台组。

以下是 client_arch 语法：

```
client_arch karch_value [karch_value...]
```

karch_value 的值包括 sun4d、sun4c、sun4m、sun4u 和 i86pc。

以下是一个示例：

```
client_arch sun4m
```

## client_root
client_root 定义为每个客户端分配的根空间量，以 MB 为单位。如果在服务器的配置文件中未指定 client_root，安装软件会自动为每个客户端分配 15MB 的根空间。客户端根区域的大小与 num_clients 关键字结合使用，以确定为 /export/root 文件系统保留多少空间。

以下是语法：

```
client_root <root_size>
```

root_size 以 MB 为单位指定。

以下是一个示例：

```
client_root 20
```

> NOTE
当分配根空间时，20MB 是一个合适的大小。15MB 是所需的最小大小。超过 20MB 只是在浪费磁盘空间。

## client_swap
client_swap 定义为每个无盘客户端分配的交换空间量，以 MB 为单位。如果未指定 client_swap，将分配 32MB 的交换空间。物理内存加上交换空间必须至少为 32MB。如果类文件未明确指定交换的大小，Solaris 安装程序会根据系统的物理内存确定交换文件可以达到的最大大小。Solaris 安装程序使交换的大小不超过其所在磁盘的 20%，除非在其他文件系统布局后磁盘上仍有空闲空间。

以下是语法：

```
client_swap <swap_size>
```

swap_size 以 MB 为单位指定。

以下是一个示例：

```
client_swap 64
```

此示例指定每个无盘客户端的交换空间为 64MB。

## cluster
cluster 指定要添加到系统的软件组。软件组列在表 21.7 中。

## 表 21.7
### 软件组
| 软件组 | group_name |
|---|---|
| Core | XSUNWCreq |
| End-user system support | SUNWCuser |
| Developer system support | SUNWCprog |
| Entire distribution | SUNWCall |
| Entire distribution plus OEM support | SUNWCXall (SPARC-based systems only) |

您只能在一个配置文件中指定一个软件组，并且它必须在其他 cluster 和 package 条目之前指定。如果使用 cluster 未指定软件组，则默认情况下会在系统上安装 end-user 软件组 SUNWCuser。

以下是 cluster 的语法：

```
cluster <group_name>
```

以下是一个示例：

```
cluster SUNWCall
```

此示例指定应安装 Entire distribution 组。

cluster 关键字还可用于指定是否应将集群添加到系统上已安装的软件组或从中删除。add 和 delete 指示是否应添加或删除集群。如果未指定 add 或 delete，则默认设置为 add。

以下是语法：

```
cluster <cluster_name> [add | delete]
```

<cluster_name> 必须采用 SUNWCname 的形式。要查看有关集群及其名称的详细信息，请在已安装的系统上启动 AdminTool 并选择 Browse、Software。

## dontuse
dontuse 指定一个或多个您不希望 Solaris 安装程序使用的磁盘。默认情况下，安装程序使用系统上的所有可用磁盘。<disk_name> 必须采用 c?t?d? 或 c’d? 的形式，例如 c0t0d0。

以下是语法：

```
dontuse disk_name [disk_name...]
```

以下是一个示例：

```
dontuse c0t0d0 c0t1d0
```

> NOTE 您不能在同一个类文件中同时指定 usedisk 关键字和 dontuse 关键字。

## filesys
filesys 设置已安装系统在启动时自动挂载远程文件系统。您可以多次指定 filesys。以下语法描述了使用 filesys 设置到远程系统的挂载：

```
filesys <server>:<path> <server_address> <mount_pt_name> \
[mount_options]
```

filesys 关键字在表 21.8 中描述。

## 表 21.8
### FILESYS 关键字
| 关键字 | 描述 |
|---|---|
| `<server>:` | 远程文件系统所在服务器的名称。不要忘记包含冒号 (:)。 |
| `<path>` | 远程文件系统的挂载点名称。 |
| `<server_address>` | `<server>:<path>` 中指定的服务器的 IP 地址。如果网络上未运行名称服务，此值可用于用服务器的 IP 地址填充 /etc/hosts 文件，但您必须指定一个减号 (-)。 |
| `<mount_pt_name>` | 远程文件系统将被挂载到的挂载点的名称。 |
| `[mount_options]` | 添加到指定 `<mount_pt_name>` 的 /etc/vfstab 条目的一个或多个挂载选项。如果需要指定多个挂载选项，挂载选项必须用逗号分隔且不带空格。一个示例是 ro,quota。 |

以下是一个示例：

```
filesys zeus:/export/home/user1 192.9.200.1 /home ro,bg,intr
```

filesys 还可用于在安装期间通过使用以下语法创建本地文件系统：

```
filesys <slice> <size> [file_system] [optional_parameters]
```

可用于 <slice> 的值列在表 21.9 中。

## 表 21.9
### <SLICE> 值
| 值 | 描述 |
|---|---|
| any | 此变量指示安装程序将文件系统放置在任何磁盘上。 |
| c?t?d?s? or c?d??z | Solaris 安装程序放置文件系统的磁盘切片，例如 c0t0d0s0。 |
| rootdisk.sn | 包含系统根磁盘值的变量，该值由 Solaris 安装程序确定。sn 后缀表示磁盘上的特定切片。 |

可用于 <size> 的值列在表 21.10 中。

## 表 21.10
### <SIZE> 值
| 值 | 描述 |
|---|---|
| num | 文件系统的大小，以 MB 为单位。 |
| existing | 现有文件系统的当前大小。 |
| auto | 文件系统的大小根据所选软件自动确定。 |
| all | 指定的切片使用整个磁盘作为文件系统。当指定此值时，不能在指定的磁盘上存在其他文件系统。 |
| free | 磁盘上剩余未使用的空间用于文件系统。 |
| <start>:<size> | 文件系统被显式分区。<start> 是切片开始的柱面，<size> 是切片的柱面数。 |

当 slice 指定为 any 或 c?t?d?s? 时，file_system 是可选字段。如果未指定 file_system，则默认设置为 unnamed，但您不能指定 optional_parameters 值。

可用于 file_system 的值列在表 21.11 中。

## 表 21.11
### FILE_SYSTEM 值
| 值 | 描述 |
|---|---|
| <mount_pt_name> | 文件系统的挂载点名称，例如 /opt。 |
| <swap> | 指定的切片用作交换。 |
| <overlap> | 指定的切片被定义为整个磁盘的表示。overlap 只能在 <size> 为 existing、all 或 start:size 时指定。 |
| <unnamed> | 指定的切片被定义为原始切片，因此切片没有挂载点名称。如果未指定 file_system，则默认设置为 unnamed。 |
| <ignore> | 指定的切片未被 Solaris 安装程序使用或识别。这可用于在安装期间忽略磁盘上的文件系统，以便 Solaris 安装程序可以在同一磁盘上使用相同名称创建新的文件系统。ignore 只能在指定现有分区时使用。 |
