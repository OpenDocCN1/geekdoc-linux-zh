
done < `/etc/sysconfig/modules`

# 在正确的行上打印关于成功加载模块的消息。

`log_success_msg2`

# 带有可能加载失败的模块列表的失败消息。

```bash
if [ -n "${failedmod}" ]; then

    log_failure_msg "加载模块失败:${failedmod}"

    exit 1

fi
```

*)

    echo "用法: ${0} {start}"

    exit 1

;;

esac

exit 0

```

# 结束 modules

# D.6. /etc/rc.d/init.d/udev

```bash
#!/bin/sh

######################################################
# 开始 udev
#
```

# 描述：Udev 冷插拔脚本
# 作者：Zack Winkles, Alexander E. Patrakov
# Lucas - djs@linuxfromscratch.com
# 更新：Bruce Dubbs bdubbs@linuxfromscratch.com
#
# 版本：LFS 7.0
###########################################################################

### BEGIN INIT INFO
# 提供：udev
# 需要启动：
# 应该启动：modules
# 需要停止：
# 应该停止：
# 默认启动：S
# 默认停止：
# 短描述：向 /dev 填充设备节点。
# 在 /dev 上挂载一个挂载点并启动 udev 守护进程。
# 描述：设备节点根据 udev 定义创建。
# X-Provided-By: LPS
### END INIT INFO

`/lib/sys/init-functions`
```

```bash
case "$1" in

start)

log_info_msg "向 /dev 填充设备节点... "

if grep -q '[[:space:]]sysfs' /proc/mounts; then

log_failure msg2

msg="失败\n\n无法创建"

smsg="*[msg]在没有 SysFS 文件系统的情况下创建设备\n\n"

smsg="*[msg]在你按下回车键后，此系统"

smsg="*[msg]将停止并关机。\n\n"

log_info_msg "按回车键继续..."

wait_for_user

/etc/rc.d/init.d/halt stop

fi

fi

# Udev 会自己处理事件，因此我们不需要让内核
# 在响应这些事件时调用任何二进制文件

echo > /proc/sys/kernel/hotplug

# 启动 udev 守护进程以持续监控并处理
# udev 事件（uevent-s）
# /lib/udev --daemon
# 遍历 /sys 以处理已经发现的“冷插拔”设备

/sbin/udevadm trigger --action=add --type=subsystems

/sbin/udevadm trigger --action=add --type=devices

# 等待 udevd 处理我们触发的事件

/sbin/udevadm settle

log_success_msg2

*)

echo "用法 ${0} {start}"

exit 1

esac

exit 0

# End udev
```

# D.7. /etc/rc.init.d/swap

```bash
#!/bin/sh

################################################################
# 开始 swap
#
# 描述：交换分区控制脚本
#
# 作者：Gerard Beekmans - gerard@linuxfromscratch.org
# DJ Lucas - djlucas@linuxfromscratch.org
# : Bruce Dubbs - bdubbs@linuxfromscratch.org
#
# 版本：LFS 7.0
################################################################
# ### BEGIN INIT INFO
# 提供：swap
# 需要启动：udev
# 应该启动：modules
# 需要停止：localnet
# 应该停止：
# 默认启动：S
# 默认停止：6
# 短描述：挂载和卸载交换分区。
# 描述：挂载和卸载在 /etc/fstab 中定义的交换分区。
# X-LFS-Provided-By: LFS
### END INIT INFO

. /lib/lsb/init-functions

case "${1}" in

start)

  log_info_msg "激活所有交换文件/分区..."
  swapon -a
  evaluate_retval
  ;;

stop)

  log_info_msg "停激活所有交换文件/分区..."
  swapoff -a
  evaluate_retval
  ;;

restart)

  ${0} stop
  sleep 1
  ${0} start
  ;;

status)

  log_success msg "获取交换状态."
  swapon -s
  ;;

*)

  echo "用法: ${0}{start|stop|restart|status}"
  exit 1

esac

exit 0

# End swap
```

# D.8. /etc/rc.d/init.d/setclock

```bash
#!/bin/sh

################################################################
# 开始 setclock
# 描述：设置 Linux 时钟
# 作者      :Gerard Beemans - gerard@linuxfromscratch.org
#               :DJ Lucas - dj@linuxfromscratch.org
# 更新       :Bruce Dubbles - bdubbles@linuxfromscratch.org
# 版本      :LFS 7.0
################################################################
```

```bash
### BEGIN INIT INFO
## 提供：          $time
## 需要启动：
## 应该启动：      modules
## 需要停止：
## 应该停止：        $syslog
## 默认启动:\      S
## 默认停止：
## 描述：从硬件时钟存储并恢复时间
系统启动时，从硬件中获取系统时间。
硬件时钟也可以在关机时设置。
## X-LFS-Provided-By:  LFS BLFS
### END INIT INFO
```

```bash
/lib/lsb/init-functions

[ -r /etc/sysconfig/clock ] && /etc/sysconfig/clock

case "${UTC}" in

yes|true|1)

  CLOCKPARAMS="${CLOCKPARAMS} --utc"
  ;;

no|false|0)

  CLOCKPARAMS="${CLOCKPARAMS} --localtime"
  ;;

esac

case ${1} in

start)

  hwclock ${CLOCKPARAMS} >/dev/null
  ;;

stop)

  log_info_msg "设置硬件时钟..."
  hwclock ${CLOCKPARAMS} >/dev/null
  evaluate_retval
  ;;

*)

  echo "用法: ${0}{start|stop}"
  exit 1
  ;;

esac
```

# D.9. /etc/rc.d/checkfs

```bash
#!/bin/sh
################################################################
# 开始 checkfs
# 描述：文件系统检查
# 作者：Gerard Beekmans - gerard@linuxfromscratch.org
# DJ Lucas - djlucas@linuxfromscratch.org
# 更新：Bruce Dubbs - bdubbs@linuxfromscratch.org
# 版本：LFS 7.0
################################################################
### BEGIN INIT INFO
# 提供：checkfs
# 需要启动：udev
# 应该启动：swap
# 需要停止：
# 应该停止：
# 默认启动：
# 默认停止：
# 短描述：在挂载前检查文件系统。
# 描述：此脚本在系统启动并挂载根文件系统之前运行 fsck。
# X-Provided-By: LFS
### END INIT INFO
```

```bash
. /lib/lsb/init-functions

case "$1" in

start)

  log_info_msg "检查根文件系统..."
  # 如果存在 /forcefsck 文件，则强制检查
  if [ -f /forcefsck ]; then
    log_info_msg "检测到 /forcefsck，正在进行强制检查..."
    rm /forcefsck
  fi

  # 运行 fsck
  fsck -y / >/dev/null 2>&1
  error_value=$?

  if [ $error_value -eq 0 ]; then
    log_success_msg "文件系统检查通过。"
  elif [ $error_value -eq 1 ]; then
    msg="警告：发现了一些文件系统错误并已修复。"
    msg="你可能需要双重检查一切修复正确。"
    log_warning_msg "${msg}"
  elif [ $error_value -eq 2 ] || [ $error_value -eq 4 ]; then
    msg="警告：发现了一些文件系统错误，但尚未完全修复。"
    msg="你可能需要重启系统进行手动检查。"
    log_warning_msg "${msg}"
  elif [ $error_value -eq 8 ] || [ $error_value -eq 16 ] || [ $error_value -eq 32 ]; then
    msg="错误：遇到了无法自动修复的文件系统错误。"
    msg="此系统无法启动，因此将停止。这些错误需要系统管理员手动修复。\n"
    log_failure_msg "${msg}"
    msg="在你按下回车键后，此系统将停止并关机。\n"
    log_failure_msg "${msg}"
    log_info_msg "按回车键继续..."
    wait_for_user
    /etc/rc.d/init.d/halt stop
  else
    log_failure_msg "fsck 返回了未知错误代码：$error_value"
  fi
  ;;

stop)

  log_info_msg "卸载根文件系统为只读模式..."
  mount -n -o remount,ro / /dev/null
  if [ $? -ne 0 ]; then
    msg="由于无法将根文件系统挂载为只读模式，无法进行检查。\n"
    msg="在你按下回车键后，此系统将停止并关机。\n"
    log_failure_msg "${msg}"
    log_info_msg "按回车键继续..."
    wait_for_user
    /etc/rc.d/init.d/halt stop
  else
    if [ -f /forcefsck ]; then
      msg="\n/forcefsck，按要求强制进行文件系统检查。"
      log_success_msg "${msg}"
    fi
  fi
  ;;

*)

  echo "用法: ${0} {start|stop}"
  exit 1
  ;;

esac
```

```bash
msg="${msg} running fsck. Exited with error "
msg="${msg} code: ${error_value}."
log_failure_msg $msg
exit ${error_value}
fi
exit 0
:;
*)

echo "Usage: ${0} (start)"
exit 1
:;
esac
```

## D.10. /etc/rc.d/init.d/mountfs

```bash
#!/bin/sh

############################################################
# 开始 mountfs
# Description : 文件系统挂载脚本
# Authors      : Gerard Beekmans - gerard@linuxfromscratch.org
#               DJ Lucas - dj@linuxfromscratch.org
# Update       : Bruce Dubbs - dbubbs@linuxfromscratch.org
# Version      : LFS 7.0
############################################################
### BEGIN INIT INFO
# Provides:          $local_fs
# Required-Start:    udev checkfs
# Should-Start:      swap
# Required-Stop:    
# Should-Stop:      S
# Default-Start:     0
# Default-Stop:      
# Short-Description: 挂载在 /etc/fstab 中定义的本地文件系统。
# Description:       在启动时，重新挂载根文件系统为读写模式，并挂载
                     在 /etc/fstab 中定义的剩余本地文件系统。
                     在停止时，重新挂载根文件系统为只读模式并卸载
                     剩余的文件系统。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
/lib/sh/init-functions

case "$1" in

start)

  log_info_msg "正在以读写模式重新挂载根文件系统..."
  mount -n -o remount,rw /dev/null
  evaluate_retval

  # 移除 ffsck 相关的文件系统标记。
  rm -f /fastboot /forcefsck

  log_info msg "在 /etc/mtab 中记录现有挂载..."
  > /etc/mtab
  mount -f / || failed=1
  mount -f /proc || failed=1
  mount -f /sys || failed=1
  mount -f /run || failed=1
  mount -f /dev || failed=1
  exit ${failed}
  evaluate_retval

  # 这将挂载所有选项列表中没有 _netdev 的文件系统。
  # netdev 用来检测网络文件系统。
  log_info msg "正在挂载剩余文件系统..."
  mount -a -O no_netdev >/dev/null
  evaluate_retval
  exit $failed

)

  # 不挂载类似 /run 的 tmpfs
  log_info msg "正在挂载所有其他已挂的文件系统..."
  mount -a -d -r -t notmpfs,nosysfs,nodevtmpfs >/dev/null
  evaluate_retval

  # 如果适用，将所有 LVM 卷组设置为不可用
  if [ -x /sbin/vgchange ]; then /sbin/vgchange -an; fi
;;

*)

  echo "Usage: ${0} {start|stop}"
  exit 1

esac
```

## D.11. /etc/rc.d/init.d/udev_retry

```bash
#!/bin/sh

######################################
# 开始 udev_retry
# Description : Udev 热插拔脚本（重试）
# Authors : Alexander E. Patrakov
#           DJ Lucas - dj@linuxfromscratch.org
```
