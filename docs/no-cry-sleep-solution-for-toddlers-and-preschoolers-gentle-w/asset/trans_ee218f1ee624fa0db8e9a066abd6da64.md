

你也可以为服务设置启动运行级别，就像使用 chkconfig 一样，不过你只能使用 3、4 和 5 级。已勾选的条目列表取决于你在“编辑运行级别”菜单中选择的运行级别。实际上，你是在选择在给定运行级别下启动哪些服务。默认是运行级别 5，即图形界面启动级别。你可能希望在运行级别 3，即命令行启动级别下启动或停止不同的服务集。在这种情况下，你可以从“编辑运行级别”菜单中选择运行级别 3，以显示运行级别 3 的服务，其复选框已被选中。

## chkconfig

你可以使用 chkconfig 命令指定要启动的服务以及要启动它的级别。与其他服务管理工具不同，chkconfig 对独立服务和 xinetd 服务都同样适用。虽然独立服务可以在任何运行级别下运行，但你也可以为 xinetd 运行的运行级别打开或关闭 xinetd 服务。表 20-3 列出了不同的 chkconfig 选项。

### 使用 chkconfig 列出服务

要查看服务列表，请使用 --list 选项。以下是 chkconfig 管理的部分服务示例。服务在每个运行级别的开启或关闭状态显示如下：xinetd 服务及其状态也显示如下：

```
chkconfig --list
dhcpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
httpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
named 0:off 1:off 2:off 3:off 4:off 5:off 6:off
lpd 0:off 1:off 2:on 3:on 4:on 5:on 6:off
nfs 0:off 1:off 2:off 3:off 4:off 5:off 6:off
crond 0:off 1:off 2:on 3:on 4:on 5:on 6:off
xinetd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
xinetd based services:
  time: off
  finger: off
  pop3s: off
  swat: on
```

### 使用 chkconfig 启动和停止服务

你使用 on 选项使服务在指定的运行级别启动，使用 off 选项禁用它。你可以使用 --level 选项指定要影响的运行级别。如果未指定级别，chkconfig 将使用服务 init.d 启动脚本中的任何 chkconfig 默认信息。Red Hat 已为其服务预先填入 chkconfig 默认信息（如果缺少此信息，chkconfig 将使用运行级别 3、4 和 5）。以下示例使 Web 服务器（httpd）在运行级别 5 启动：

```
chkconfig --level 5 httpd on
```

off 选项将服务配置为在系统进入指定运行级别时关闭。下一个示例在进入运行级别 3 时关闭 Web 服务器。如果服务未运行，则保持关闭状态：

```
chkconfig --level 3 httpd off
```

## TABLE 20-3
chkconfig 选项

| 选项 | 描述 |
|---|---|
| --level runlevel | 指定要打开、关闭或重置服务的运行级别。 |
| --list service | 列出不同运行级别下服务的启动信息。xinetd 服务仅为开启或关闭。无参数时，列出所有服务，包括 xinetd 服务。 |
| --add service | 添加服务，在默认指定的运行级别（或如果未指定则所有运行级别）中创建链接。 |
| --del service | 删除服务在所有运行级别目录中的所有链接（启动和关闭）。 |
| service on | 打开服务，在指定的或默认运行级别目录中创建启动链接。 |
| service off | 关闭服务，在指定的或默认目录中创建关闭链接。 |
| service reset | 重置服务启动信息，根据服务 init.d 启动脚本中的 chkconfig 条目创建默认链接。 |

reset 选项将服务恢复为其在服务 init.d 启动脚本中指定的 chkconfig 默认选项：

```
chkconfig httpd reset
```

要仅查看服务的启动信息，你只需使用 --list 选项并加上服务名称：

```
chkconfig --list httpd
httpd 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

### 使用 chkconfig 启用和禁用 xinetd 服务

与 redhat-config-services 不同，chkconfig 还可以启用或禁用 xinetd 服务。只需输入 xinetd 服务并使用 on 或 off 选项即可。服务将被启动或关闭，并且其在 /etc/xinetd.d 目录中的 xinetd 配置脚本中的 disable 行会相应地编辑。例如，要启动 Samba 配置服务器 swat，该服务器运行于 xinetd，只需输入：

```
chkconfig swat on
chkconfig --list swat
          swat           on
```

xinetd 的 swat 配置文件 /etc/xinetd.d/swat 中的 disable 行将被编辑为 no，如下所示：

```
disable=no
```
