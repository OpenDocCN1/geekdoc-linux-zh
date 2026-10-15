
```
echo "done"

killall -q -9 carpald &

rm -f /var/lock/subsys/carpald

;;

status)

status carpald

;;

restart|reload)

$0 stop

$0 start

;;

*)

echo "Usage: carpal start|status|restart|reload"

exit 1

esac

exit 0
```

关于上述启动脚本的几点注释：

- 尽管脚本的第一行以 `#!/bin/sh` 开头，但请注意 `/bin/sh` 是 `/bin/bash` 的符号链接。这在其他 UNIX 系统上可能并非如此。
- `chkconfig: 35 99 01` 这一行对于我们使用的 `chkconfig` 工具实际上非常重要。数字 `35` 表示默认为运行级别 3 和 5 创建启动和停止条目——即将在 `/etc/rc.d/rc3.d` 和 `/etc/rc.d/rc5.d` 目录中创建条目。
- `99` 和 `01` 意味着 `chkconfig` 应该将我们的程序启动优先级设置为 99，停止优先级设置为 01——即晚启动和早收结束。

- 2. 将脚本保存为名为 `carpald` 的文件。

- 3. 使文件具有可执行权限：

```
[root@fedora-server ~]# chmod 755 carpald
```

4. 将脚本复制或移动到存储启动脚本的目录——`/etc/init.d/` 目录：

```
[root@fedora-server ~]# mv -f carpal /etc/init.d/
```

5. 现在你需要告诉 `chkconfig` 关于这个新启动/停止脚本的存在以及你想对它做什么：

```
[root@fedora-server ~]# chkconfig --add carpal
```

这将自动创建此处列出的一些符号链接：
lrwxrxrwx. 1 root 17 Dec 15 11:58 S10carpal -> .../init.d/carpal
lrwxrxrwx. 1 root 17 Dec 15 11:58 S99carpal -> .../init.d/carpal
lrwxrxrwx. 1 root 17 Dec 15 11:58 KOcarpal -> .../init.d/carpal
lrwxrxrwx. 1 root 17 Dec 15 11:58 S99carpal -> .../init.d/carpal

（前文已解释过列表中 K (kill) 和 S (start) 前缀的意义和重要性）。

这看起来可能相当复杂，但好消息是，由于你设置了这个 rc 脚本，你再也不需要重复这样做了。更重要的是，脚本将在启动和关机期间自动运行，并能够自我管理，这种开销对于避免腕管隧道综合症的长期收益是非常值得的：我们已经设置好了基础设施周围的“基础设施”，但在运行它之前，它并不能完全发挥。我们将运行它。

# Linux 管理：入门指南

![](img/9f6657924397c33f088db5321b751a83_201_0.png)

图 6-1 Fedora 服务配置工具

![](img/9f6657924397c33f088db5321b751a83_201_1.png)

图 6-2 Cockpit–系统服务标签

# 第 6 章 启动与关机

![](img/9f6657924397c33f088db5321b751a83_202_0.png)

图 6-3 openSUSE 服务管理器

在 Ubuntu 系统上，具有 GUI 前端的服务的管理工具是 bum 应用程序（启动管理器）。参见图 6-4。您可以通过输入以下命令启动它：

```
master@ubuntu-server:-$ sudo bum
```

![](img/9f6657924397c33f088db5321b751a83_202_1.png)

图 6-4 Ubuntu 启动管理器

# 178 Linux 管理：入门指南

注意 如果您的 Ubuntu 服务器默认没有安装 bum 应用程序，可以通过输入快速安装：

```
# sudo apt-get install bum
```
