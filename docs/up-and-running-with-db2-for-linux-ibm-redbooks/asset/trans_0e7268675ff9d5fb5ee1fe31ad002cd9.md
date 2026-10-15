

| 所需用户 | 用户名 | 组名 | 描述 |
|---|---|---|---|
| 实例所有者 | db2inst1 | db2iadm1 | 管理实例 |
| 受限用户 | db2fenc1 | db2iadm1 | 负责执行受限用户定义函数，例如 UDF 和存储过程。 |
| DAS 用户 | dasusr1 | db2asgrp | 管理 DB2 Administration Server |

## 创建用户

您必须具有 root 权限才能创建用户和组。创建 DB2 用户 ID 有三种方法：(1) 使用 DB2 Setup 向导，(2) 响应文件或 (3) 手动使用命令行。

- 1. DB2 Setup Wizard

DB2 Setup 向导在安装期间为您创建所有必需的用户和组。创建的默认用户和组显示在表 2-8 中。DB2 Setup 还允许您指定自己的用户和组名称。

- 2. Response file

如果在响应文件中指定用户和组信息，也可以在响应文件安装期间创建用户。例如，以下响应文件中的条目为 DB2 创建了三个必需的用户和组：

Example 2-10 Using a response file to create users and groups

```
* DAS user
DAS_USERNAME = dasusr1
DAS_GROUP_NAME = dasadm1
DAS_HOME_DIRECTORY = /home/dasusr1
DAS_PASSWORD = 23526233328355231346
ENCRYPTED = DAS_PASSWORD
* Instance-owning user
inst1.NAME = db2inst1
inst1.GROUP_NAME = db2grp1
inst1.HOME_DIRECTORY = /db2home/db2inst1
inst1.PASSWORD = 23526233328355231346
```

```
ENCRYPTED = inst1.PASSWORD
inst1.AUTOSTART = YES
inst1.AUTHENTICATION = SERVER
inst1.SVCNAME = db2c_db2inst1
inst1.PORT_NUMBER = 50001
inst1.FCM_PORT_NUMBER = 60000
inst1.MAX_LOGICAL_NODES = 4
* fenced user
inst1.FENCED_USERNAME = db2fenc1
inst1.FENCED_GROUP_NAME = db2fgrp1
inst1.FENCED_HOME_DIRECTORY = /db2home/db2fenc1
inst1.FENCED_PASSWORD = 235262333285355231346
ENCRYPTED = inst1.FENCED_PASSWORD
```

3. Manually using command line. To use this method, follow these steps:

- a. Log on to your machine as root.

- b. Create groups for the instance owner, the fenced user and the DAS user by using the following commands:

```
groupadd -g 999 db2iadm1
groupadd -g 998 db2fadm1
groupadd -g 997 db2asgrp
```

在我们的设置中我们使用了数字 997、998 和 999。请确保您选择的数字在机器上尚未存在。

- c. Create a user that belongs to each group and specify the home directory. We chose to place all home directories in /db2home by entering the following commands:

```
useradd -u 1004 -g db2iadm1 -m -d /db2home/db2inst1 db2inst1 -p password1
useradd -u 1003 -g db2fadm1 -m -d /db2home/db2fenc1 db2fenc1 -p password2
useradd -u 1002 -g db2asgrp -m -d /db2home/dasusr1 dasusr1 -p password3
```

- d. As root user, set a password for each user that you created by entering the following commands:

```
passwd db2inst1
passwd db2fenc1
passwd dasusr1
```

## 创建用户：多分区注意事项

在分区数据库环境中，您只需要为实例所有者和受限用户创建一个共享主目录（但请记住要在每台机器上创建用户！）。在分区环境中创建用户时，请确保用户和组 ID 在每台机器上相同。在我们的设置中我们有：

- 实例所有者机器上的共享主目录 /db2home，该目录通过 NFS 挂载到集群中的其余机器上。在此目录中我们有实例所有者用户和受限用户的主目录：db2inst1 和 db2fenc1。

- 每台机器上 DAS 用户的本地主目录 dasusr1，存储在 /home 目录中。

我们无法将 DAS 用户主目录放在共享文件夹中，因为我们在集群中的每台机器上都有相同的 DAS 用户 ID。DB2 Administration Server (DAS) 在 DB2 Version 8 中发生了显著变化；因此，您应注意以下 DAS 用户注意事项。

## 分区数据库的 DAS 用户注意事项

- 分区数据库中的每台物理机器上必须运行一个 DAS，以便图形化管理工具（例如 Control Center）能够工作。

- 每台机器上只能有一个 V8 DAS（尽管 V7 和 V8 DAS 可以共存于一台机器上）。

- 就像实例一样，每个 DAS 必须在用户 ID 下创建。无论环境中使用不同的用户 ID 为每个 DAS，还是使用相同的用户 ID 且该用户 ID 的主目录不共享，都无关紧要。（后者是我们环境的情况——我们在每台机器上都有一个单独的用户 ID dasusr1，每个都有自己的本地主目录 dasusr1。它工作得很好）。

- 如果要在每台机器上使用相同的用户 ID，则该用户 ID 的主目录不能与其他机器共享。

- 如果为每个 DAS 使用不同的用户 ID，则所使用的用户 ID 的主目录可以共享。

- 如果使用现有用户作为 DAS 用户，则在安装之前该用户必须存在于所有参与计算机上。

- 对于响应文件安装：如果您的响应文件指定在集群中的每台机器上创建新的 DAS 用户，并且该用户已存在于任何参与计算机上，则该用户必须具有与新的 DAS 用户相同的初级组。

