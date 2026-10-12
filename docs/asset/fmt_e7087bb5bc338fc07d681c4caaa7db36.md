
$ cp `/directory_path/response/netca.rsp` `local_directory`

在此示例中，`directory_path` 是 DVD 中数据库目录的路径。如果您已将软件复制到硬盘，您可以在您偏好的响应文件位置编辑该文件。

- 2. 使用文本编辑器打开响应文件：

```
$ /local_dir/netca.rsp
```

- 3. 按照文件中的说明进行编辑。

> 注意：如果您没有正确配置响应文件，网络配置助手将失败。

- 4. 以 Oracle 软件所有者的身份登录，并设置 `ORACLE_HOME` 环境变量以指定正确的 Oracle 目录。静默模式：

- 5. 输入类似下面的命令以静默模式运行网络配置助手：

```
$ ORACLE_HOME/bin/netca -silent -responsefile /local_dir/netca.rsp
```

在此命令中：

- `-silent` 选项表示网络配置助手在静默模式下运行。
- `local_dir` 是您复制 `netca.rsp` 响应模板的目录的完整路径。

### B.5 使用响应文件进行安装后配置

使用以下章节在安装 Oracle 软件后创建并运行响应文件。

#### B.5.1 关于安装后配置文件

当您运行静默安装或响应文件安装时，您会在响应文件中提供有关服务器的信息，而这些信息通常是在图形用户界面中手动提供的。然而，响应文件不包含配置助手在软件安装完成后所需的用户账户密码。配置助手是通过名为 `configGetAllCommands` 的脚本启动的。您可以使用响应文件在响应模式下运行此脚本。该脚本使用密码连续运行配置工具以完成配置。

如果您保留了用于克隆安装的密码文件，Oracle 建议将其存储在安全位置。此外，如果您想停止安装以修复错误，可以使用 `configToolAllCommands` 和密码响应文件运行配置助手。

`configToolAllCommands` 响应文件包含以下语法选项：

- `internal_component_name` 是配置助手配置的组件名称
- `variable_name` 是配置文件变量的名称
- `value` 是配置时所需的预期值。

命令语法如下：
`internal_component_name|variable_name=value`

例如：
`oracle.assistants.asm|S_ASMPASSWORD=welcome`

Oracle 强烈建议通过密码响应文件维护安全性：

- 响应文件的权限应设置为 `600`。
- 响应文件的所有者应为安装所有者用户，组设置为中心清单（`oralInventory`）组。

#### B.5.2 使用响应文件运行安装后配置

使用 `configToolAllCommands` 脚本运行配置助手：

- 1. 使用 `filename.properties` 语法创建响应文件。例如：
  `$ touch cfgprop.properties`
- 2. 使用文本编辑器打开文件，并编辑密码模板，根据需要进行修改。

> 示例 B–1 用于群集 Oracle Grid Infrastructure 安装的密码响应文件

Oracle Grid Infrastructure 需要 Oracle 自动存储管理配置助手 (`ASMCA`) 的密码，如果您有 BMC 卡并想启用此功能，还需要智能管理接口配置助手 (`IPICA`) 的密码。提供以下响应文件：

```
oracle.assistants.asm|S_ASMPASSWORD=password

oracle.assistants.asm|S_ASMMITORPASSWORD=password

oracle.crs|S_BMCPASSWORD=password
```

如果您没有 BMC 卡或不想启用 IPMI，请留空 `S_BMCPASSWORD` 字段。

示例 B–2 用于 Oracle Real Application Clusters 的密码响应文件

数据库配置需要 `SYS`、`SYSTEM`、`SYSMAN` 和 `DBSNMP` 密码用于数据库配置助手 (`DBCA`)。此外，如果使用 Oracle 存储，则配置 `ASMNMP` 密码。如果如果选择了 Oracle Enterprise Manager，则为 Oracle 软件所有者提供 `S_HOSTUSERPASSWORD` 响应。

```
oracle.assistants.server|S_ASMPPASSWORD=password

oracle.assistants.server|S_SYSTEMPASSWORD=password

oracle.assistants.server|S_SYSMANPASSWORD=password

oracle.assistants.server|S_DBSNMPPASSWORD=password

oracle.assistants.server|S_HOSTUSERPASSWORD=password

oracle.assistants.server|S_ASMNOPPASSWORD=password
```

如果您不想启用 Oracle Enterprise Manager 或 Oracle ASM，请留空这些字段。

- 3. 修改文件权限。例如：

```
$ ls -al cfgprop.properties

-rw------- 1 oracle 0
```

- 4. 切换到 `$ORACLE_HOME/cfgtool`，并使用以下语法运行配置脚本：`RESPONSE_FILE=/path/name.properties`，例如：

```
$ ./configToolAllCommands
```

## C 配置大内存优化

本附录提供了在 Linux 系统上使用 Hugepages 配置大内存优化的信息。它包含以下主题：

- HugePages 概述
- HugePage 配置限制
- 禁用透明 HugePages

### C.1 HugePages 概述

您可以选择配置 HugePages。对于某些用途，HugePages 可以提供增强性能。然而，这是一个高级配置选项，并不是 Oracle RAC 的要求。以下是 HugePages 的概述。您必须执行的配置任务取决于内核发行和硬件。如果您决定配置集群节点使用 HugePages，请参考您的发行文档以及 Oracle 技术网络 (`OTN`) 和 Oracle Support 获取更多信息。

#### HugePages 提供什么

HugePages 是集成到 2.6 版本 Linux 内核中的功能，是一种处理大内存的大页方法。它适用于 32 位和 64 位配置。HugePage 的大小从 2MB 到 256MB 不等，取决于内核版本和架构。数据库减少了操作系统对页状态的维护并增强了 TLB（转换缓冲区）命中。如果没有 HugePages，操作系统将每个 4 KB 的内存作为一个页，当分配给 SGA 时，操作系统必须更新该页的生命周期（脏、空闲、映射到进程等）。使用 HugePages 后，页表（虚拟内存映射）更小，因为每个页表项指向 2MB 到 256MB 的页。此外，内核需要监控的页更少。例如，如果您在 64 位硬件上使用 HugePages 并映射 256 MB 内存，您可能需要一个页表项 (`PTE`)。如果不使用 HugePages 且要映射 256 MB，则需要 256 MB * 1024 KB / 4 KB = 65536 个 PTE。

### C2 HugePage 配置限制

要使用 HugePages，必须配置 Grub 在启动期间为 HugePages 分配内存。预留空间后，可以根据需要使用 HugePages。然而，如果系统启动时未预留空间，则 HugePages 分配可能会失败。

除非系统管理员通过修改可用页数或池大小来更改 hugepages 配置，否则 HugePages 在系统启动后不会分配或释放。

### C3 禁用透明 HugePages

Red Hat Enterprise Linux 6、SUSE Enterprise Server 11 以及早期版本的 Oracle Linux 6 UEK 内核默认禁用透明 HugePages 内存。在较版本的 Oracle Linux UEK 内核中禁用了透明 HugePages。

透明 HugePages 会导致运行时内存分配延迟。为了避免性能问题，Oracle 建议在所有 Oracle 数据库服务器上禁用透明 HugePages。Oracle 建议使用标准的 HugePages 来增强性能。透明 HugePages 内存与标准 HugePages 的区别在于内核在运行时动态分配内存。标准 HugePages 在启动时预分配，且在运行时不会改变。

> **另参：**《Linux 和 UNIX 系统的 Oracle 数据库管理员参考》中的 HugePages 信息

以 `root` 用户身份运行以下命令之一检查是否启用了透明 HugePages 内存：

Red Hat Enterprise Linux 内核：
