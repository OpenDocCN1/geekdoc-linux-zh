
如果系统进入多用户模式，`/etc/rc`会在`/etc/rc.boot`之后立即运行（请记住，`rc.boot`执行了`rc.single`）。`/etc/rc`首先检查`rc.boot`和`rc.single`所做的工作。一旦它确信其“表亲”已完成工作，它就会检查`passwd`文件在系统崩溃时是否未打开。如果已打开，`passwd`文件将从`/etc/ptmp`恢复。`/etc/rc`然后挂载所有本地文件系统。

**图 3.3** BSD 启动序列。

![](img/415c89a1ede71e11e5040a0038b6916c_100_0.png)

![](img/415c89a1ede71e11e5040a0038b6916c_101_0.png)

`loadkeys`和`dumpkeys`（SysV 和 BSD）分别加载和转储键盘转换表。

## 更改系统启动

更改系统启动脚本应谨慎进行。您几乎不需要对单用户启动中使用的任一启动脚本进行更改。同样，在正常情况下不应篡改`/etc/rc`。`/etc/rc.local`，正如其名称所示，是在本地系统配置中进行更改的地方。然而，请记住大多数厂商已在`rc.local`脚本中添加了与其特定版本相关的启动调用，因此在编辑此脚本时也必须谨慎。DNS、NFS 以及其他本地后台进程所调用的守护进程，如`sendmail`，通常从此脚本启动。`rc.local`脚本的典型添加包括：

- 许可证管理器。

- 第三方应用程序启动脚本。

- 特殊打印机驱动程序或管理器。

### RC.LOCAL

在对启动脚本进行更改时，始终尝试将其添加到文件底部附近。以下是从`rc.local`启动第三方许可证文件的示例：

```
#
## Matlab license manager.
#
if [ -f /etc/lmboot ]; then
    sh /etc/lmboot && echo -n ' Matlab '
fi
```

`#`符号表示注释，其右侧的所有内容都会被忽略。在本例中，我们调用的是 Matlab 许可证管理器`/etc/lmboot`。逻辑调用`if`以结束调用`fi`结尾。测试`[-f /etc/lmboot ]`很重要。它检查文件是否存在，然后执行该文件，并显示一行文字确认你已经执行了该脚本。在添加你自己的内容时，始终使用`-f`谓词确认文件存在后再执行；输出确认信息能让你在启动脚本挂起时更容易调试。

> 如前所述，这些脚本只是 Bourne shell 脚本，因此 Bourne 脚本可用的任何逻辑在`rc`脚本中同样可用。一个重要的经验法则是保持简单。另一个规则是永远不要删除`rc`脚本中的代码。如果你希望禁用某些行，请使用`#`符号将它们注释掉。`rc`脚本中的大量代码依赖于系统环境，重新创建它们非常困难。除非绝对必要，否则不要编辑这些脚本。

## 跟随 System V 启动脚本

System V（SysV）启动过程更复杂，同时也提供了更多选项。与 BSD 中的三个运行级别不同，SysV 启动有八个运行级别。运行级别为 0-6 以及`s`（或`S`）表示单用户模式。每个运行级别具有不同的功能。运行级别由一系列由`init`调用的脚本定义。运行级别和脚本之间的关系包含在系统文件`inittab`中。运行级别如表 3.2 所示。

## INITTAB

上述运行级别由名为`/etc/inittab`的文件控制。该文件控制`init`进程的操作。下面是来自 Solaris 2.6 系统的示例`inittab`文件：

```
mars# cat /etc/inittab

ap::sysinit:/sbin/autopush -f /etc/iu.ap

ap::sysinit:/sbin/soconfig -f /etc/sock2path

fs::sysinit:/sbin/rcS          >/dev/console 2>&1 </dev/console

is:3:initdefault:
```

**表 3.2 SysV 运行级别**

| 运行级别 | 用途 |
|---|---|
| 0 | 停机。 |
| S, s | 用于管理和诊断的单用户模式。只允许控制台登录；网络尚未激活。如果系统正在启动，用户文件系统不会被挂载；但如果正在关闭到该状态，则会保留这些文件系统。`init`派生的进程将被终止。 |
| 1 | 另一种单用户模式。所有文件系统保持挂载，许多脚本保持运行，只允许控制台登录。 |
| 2 | 具有有限网络功能的多用户模式。 |
| 3 | 具有网络功能的多用户模式；常见的默认运行状态。 |
| 4 | 在大多数系统上未使用的状态。 |
| 5 | 停机并重新启动。 |
| 6 | 停机并重新启动到默认状态。 |

```
p3:s1234:powerfail:/usr/sbin/shutdown -y -15 -g0 >/dev/console 2>/dev/console

s0:0:wait:/sbin/rc0 >/dev/console 2>/dev/console </dev/console

s1:1:wait:/usr/sbin/shutdown -y -1S -g0 >/dev/console 2>/dev/console </dev/console

s2:23:wait:/sbin/rc2 >/dev/console 2>/dev/console </dev/console

s3:3:wait:/sbin/rc3 >/dev/console 2>/dev/console </dev/console

s5:5:wait:/sbin/rc5 >/dev/console 2>/dev/console </dev/console

s6:6:wait:/sbin/rc6 >/dev/console 2>/dev/console </dev/console

fw:0:wait:/sbin/uadmin 2 0 >/dev/console 2>/dev/console </dev/console

of:5:wait:/sbin/uadmin 2 6 >/dev/console 2>/dev/console </dev/console

rb:6:wait:/sbin/uadmin 2 1 >/dev/console 2>/dev/console </dev/console

sc:234:respawn:/usr/lib/saf/sac -t 300

co:234:respawn:/usr/lib/saf/ttymon -g -h -p "uname -n" console login: " -T sun -d /dev/console -l console -m ldterm,ttcompat
```

该文件的结构为：

```
label : run-level : action : process
```

`label`是一个助记符：对于状态，通常是字母`s`加上状态编号；对于终端，通常是终端编号。`run-level`是一个数字（或`s`），表示应执行动作和命令的状态。如果该字段为空，则动作适用于所有运行级别。如果包含多个数字，如`234`，则表示动作适用于运行级别 2、3 和 4。`action`描述如何处理后面的`process`。

可以分配许多动作。不同 UNIX 操作系统风格之间略有差异。以下是对上面展示的`inittab`中动作的解释：

- `sysinit`：在尝试访问控制台之前执行此过程。

- `initdefault`：设置默认运行级别。

- `powerfail`：当`init`收到电源故障信号时执行此过程。

- `wait`：在继续之前等待此动作完成。

- `respawn`：在必要时重新启动此过程。

两个更有用的动作是：

- `bootwait`：仅在启动期间等待此动作。

- `off`：不执行此过程。

> 最后一个动作用于注释掉不再使用的运行级别动作。与 BSD 的`rc`脚本一样，你永远不应从`inittab`中删除代码；只需使用`off`动作来禁用它们。

因此，下面这行会告诉我们，在状态 2 和 3 中，你应该运行`/sbin/rc2`并等待脚本完成后再继续：

## RC 脚本

大部分工作都是在通常称为运行级脚本的进程中完成的（`/sbin/rc2`或`/sbin/rc3`等）。这些脚本在位于`/etc/rc2.d`和`/etc/rc3.d`的目录层次结构上工作。如果查看`/sbin/rc2`的一部分，你会看到基本过程是如何工作的。

脚本做的第一件事是使用`who -r`命令确定系统的状态。

```
set `/usr/bin/who -r`
```

如果系统正在启动，它会将`boot`变量设为`yes`。

```
if [ $x9 = "xS" -o $x9 = "x1" ]
then
```
