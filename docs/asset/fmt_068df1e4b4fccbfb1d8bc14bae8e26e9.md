
http://www.oracle.com/technwork/database/enterprise-edition/downloads

您可以随同完整的 Oracle Database 11g Release 2 版本一起下载卸载工具，或者作为归档文件下载。如需单独下载卸载工具，请点击“查看全部”（See All）链接以选择软件版本。

卸载工具使用您提供的信息以及从软件 home 收集的信息来创建参数文件。或者，您可以使用使用 `deinstall` 命令配合 `-checkonly` 标记和 `-o` 标记生成的参数文件。您也可以编辑响应文件来创建参数文件。

`Deinstall` 命令停止 Oracle 软件，并移除特定 Oracle home 操作系统上的 Oracle 软件和配置文件。如果您运行卸载工具来移除集群的 Oracle Grid Infrastructure 安装，则工具会提示您以 root 身份运行 `rootcrs` 脚本。

> 警告：当您运行 `deinstall` 命令时，如果中心清单（Inventory）中除了您正在配置和移除的 home 之外没有其他注册的 home，则 `deinstall` 命令将移除 Oracle RAC 基础安装用户下的以下文件和目录内容：
>
> - `admin`
> - `cfgptools`
> - `checkpoints`
> - `diag`
> - `oradata`
> - `flash_recovery_area`

Oracle 建议使用优化灵活架构（OFA）配置您的安装，并预留 Oracle base 和 Oracle home 路径供 Oracle 软件专门使用。如果您在 Oracle base 的这些位置中有任何由 Oracle 软件所有账户所属的用户数据，则 `deinstall` 命令将删除这些数据。

该命令使用以下语法，其中变量内容用斜体表示：

```
deinstall -home [Oracle home 的完整路径] [-silent] [-checkonly] [-local] [-paramfile [输入参数属性文件的完整路径]] [-params name1=value name2=value ...] [-o [保存文件的目录完整路径]]
```

运行卸载工具的默认方法是从 Grid home 中的 `deinstall` 目录运行的。例如：

```
$ cd /u01/app/11.2.0/grid/deinstall

$ ./deinstall
```

此外，您还可以从其他位置运行卸载工具，或使用参数文件运行，或选择其他选项运行该工具。

### 选项

- `-home`
  使用此标记指示您想要检查或重新安装的 Oracle home 路径。如需要在您计划卸载的 Oracle home 中使用 `deinstall` 命令移除 Oracle 软件，请在另一个位置提供参数文件，且不要使用 `-home` 标记。

- `-silent`
  如果您在 `$ORACLE_HOME/deinstall` 路径下运行 `deinstall`，则不需要 `-home` 标记，因为工具知道它是从哪个 home 运行的。如果您使用该工具的独立版本，则 `-silent` 是强制性的。
  要创建属性文件并提供所需的参数，请参考位于卸载工具或 Oracle home 响应（response）文件夹中的模板文件 `deinstall.rsp`。
  如果您有一个运行系统，与其使用模板文件，可以通过使用 `-checkonly` 标记运行 `deinstall` 命令来生成属性文件。然后 `deinstall` 命令将从您想要卸载和取消配置的 Oracle home 中发现信息。它会生成属性文件，您可以配合 `-silent` 选项使用它。

- `-checkonly`
  使用此标记检查 Oracle 软件 home 配置的状态。带有 `checkonly` 标记运行命令不会移除 Oracle 配置。

- `-local`
  在多节点非共享环境中使用此标记来取消集群中 Oracle 软件的配置。
  当您带有此标记运行 `deinstall` 时，它将对本地节点（运行 `deinstall` 的节点）的非共享目录进行取消配置并重新安装 Oracle 软件。在远程节点上，它会取消配置 Oracle 软件，但不会卸载 Oracle 软件。

- `-paramfile [输入参数文件的完整路径]`
  使用此标记在默认位置以外的位置使用参数文件运行重新安装。当使用此标记时，请提供参数文件所在的完整路径。如果您从计划卸载的 Oracle home 运行重新安装命令，则不需要使用 `-paramfile` 标记。
  参数文件的默认位置取决于 `deinstall` 的位置：
  - 来自安装介质或阶段位置：`$ORACLE_HOME/inventory/response`。
  - 来自 Oracle 技术网络 (OTN) 的解压归档文件：`/ziplocation/response`。
  - 安装后从 Oracle home 来自：`$ORACLE_HOME/deinstall/response`。

- `-params name1=value name2=value...`
  使用此标记配合参数文件覆盖您创建的参数文件中的一个或多个值。

- `-o [保存文件的目录完整路径]`
  使用此标记提供默认位置以外的路径来保存属性文件（`deinstall.rsp`）。
  参数文件的默认位置取决于 `deinstall` 的位置：
  - 从安装前的安装介质或阶段位置：`$ORACLE_HOME/inventory/response`。
  - 来自 OTN 的解压归档文件：`/ziplocation/response`。
  - 安装后从 Oracle home 来自：`$ORACLE_HOME/deinstall/response`。

- `-help`
  使用此标记获取有关命令的附加信息。

## 6.6.2 卸载之前的版本

如果您要在卸载之前的 release 运行 `deinstall` 命令，则必须以 root 用户身份更改之前的 release 权限并运行 `deinstall` 命令。例如：

```
# chmod 775 /u01/app/grid/11.2.0
```
这里的 `11.2.0` 是之前的 release home。

## 6.6.3 下载失败安装的卸载工具

您可以使用卸载工具（`deinstall`）来移除失败或不完整的安装。它是 Oracle 技术网络 (OTN) 提供的。
要下载卸载工具：
1. 访问 URL：`http://www.oracle.com/technwork/database/enterprise-edition/downloads`
2. 在 Oracle Database 11g Release 2 下，点击适用于您 way的“查看全部”（See All）。
卸载工具位于页面的末尾。

## 6.6.4 运行卸载工具

Oracle 建议使用优化灵活架构（OFA）配置您的安装，并预留 Oracle base 和 Oracle home 路径供 Oracle 软件专门使用。
在下载卸载工具后，请确保：
- 运行卸载工具的用户在所有节点上都是相同的
- 设置了用户等效

运行卸载工具请遵循以下步骤：
1. 将卸载工具下载到 grid 用户目录。
2. 验证 `deinstall` 二进制文件属于 grid 用户。
3. 运行卸载工具。

## 6.6.5 Clusterware 和 ASM 的 Deinstall 命令示例

当 `deinstall` 命令运行时，会提示提供要从系统中移除的 Oracle 软件 home 目录。按照提示提供附加信息。
从集群 Grid home 运行 `deinstall` 命令：

```
$ cd /u01/app/11.2.0/grid/deinstall

$ deinstall
```
您可以通过使用 `-checking` 标记运行 `deinstall` 命令在运行安装 home 之前生成参数文件，或者可以使用响应文件模板并手动编辑它来更改参数文件。

## 6.6.6 集群 Grid Infrastructure 的卸载参数文件

您可以使用 `-paramfile` 选项使用在参数文件中指定的值运行 `deinstall` 命令。以下是位于 node1 和 node2 的集群的参数文件示例，其中 Oracle Grid Infrastructure home (`grid`) 位于路径 `/u01/app/11.2.0/grid/`，Oracle Grid Infrastructure 的 base（包含 ASM 日志、Oracle Clusterware 日志和其他管理文件）为 `/u01/app/11.2.0/`，中心 Oracle Inventory (`oraInventory`) 为 `/u01/app/oraInventory`，虚拟 IP 地址 (VIP) 为 `192.0.2.2` 和 `192.0.2.4`，本地（您运行卸载会话的节点）来自 node1：

```
#Copyright (c) 2005, 2006 Oracle Corporation. All rights reserved.
```
