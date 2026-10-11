
# Required-Stop: `localnet`

# Should-Stop: `$local_fs`

# Default-Start: `S`

# Default-Stop: `0 6`

# Short-Description: 激活和禁用交换分区。

# Description: 激活和禁用在 `/etc/fstab` 中定义的交换分区。

# X-LFS-Provided-By: `LFS`

### END INIT INFO

```bash
.lib/libd/init-functions

case "$1" in

start)

  log_info_msg "激活所有交换文件/分区..."

  swapon -a

  evaluate_retval

  ;;

stop)

  log_info_msg "禁用所有交换文件/分区..."

  swapoff -a

  evaluate_retval

  ;;

restart)

  $(0) stop

  sleep 1

  $(0) start

  ;;

status)

  log_info_msg "正在检索交换状态。"

  swapon -s

  ;;

*)

  echo "用法: $(0) (start|stop|restart|status)"

  exit 1

  ;;

esac

exit 0
```

# swap

## D.7. `/etc/rc.cd/init.d/setclock`

```bash
#!/bin/sh

######################################################################
# 开始 setclock
# Description : 设置 Linux 时钟
# Authors : Gerard Beekmans gerard@linuxfromscratch.org
           DJ Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubbs - bdbubbs@linuxfromscratch.org
# Version : LFS 7.0
######################################################################
```

```bash
### BEGIN INIT INFO
# Provides:
# Required-Start:
# Should-Start:      modules
# Required-Stop:
# Should-Stop:       $syslog
# Default-Start:    S
# Default-Stop:
# Short-Description:  从硬件时钟存储并恢复时间

在启动时，系统时间从 hwclock 获取。时钟也可以在关机时设置。

# Description:
# X-LFS-Provided-By:

LFS

### END INIT INFO
```

```bash
. /lib/sh/init-functions

[ -r /etc/sysconfig/clock ] && . /etc/sysconfig/clock
```

```bash
case "$1" in

yes|1)

    CLOCKPARAMS="$(CLOCKPARAMS) --utc"

    ;;

false|0)

    CLOCKPARAMS="$(CLOCKPARAMS) --localtime"

    ;;

esac

case $(1) in

start)

    hwclock --hctosys $CLOCKPARAMS >/dev/null

    ;;

stop)

    log_info_msg "正在设置硬件时钟..."

    hwclock --systohc $CLOCKPARAMS >/dev/null

    evaluate-retval

    ;;

*)

    echo "用法: $(0) (start|stop)"

    exit 1

    ;;

esac

exit 0
```

## D.8. `/etc/rc.d/init.d/checkfs`

```bash
#!/bin/sh

######################################################################################
# 开始 checkfs
# Description : 文件系统检查
# Authors      : Gerard Beekmans - gerard@linuxfromscratch.org
               A. Luebe - lubeeke@sourceforge.net
               DJ Lucas - dj@linuxfromscratch.org
               Witi - witelson@linuxscratch.org
# Update : Bruce Dubbs - dbubbs@linuxscratch.org
# Version : LFS 7.0
# Linux From Scratch - Version 11.3
# 基于 LFS 早期的 checkfs 脚本。
# 0 无错误
# 1 文件系统已修复
# 2 系统应重启
# 4 留有文件错误
# 8 操作错误
# 12 库错误
# 16 用法或语法错误
# 32 用户取消
********************************

### BEGIN INIT INFO
# Provides: checkfs
# Required-Start: udev swap
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start: S
# Default-Stop:
# Short-Description: 在挂载前检查文件系统。
# Description: 在挂载前检查文件系统。
# X-LFS-Provided-By: LFS

### END INIT INFO
```
