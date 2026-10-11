
# 安装日志

```
检查依赖项...
Glibc version >= 2.1.2...OK
Libjpeg version >= 6.2.0...OK
Libgtk version >= 1.2.0...OK
```

您正在运行带有 glibc-2.1 的 x86 机器
随时按 `Control-C` 均取消此安装程序。

## 许可条款

许可协议将在此处显示，但由于空间限制已移除。

Scotts Valley, 95066-3249
您同意许可协议吗？[Y/n] Y
您想阅读 `/mnt/cdrom/README` 文件吗？[Y/n] Y

发布说明将在此处显示，但由于空间限制已移除。

请输入安装路径 `[/usr/local/kylix2]` `/opt/kylix2`
请输入创建符号链接的路径 `[/usr/local/bin]`
安装主程序文件？[Y/n] Y
安装 dbExpress（包括 InterBase 和 MySQL 驱动程序）？[Y/n] Y
安装 dbExpress Oracle 驱动程序？[Y/n] Y
安装 dbExpress DB2 驱动程序？[Y/n] Y
安装 dbExpress Informix 驱动程序？[Y/n] Y
安装帮助文件？[Y/n] Y
安装 Internet组件？[Y/n] Y
安装 WebSnap？[Y/n] Y
安装 Mozilla Preview Widget？[Y/n] Y
安装 Web Services？[Y/n] Y
安装 VisiBroker/CORBA 组件？[N/y] Y (默认 N)
您是否要安装 GNOME/KDE 菜单项？[Y/n] Y
安装到 `/opt/kylix`
5641 MB 可用，将安装 243 MB。

继续安装？[Y/n]
安装主程序文件 ...
100% - setup/data/packages/kylix2_main_program_files-1.0-1.i386.rpm
100% - setup/data/packages/kylix2_ide-1.0-1.i386.rpm
0% - 执行脚本
安装 dbExpress（包括 InterBase 和 MySQL 驱动程序）...
100% - setup/data/packages/kylix2_db_express-1.0-1.i386.rpm
安装 dbExpress Oracle 驱动程序 ...
100% - setup/data/packages/kylix2_db_oracle-1.0-1.i386.rpm
安装 dbExpress DB2 驱动程序 ...
100% - setup/data/packages/kylix2_db_db2-1.0-1.i386.rpm
安装 dbExpress Informix 驱动程序 ...
100% - setup/data/packages/kylix2_db_informix-1.0-1.i386.rpm
安装帮助文件 ...

100% - setup.data/packages/kylix2_help_files-1.0-1.i386.rpm
0% - 运行脚本
正在安装 Internet Components ...

100% - setup.data/packages/kylix2_internet-1.0-1.i386.rpm
0% - 运行脚本
正在安装 WebSnap ...

100% - setup.data/packages/kylix2_web_snap-1.0-1.i386.rpm
0% - 运行脚本
正在安装 Mozilla Preview Widget ...

100% - setup.data/packages/kylix2_mozilla-1.0-1.i386.rpm
0% - 运行脚本
正在安装 Web Services ...

100% - setup.data/packages/kylix2_web_services-1.0-1.i386.rpm
0% - 运行脚本
正在安装 VisiBroker/CORBA Components ...

100% - setup.data/packages/kylix2_visicorba-1.0-1.i386.rpm
0% - 运行脚本

100% - `/opt/kylix2/README`
100% - `/opt/kylix2/license.txt`

> **** 重要提示 ****
如果您安装了 GNOME/KDE 菜单项，请重启 X Windows 以使菜单项出现。

> 为确保运行环境设置妥当，请始终从 GNOME/KDE 菜单启动 Kylix，或使用此命令：`"startkylix"`。

图形化安装需要与非图形化安装相同的信息。Kylix 1 用户应注意，当作为 root 用户安装时，默认安装路径为 `/root/kylix`。

在安装 Kylix 过程中，安装程序会显示进度条。一个非常实用的功能是，在安装程序正在执行工作期间，View Readme（查看说明）按钮也是启用的。

无论如何进行安装，选项都是相同的。下表列出了需要进一步说明的选项摘要。

| 安装选项 | 描述 |

> **警告：** 建议以 root 用户身份安装 Kylix。然而，以 root 用户身份运行 Kylix 是非常危险的。相反，请作为普通用户运行 Kylix。

## 安装后配置与测试

安装好 Kylix 后，在情况允许的情况下退出 root shell。在首次启动 Kylix 之前，请在名为名为 `.bashrc` 的文件中添加一个条目。注意文件名前的点（.`）。该文件在每次启动新 shell 时都会被执行。只需在该文件中添加一行即可让操作变得更方便，它设置了从命令行编译以及运行需要某些共享对象文件的应用程序所需的环境变量。这些所需文件将在附录 A“部署 Kylix 应用程序”中详细讨论。

使用不带参数的 `cd` 命令切换到主目录。编辑 `.bashrc` 以包含以下行：

```
source <installation Kylix path>/bin/kylixpath
# 下行仅在你安装了 Visibroker/
# CORBA 组件时才需要
source <installation Kylix root path>/vbroker/vbroker.sh
```

其中 `<installation Kylix root path>` 是 `/opt/kylix2` 或 `/usr/kylix2` 或 Kylix 安装的任何目录。保存文件并退出编辑器。现在退出 shell 并打开一个新 shell。你应该会看到类似下面的信息：

`PATH` 现在已设置为：
`/opt/kylix2/bin:/opt/kylix2/lib:/opt/kylix2/help:/opt/kylix2/vbroker:/usr/local/bin:/bin:/bin:/0/usr/X11R6/bin`

`LD_LIBRARY_PATH` 现在已设置为：
`/opt/kylix2/bin:/opt/kylix2/vbroker:`

`XPPATH` 现在已设置为：
`/opt/kylix2/help/xprinter`

`HOME` 现在已设置为：
`/opt/kylix2/help`
auser@lnbox: ->

当确认脚本运行正常后，再次编辑 `.bashrc` 文件并在 `source` 命令末尾添加 " `/dev/null`"，以便将输出重定向到其他处。命令现在应该看起来像：

```
source <installation Kylix root path>/bin/kylixpath > /dev/null
```

当下次启动 shell 时，将不再显示任何输出。

现在是时候启动 Kylix 了。启动 Kylix 有两种方法。如果在安装过程中选择了“桌面菜单项”选项，在菜单中将找到一个名为“Kylix 2”的菜单标题。

> 提示：作者强烈建议从终端启动 Kylix。无论使用何种方法首次启动 Kylix，都会弹出一个小型对话框。或者，使用 `startkylix` 脚本。

首次运行 Kylix 时，它会在主目录下创建一个 `.bashland` 目录（例如 `/root/.bashland`）。该目录包含了四个配置文件以及 Kylix 使用的其他共享库文件。

| 配置文件 | 描述 |
| delphi65ci | 用户对代码宏的修改。 |
| delphi65mt | 用户对菜单模板的修改。 |
| delphi65rc | 存储 IDE 选项。 |

除了上述文件，安装 Kylix 的用户的 `.bashland` 目录包含下表所示的文件。
### 表 2-4
| 配置文件 | 描述 |
| --- | --- |
| dbconnections | 可用的 dbExpress 连接。 |

更多关于 dbExpress 的信息请参见12章。

VisiBroker 需要安装的 Java 运行时环境 (JRE) 运行。在 Kylix 安装光品的 `/jre` 目录下提供了可以安装的版本。安装 JRE 的详细说明可以在 `INSTALL` 文件找到。安装 JRE 后，确保将 `jre1.3.1_01/bin` 目录添加到 `PATH` 环境变量中。验证环境变量设置是否正确的简单方法是在 shell 提示符处输入“`java`”。如果出现用法界面，则说明环境变量已设置正确。某些 VisiBroker 工具使用 Korn Shell 执行。遗憾的是，并非所有的 Linux 发行版都带有 Korn Shell。幸运的是，可以通过以下地址获取各种发行版的公有 Korn Shell：http://rpmmind.net/linux/rpm2html.php?query=pdksh。

Kylix 2 安装光盘包含名为 Interbase 的数据库。设置脚本位于 `/interbase/IB60_linux` 目录。以 root 用户身份运行设置脚本。如果安装了之前的 Interbase 版本，请在继续之前咨询 Install.txt 文件。

```
root@lnbox:~ ~ cd interbase/IB60_linux/
root@lnbox:~/IB60_linux > ./setup
```

使用 RPM 安装 Interbase 客户端和服务器
2. 以 PDF 格式安装 Interbase 文档
3. 安装 InterClient JDBC 软件
5. 安装 Adobe Acrobat(R) Reader 软件

许可证声明和有限责任保证

此处应显示许可协议，但由于空间限制已移除。

请在下方选择一个选项以接受或拒绝许可协议的条款：

- 1. 我接受
- 2. 我不接受

输入选择 [1-2] : 1

已接受许可

输入安装目录的绝对路径
[default: `/opt`] :

正在启动 InterBase 客户端和服务器 RPM 安装，请等待...

- 1. 使用 RPM 安装 InterBase 客户端和服务器软件
- 2. 以 PDF 格式安装 InterBase 文档
- 3. 安装 InterClient JDBC 软件
- 4. 安装 Easysoft ODBC 驱动软件
- 5. 安装 Adobe Acrobat(R) Reader 软件
- 6. 退出
输入选择。（默认 1）[1-6] : 6
