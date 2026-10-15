
# 配置打印机

```
# lpadmin -p <printername> \
-o dest=<accessname:port> \
-o protoc=<protoco>
```

4. 然后设置打印机的文件内容类型和打印机类型：

```
# lpadmin -p <printername> \
-I <content-type> \
-T <printer-type>
```

5. 添加打印过滤器：

```
# cd /etc/lp/fd
# for <filter> in *.fd;do
> name="${basename $<filter>}.fd"
> lpfilter -f $<name> -F $<filter>
> done
```

6. 启用打印机以接受打印作业：

```
# accept <printername>
# enable <printername>
```

7. 使用 `lpstat -p <printername>` 命令验证打印机的设置。

8. 如下一节所述，为网络打印机添加客户端访问。

## 添加打印机访问

要为打印客户端添加网络打印机访问，请遵循以下步骤：

1. 在终端窗口使用以下命令启动 Solaris 打印管理器：

```
# /usr/sadm/admin/bin/printmgr&
```

2. 在“选择名称服务”对话框中，选择名称服务并点击“确定”按钮。

3. 从“打印机”菜单中选择“添加打印机访问”命令。如图 10.6 所示，会出现“添加打印机访问”对话框。

4. 输入打印机名称、打印服务器名称以及打印机描述。

![](img/256e02a6afce528d264a8d911fa0ff20_434_0.png)

![](img/256e02a6afce528d264a8d911fa0ff20_434_1.png)

5. 如果希望所有打印作业默认发送到此打印机，请选中“默认打印机”复选框。

6. 点击“应用”按钮以继续添加打印机。或者点击“确定”按钮返回到主打印管理器窗口。

您将看到打印机已添加到打印管理器，并且该打印机的信息将被添加到相应的名称服务配置文件中。

若要使用命令行通过 LP 命令添加打印机访问，请输入以下内容：

```
# lpadmin -p flash -s sunserver
# lpadmin -p flash -D "First floor laser"
# lpadmin -p flash -d flash
# lpstat -p flash
```

printer flash is idle. enabled since Dec 20 10:50 2001 available.

前三行将打印机附加到打印服务器，添加描述，并设置打印机为默认。最后一行验证打印机是否在线。

您还可以使用本地打印客户端上的管理工具来添加对网络打印机的访问，方法如下：

1. 在终端窗口中给出 `admirin` 命令以在屏幕上打开管理工具。

2. 选择“浏览”菜单上的“打印机”命令以查看打印机窗口。

3. 从“编辑”菜单的“添加”子菜单中选择“打印机访问”命令。如图 10.7 所示，会出现“添加打印机访问”对话框。

4. 输入打印机名称、打印服务器名称和描述，然后打开或关闭“默认打印机”复选框。

5. 点击“应用”按钮以继续添加打印机。或者点击“确定”按钮返回到主管理工具窗口。

您将看到打印机已添加到管理工具。不会对名称服务列表进行任何更改。

## 连接打印服务器

将打印机连接到打印服务器的过程与刚才显示的添加网络打印机的步骤类似。除了已经为打印机访问请求的信息外，您还需要提供以下额外信息：打印机端口、文件内容、故障通知策略、横幅的打印策略以及用户访问列表。

## 图 10.7

*管理工具（Admintool）的“添加打印机访问权限”对话框*

![](img/256e02a6afce528d264a8d911fa0ff20_436_0.png)

按照以下步骤向打印服务器添加新的连接式打印机（attached printer）：

1. 启动 Solaris 打印管理器（参见“添加打印机访问权限”）。

2. 从“打印机”菜单中选择“新连接式打印机”命令。此时会出现“新连接式打印机”对话框。

3. 输入打印机名称，并选择打印机端口、打印机类型、文件内容以及故障通知选项。设置默认打印机和始终打印横幅页选项。

4. 在“用户访问列表”列表框中，输入用户或组的名称，或者输入 `all`（全部）以表示所有用户。

5. 单击“应用”按钮以继续添加其他连接式打印机。或者单击“确定”按钮返回到主打印管理器窗口。

您将看到连接式打印机已被添加到打印管理器中，并且该打印机的信息会被添加到相应的配置文件中。

最后，使用 `lp -d <printname> <filename>` 命令打印测试文件，以测试网络打印机是否已正确连接。

您可以在命令行输入以下命令序列来连接打印机并为打印服务器设置其属性：

```bash
# chown lp /dev/term/b
# chmod 600 /dev/term/b
# lpadmin -p flash -v /dev/term/b
# lpadmin -p flash -T PS
# lpadmin -p flash -I postscript
# cd /etc/lp/pd
# for <filter> in *fd;do
> name=basename $<filter> .fd'
> lpfilter -f $name -F $<filter>
# accept flash
destination 'flash' now accepting requests
# enable flash
printer 'flash' now enabled
# lpadmin -p flash -D 'First floor laser'
# lpstat -p flash
printer flash is idle. enabled since Dec 20 10:50 2001.
available.
```

在上面的命令序列中，第二行授予 LP 打印服务对该端口的所有权，以便其他进程无法访问该端口。第 4 行设置打印机类型，第 5 行设置文件内容类型（PS）。第 7 行至第 9 行为打印服务器设置打印过滤器。`-D` 选项用于设置描述，最后两行（以 `lpstat` 开头）显示打印机已准备就绪，可以打印。

最后，您可以使用非常相似的过程向网络中其他位置的打印服务器添加新的网络打印机（非连接式）。除了为打印服务器添加连接式打印机所需的所有参数外，您还需要指定目标和协议。对于由打印服务器服务的非连接式网络打印机，您不需要指定端口地址。

要将新的连接式打印机添加到打印服务器，请遵循以下步骤：

1. 启动 Solaris 打印管理器。

2. 从“打印机”菜单中选择“新网络打印机”命令。此时会出现如图 10.8 所示的“新网络打印机”对话框。

3. 输入打印机名称和描述，并为打印机类型、文件内容、故障通知、目标和协议选择正确的设置。与此前一样，使用相应的复选框来设置默认打印机和始终打印横幅页的行为。

4. 在“用户访问列表”列表框中，输入用户或组的名称，或者输入 `all` 以表示所有用户。

5. 单击“应用”按钮以继续添加其他网络打印机。或者单击“确定”按钮返回到主打印管理器窗口。

您将看到网络打印机已被添加到打印管理器中，并且该打印机的信息会被添加到相应的配置文件中。

![](img/256e02a6afce528d264a8d911fa0ff20_438_0.png)

## 图 10.8

新网络打印机对话框

### 打印文件

您可以使用 CDE 前面板上的“默认打印”控件在 Solaris 桌面上打印文件。只需将文件从文件管理器的任一窗口拖放到前面板上的打印机控件即可。

在命令行中，您使用 `lp` 命令进行打印。当使用 `lp` 命令指定打印作业时，该作业会被放入指定打印机的 LP 打印服务打印队列中，系统返回请求 ID 号，并且刷新 shell 提示符。当不指定打印机时，`lp` 命令使用默认打印机。在这种情况下，命令简单输入为 `lp <Filename>`。当打印作业完成时，Solaris 会向发起打印请求的用户发送电子邮件。

当您希望指定除默认打印机以外的打印机时，请使用以下命令：

```bash
$ lp -d flash /<mydirectory>/<myfile name>
```

Solaris 返回的输出类似于以下内容：

```text
Request id is flash-7 (1 file)
$
```

如果您打印到系统中不可用的打印机，Solaris 将显示以下错误消息：

```text
$ lp -d spot /<mydirectory>/<myfilename>
UX:lp: ERROR: Destination `spot' is unknown to the LP print
service
$
```

`lp` 命令接受以下选项：
