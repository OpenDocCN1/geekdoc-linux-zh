
# DJ Lucas - `dj@linuxfrom.com`

# Update : Bruce Dubbs - `dububs@linuxfrom.com`

# Version : 7.0

################################################

### BEGIN INIT INFO

# Provides:

# Required-Start: modules

# Should-Start:

# Required-Stop: syslog

# Default-Start: S

# Default-Stop:

# Short-Description: 从硬件时钟存储和恢复时间

# 在系统启动时，系统时间从 hwclock 获取。硬件时钟也可以在关机时设置。

# X-LFS-Provided-By: LFS

### END INIT INFO

```bash
. /lib/lsb/init-functions

[ -r /etc/sysconfig/clock ] && . /etc/sysconfig/clock

case "$(UTC)" in

yes|true|1)

CLOCKPARAMS="${CLOCKPARAMS} --utc"

;;

false|0)

CLOCKPARAMS="${CLOCKPARAMS} --localtime"

;;

esac

case "$1}" in

start)

hwclock ${CLOCKPARAMS} >dev/null

;;

stop)

log_info_msg "正在设置硬件时钟..."

hwclock ${CLOCKPARAMS} >dev/null

evaluate_retval

;;

*)

echo "用法: ${0} {start|stop}"

exit 1

;;

esac

exit 0
```

## D.8. `/etc/rc/init.d/checkfs`

```bash
#!/bin/sh
####################################################################
# Begin checksfs
# Description : 文件系统检查
# Authors : Gerard Beekemans - gerard@linuxfrom.com
# Luebeck - luebek@users.sourceforge.net
# DJ Lucas - dj@linuxfrom.com
# Update : Bruce Dubbs - dububs@linuxfrom.com
# Version : 7.0
# 基于 LFS-3.1 及早版本的 checksfs 脚本。
# 来自 man fsck
# 0 - 无错误
# 1 - 已纠正文件系统错误
# 2 - 系统已重启
# 4 - 留有未修复的文件系统错误
# 8 - 运行错误
# 16 - 使用或语法错误
# 32 - 用户取消
# 128 - 共享库错误
####################################################################

### BEGIN INIT INFO
# Provides: checksfs
# Required-Start: udev swap
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start:
# Default-Stop:
# Short-Description: 在挂载前检查本地文件系统。
# Description: 在挂载前检查本地文件系统。
# X-LFS-Provided-By: LFS
### END INIT INFO

. /lib/lsb/init-functions

case "${1}" in
start)
  if [ -f /fastboot ]; then
    msg="发现 fastboot，将跳过"
    msg="${msg}按请求的文件系统检查。\n"
    log_info "${msg}"
    exit 0
  fi

  log_info "正在以只读模式挂载文件系统..."
  mount -n -o remount,ro /dev/null

  if [ $? != 0 ]; then
    log_failure_msg2
    msg="${msg}\n无法检查，因为无法挂载"
    msg="${msg}只读模式下的文件系统，n\n"
    msg="${msg}在您按下回键后，此系统将"
    msg="${msg}停止并关机。\n\n"
    log_failure_msg2 "${msg}"

    log_info "按回车继续..."
    wait_for_user
  fi

  if [ -f /forcefsck ]; then
    msg="发现 /forcefsck，强制强制"
    msg="${msg}按请求的文件系统检查。\n"
    log_info "${msg}"
  fi

  log_info "正在检查文件系统..."
  # （注意：提供的 OCR 文本是片段化的；
  # 以下逻辑遵循所提供页面的流程。）
```

# Linux From Scratch - 版本 11.0

```bash
;;
stop)
  # 不要卸载虚拟文件系统如 /run
  log_info_msg "Unmounting all currently mounted file systems..."
  # 确保移除任何回环设备
  elsetup -D
  umount --all --detach-loop --read-only \
      --types notmpfs,nosysfs,nodevmtfs,noproced,nodepvts >/dev/null
  evaluate_retval

  # 确保 / 以只读模式挂载（仅限 bug）
  mount --options remount, / /

  # 在适当的情况下将所有 LVM 卷组设置为不可用
  # 如果 swap 或 / 在 LVM 分区上，此操作将失败
  #if [ -x /sbin/vgchange ]; then /sbin/vgchange -an /dev/null; fi
  ;;

  *)
    echo "Usage: $0 (start|stop)"
    exit 1
    ;;
esac
# End mountfs
```

## D.10.`/etc/rc.d/init.d/udev_retry`

```bash
#!/bin/sh
################################################################
# 开始 udev_retry
# Description : Udev 热插拔脚本（重试）
# Authors     : Alexander E. Patrakov
#              DJ Lucas - dj@linuxfromscratch.org
# Update      : Bruce Dubbs - dbubbs@linuxfromscratch.org
#              Bryan Kadban
# Version      : LFS 7.0
################################################################

### BEGIN INIT INFO
# Provides       : udev_retry
# Required-Start: udev
# Should-Start:  $local_fs cleansfs
# Required-Stop:
# Should-Stop:
# Default-Start:  S
# Default-Stop: 
# Short-Description: 重放失败的 uevents 并创建额外的设备。
# Description    : 重放任何因初始化缓慢而跳过的失败的 uevents，
#                   并创建所需的设备节点
#
# X-LFS-Provided-By: LFS
### END INIT INFO

/lib/lsb/init-functions

case "${1}" in
  start)
    log_info_msg "Retrying failed uevents, if any..."

    # 从 udev-186 开始开始，--run 选项不再有效
    #rundir=$(/sbin/udevadm --run)
    rundir=/run/udev
    # 自于 Debian：“复制在 / 挂载为可读写之前生成的规则”

    for file in ${rundir}/tmp-rules--*; do
      dest=${file##tmp-rules--}
      [ "${dest}" = "" ] && break
      cat "$file" >> /etc/udev/rules.d/$dest
      rm -f "$file"
    done

    # 重新触发可能失败的 uevents，
    # 期望它们现在可以成功
    /bin/sed -e 's/$.//*//' /etc/sysconfig/udev_retry | /bin/grep -v '^$' | \
    while read line; do
      for subsystem in $line; do
        /sbin/udevadm trigger --subsystem-match=$subsystem --action=add
      done
    done

    # 现在等待 udev 处理我们触发的 uevents
    if ! is_true "OMIT_UDEV_RETRY_SETTLE"; then
      /sbin/udevadm settle
    fi

    evaluate_retval
    ;;

  *)
    echo "Usage ${0} {start}"
    exit 1
    ;;
esac
```

## D.11.`/etc/rc.d/init.d/cleansfs`

```bash
#!/bin/sh
#####################################################################
# 开始 cleansfs
#
# Description : 清理文件系统
# Authors : Gerard Beekmans - gerard@linuxfromscratch.org
# Update : Bruce Dubbs - bdbubms@linuxfromscratch.org
# Version : LFS 7.0

################################################### BEGIN INIT INFO
# Provides: cleansfs
# Required-Start: $local_fs
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start: S
# Default-Stop:
# Short-Description: 在启动过程早期清理临时目录。
# Description: 清理临时目录 /run、/var/lock 以及可选的 /tmp。cleansfs 还会创建 /run/utmp 以及在 /etc/sysconfig/createfiles 中定义的文件。
# X-LFS-Provided-By: LFS
### END INIT INFO

. /lib/lsb/init-functions

# 在启动时创建文件/目录的函数
{
  # 输入到文件描述符 9 并输出到标准输入（重定向）
  exec 9</ /etc/sysconfig/createfiles
  while read name type usr grp dtype maj min
  do
    # 忽略注释和空行
    case "${name}" in
      ""|"(\#*") continue; ;;
    esac

    # 忽略已存在的文件
    if [ ! -e "${name}" ]; then
      # 根据类型创建内容。
      case "${type}" in
        dir)
          mkdir "${name}"
          ;;
        file)
          > "${name}"
          ;;
        dev)
          case "${dtype}" in
            char)
              mkfont "${name}" c ${maj}
              ;;
            block)
              mkfont "${name}" b ${maj}
              ;;
          esac
          ;;
        pipe)
          mkfifo "${name}"
          ;;
        *)
          echo "Unknown type: ${type}" >&2
          ;;
      esac
    fi
  done
  exec 9>&-
}
```

```
exit 1
esac
# End console
```

## D.13. `/etc/rc.d/init.d/localnet`

```bash
#!/bin/sh
############################################################
# Begin localnet
#
# Description : 回环设备
# Authors : Gerard Beekemans - gerard@linuxfromscratch.org
# DJ Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubbs - bdubbs@linuxfromscratch.org
#
# Version : LFS 7.0
############################################################
```

```bash
### BEGIN INIT INFO
# Provides: localnet
# Required-Start: mountvirtfs
# Should-Start: modules
# Required-Stop: 
# Should-Stop: 
# Default-Start: S
# Default-Stop: 0
# Short-Description: 启动本地网络。
# Description: 设置机器的主机并启动回环接口。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
- /lib/lsb/init-functions
[ - /etc/sysconfig/network ] && . /etc/sysconfig/network
[ - /etc/hostname ] && HOSTNAME=$(cat /etc/hostname)
```

```bash
case "$1" in
start)
  log_info_msg "正在启动回环接口..."
  ip addr add 127.0.0.1/8 dev lo
  ip link set lo up
  evaluate_retval

  log_info_msg "正在设置主机名为 ${HOSTNAME}..."
  hostname ${HOSTNAME}
  evaluate_retval
  ;;

stop)
  log_info_msg "正在关闭回环接口..."
  ip link set lo down
  evaluate_retval
  ;;

restart)
  ($0) stop
  sleep 1
  ($0) start
  ;;

status)
  echo "Hostname is: $(hostname)"
  ip link show lo
  ;;

*)
  echo "Usage: $(0) {start|stop|restart|status}"
  exit 1
  ;;
esac

exit 0

# End localnet
```

## D.14. `/etc/rc.d/init.d/sysctl`

```bash
#!/bin/sh
############################################################
# Begin sysctl
#
# Description : 使用 /etc/sysctl.conf 设置内核运行时
#              参数
# Authors : Nathan Coulson (nathan@linuxfromscratch.org)
#           Matthew Burgess (matthew@linuxfromscratch.org)
#           DJ Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubbs - bdbubbs@linuxfromscratch.org
# Version : LFS 7.0
############################################################
```
