
在许多情况下，`/etc/rc.d/init.d`目录指向的脚本是工作主体；它们执行了启动和停止服务的实际过程。当`/etc/rc`遍历特定运行级别的目录时，它会按数字顺序调用每个脚本。它首先从K开始的脚本，然后调用每个以S开头的脚本。对于以K开头的脚本，会传递一个`stop`参数。同样，对于以S开头的脚本，会传递一个`start`参数。

让我们查看一下`/etc/rc/rc3.d`目录看看里面有什么：

```
[root@fedora-servera-~#] ls -l /etc/rc/rc3.d/
total 232
lrwrrxw root root 22 2008-11-05 01:34 S97yum-updateds -> ..//init.d/yum-updateds
lrwrrxw root root 24 2008-11-05 01:42 K02NetworkManager -> ..//init.d/NetworkManager
lrwrrxw root root 34 2008-11-05 01:42 K02NetworkManagerDispatcher -> ..//init.d/NetworkManagerDispatcher
lrwrrxw root root 19 2008-11-05 01:34 S97yum-updateds -> ..//init.d/yum-updateds
lrwrrxw root root 22 2008-11-05 01:34 S97yum-updateds -> ..//init.d/yum-updateds
```

（注：`ls`命令的输出包含大量的重复和干扰；这些已清理以表示预期的结构）。

## 编写你自己的脚本

假设你想要一个每小时弹出消息的程序以防止鼠标管综合症。启动该程序的脚本将包含以下内容：

- 脚本描述（以便你以后不会忘记它）
- 在尝试启动之前验证程序是否存在
- 接受启动和停止参数

1. 启动你喜欢的任何文本编辑器，输入以下文本：

```bash
#!/bin/sh
#Description: 这个简单的脚本每小时向 ADDR 变量指定的任何电子邮件地址
#发送邮件，提醒用户离开电脑休息以防止鼠标管综合症。脚本的智能性很低，
只要系统运行，它就会发送电子邮件——即使用户正在熟睡！
#所以事后忘记禁用它。
#Author: Wale Soyinka

ADDR=root@localhost
while
sleep 1h
echo -s "Carpal Tunnel Warning" $ADDR | \
mail -s "Carpal Tunnel Warning" $ADDR
done
```

2. 将脚本文本保存为名为`carpald.sh`的文件。

3. 你接下来需要使脚本具有执行权限。输入：

```bash
[root@fedora-serverA ~]# chmod 755 carpald.sh
```

4. 将脚本复制或移动到启动脚本能够找到的目录，即`/usr/local/sbin/`目录。输入：

```bash
[root@fedora-serverA ~]# mv carpald.sh /usr/local/sbin/
```

## 创建启动脚本

在这里，你将创建一个在系统启动和关机期间执行的实际启动脚本。你在此创建的文件将命名为`carpald`。该文件将启用`chkconfig`支持。这意味着如果我们需要的话，可以使用`chkconfig`工具来控制程序启动和停止的运行级别（levels）。这是一个非常有用且节省时间的功能。

- 启动你选择的任何文本编辑器，并输入以下文本：

```
#!/bin/sh
#Carpal Start/Stop the Carpal Notice Daemon
#chkconfig: 35 99 01
## description: Carpald 是一个每 1 小时唤醒一次的程序，
## 告诉我们需要离开键盘休息一下，否则我们将失去手腕的所有功能，
并在余生中再也无法打字。
## Source function library.
/ /etc/rc.d/init.d/functions
[ -f /usr/local/sbin/carpald.sh ] || exit 0
## 查看我们是如何调用的。
case "$1" in
start)
echo "Starting carpald: "
/usr/local/sbin/carpald.sh &
echo "done"
touch /var/lock/subsys/carpald
;
stop)
echo -n "Stopping carpald services: "
echo "done"
killall -q -9 carpald
rm -f /var/lock/subsys/carpald
;
status)
status carpald
;
restart|reload)
$0 stop
$0 start
;
*)
echo "Usage: carpald start|stop|status|restart|reload"
exit 1
esac
exit 0
```

关于上述启动脚本的注释：

- 尽管脚本的第一行以`#!/bin/sh`开头，但需要注意的是`/bin/sh`是`/bin/bash`的符号链接。这在UNIX系统上并非如此。
- “`chkconfig: 35 99 01`”这一行对于我们想要使用的`chkconfig`工具实际上非常重要。`chkconfig`默认为运行级别3和5的程序创建启动和停止条目，即会在`/etc/rc.d/rc3d`和`/etc/rc.d/rc5d`目录中创建条目。
- “`99`”和“`01`”字段意味着`chkconfig`将将我们程序的启动优先级设置为99，停止优先级设置为01，即尽早启动和尽早结束。
- 将测试脚本保存为文件`carpald`。
- 接下来你需要使该文件具有执行权限。输入：

```
[root@fedora-serverA ~]# chmod 755 carpald
```

- 将脚本复制或移动到存储启动脚本的目录，即`/etc/rc.d/init.d/`目录。输入：

```
[root@fedora-serverA ~]# mv carpald /etc/rc.d/init.d/
```

- 现在需要告诉`chkconfig`这个新启动/停止脚本的存在以及我们想对它做什么。输入：

```
[root@fedora-serverA ~]# chkconfig --add carpald
```

这将为你自动创建符号链接：.../init.d/carpald

```
lrwxr-xrx 1 root root  2009-11-12 12:43 37 Kcarpald -> .../init.d/carpald
lrwxr-xrx 1 root root  2009-11-12 12:43 37 Kcarpald -> .../init.d/carpald
lrwxr-xrx 1 root root  2009-11-12 12:43 37 Scarpald -> .../init.d/carpald
lrwxr-xrx 1 root root  2009-11-12 12:43 37 Scarpald -> .../init.d/carpald
lrwxr-xrx 1 root root  2009-11-12 12:43 37 Scarpald -> .../init.d/carpald
lrwxr-xrx 1 root root  2009-11-12 12:43 37 Kcarpald -> .../init.d/carpald
```

（上述列列表中 (kill) 和 S (start) 前缀的意义和重要性[之前解释过](https://linux.fedora.org/docs/latest/admin-guide/chkconfig.html)）。

这一切看起来可能相当复杂，但好消息是，一旦你设置了这个 rc 脚本，就再也不需要这样做了。更重要的是，脚本将在启动和关机期间自动运行，并能够管理自己。初期的投入对于避免卡帕隧道综合征的长期利益来说是非常值得的！

# 第 6 章：启动与关机

6. 使用`service`命令查看`carpald.sh`程序的状态。

```
[root@fedora-serverA ~]# service carpald status
carpald is stopped
```

7. 手动启动`carpald`程序，以确保它在系统启动时确实正确启动。

```
[root@fedora-serverA ~]# service carpald start
Starting carpald:
```

- 如果你等大约一小时，你应该会收到一条来自`carpald.sh`脚本的邮件。你可以通过命令行使用`mail`程序：
