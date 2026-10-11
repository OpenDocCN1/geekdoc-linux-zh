
## D.9. `/etc/rc.d/init.d/mountfs`

```bash
#!/bin/sh
##################################################
# 开始 mountfs
# Description : 文件系统挂载脚本
# Authors : Gerard Beekmans gerard@linuxfromscratch.org
          DL Lucas dlucas@linuxfromscratch.org
# Update : Bruce Dubbs bdubbs@linuxfromscratch.org
# Version : LFS 7.0
##################################################

### BEGIN INIT INFO
# Provides: local_fs
# Required-Start: udev checkfs
# Should-Start: modules
# Required-Stop: localnet
# Should-Stop:
# Default-Start: S
# Default-Stop: 6
# Short-Description: 重新挂载 /etc/fstab 中定义的本地文件系统。
# Description: 启动时重新挂载根文件系统为读写，并挂载 /etc/fstab 中定义的剩余本地文件系统。停止时重新挂载根文件系统为只读并卸载剩余文件系统。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
/lib/fs/init-functions

case $1 in
start)
  log_info_msg "正在以读写模式重新挂载根文件系统..."
  mount --options remount, rw /</dev/null
  evaluate_retval

  # 移除 fsck 相关的标记。
  rm -f /fastboot /forceck

  # 确保 /dev/pts 存在
  mkdir -p /dev/pts

  # 将挂载所有没有 _netdev 的文件系统
```

# Linux From Scratch - 版本 11.3

```
# 它们的选项列表。 .netdev 表示网络文件系统。

log_info_msg "挂载剩余的文件系统..."
failed=0
mount --all --test-opts no_netdev /dev/null || failed=1
evaluate_retval
exit $failed
;

stop)
    # 卸载虚拟文件系统 /run
    log_info_msg "卸载所有当前挂载的文件系统..."
    # 确保移除任何回环设备
    losetup -D
    mount --all --detach-loop --read-only \
        --types notmpfs, nosysfs, nodevmpfs, noproproc, nodevdevs /dev/null
    evaluate_retval

    # 确保以只读模式挂载 (imount bug)
    mount --options remont,ro /

    # 将所有 LVM 卷组设置为不可用（如果适用）
    # 如果 swap 或 / 位于 LVM 分区，则此处会失败
    #if [ -x /sbin/vgchange ]; then /sbin/vgchange -an > /dev/null; fi
    if [ -f /mdadm.conf ]; then
        log_info_msg "标记数组为洁净..."
        mdadm --wait-clean --scan
        evaluate_retval
    fi
    ;

*)
    echo "用法: ${0} [start|stop]"
    exit 1
    ;

esac

# 结束 mountfs
```

## D.10. `/etc/rc.d/init.d/udev_retry`

```bash
#!/bin/sh
######################################################################
# 开始 udev_retry
# 说明 : Udev 热插拔脚本（重试）
# 作者      : Alexander E. Patrakov
# DJ Lucas - dj@linuxfromscratch.org
# 更新      : Bruce Dubbs - bdubbs@linuxfromscratch.org
# Bryan Kadzban -
# 版本     : LFS 7.0
######################################################################
```

```bash
/lib/fs/init-functions
case ${1} in
  start)
    if [ -f /fastboot ]; then
      msg="发现 fastboot，跳过文件检查。"
      log_info_msg "${msg}"
      exit 0
    fi

    log_info_msg "正在以只读模式挂载根目录..."
    mount -n -o remount -ro /</dev/null

    if [ $? -ne 0 ]; then
      log_failure_msg
      msg="\无法以只读模式挂载根目录。\n在您按下回车后，系统将停止并关机。\n"
      log_failure_msg "${msg}"

      log_info_msg "按下回车继续..."
      wait_for_user
      etc/rc.d/init.halt stop
    else
      log_success_msg

    if [ -f /force ]; then
      msg="发现 force，按请求强制文件检查。"
      log_success_msg="${msg}"
      options="-f"
    else
      options=""
      log_info_msg="正在检查文件系统"
      # 注意：以前选项是 -p；但在 fsck.minix 上会失败。
      if is_true VERBOSE; then
        fsck($options) -a -C -T
      else
        fsck($options) -A -C >/dev/null
      fi

      if [ "${error_value}" = 0 ]; then
        log_success_msg
      fi

      if [ "${error_value}" = 1 ]; then
        msg="警告：发现并修复了文件错误。\n您可能需要双检是否修复良好。"
        log_warning_msg="${msg}"
      fi

      if [ "${error_value}" = 2 -o "${error_value}" = 3 ]; then
        msg="警告：发现并修复了文件错误，但由于性质原因系统需要重启。\n在您按下回车后，系统将重启。\n"
        log_failure="${msg}"
      fi

      if [ "${error_value}" -gt 3 -a "${error_value}" -lt 16 ]; then
        msg="失败：遇到了无法自动修复的文件系统错误。\n系统无法继续启动，直到由系统管理员手动修复错误。\n在您按下回车后，系统将停止并关机。\n"
        log_failure="${msg}"
        log_info_msg="按下回车继续..."
        wait_for_user
        reboot -f
        etc/rc.d/init.d halt
      fi

      if [ "${error_value}" -ge 16 ]; then
        msg="失败：运行 fsck 时出现意外失败。退出代码为：${error_value}.\n"
        log_info_msg $msg
        exit ${error_value}
      fi

      exit 0
    ;;
  *
    echo "用法: $(0) (start)"
    exit 1
;;
esac

# End checkfs
```
