
HP-UX 11.x 的启动和关闭脚本基于一种机制，该机制将实际的启动和关闭脚本与配置信息分离开来。为了修改系统的启动或停止方式，你通常不需要修改脚本（这通常被认为有些风险）；相反，你可以修改配置变量。启动和关闭顺序基于一种行业标准，与许多其他基于 UNIX 的系统相似，因此你对 HP-UX 的知识适用于许多其他系统。

随着你的系统管理工作变得日益复杂，启动和关闭对你将变得越来越重要。当你加载和定制更多的应用程序时，你将需要更多的启动和关闭知识。在本节中，我将为你提供启动和关闭的概述以及你可以用来控制系统的命令。

启动和关闭模型中包含以下组件：

### 执行脚本

执行脚本从配置变量文件中读取变量，并执行启动或关闭序列。这些脚本位于 `/sbin/init.d` 中。

### 配置变量脚本

这些是你需要修改的文件，用于设置在系统启动或关闭时启用或禁用子系统或执行其他功能的变量。这些文件位于 `/etc/rc.config.d` 中。

### 链接文件

这些文件用于控制脚本的执行顺序。它们实际上是指向执行脚本的链接，当从一个运行级别转换到另一个运行级别时执行这些链接。这些文件位于相应运行级别的目录中，例如运行级别 0 的 `/sbin/rc0.d`，运行级别 1 的 `/sbin/rc1.d`，等等。

### 排序器脚本

此脚本根据运行级别转换调用执行脚本。此脚本位于 `/sbin/rc` 中。

图 8-1 显示了启动和关闭脚本的目录结构。

![](img/eff8b9287a5f38c5adf538f24aacf29e_457_0.png)

### 图 8-1 启动和关闭文件的组织

执行脚本执行启动和关闭任务。`/sbin/rc` 使用适当的 `start` 或 `stop` 参数调用执行脚本，你可以控制台上查看相应的 `start` 或 `stop` 消息。你看到的信息将具有以下三个值之一：

- `OK` 表示执行脚本正确启动或关闭。
- `FAIL` 在启动或关闭过程中发生了问题。
- `N/A` 脚本未配置为启动。

为了启动一个子系统，你只需编辑 `/etc/rc.config.d` 中相应的配置文件。

### 系统启动和关闭脚本

让我们看一个示例启动和关闭文件，该文件用于一个加载到 HP-UX 系统上的应用程序，该应用程序广泛用于 Internet 应用程序，名为 Cold Fusion。与加载在 HP-UX 系统上的许多应用程序一样，Cold Fusion 将启动和关闭脚本作为产品安装过程的标准部分进行安装。

如前所述，用作启动和关闭过程一部分的脚本位于 `/etc/init.d` 中。在我们的情况下，该程序的名称是 `/etc/init.d/coldfusion`，如下所示：

```bash
# cat /sbin/init.d/coldfusion
#!/bin/sh
#
# Start the Cold Fusion servers
#
export CFHOME

#
# Start/stop processes for Cold Fusion
#

rval=0
case "$1" in

        start_msg)
                print "Starting ColdFusion Application Server"
                ;;
        stop_msg)
                print "Stopping ColdFusion Application Server"
                ;;
        start)
                #Start_check "on/off switch", to set CF_AUTOSTART, in config.d file.
                RCFILE=/etc/rc.config.d/coldfusion
                if [ -f $RCFILE ]; then
                        . $RCFILE
                else
                        print "Warning: $RCFILE defaults file missing."
                        print "Starting ColdFusion by default."
                        CF_AUTOSTART=1
                fi
        # Start CP if switch is on.
                if [ "$CF_AUTOSTART" -eq 1 ]; then
                        if [ ! -x $CPBIN/start ]; then
                                rval=$?
                        else
                                print "Error: ColdFusion startup script $CPBIN/start missing."
                                print "      ColdFusion not started."
                                rval=1
                        fi
                else
                        print "Notice: ColdFusion startup disabled in $RCFILE"
                        rval=2
                fi
                ;;
        stop)
                if [ -x $CPBIN/stop ]; then
                        $CPBIN/stop -force
                fi
                ;;

        *)
                echo "Usage: $0 [ start | stop ]"
                rval=1
                ;;
esac
exit $rval
```

`/etc/init.d` 中的启动和关闭脚本通常同时执行启动和关闭功能。启动和关闭脚本（包括我们示例中的那个）识别以下四个参数：

- `start_msg` - 这是传递给脚本的参数，以便脚本可以报告一条消息，指示 "`start`" 操作将执行什么。
- `stop_msg` - 这是传递给脚本的参数，以便脚本可以报告一条消息，指示 "`stop`" 操作将执行什么。
- `start` - 脚本将启动应用程序。
- `stop` - 脚本将关闭应用程序。

所有启动和关闭脚本（包括前面列表中的那个）都从 `/etc/rc.config.d` 中的变量获取配置数据。我们的示例脚本检查 `/etc/rc.config.d/coldfusion` 中 "开/关" 开关的值，以判断是否应该启动 Cold Fusion，如下所示：

```bash
# cat /etc/rc.config.d/coldfusion
# ColdFusion Application Server configuration file
#
CF_AUTOSTART=1  #Set to 1 to restart at boot time
```

该文件中的变量被设置为 1，因此应用程序将在系统启动时启动。

### 系统启动和关闭脚本

启动和关闭脚本根据脚本链接所在的目录来运行。我们示例中的脚本应在运行级别三时启动。因此，其脚本链接出现在目录 `/sbin/rc3.d` 中，如下所示列表中的第三个链接：

```
# ls -l /sbin/rc3.d
total
lrwxr-xr-x    1 root     sys        23 Apr 26 14:32 G100nfs.server -> /sbin/init.d/nfs.server
lrwxr-xr-x    1 root     sys        19 Apr 26 14:52 S200tpc.rc -> /sbin/init.d/tps.rc
lrwxrwxrwx    1 root     sys        20 May 16 20:57 S790coldfusion -> ../init.d/coldfusion
lrwxr-xr-x    1 root     sys        23 Apr 26 14:44 S890dologin.rc -> /sbin/init.d/dologin.rc
```

我们稍后会解释链接命名的意义。目前，只需知道名为 `/sbin/rc3.d/S790coldfusion` 的链接指向我们的脚本 `/init.d/coldfusion` 即可。
