
# 第 9 章 系统初始化

## 项目 9-2

在实验项目中，你安装并配置 `GRUB` 加载程序。

1.  按下`Ctrl-Alt-F2`切换到命令行终端（`tty2`），使用用户名`root`和密码`secret`登录终端。

2.  在命令提示符处，输入`cat /boot/grub.conf`并按回车查看`GRUB`配置。你能看出加载程序安装在哪里吗？

3.  在命令提示符处，输入`vi /boot/grub.conf`并按回车编辑配置文件。将`timeout`值从 10 改为 60。你必须等待多久？保存更改并退出`vi`编辑。

4.  接下来，在命令提示符处输入`grub-install /sda`并回车在第一个磁盘的`MBR`上安装`GRUB`。如果你再次编辑`/boot/grub.conf`文件，你需要重新运行`grub-install`命令吗？

5.  输入`reboot`并按回车重启系统。当系统重启时，观察图形化`GRUB`界面。在此界面上，按`e`编辑配置。你认识列出的条目吗？

6.  在`grub>`提示符处输入`c`。

7.  在`grub>`提示符处，输入`help`并按回车查看`grub>`提示符处可以使用命令列表。接下来，在`grub>`提示符处输入计算机的所有内存并按回车。`GRUB`在`/boot/grub.conf`命令中识别计算机的所有内存吗？

8.  在`grub>`提示符处，输入`cat /boot/grub.conf`并按回车查看`/boot/grub.conf`文件。为什么在`cat /grub.conf`命令中需要使用从`/boot`目录开始绝对路径？

9.  在`grub>`提示符处，输入`kernel /vmlinuz root=/sda2`并按回车将`Linux`内核（`/boot/vmlinuz`）加载到内存中。（注意：`/boot/vmlinuz`是当前内核的符号链接。）

10. 在`grub>`提示符处，输入`boot`并按回车，使用上一步加载到内存中的`Linux`内核继续启动过程。允许系统正常启动。

11. 系统成功加载后，按下`Ctrl-Alt-F2`切换到命令行终端（`tty2`），使用用户名`root`和密码`secret`登录终端。

12. 在命令提示符处，输入`grub-md5-crypt passfail`并按回车。这将产生空行；在此空行处，输入`secret`并按回车。

13. 在命令提示符下，输入`cat passfile`并按`Enter`。加密后的密码在那里吗？

14. 在命令提示符下，输入`vi /boot/grub/grub.conf`并按`Enter`编辑`GRUB`配置文件。在`vi`编辑器中，将光标置于显示`splashimage=(h0,0)/grub/splash.xpm.gz`的一行。

15. 接下来，输入以获取屏幕底部的交互式提示符，然后输入`r -1 passfile`来读取文档当前行下方`passfile`的最后一行。现在你的光标应该位于加密密码的第一个字符上。

16. 输入`i`进入插入模式并输入以下内容：

```
password --md5
```

整行看起来应该类似于：

```
password --md5 <encrypted password>
```

17. 保存更改并退出`vi`编辑器。

18. 输入`ls -l /boot/grub/grub.conf`并按`Enter`检查`/boot/grub/grub.conf`文件的权限。这些是安全隐患吗？即使所有人都被允许读取权限，他们能看到启动密码吗？

19. 输入`reboot`并按`Enter`重启系统。当系统重启时，观察图形化`GRUB`屏幕。在此屏幕上，按`p`编辑`GRUB`的配置。输入密码`secret`并按`Enter`。你认识显示的屏幕吗？屏幕上的信息内容是什么？

20. 按`Enter`启动默认操作系统。

## 项目 9-3

在本项目项目中，你将探索运行级别（`runlevels`）以及用于在系统启动时及之后更改运行级别的`/etc/inittab`文件。

1.  按下`Ctrl-Alt-F2`切换到命令行终端（`try2`），并使用用户名`root`和密码`secret`登录终端。

2.  在命令提示符下，输入`runlevel`并按`Enter`。你当前的运行级别是多少？这个级别是在安装期间选择的吗？如果不是，最近的运行级别是多少？

3.  在命令提示符下，输入`/etc/inittab`并按`Enter`。此文件中的哪一行决定了启动时的默认运行级别？这可以更改吗？

4.  在命令提示符下，输入`init 2`并按`Enter`。你的终端屏幕上显示了什么？是否有守护进程（`daemons`）启动？是否有守护进程停止？为什么会停止？为什么你需要登录？为什么？

5.  使用用户名`root`和密码`secret`登录当前终端。接下来，在命令提示符下输入`runlevel`并按`Enter`。你当前的运行级别是多少？最近的运行级别是多少？

6.  在命令提示符下，输入`init 1`并按`Enter`。你的终端屏幕上显示了什么？是否有守护进程启动？是否有守护进程停止？为什么？为什么你需要登录？为什么？

7.  接下来，在命令提示符下输入`runlevel`并按`Enter`。你当前的运行级别是多少？最近的运行级别是多少？

8.  在命令提示符下，输入`init 5`并按`Enter`。你的终端屏幕上显示了什么？是否有守护进程启动？是否有守护进程停止？为什么？切换到运行级别 5 后显示了什么？

9.  按下`Ctrl-Alt-F2`切换到命令行终端（`tryt2`），并使用用户名`root`和密码`secret`登录终端。

10. 接下来，在命令提示符下输入`runlevel`并按`Enter`。你的运行级别是多少？最近的运行级别是多少？

11. 在命令提示符下，输入`less /etc/inittab`并按`Enter`。解释`init`进程在第 4、6、8 步中读取了该文件的哪些行。

12. 输入`exit`并按`Enter`退出`shell`。

## 项目 9-4

在这个项目中，你将在系统启动时检查运行级别目录以及伪守护进程进程。

1.  按下`Ctrl-Alt-F2`切换到命令行终端（`tryt2`），并使用用户名`root`和密码`secret`登录终端。

2.  在命令提示符下，输入`ls /etc/rc.d`并按`Enter`。列出了哪些目录？每个目录下包含什么？

3.  在命令提示符下，输入`ls -F /etc/rc.d/rc0.d`并按`Enter`。列出了哪些文件？`init`进程以什么顺序执行这些文件？

4.  在命令提示符下，输入`ls -F /etc/rc.d/rc5.d`并按`Enter`。列出了哪些文件？与`S`相比，有多少文件以`K`开头？为什么？

5.  在命令提示符下，输入`ls -F /etc/rc.d/init.d`并按`Enter`。列出了哪些文件？执行`init`目录下的文件时会发生什么？

6.  在命令提示符下，输入`/etc/rc.d/init.d/atd stop`。发生了什么？

7.  在命令提示符下，输入`/etc/rc.d/init.d/atd start`。发生了什么？

8.  在命令提示符下，输入`/etc/rc.d/init.d/atd restart`。发生了什么？

9.  在命令提示符下，输入`vi /etc/rc.d/init.d/atd`。

10. 在`vi`编辑器中输入以下内容（注意：`$1`指向第一个参数）：

```
#!/bin/bash
if [ $1 = "start" ]; then
    echo "The daemon has started"
    sleep 2
elif [ $1 = "stop" ]; then
    echo "The daemon has been stopped"
    sleep 2
elif [ $1 = "restart" ]; then
    echo "The daemon has been restarted"
    sleep 2
fi
```

11. 在命令提示符下，输入`ls -l /etc/rc.d/init.d/atd`。权限是什么？

12. 在命令提示符下，输入`chmod 755 /etc/rc.d/init.d/atd`。

13. 在命令提示符下，输入`ln -s /etc/rc.d/init.d/atd /etc/rc.d/rc5.d/S99atd`。此命令做了什么？

14. 在命令提示符下，输入`reboot`并按`Enter`重启系统。在守护进程启动时，注意启动屏幕。
