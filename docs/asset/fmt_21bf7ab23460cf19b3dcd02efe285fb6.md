
# 586 Corel6 Corel Linux OS 启动包：官方指南

```bash
#!/bin/sh
# 启动 kerneld (按需加载模块)
# (见 /doc/modules)
KDOPT="*"

test -f /proc/sys/kernel/modprobe && exit 0
test -f /sbin/kerneld || exit 0

# 检查是否有任何模块。
cd /lib/modules/`uname -r` >/dev/null || exit 0

case "$1" in
start)
  # /proc 和 /sbin 挂载了吗？
  if cd /proc/sys > /dev/null 2>&1 && cd /sbin > /dev/null 2>&1; then
    # 检查是否设置了 noauto
    grep -q ^noauto /etc/modules 2>&1 > /dev/null && exit 0
    start-stop-daemon --stop --quiet --exec /sbin/kerneld "$KDOPT"
    /sbin/kerneld $KDOPT
  fi
  ;;
stop)
  start-stop-daemon --stop --quiet --oknodo --exec /sbin/kerneld "$KDOPT"
  ;;
restart)
  $0 stop
  $0 start
  ;;
reload)
  start-stop-daemon --stop --signal 1 --quiet --exec
  ;;
force-reload)
  $0 reload
  ;;
*)
  echo "用法: /etc/init.d/kerneld (start|stop|restart|reload|force-reload)"
  exit 1
  ;;
esac

exit 0
```

### keymaps.sh

此脚本控制操作系统如何解释和使用来自键盘的输入。

```bash
#!/bin/sh

# *尽快* 加载键映射

test -f /bin/loadkeys || exit 0

PACKAGE=kbd
CONFDIR=/etc/$(PACKAGE)

case $PACKAGE in
kbd) EXT=map ;;
console-tools) EXT=kmap ;;
esac

KERNEL_KEYMAP=/var/lib/$(PACKAGE)/kernel.$(EXT)

case "$1" in
start | restart | force-reload | reload)
  # 保存内核键映射
  if [ -d ${KERNEL_KEYMAP} ] && [ ! -r ${KERNEL_KEYMAP} ]; then
    /usr/bin/dumpkeys > ${KERNEL_KEYMAP}
  fi
# 加载新映射
  if [ -r $(CONFDIR)/default.${EXT} ]; then
    /bin/loadkeys $(CONFDIR)/default.${EXT}
  elif [ -r $(CONFDIR)/default.${EXT}.gz ]; then
    /bin/loadkeys $(CONFDIR)/default.${EXT}.gz
  fi
  ;;
stop)
  # 确保关机/重启之前删除保存的内核键映射
  rm -f ${KERNEL_KEYMAP}
  ;;
*)
  echo "用法: $0 (start|stop|restart|reload|force-reload)"
  exit 1
  ;;
esac

exit 0
```

### logoutd

`logoutd` 脚本管理在注销操作系统时执行的各种功能和进程。

```bash
#! /bin/sh
# start/stop logoutd

-f /usr/sbin/logoutd || exit 0

# 大多数不需要 logoutd，所以我们只运行它
# /etc/porttime 没有注释行
grep -vq '^#|^$' /etc/porttime || exit 0

case "$1" in
start)
  echo -n "启动登录时间和限制执行器: logoutd"
  start-stop-daemon --start --quiet --exec /usr/sbin/logoutd
  echo "."
  ;;
stop)
  echo -n "停止登录时间和限制执行器: logoutd"
  start-stop-daemon --stop --quiet --exec /usr/sbin/logoutd
  echo "."
  ;;
*)
  echo "用法: /etc/init.d/logout start|stop"
  exit 1
  ;;
esac

exit 0
```

### lpd

`lpd` 启动并停止打印守护进程，控制从应用程序发送的打印作业。

```bash
#!/bin/sh

PATH=/bin:/usr/bin:/sbin:/usr/sbin
DAEMON=/usr/sbin/lpd
PIDFILE=/var/spool/lpd.lock

test -x $DAEMON -a -f /usr/sbin/lpd || exit 0

case "$1" in
start)
  echo -n "启动打印守护进程: lpd"
  if start-stop-daemon --stop --signal 0 --pidfile $PIDFILE -name lpd;
  then
    echo " 已经在运行。"
    exit
  fi
  /sbin/start-stop-daemon --start --quiet --exec $DAEMON
  echo "."
  ;;
stop)
  echo -n "停止打印守护进程: lpd"
  if start-stop-daemon --quiet --stop --signal 0 --pidfile $PIDFILE -name lpd;
  then
    PID=`cat $PIDFILE'
    start-stop-daemon --quiet --stop --exec $DAEMON --pidfile -name lpd
    # 现在我们等待它退出
    while kill -0 $PID 2>/dev/null; sleep 1; done
    echo "."
  fi
  ;;
esac
```

```bash
echo " not running.";
fi
;;
force-reload(restart)
$0 stop
$0 start
;;
*) echo "Usage: /etc/init.d/lpd {start|stop|restart|force-reload}"
exit 1
esac

exit 0
```

## mdutils

此脚本控制多个设备。多个设备也称为 RAID 系统，是作为一个单元运行的磁盘组。这是通过在磁盘上进行数据条分层（striping）来实现的，例如，单个文件可能会按照规律模式分布在多个磁盘上。数据分层数据的目的是缩短在大容量设备上查找特定数据所需的时间。通过同时使用多个磁盘和磁头，查找和读取文件的时间被显著缩短。此脚本的意义不在于它的功能，而在于它的用途。

```bash
#! /bin/sh

#

# md

# 启用或禁用多个设备。如果 /etc/mdtab 不存在

# 或为空，我们不予会；同样，如果没有安装 mdadd 或

# mdstop 亦然。

#

#

# 注意，由于这是在启动过程早期调用的，

# 我们无法交换到 MD 设备；但你也不想这样做

# 因为 Linux 内核本身可以对分区进行分层处理

#（参见 swapon 管理）。

#

#

# Version: @#md 2.73 08-Jan-1998 miquels@cistron.nl

#

case "*" in

    start|*)

        if [ -s /etc/mdtab -f /sbin/mdadd ]

        then

            [ "$VERBOSE" != no ] && echo "Adding md devices."

            mdadd -ar

        fi

        ;;

    stop)

        if [ -r /etc/mdtab -a -x /sbin/mdstop ]

        then

            [ "$VERBOSE" != no ] && echo "Stopping md devices."

            mdstop -a

        fi

        ;;

        reload)
```
