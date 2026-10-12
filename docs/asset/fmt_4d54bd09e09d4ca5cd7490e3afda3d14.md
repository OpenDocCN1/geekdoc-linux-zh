
在 Linux 上安装 Oracle 之前，有必要创建一个 Oracle 用户账户。该账户必须属于 `oinstall` 组，并且也是 `dba` 组的成员。组使用 `groupadd` 命令添加（`/usr/sbin/groupadd`）：

```
groupadd oinstall
groupadd dba
```

Oracle 用户账户使用 `useradd` 命令（`/usr/sbin/useradd`）创建，如下所示：

```
useradd -g oinstall -G dba oracle  (on Red Hat)
useradd -m -g oinstall -G dba oracle  (on SUSE)
```

这将创建 Oracle 用户账户，其主目录为 `/home/oracle`，主要组为 `oinstall`，并将其生成为 `dba` 组的成员。

### 为 Oracle 用户配置 Shell 限制

还有一些可选任务必须完成，以便 Oracle 10g 安装能够工作。这些任务与增加 shell 限制有关，以便 Oracle 可以创建和打开大文件。这些步骤涉及编辑 `/etc/profile` 文件以增加 `ulimit`。以下内容应添加到 `/etc/profile` 中：

```
if [ $USER = "oracle" ]; then
    if [ $SHELL = "/bin/ksh" ]; then
        ulimit -p 16384
        ulimit -n 65536
    else
        ulimit -u 16384 -n 65536
    fi
fi
```

此外，以下行需要添加到 `/etc/security/limits.conf` 中，以便更改单个用户可以使用进程和文件的数量：

```
* soft  nproc  2047
* hard  nproc  16384
* soft  nofile 1024
* hard  nofile 65536
```

最后一步是修改 `/etc/pam.d/login` 文件。因此，应添加以下行：

```
session    required    /lib/security/pam_limits.so
```

完成这些任务后，您几乎就可以安装 Oracle Database 10g 服务器了。剩下的就是创建放置 Oracle 二进制文件和数据文件的目录，然后设置 Oracle 环境。

### 创建目录结构

Oracle 安装需要三个目录。这三个目录服务于不同的目的，包括：

- **Oracle Base** 用作其余 Oracle 树的基目录。
- **Oracle Inventory** 此位置用于 Oracle Universal Installer。
- **Oracle Home** Oracle Home 目录是安装特定软件版本的目录，通常是 Oracle Base 的子目录。

Oracle 基目录可能存在于不同安装的多个不同的挂载点上，并且 Oracle 数据文件可能位于与 Oracle 二进制文件不同的基树上。

将安装 Oracle 二进制文件的目录结构（`ORACLE_HOME` 目录）中的 I/O 要求相当轻。您必须有足够的可用空间，但实际上无需担心 I/O 性能。然而，存放 Oracle 二进制文件的位置应配置一定的容错能力。建议使用 RAID1。

对于 Oracle 数据文件，目录命名结构遵循 OFA 命名约定：

```
Mount_point/app/oracle
```

典型的挂载点为 Oracle 数据文件使用 `/u01`、`/u02`、`/u03`...，Oracle 主目录使用 `/opt/oracle`。

Oracle 库存目录的路径为 `oracle_base`/orainventory。

### Oracle 目录结构示例

典型的 Oracle 10g 系统的目录结构如下：

`/opt/oracle` Oracle 基目录

`/opt/oracle/orainventory` Oracle 库存目录

`/opt/oracle/product/10.1.0/db_1` 版本 10.1.0 的 Oracle 主目录

`/opt/oracle/product/10.2.0/db_1` 版本 10.2.0 的 Oracle 主目录

`/opt/oracle/product/10.2.0/client_1` Oracle 10.2.0 的客户端软件

`/u01/app/oracle/oradata/SID` 系统标识符（SID）名为 `SID` 的 Oracle 日志或数据文件的位置

`/u02/app/oracle/oradata/SID` SID 名为 `SID` 的 Oracle 数据文件的位置

### 设置 Oracle 环境

对于过去安装过以前版本 Oracle 的用户，您会注意到 Oracle 环境设置已发生变化。与 Oracle9i 安装不同，Oracle 10g 安装不需要 Oracle 环境变量

## Oracle 目录权限

先前提及的 Oracle 目录应由 Oracle 用户拥有，组为 `oinstall`，权限为 755。为实现此目的，请运行以下命令：

```
mkdir /opt/oracle
chown -R oracle.oinstall /opt/oracle
chmod -R 755 /opt/oracle
```

用于安装的配置文件中设置。实际上，这些变量不应在系统安装前设置在配置文件中。在 Oracle 10g 安装中，对 `bash_profile`（或您合适的 shell 配置文件）的唯一添加如下：

```
umask 022
```

此命令设置默认文件创建掩码。掩码 022 将创建具有 644 或 rw-r--r-- 权限的文件。

如果临时目录空间不足，则应按如下方式设置 `TEMP` 和 `TMPDIR` 环境变量：

```
TEMP=/u01/temp
TMPDIR=/u01/temp
export  TEMP  TMPDIR
```

最后一步是设置 `ORACLE_BASE` 和 `ORACLE_SID` 环境变量。它们与之前看到的类似设置：

```
ORACLE_BASE=/opt/oracle
ORACLE_SID=orac
export  ORACLE_BASE  ORACLE_SID
```

完成这些任务后，Oracle 安装即可开始。Oracle Database 10g 服务器的安装将在下一章介绍。

## 安装清单

拥有安装清单通常非常有价值。清单（如下所示）是对执行安装所需的要求和步骤的提醒，并有助于确保不会遗漏任何步骤。

## Oracle 10g R1 安装清单

| Step | Completed? |
|---|---|
| 1. Check hardware requirements. | |
| 512MB of RAM | |
| 1GB of swap space | |
| 400MB of temp space | |
| 1.5GB of Oracle binary space | |
| 1.2GB of Oracle data file space | |
| 2. Check Linux software for Oracle 10g R1. | |
| Red Hat Enterprise Linux AS 2.1 or ES 3.0 | |
| Software Development system installed? | |
| Kernel Development system installed? | |
| Red Hat Package Requirements | |
| *Red Hat 2.1 and 3.0* | |
| make-3.79 | |
| binutils-2.11.90.0.8-12 | |
| *Red Hat Enterprise Linux 2.1* (x86) | |
| gcc-2.96.108.1 | |
| openmotif-2.1.30-11 | |
| *Red Hat Enterprise Linux 3* | |
| gcc-3.3.2-2 | |
| compat-db-4.0.14.5 | |
| compat-gcc-7.3-2.96.122 | |
| compat-gcc-c++-7.3-2.96.122 | |
| compat-libstdc++-7.3-2.96.122 | |
| compat-libstdc++-devel-7.3-2.96.122 | |
| openmotif-2.2.2-16 | |
| setarch-1.3-1 | |
| *SUSE Linux Enterprise Server 8.0* (United Linux 1.0) | |
| Development Tools installed? | |
| Kernel Development installed? | |
| *SUSE Package Requirements* | |
| gcc-3.2.2-38 | |
