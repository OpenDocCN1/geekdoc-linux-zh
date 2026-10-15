

2. 选择 From a file 选项并选择适当的目录。如果您购买了完全授权的 DB2 产品，db2ese.lic 许可证文件位于 /cdrom/db2/1/license，其中 /cdrom 是您的 CD-ROM 的根目录。单击 OK。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_142_0.png)

图 3-30 添加许可证文件

要删除许可证文件，请从 License 菜单中选择 Remove。

## 设置 Registered user 策略

如果您购买了 Registered User 许可证，则需要将 Registered users 添加到 Registered users 列表中。操作方法如下：

- 1. 从 License 菜单中选择 Change。
- 2. 勾选 Registered DB2 Connect users 旁边的框，然后按 OK。这将启用 License Center 中的 Users 选项卡。
- 3. 在 License Center 中选择 Users 选项卡，然后单击 Add。输入用户 ID 并单击 Apply。添加完所有 Registered users 后，单击 OK。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_143_0.png)

图 3-31 添加 Registered users

## 更新许可处理器数量

要更改 DB2 产品的许可处理器数量，请执行以下操作：

- 1. 从 License 菜单中选择 Change。
- 2. 在 Number of licensed processors 框中，使用上下箭头设置数量，然后单击 OK。

## 更改执行策略

默认执行策略是 Soft Stop。这意味着即使违反许可证策略，所有对 DB2 数据库的连接仍会通过。当发生违规时，会将许可证违规消息写入 db2diag.log。Hard Stop 执行策略不允许任何违反许可证策略的连接。要指定执行策略类型，请执行以下操作：

- 1. 从 License 菜单中选择 Change。
- 2. 在 Enforcement policy 下选择适当的单选按钮。

## 3.7.2 db2licm 和 db2licd

db2licm 和 db2licd 实用程序是管理许可的命令行工具。db2licm 命令用于查看许可证信息、添加和删除许可证密钥、指定用户和执行策略以及指定许可处理器数量。db2licd 实用程序显示当前用户的连接信息。

要查看所有许可信息，请输入 db2licm -l。例如，这是我们的输出：

```
db2inst1@db2lnx03:~/sqllib> db2licm -l
Product Name                = "DB2 Enterprise Server"
Edition                      = ""
Product Password             = "DB2ESE"
Version Information          = "8.1"
Expiry Date                  = "Permanent"
Registered User Policy       = "Enabled"
Number Of Entitled Users     = "5"
Enforcement Policy           = "Soft Stop"
Number of processors         = "1"
Number of licensed processors = "1"
Annotation                   = ""
Other information            = ""
```

要查看当前已连接用户的连接信息，请运行 db2licd：

```
db2licd -q
```

## 安装许可证密钥

要安装许可证密钥，必须使用 db2licm 命令添加 db2ese.lic 许可证文件。要添加 DB2 许可证文件：

- 1. 以实例所有者身份登录。
- 2. 输入以下命令：
  /opt/IBM/db2/V8.1/adm/db2licm -a <filename>

其中，filename 是 DB2 ESE 许可证文件 db2ese.lic 的完整路径名和文件名。该许可证文件位于 CD-ROM 根目录的 /db2/license 中。例如，如果 CD-ROM 挂载在 /cdrom 目录中，请输入以下命令：

```
/opt/IBM/db2/V8.1/adm/db2licm -a /cdrom/db2/license/db2ese.lic
```

如果您设置的是多分区数据库系统，请在每台机器上执行此任务。

在 Linux 上，DB2 许可证密钥位于 /var/lum 中的一个名为 nodelock 的文件中。

要删除许可证文件，请使用 db2licm -r。例如：db2licm -r db2ese。

## 设置 Registered user 策略

如果您的公司购买了 Registered user 许可证，请执行此任务。

- 1. 以实例所有者身份登录。
- 2. 通过输入以下命令启用 DB2 ESE 的 Registered users 策略：

```
db2licm -p db2ese registered
```

- 3. 进入 /opt/IBM/db2/V8.1/misc 目录。
- 4. 在此目录中，创建一个名为 db2ese.reg 的文本文件。使用文本编辑器，将注册用户条目添加到此文件中。例如：

```
db2inst1
user2
user3
```

- 5. 重新启动 db2licd 进程以使更改生效

运行以下命令停止许可证守护进程：

```
db2licd -end
```

许可证守护进程将在连接请求或许可证中心更新期间自动重新启动，此时需要 db2licd。

## 更新许可处理器数量

使用 db2licm -n 命令。例如，要将许可处理器数量更改为 4，请输入以下命令：

```
db2licm -n db2ese 4
```

## 更改执行策略

默认执行策略是 Soft Stop。这意味着即使违反许可证策略，所有对 DB2 数据库的连接仍会通过。当发生违规时，会将许可证违规消息写入 db2diag.log。Hard Stop 执行策略不允许任何违反许可证策略的连接。要将执行策略从 Soft Stop 更改为 Hard Stop，请输入以下命令：

```
db2licm -e db2ese HARD
```

同样，要将执行策略从 Hard Stop 更改为 Soft Stop，请输入：

```
db2licm -e db2ese SOFT
```

