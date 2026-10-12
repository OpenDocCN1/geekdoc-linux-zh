
HOSTS = (updater@student1.an-university.edu \
 updater@student2.an-university.edu)

# 列出需要更新的目录。
# 
FILES = (/csc101)

# 列出需要从更新过程中排除的目录。
EXCLUDE_DIR = (/csc101/instructor /csc101/secret)

# 以下是命令：
# 为HOSTS中列出的所有主机安装FILES中列出的所有目录，但排除EXCLUDE_DIR中列出的目录。
#
${FILES} -> ${HOSTS}
    install ;
    except ${EXCLUDE_DIR};

这个非常简单的distfile定义了一个名为HOSTS的变量，它有两个值：updater@student1.an-university.edu和updater@student2.an-university.edu。这告诉rdist在student1.an-university.edu和student2.an-university.edu上使用updater用户账户进行连接。

下一个变量FILES定义了rdist要分发的目录。这里只分发/csc101目录。

第三个变量是EXCLUDE_DIR，它被设置为列出所有你想要从分发中排除的文件和目录。示例中的值是/csc101/instructors（这可能包含只有教师才能访问的文件）和/csc101/secret（学生不应有权访问的目录）。文件的其余部分描述了一个简单的命令：

```
${FILES} -> ${HOSTS}
    install ;
    except ${EXCLUDE_DIR};
```

此命令获取**FILES**变量指向的所有文件和目录，并将它们安装在**HOSTS**变量指示的主机上。它还告诉rdist排除由EXCLUDE_DIR变量指定的文件和目录。要以(updater)身份运行rdist，请从命令行执行以下操作：

- **以updater身份登录。**（如果你是主系统上的root，也可以使用su将UID更改为updater。）
- **以updater身份运行以下命令：**
    ```
    /usr/bin/rdist -p /usr/sbin/rdist -oremove,quiet \
      -f /usr/local/rdist/rdist_distfile
    ```
    以下是选项的说明：
    - **-p.** 指定rdist所需的rdist程序的位置。
    - **-o.** 指定后面跟随一个或多个选项——在本例中为remove和quiet。
    - **remove.** 告诉rdist删除在目标系统目标目录中发现的任何多余文件。这为在每个学生系统上维护文件的相同副本提供了一种简单的方法。
    - **quiet.** 告诉rdist在操作期间尽可能安静。
    - **-f.** 指定distfile的位置。

为了减少运行此命令时的人为错误，请创建一个名为r-distribute.sh的sh脚本，如清单13-2所示。

### 清单13-2：rdistribute.sh脚本

```
#!/bin/sh
#
# This script runs rdist to update Web servers via the
# non-routable lan an-university.edu. The script is run
# by cron at a fixed interval.
#
# /etc/rc.d/rc.local starts the script to clean up
# left-over tempfile that might have been left
# at shutdown. This process also removes the
# log file.
```

```
# $Author$ (kabir@nitec.com)
# $Version$
# $ID$
# $Date$
# $Status
###############################################

# If the script is called with an
# argument then
case "$1" in
boot)

    # since the argument is 'boot' the script is being
    # called at system start-up so remove all old lock
    # files and logs.
    echo -n "Cleaning up rdist.rsh tmp files: "
    rm -f /tmp/rdist.lck
    rm -f /tmp/rdist.log
    echo "Complete."
    exit 0;
 ;;

    # since the argument is 'restart' the script
    # needs to clean up as if the system just booted.
restart)
    $0 boot
 ;;

esac
```

### 清单13-2（续）

```
# If the lock file exists then don't do anything.
if [ -f /tmp/rdist.lck ]; then
  exit 0
fi

# Otherwise create the lock file using /bin/touch
/bin/touch  /tmp/rdist.lck

# Run rdist
/usr/bin/rdist -p /usr/sbin/rdistd \
  -oremove,nochkgroup,nochkmode,nochkowner,quiet -f \
  /usr/local/rdist/rdist_distfile

# Remove the lock file
rm -f /tmp/rdist.lck

# Write the time and date in the log file
echo `date` >> /tmp/rdist.log

# Exit the script
exit 0
```

该脚本足够智能，可以通过使用锁文件来检测正在进行的rdistribute.sh进程，锁文件可以判断之前的rdistribute.sh是否已经在运行并继续。当大量文件在多个服务器上更新时，可能会发生这种情况。该脚本还接受一个名为boot的参数，可用于在启动过程中清理它创建的锁文件和日志文件。该脚本应从/etc/rc.d/rc.local调用，如下所示：

```
/usr/local/rdistribute.sh boot
```

可以通过/etc/crontab中的cron条目来安排此脚本运行。例如，要每小时运行此脚本一次，可以在/etc/crontab中添加以下cron条目：

```
01 * * * * updater /usr/local/rdistribute.sh > /dev/null
```

cron守护进程将以`updater`身份运行该脚本。或者，你可以根据需要从`/etc/cron.hourly`（或`/etc/cron.daily`、`/etc/cron.monthly`等）创建指向`rdistribute.sh`的链接。

## 第14章：配置X Window

### 安装XFree86

当你从官方CD-ROM安装Red Hat Linux时，你有机会安装和配置XFree86。如果你还没有这样做，可以使用CD-ROM上的RPM包轻松安装XFree86。要从CD-ROM的RPMs目录安装XFree86，请运行以下命令：

```
rpm -ivh XFree86*.rpm
```

这将从CD-ROM安装所有XFree86包。

### 配置XFree86

在为你的系统配置XFree86之前，你需要知道以下信息：

- 你拥有的显卡制造商和型号
- 你拥有的显存大小
- 你的显卡使用的芯片组类型
- 显示器的最大分辨率
- 显示器的水平和垂直刷新率、制造商和型号

如果你不知道显卡的信息，请运行XFree86附带的SuperProbe实用程序来确定它：

```
/usr/X11R6/bin/SuperProbe
```

以下是SuperProbe输出的示例：

```
WARNING - THIS SOFTWARE COULD HANG YOUR MACHINE.
READ THE SuperProbe.1 MANUAL PAGE BEFORE
RUNNING THIS PROGRAM.

INTERRUPT WITHIN FIVE SECONDS TO ABORT!
```

```
First video: Super-VGA
   Chipset: S3 Trio64V+ (Port Probed)
   Memory: 2048 Kbytes
   RAMDAC: Generic 8-bit pseudo-color DAC
```

6位模式

![](img/f9ec99365f159bfe663f8ac29732663c_421_0.png)

> **警告**
> >
> > 正如输出中的警告消息清楚地表明的那样，该程序可能会使你的系统无响应。请务必在运行此程序前阅读手册页。

在确定系统信息后，你需要决定如何配置XFree86。你有三种选择：

- 使用名为Xconfigurator的全屏幕、菜单驱动实用程序。
- 使用名为xf86config的命令行、提示式实用程序。
- 手动创建XF86Config文件。这是在XFree86中创建可用的X Window环境所需的主要配置文件。它通常位于*/etc/X11*目录中，通常有一个符号链接(/usr/X11R6/lib/X11/XF86Config)指向*/etc/X11/XF86Config*。

### 使用Xconfigurator创建XF86Config文件

Xconfigurator实用程序允许你非常容易地创建XF86Config文件：

- 按如下方式运行程序：
    ```
    /usr/X11R6/bin/Xconfigurator
    ```
    这将显示一个屏幕，说明该程序的功能。正如启动屏幕所建议的，请阅读`/usr/X11R6/lib/X11/doc/README.Config`文件，以了解有关文件结构的最新详细信息。

- 单击**OK**继续。如果由于某些原因`/usr/X11R6/lib/X11/XF86Config`符号链接损坏，Xconfigurator将显示一个屏幕要求你修复问题。

- 单击**OK**创建符号链接。如果你没有符号链接问题或刚刚修复了它，你将在下一个屏幕中看到结果，该屏幕列出了显卡信息和选定的X服务器名称。

- 单击**OK**继续。使用上下箭头键滚动选择显示器类型，以找到你的显示器品牌和型号。如果你在列表中找到了你的显示器，请选择它并按**OK**继续。如果你的显示器未在列表中，请选择Custom monitor（自定义显示器）并按**OK**继续。下一个屏幕会让你指定显示器的垂直刷新率和水平同步率。请查阅显示器手册以找到这些数字。如果你仍然找不到显示器的信息，请查看`/usr/X11R6/lib/X11/doc/Monitor`文件。

> 如果你丢失或扔掉了显示器手册，你可能能在显示器供应商的网站上找到相关信息。
