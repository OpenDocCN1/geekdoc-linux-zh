

## 编写你自己的 rc 脚本

在维护 Linux 系统运行的过程中，你迟早需要修改启动或关机脚本。你有两条路可以走：

- 如果你的更改仅在启动时生效，并且更改内容较小，你可能希望直接编辑 **/etc/rc.local** 脚本。此脚本在启动过程的最后执行。

- 另一方面，如果你的添加内容更复杂，和/或需要关机过程显式停止服务，你应该在 **/etc/init.d** 目录中添加一个脚本。此脚本应接受 **start** 和 **stop** 参数，并相应地执行操作。

当然，第一个选项，编辑 **/etc/rc.local** 脚本，是两者中更简单的一种。要向该脚本添加内容，只需使用你选择的编辑器打开它，并在末尾添加你想执行的命令。这适用于简单的一两行更改。

然而，如果你确实需要一个单独的脚本，你将需要选择第二个选项。编写 **rc** 脚本的过程并不像看起来那么困难。让我们通过一个示例逐步讲解，看看它是如何工作的。（顺便说一下，你可以将此示例作为骨架脚本，根据需要修改以添加任何内容。）

假设你想启动一个特殊程序，它每 60 分钟弹出一条消息，提醒你该从键盘休息一下了（如果你不想患上腕管综合征，这是个不错的主意！）。启动该程序的脚本将包括以下内容：

- 对脚本目的的描述（以免你一年后忘了！）
- 在尝试启动之前，验证该程序是否真的存在
- 接受 **start** 和 **stop** 参数并执行所需的操作

给定这些参数，这就是你将编写的脚本。（请注意，以井号 (#) 开头的行只是注释，而不是脚本操作的一部分，第一行除外。）

```bash
#!/bin/sh
# 
# Carpal    Start/Stop the Carpal Notice Daemon
# 
# description: Carpald is a program which wakes up every 60 minutes and
# tells us that we need to take a break from the keyboard
# or we'll lose all functionality of our wrists and never
# be able to type again as long as we live.
#
# processname: carpal

# Source function library.
. /etc/rc.d/init.d/functions
[ -f /usr/local/sbin/carpald ] || exit 0
# See how we were called.
case "$1" in
start)
echo -n "Starting carpald: "
daemon carpald

echo
touch /var/lock/subsys/carpald
;;
stop)
echo -n "Stopping carpald services: "
killproc carpald

echo
rm -f /var/lock/subsys/carpald
;;
status)
status carpald
;;
restart | reload)
$0 stop
$0 start
;;
*)
echo "Usage: carpald start | stop | status | restart | reload"
exit 1
esac

exit 0
```

一旦你编写了新的脚本，只需添加必要的符号链接（symlinks，如模块 6 中所述），从相应的运行级别目录指向该脚本，以便让脚本启动或停止。在示例脚本中，你希望它仅在运行级别 3 或运行级别 5 中启动。这是因为假设这两个运行级别是你进行日常正常工作的唯一两个级别。最后，当你进入运行级别 6（重新启动）时，你希望守护进程关闭。以下是你输入以创建所需符号链接的命令：

```bash
[root@tedford /root]# cd /etc/rc3.d
[root@tedford rc3.d]# ln -s ../init.d/carpald S99carpald
[root@tedford rc3.d]# cd ../rc5.d
[root@tedford rc5.d]# ln -s ../init.d/carpald S99carpald
[root@tedford rc5.d]# cd ../rc6.d
[root@tedford rc6.d]# ln -s ../init.d/carpald K00carpald
```

注意，对于运行级别 3 和 5，你在 S 前缀后使用了数字 99；这确保该脚本将是启动过程中最后启动的事项之一。对于运行级别 6，你希望相反——carpals 应该在其余组件之前关闭。（组件启动的顺序通常是从最关键到最不关键，而组件关闭的顺序则是从最不关键到最关键。）

看起来相当复杂，不是吗？好消息是，既然你已经设置了这个 rc 脚本，你就再也不必这样做。更重要的是，脚本将在启动和关机期间自动运行，并能自我 managing。长期的收益完全值得前期的投入。

## 项目 8-2 创建 rc 脚本

本模块介绍了一个为重复性压力警告消息创建的 **rc** 脚本示例。在本项目中，你将为一个守护进程编写一个 **rc** 脚本，该守护进程监控目录并维护其内容的归档。对于此项目，假设存在一个程序 */usr/local/sbin/arch_data*，它检测指定目录中的变化并创建该目录内容的归档。调用该程序的方式如下：*/usr/local/sbin/arch_data monitored-directory archive-directory*。

### 分步操作

1. 成为 **root** 用户，在你首选的文本编辑器中编辑文件 */etc/init.d/arch_data*。
2. 这将是一个 shell 脚本，因此你需要通过以字符串 *#!/bin/sh* 开头来告诉系统这一点。
3. 添加注释说明此脚本的目的及其指向的程序。你可能想添加其他有用的信息，例如传递给程序的参数、你编写该脚本的日期以及你的姓名。
4. 通过添加字符串 *. /etc/init.d/functions* 来告诉脚本使用 Red Hat 已经在 */etc/init.d/functions* 文件中提供的函数。
5. 确保 *arch_data* 程序存在；如果不存在，则退出。
6. 将变量 *MON_DIR* 设置为要监控的目录名称：*MON_DIR="~/export/research/current"*。
7. 将变量 *SAVE_DIR* 设置为保存更改的目录名称：*SAVE_DIR="~/export/research/archive"*。
8. 设置 **case** 语句以读取 **rc** 指令，该指令将存储在 $1 变量中。
9. 如果指令是 **start**，则 `echo` 一条消息，表明服务正在启动，并对 `arch_data` 运行 `daemon` 命令，传递 $MON_DIR 和 $SAVE_DIR，以便归档程序知道如何处理。使用 `touch` 命令创建 /var/lock/subsys/arch_data 锁文件。
10. 如果指令是 **stop**，则打印一条消息，表明服务正在停止，并对 `arch_data` 程序运行 `killproc` 命令以停止它。删除你创建的锁文件。
11. 如果指令是 **status**，则对 `arch_data` 运行 **status** 命令。
12. 如果指令是 **restart** 或 **reload**，则先停止 `arch_data`，然后启动它。
13. 如果指令是其他任何值，则打印一条列出有效指令的消息并以错误状态退出。
14. 不要忘记关闭 case 语句并无错退出。
15. 添加链接到新脚本，使其在运行级别 2、3 和 5 中正确启动和关闭。

### 项目总结

如果你从未进行过任何脚本编程，这可能不是世界上最简单的项目。没关系，但请务必查看本模块中的示例以帮助澄清问题。你还可以查看 /etc/init.d 目录的内容，以了解一些更高级的示例。这些脚本中的每一个都使用了在 /etc/init.d/functions 文件中定义的函数（包括 killproc、status 和 daemon），你可以通过遵循其中的一些示例来完善你的脚本。

通过将程序的输入参数 *monitored-directory* 和 *archive-directory* 存储在脚本开头的变量中，你使配置更改变得更加容易。但创建一个配置文件来存储这些值（例如 /etc/arch_data.conf）会更好，这样更改守护进程的配置就不需要编辑启动脚本了。

而不是像在本项目中那样使用后台进程，你可以通过使用 **cron** 作业定期目录内容并在有变化时更新归档来解决同样的问题。区别在于功能：我们假设的备份进程是由目录中的变化触发的，而 **cron** 作业将在设定时间触发。但这值得思考：Linux 的一个美好方面是可以用不同的工具来解决同一个问题的机会。

