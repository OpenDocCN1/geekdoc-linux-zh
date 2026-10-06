
在此脚本中，`awk` 从 `/etc/passwd` 文件中选择特定的信息。通过使用冒号作为分隔符（`-F:` 选项），`awk` 检查每行的第三字段（用户 ID，或 UID）是否大于或等于 500（默认情况下，普通用户账户的起始点）。如果是，则返回用户的家目录（第六个字段）。`for` 循环遍历 `awk` 返回的列表，并对每个目录执行磁盘占用检查。结果存储在一个唯一的临时文件中（`$$` 变量代表运行程序的进程 ID）。临时文件按数字排序，然后被删除。之前每个程序的输出可能如下：

```
936890 /home/jsmith
48934 /home/oracle
20439 /home/wilhelm
748 /home/acorad
8 /home/gandalf
8 /home/johnson
8 /home/cseitz
8 /home/buchanan
```

> 注意：`awk` 命令用于根据你提供的规则扫描文件中的特定模式。它可以以你选择的格式输出这些信息。

## 用于检查脚本的脚本

偶尔在测试脚本时，查看脚本目前完成的任务是有帮助的。当从另一个 shell 脚本调用时，以下脚本会挂起运行中的程序，并允许（通过另一个终端窗口或虚拟终端）查找预期的临时文件或更改后的条件。这可以指示程序是否按预期运行，或者它是否需要进一步改进。

```bash
#!/bin/bash
#
Count=1
while :
do
  echo -n "$Count Continue? (y/n): "
  read ANS
  case "$ANS" in
    y|Y)
      break
  esac
  let Count+=1
done
exit 0
```

第四行的冒号（`:`）什么都不做。它仅作为一个占位符，允许 `while` 循环重复，直到输入 `a` 或 `Y`（导致 `break` 退出循环）。`Count` 变量跟踪循环运行的次数。`echo` 的 `-n` 选项抑制打印新行，并将光标置在 `Continue? (y/n) :` 提示之后之后等待输入。

## 用于杀死进程的脚本

另一个可能经常使用的示例是以下优雅杀死进程的脚本。该脚本赋予进程清理任何临时文件的机会，通知正在退出的父进程并安静地终止。

```bash
#!/bin/bash
for I in `echo *`
do
  for J in 15 2 9
  do
    kill -$J $I && sleep 1
  done
done
exit 0
```

该脚本循环指定的进程 ID 列表。该脚本赋予进程清理任何临时文件的机会，通知正在退出的父进程并安静地终止。该脚本通过 15, 2, 9 信号来尝试终止进程。15 信号是 SIGTERM，允许进程进行清理；2 信号是 SIGINT，类似于中断；9 信号是 SIGKILL，用于强制终止。如果 15 信号没有起作用，它会尝试 2 信号并等待 1 秒；如果仍然无效，最后会使用 9 信号。

# 表 12-3 命令的运行方式

| 动作 | 命令运行方式 |
|---|---|
| wait | 与一次执行相同，但 init 会在继续处理其他 inittab 条目之前等待命令完成。 |
| respawn | 对该进程进行监控，如果原始进程终止，则启动一个新实例。 |
| powerfail | 在接收到与 UPS 单元关联软件发送的 SIGPWR 信号时执行命令。 |
| powerwait | 与 powerfail 相同，但 init 会等待命令完成后再继续处理其他 inittab 条目。 |
| powerwaitok | 如果 `/etc/powerstatus` 文件包含单词 OK，则在收接收到 SIGPWR 信号时执行命令。这通常由 UPS 软件完成，表示电源已恢复到正常水平。 |
| ondemand | 当手动指示进入某个特殊运行级别 a、b 或 c（分别相当于 A、B 和 C）时执行命令。实际上运行级别不会发生实际变化。如果原始进程终止，则会重启程序。 |
| sysinit | 在系统启动阶段执行命令；忽略运行级别（runlevels）。 |
| boot | 在系统启动阶段、所有 sysinit 条目处理完成后执行命令；忽略运行级别（runlevels）。 |
| bootwait | 与 boot 相同，但 init 会在继续处理其他 inittab 条目之前等待命令完成；运行级别字段也被忽略。 |
| initdefault | 在完成 boot 和 sysinit 动作后进入的默认运行级别。 |
| off | 什么都不发生（可能用于测试和调试） |
| ctrlaltelt | 捕获 Ctrl+Alt+Del 键键序列，通常用于优雅地关闭系统。 |
| kbrequest | 用于捕获键盘处理程序解释的特殊键序列。 |

# 第 12 节：系统任务自动化 439

# inittab 文件的解析

由于 `inittab` 文件是配置文件而不是顺序执行的 shell 脚本，因此行的顺序并不重要。以 `#` 字符开头的行被视为注释且不会被处理。

在上述的示例 `inittab` 文件中，第一个非注释行将默认运行级别设置为 3。默认值为 3 意味着在完成所有与 sysinit、boot 和 bootwait 动作相关的命令后，将启用运行级别 3（引导到文本登录界面）。另一个常见的 initdefault 是运行级别 5（引导到 GUI）。表 12-4 描述了每个运行级别，并帮助你选择最适合你环境默认值的运行级别。

# 表 12-4：可能的运行级别

| 运行级别 | 在此运行级别会发生什么 |
|---|---|
| 0 | 所有进程被终止，机器有序停止。正如 inittab 注释所指出的，这不是 initdefault 的良好选择，因为内核、模块和驱动程序一加载，机器就会停止。 |
| 1, s, S | 这代表单用户模式，最常用于系统维护以及在某些特定情况下运行，在这种情况下，激活较少进程且不启动任何服务可能是更优的。在单用户模式下，网络不存在，X 服务器未运行，且某些文件系统可能未挂载。 |
| 2 | 多用户模式。允许多个用户登录，挂载所有已配置的文件系统，并启动除 X、at 守护进程、xinetd 守护进程和 NIS/NFS 以外的所有进程。如果你的机器没有（或可能不需要）永久网络连接，这是 initdefault 的良好选择。 |
| 3, 4 | 带有网络服务的多用户模式。运行级别 3 是 Red Hat Linux 服务器 initdefault 的典型值，但运行级别 4（通常留给用户自定义）在默认 Red Hat Linux 配置中几乎完全相同。 |
| 5 | 带有网络服务和 X 的多用户模式。此运行级别启动 X 服务器并显示图形化登录窗口，视觉上类似于任何昂贵的基于 UNIX 的工作站。这是 Red Hat Linux 工作站的常用 initdefault 值。 |
| 6 | 所有进程被终止，机器优雅地重启。再次，inittab 文件中的注释提到，这不是 initdefault 的良好选择，甚至比运行级别 0 更糟糕。其结果可能是陷入无限循环的启动，随后紧接着是重启。 |

# 表 12-4（续））

| 运行级别 | 在此运行级别会发生什么 |
|---|---|
| 7, 8, 9 | 通常不使用且未定义，这些运行级别具有可能涵盖任何默认选项未覆盖的情况。 |
| a, b, c, A, B, C | 与 ondemand 动作配合使用。它们并没有真正指定运行级别，但在受命时可以“按需”启动程序或守护进程。 |

**注意：** 如果 `inittab` 表中没有指定 initdefault，启动序列将被中断，并会被提示指定一个机器将引导至的默认运行级别。

`inittab` 文件中的下一行指示在进入默认运行级别之前执行 `/etc/rc.d/rc.sysinit` 脚本。该脚本执行许多初始化例程，例如选择键映射文件、检查并挂载根文件系统和 proc 系统、设置时钟主机名、配置交换空间、清理临时文件以及加载模块。

以下行控制在每个主要运行级别内执行的命令。每个级别都会调用 `/etc/rc.d/rc` 脚本，并使用所需的运行级别作为参数。

# 系统启动与关闭

在系统启动期间，会运行一系列脚本来启动你所需的服务。这些包括启动网络接口、挂载目录和监控系统的脚本。这些脚本大部分从 `/etc/rc.d` 的子目录运行。启动这些大多数服务的程序在引导时运行，在关机系统 `/etc/rc.d` 脚本时停止。

## 运行级别脚本

如前所述，`/etc/rc.d/rc` 脚本是运行级别概念中不可或缺的脚本。任何运行级别的改变都会导致脚本被执行，并将新的运行级别作为参数。这个简单而强大的脚本在此处展示并讨论：

## 442 第三部分：管理 Red Hat Linux

`export CONFIRM`

```bash
# 获取第一个参数。将新的运行级别设置为此参数
[ "$S1" != "~" ] && runlevel="$arg1"
```

```bash
# 测试 linux 当前处于什么运行级别
[ -d /var/run ] && echo "/etc/rcrunlevel.d" > /var/run/runlevel.dir
```

```bash
# 是否为这个新的运行级别存在 rc 目录？
if [ -d /etc/rc$runlevel.d ]; then
  # 首先运行 KILL 脚本。
  for i in /etc/rc$runlevel.d/*; do
    # 检查脚本是否存在。
    [ -f "$i" ] && continue
```

```bash
# 不要运行 [KkS][Ss]?foo.rmpsave, rmprorig 脚本
[ "${i}.rmpsave" != "${i}" ] && continue
[ "${i}.rmrorig" != "${i}" ] && continue
[ "${i}.rmpsnew" != "${i}" ] && continue
```

```bash
# 检查子系统是否已经启动。
subsys=${i#/etc/rc$runlevel.d/K??}
[ -f /var/lock/subsys/$subsys ] && \
  [ -f /var/lock/subsys/$subsys.init ] && continue
```

```bash
# 将子系统关闭。
if egrep -q "killproc [action]*" $i; then
  stop
else
  action "Stopping $subsys" $i
fi
done # （等待，原文中缺少循环逻辑，根据上下文推断）
```

```bash
# 现在运行 START 脚本。
for i in /etc/rc$runlevel.d/*; do
  # 检查脚本是否存在。
  [ -f "$i" ] && continue
```

```bash
# 不要运行 [KkS][Ss]?foo.rmpsave, rmprorig 脚本
[ "${i}.rmpsave" != "${i}" ] && continue
[ "${i}.rmrorig" != "${i}" ] && continue
[ "${i}.rmpsnew" != "${i}" ] && continue
```

```bash
# 检查子系统是否已经启动。
subsys=${i#/etc/rc$runlevel.d/S??}
[ -f /var/lock/subsys/$subsys ] || \
  [ -f /var/lock/subsys/$subsys.init ] && continue
```

# 如果处于确认模式，则获取用户确认

```bash
if [ -n "$CONFIRM" ] && (
  confirm $subsys
  case $7 in
    0)
      ;;
    2)
      CONFIRM=
      ;;
    *)
      continue
  esac
)
# 将子系统启动。
if egrep -q "daemon|action" $i ; then
  if [ "$subsys" = "halt" -o "$subsys" = "reboot" ]; then
    unset LANG
    unset LC_ALL
    exec $i start
  else
    $i start
  fi
elif [ "$subsys" = "halt" -o "$subsys" = "reboot" -o 
  "$subsys" = "single" -o "$subsys" = "local" ]; then
  if [ "$subsys" = "halt" -o "$subsys" = "reboot" ]; then
    unset LANG
    unset LC_ALL
    exec $i start
  else
    $i start
  fi
else
  action "Starting $subsys $i"
fi
done
```

与 `inittab` 一样，以 `#` 字符开头的行被视为注释。嗯，第一行表示将为执行该脚本运行一个唯一的 `/bin/bash` 实例。前几行非注释内容处理过去、现在和未来的运行级别。变量 `arg` 获取第一个（以及）命令行参数（`$1`）的值的值。这代表了期望的运行级别。`set` 命令将 `runlevel` 命令的输出（在本节稍后的部分解释）放入 `$1` 和 `$2` 中，然后将其分发给 `previous`（上一个运行级别）和 `runlevel`（当前运行级别）变量。

下一行读取 `/etc/init.d/functions`，它包含了多个 shell 脚本代码段（如 `action`、`killproc` 和 `confirm` 子程序），用于为从 rc 脚本启动的每个进程提供一致的接口。

如果在启动时向引导加载程序传递了 `confirm` 选项，在没有系统控制台用户确认的情况下，没有任何守护进程或服务器进程启动。这段代码检查进程是否需要确认，并相应设置 `CONFIRM` 变量。

在下一行中，如果第一部分求值为真值（0）（`$1` 的值不等于空字符串），则运行 `&&` 之后的第二部分。`runlevel` 变量被设置为存储在变量 `arg1` 中的期望运行级别。

同样，下一行如果目录 `/var/run` 存在，则 `/var/run/level` 将被覆盖。该文件将包含要运行的命令的目录名称（例如 `/etc/rc3`）。

下一个块检查目录是否存在，如果不存在则终止。此时，程序开始循环，遍历运行级别目录中所有以字母 K 开头的脚本（代表在新运行级别下应该停止的程序），并跳过那些损坏的符号链接（即指向的实际文件不存在）并将其搁置。

# 表 12-5（续）

| 运行级别脚本 | 作用是什么 |
| :--- | :--- |
| crond | 启动或停止 cron 守护进程以定期运行常规命令。 |
| dhcpd | 启动或停止 dhcpd 守护进程，该进程自动为局域网上的计算机分配 IP 地址。 |
| gpm | 控制 gpm 守护进程，允许鼠标与控制台及文本应用程序交互。 |
| halt | 终止所有进程，写入计费记录，移除交换空间，卸载所有文件系统，并关闭或重启机器（取决于命令的调用方式）。 |
| httpd | 启动 httpd 守护进程，使您的计算机充 HTTP 服务器（即提供 Web 页面服务）。 |
| iptables | 启动 iptables 防火墙守护进程，管理为计算机设置的任何 iptables 风格的防火墙规则。 |
| key | 加载预定义的键盘映射。 |
| killall | 在关闭或重启之前关闭可能仍在运行的子系统。 |
| kudzu | 在启动时检测并配置新硬件。 |
| lpd | 控制处理打印请求的 lpd 打印机守护进程。 |
| netfs | 挂载或卸载网络（NFS、SMB 和 NCP）文件系统。 |
| network | 启动或停止所有配置的网络接口并初始化 TCP/IP 和 IPX 协议。 |
| nfs | 启动或停止 NFS 相关的守护进程（rpc.nfsd, rpc.mountd, rpc.statad 和 rpc.quotad）并导出共享文件系统。 |
| pcmcia | 加载或卸载模块、驱动程序和程序（包括 cardmgr），以支持笔记本电脑中的 PCMCIA 卡（以太网适配器、调制解调器、内存卡等）。 |
| portmap | 启动或停止 portmap 守护进程，管理利用远程过程调用（RPC）机制的程序和协议。 |
| random | 加载或保存机器随机数生成器的当前状态以确保随机性。 |
| reconfig | 在特定的启动情况下运行 anaconda 重配置界面（例如来自 LILO 启动提示符的重配置请求）。 |
| routed daemon | 启动或停止停止通过路由信息协议（RIP）控制动态路由表更新的 routed 守护进程。 |
| rstatd | 启动或停止 rpc.rstatd 守护进程，允许网络上的其他机器探测其性能统计数据。 |
| rersd | 启动或停止 rpc.rersd 守护进程，允许网络上的其他机器定位机器上的用户。 |
| rwhod | 启动或停止 rwhod 守护进程，允许网络上的其他机器获取当前登录用户列表。 |
| sendmail | 控制 sendmail 守护进程，处理入站和出口 SMTP（简单邮件传输协议）邮件。 |
| single | 终止所有运行进程并进入运行级别 1（单用户模式）。 |
| smb | 启动或停止 smbd 和 nmbd 守护进程，允许访问 Samba 文件和打印服务。 |
| snmpd | 启动或停止 snmpd（简单网络管理协议）守护进程，允许他人查看机器配置信息。 |
| squid | 启动或停止 squid 服务，为您网络上的客户端提供代理服务。 |
| syslog | 启动或停止 klogd 和 syslog 守护进程，分别处理来自内核和其他进程的日志事件。 |
| xfs | 启动或停止 xfs，X Window 前端服务器守护进程。 |
