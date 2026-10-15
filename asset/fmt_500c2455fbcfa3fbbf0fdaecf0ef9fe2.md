
```bash
######################################################################
# check_sig_type() [-signal] | [signal ]
# 目的: 检查信号是程序终止信号还是控制信号
# 这在 LSB 草案中没有定义，但需要
# 检查信号以确定它们是用于结束
# 程序还是仅仅为了控制它。
######################################################################
```

# Linux 从头构建 - 版本 11.3

# 输入: 接收格式为或 `-(signal)` 或 `(signal)` 的单个字符串值

# 返回值:

# 0 - 信号用于程序终止

# 1 - 信号用于程序控制

######################################################################

```bash
check_sig_type() {
  local vaisig

  # 终止信号列表（限制为通用使用的项目）
  vaisig="ALRM -INT -KILL -TERM -PWR -STOP -ABRT -QUIT -2 -3 -6 -9 -14 -15"

  echo "$vaisig" | grep -E "$1" /dev/null

  if [ "$1" -eq "0" ]; then
    return 0
  else
    return 1
  fi
}
```

```bash
######################################################################
# wait_for_user()
# 目的: 如果不是无头系统，则等待用户响应
######################################################################
```

```bash
wait_for_user() {

  # 默认等待用户

  [ "(HEADLESS=0)" = "0" ] && read ENTER

  return 0

}
```

```bash
######################################################################
# is_true()
# 目的: 测试变量是否为 true | yes | 1 的工具
######################################################################
```

```bash
is_true() {

  [ "$1" = "1" ] || [ "$1" = "yes" ] || [ "$1" = "true" ] || [ "$1" = "y" ] ||

  [ "$1" = "t" ]

}
```

# End `/lib/lsb/init-functions`

## D.3. `/etc/rc.d/init.d/mountvirtfs`

```bash
#!/bin/sh
# 开始挂载 mountvirtfs
# 描述：确保 proc, sysfs, run 和 dev 已挂载

+   - # 作者：Gerard Beekemans - gerard@linuxfromscratch.org
- # DJ Lucas - dj@linuxfromscratch.org
- # 更新：Bruce Dubbs - bdubbs@linuxfromscratch.org
- # 版本：LFS 7.0

# Linux 从头构建 - 版本 11.3
```

```bash
### BEGIN INIT INFO

# Provides: mountvirttfs

# Required-Start: $first

# Should-Stop:

# Required-Stop:

# Should-Stop:

# Default-Start:

# Default-Stop:

# Description: 挂载启动时所需的特殊 fs

# 挂载 /sys 和 /dev/proc (内核) 文件系统。

# 挂载 /run (tmpfs) 和 /dev (devtmpfs)。

# 仅在它们尚未挂载时才执行操作。

# 使用书中建议的内核配置，dev

# 应该由内核自动挂载。

### X-LFS-Provided-By: LFS

### END INIT INFO
```

```bash
/lib//init-functions

case "$1" in

start)

  # 在记录消息之前确保 /run 可用

  if mountpoint /run >/dev/null; then

    mount /run || failed=1

  fi

  mkdir -p /run/lock

  chmod 1777 /run/lock

  log_info "Mounting virtual systems"

  if mountpoint /proc >/dev/null; then

    log_info "proc"

  fi

  if mountpoint /sys >/dev/null; then

    log_info "sys"

  fi

  if mountpoint /run >/dev/null; then

    log_info "run"

  fi

  if mountpoint /dev >/dev/null; then

    log_info "dev"

  fi
```
```

```bash
log_failure_msg2
\无法创建 "nmsg=FAILURE:\n无法创建 "\nmsg=$($)没有 SysFS 文件系统的设备\n\nmsg=$($)在您按下回车键后，系统 "\nmsg=$($)将停止并关机。\n\n\"
log_info_msg "$msg"
log_info_msg "按下回车继续..."
wait_for_closure
/etc/rc.d/init.d/halt stop
```

```bash
# 启动 udev 进程以持续监控并处理
# udev事件
/sbin/udevd --daemon

# 遍历 /sys 以对设备进行“冷热插”
/sbin/udevadm trigger --action --add --type=subsystems
/sbin/udevadm trigger --action --add --type=devices
/sbin/udevadm trigger --action --change --type=devices
```

```bash
# 等待 udev 产生我们触发的事件
if ! is_true "$0_UDEV_SETTLE"; then
/sbin/udev settle
```

```bash
# 如果系统上有任何 LVM 分区，确保它们已激活
# 以便可以使用。
if [ -x /sbin/vgchange ]; then /sbin/vgchange -a y >/dev/null; fi

log_success_msg2;
```

```bash
*)
echo "用法: ${0} (start)"
exit 1
;;

esac

exit 0

#  udev
```

## D.6. `/etc/rc.d/init.d/swap`

```bash
#!/bin/sh

################################################################################

# 开始 swap

# Description : 交换控制脚本

# Authors       : Gerard Beekemans - gerard@linuxfromscratch.org

               # DJ Lucas - dj@linuxfromscratch.org

               # Bruce Dubbs - bdubbs@linuxfromscratch.org

# Update        

# Version       : LFS 7.0

#

################################################################################
```

```bash
### BEGIN INIT INFO

# Provides:      swap

# Required-Start: udev

# Linux From Scratch - Version 11.3

# Should-Start: modules
```
