

DAS_CONTACT_LIST      = REMOTE
DAS_CONTACT_LIST_HOSTNAME  = udb1nx01
DAS_SMTP_SERVER       = null
* DAS user
DAS_USERNAME          = dasusr1
DAS_GROUP_NAME        = dasadm1
DAS_HOME_DIRECTORY    = /home/dasusr1
DAS_PASSWORD          = 235262333285355231346
ENCRYPTED             = DAS_PASSWORD
*----------------------------------------
* Installed Languages
*----------------------------------------
LANG                  = EN

> 提示：从文件系统网络驱动器执行响应文件安装比从 CD-ROM 驱动器快得多。如果您计划安装多个客户端，应在代码服务器上设置挂载的文件系统以提高性能。

要执行响应文件安装，请找到 db2ese2.rsp 文件并执行以下操作：

+   1. 以 root 身份，使用以下格式输入 db2setup 命令：
+   `<cd-rom>/db2setup -r <responsefile_directory>/<response_file>`
+   其中：
+   - `<cd-rom>` 表示 DB2 安装映像的位置；
+   - `<responsefile_directory>` 表示响应文件所在的目录；以及
+   - `<response_file>` 表示响应文件的名称（例如，db2ese2.rsp）。

在我们的设置中，DB2 安装映像位于 /software，响应文件 db2ese2.rsp 位于 /db2home。因此，我们在 /software 中执行了以下命令：

```
[root@udb1nx01]/# ./db2setup -r /db2home/db2ese2.rsp
```

+   2. 安装完成后，检查安装日志以确保未发生错误。主要的安装日志文件是 /tmp/db2setup.log。

## 使用示例响应文件安装 DB2

另一种在多个物理节点上安装 DB2 的方法是对示例响应文件进行编辑，并使用此文件在集群中的每台机器上安装 DB2。示例响应文件对于单分区安装也很有用，如果您想绕过图形向导，同时利用 DB2 Setup 的配置功能。

## 使用示例响应文件创建响应文件

DB2 CD-ROM 包含一个即用型示例响应文件，其中包含默认条目。该文件名为 db2ese.rsp，位于：

```
`<cd-rom>/db2/linux/samples`
```

其中，`<cd-rom>` 表示 DB2 安装映像的位置。该目录还包含 Application Development Client 和 Administration Client 的示例响应文件，分别命名为 *db2adcl.rsp* 和 *db2admcl.rsp*。

要从示例创建自己的响应文件，您必须将示例响应文件复制到本地文件系统并对其进行编辑。

+   - 通过删除关键字左侧的星号 (*) 来激活响应文件中的项目，然后用新设置覆盖默认设置。可能的设置范围列在等号右侧。请参阅“Administration”指南（在第 301 页的“Other publications”中列出）以获取配置这些参数的指导。
+   - 将文件保存在导出的文件系统上（例如，/software），网络上的每个人都可以使用。

## 使用响应文件安装 DB2

+   - 以 root 身份发出 `db2setup -r` 命令执行安装。例如，如果 DB2 安装映像位于 /software，而 db2ese.rsp 响应文件位于 /db2home，则以 root 身份输入以下命令：

```
`/software/db2setup -r /db2home/db2ese.rsp`
```

您的自定义响应文件由您决定。要让您了解最终产品，以下响应文件是由 DB2 Setup 向导生成的：

```
*>-----------------------------------------------------
* Generated response file used by the DB2 Setup wizard
* generation time: 10/18/02 11:51 AM
*>-----------------------------------------------------
* Product Installation LIC_AGREEMENT = ACCEPT
PROD = ENTERPRISE_SERVER_EDITION
INSTALL_TYPE = TYPICAL
*>-----------------------------------------------------
*
Das properties
*>-----------------------------------------------------
DAS_CONTACT_LIST = LOCAL
* DAS user
DAS_USERNAME = dasusr1
DAS_GROUP_NAME = dasadm1
```
