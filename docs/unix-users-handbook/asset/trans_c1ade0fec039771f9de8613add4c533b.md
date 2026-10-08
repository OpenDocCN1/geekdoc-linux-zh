

![](img/75f39fc91296b889c0653851accdfd46_1298_0.png)

**图 19-2** *已暂停 Net Logon 服务的服务对话框*

我们现在可以使用以下 NET CONTINUE 命令恢复 *Net Logon* 服务：

```
C:\NET CONTINUE NTLOGON
```

*Net Logon 服务已成功恢复。*

## NET FILE

**NET FILE** - 该命令用于列出和关闭打开的文件。

以下是 **NET FILE** 命令的摘要。

```
C:\ NET FILE /?

NET FILE   [id [/CLOSE]]
```

以下是一些常用选项：

- *id* - 指定要查看的文件的标识号。
- *id /CLOSE* - 关闭由 *id* 号指定的文件。

以下示例展示了不带选项发出 **NET FILE** 命令：

```
C:\ NET FILE

ID          Path                            User name          # Locks

----------  ------------------------------  ----------------  -------
97          C:\tiff_map_proj\sql             leung_k            0
147         \\PIPE\samr                     administrator      0
149         \\PIPE\lsarpc                   administrator      0

命令成功完成。
```

此输出显示了服务器上的打开文件。您可以关闭其中一个共享文件或移除该文件的锁定。

## NET GROUP

**NET GROUP** - 该命令显示并允许您在服务器上操作组。如果不指定任何选项，此命令将列出组。

以下是 **NET GROUP** 命令的摘要。

```
C:\ NET GROUP /?

NET GROUP [groupname [[/COMMENT:"text"]] [/DOMAIN]
          groupname [/ADD [[/COMMENT:"text"]] | [/DELETE]] [/DOMAIN]
          groupname username [...] [/ADD | /DELETE] [/DOMAIN]
```

以下是一些常用选项：

- **/ADD** - 将组添加到域或将 *用户名* 添加到组。
- **/DELETE** - 从域中删除组或从组中删除 *用户名*。
- **groupname** - 指定操作的 *组名*。如果没有选项，将显示属于该组的用户。您还可以将 *ADD* 或 *DELETE* 选项与 *groupname* 一起使用，以指定要添加到组中的 *用户名*。
- **/COMMENT:"text"** - 将此注释添加到 *groupname*。
- **/DOMAIN** - 操作将在主域控制器上执行。此选项是 Windows 服务器系统的默认设置。
- **username** - 此用户将被添加或从组中移除。可以指定任意数量的用户。

以下示例展示了发出 NET GROUP 命令以添加组 *hp consultants*：

```
C:\ NET GROUP "hp consultants" /ADD
该请求将在域 NSDNIS 的主域控制器上处理。
命令成功完成。
```

接下来，我们在本地系统中将用户 *marty* 添加到组 *hp consultants*：

```
C:\ NET GROUP "hp consultants" marty /ADD
该请求将在域 NSDNIS 的主域控制器上处理。
命令成功完成。
```

接下来，我们为 *hp consultants* 添加注释：

```
C:\ NET GROUP "hp consultants" /COMMENT:"Group For HP Consultants"
该请求将在域 NSDNIS 的主域控制器上处理。
命令成功完成。
```

我们现在可以通过查看与组 *hp consultants* 关联的我们添加的信息来检查我们的工作成果：

```
C:\ NET GROUP "hp consultants"

Group name    hp consultants
Comment       Group For HP Consultants

成员
--------------------------------------------------------------
marty
命令成功完成。
```

此输出确认我们已创建组 *hp consultants*，*marty* 是该组的成员，并且我们的注释确实已与该组关联。

## NET HELP

**NET HELP** - 使用此命令获取任何 NET 命令的帮助。

一个常用选项如下：

NET HELP command \| more - 这提供有关您指定的 *命令* 的信息。

以下示例展示了发出 **NET HELP** 命令以获取可用帮助的命令列表：

```
C:\ NET HELP
此命令的语法为：
NET HELP_command
或者
NET command /HELP
可用命令如下：
NET ACCOUNTS      NET HELP          NET SHARE
NET COMPUTER      NET HELPMSG       NET START
NET CONFIG        NET LOCALGROUP    NET STATISTICS
NET CONFIG SERVER NET NAME          NET STOP
NET CONFIG WORKSTATION NET PAUSE    NET TIME
NET CONTINUE      NET PRINT         NET USE
NET FILE          NET SEND          NET USER
NET GROUP         NET SESSION       NET VIEW
NET HELP SERVICES 列出您可以启动的网络服务。
NET HELP SYNTAX 解释如何阅读 NET HELP 语法行。
NET HELP command \| MORE 一次显示一屏帮助。
```

以下示例展示了发出 **NET HELP** 命令以获取有关 **NET GROUP** 命令的信息：

```
C:\ NET HELP NET GROUP
此命令的语法为：
NET GROUP  [groupname [[/COMMENT:"text"]] [/DOMAIN]
          groupname [/ADD [[/COMMENT:"text"]] | [/DELETE]] [/DOMAIN]
          groupname username [...] [/ADD | /DELETE] [/DOMAIN]
NET GROUP 在服务器上添加、显示或修改全局组。
如果没有参数，它将显示服务器上的组名。
```

**参数：**

*groupname*  
是添加、扩展或删除的组的名称。  
仅提供一个组名以查看组中的用户列表。

*/COMMENT:"text"*  
为新组或现有组添加注释。  
注释最多可以包含 48 个字符。用引号将文本括起来。

*/DOMAIN*  
在当前域的主域控制器上执行操作。否则，操作将在本地计算机上执行。  
此参数仅适用于属于 Windows Server 域的 Windows 工作站计算机。默认情况下，Windows Server 计算机在主域控制器上执行操作。

*username[...] *  
列出要添加到组中或从组中移除的一个或多个用户名。用空格分隔多个用户名条目。

*/ADD*  
添加组，或将用户名添加到组中。

*/DELETE*  
删除组，或将用户名从组中移除。

NET HELP command | MORE 一次显示一屏帮助。

## NET HELPMSG

**NET HELPMSG** - 获取四位网络消息代码的信息。仅使用四位数字来获取代码的信息。

以下是 **NET HELPMSG** 命令的格式：

```
NET HELPMSG message#
```

以下命令展示了发出 **NET GROUP** 命令以向系统添加组。发出此命令后，会提供一个错误编号：

```
C:\ NET GROUP "hp consultants" /ADD
该组已存在。
更多帮助可通过输入 NET HELPMSG 2233 获取。
```

我们现在可以使用 **NET HELPMSG** 命令获取关于特定四位代码的信息：

```
C:\ NET HELPMSG 2223
该组已存在。
解释
您尝试创建一个组名已存在的组。
操作
为新组使用不同的组名。要显示服务器上已建立的组名列表，请键入：
NET GROUP
```

## NET LOCALGROUP

**NET LOCALGROUP** - 该命令显示并允许您在计算机上操作组。如果不指定任何选项，此命令将列出组。

以下是 **NET LOCALGROUP** 命令的摘要。

```
C:\> NET LOCALGROUP /?

NET LOCALGROUP [groupname [[/COMMENT:"text"]] [DOMAIN]
              groupname [/ADD [][/COMMENT:"text"] | [/DELETE)] [(/DOMAIN]
              groupname name [...] [/ADD | /DELETE] [][/DOMAIN]
```

以下是一些常用选项：

- **/ADD** - 将组添加到域或将 *用户名* 添加到组。
- **/DELETE** - 从域中删除组或从组中删除 *用户名*。
- **groupname** - 指定操作的 *groupname*。如果没有选项，将显示属于本地组的用户。您还可以将 *ADD* 或 *DELETE* 选项与 *groupname* 一起使用，以指定要添加到组中的 *用户名*。
- **/COMMENT:"text"** - 将此注释添加到 *groupname*。
- **/DOMAIN** - 操作将在主域控制器上执行。如果不使用此选项，操作将在本地计算机上进行。这是 Windows 服务器系统的默认设置。
- **name** - 这是要添加或从组中移除的用户名或组名。可以指定任意数量。

