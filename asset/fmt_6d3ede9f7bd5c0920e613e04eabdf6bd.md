
[ `-d /sys/class/graphics/fb0` ] && use_fb=1 || use_fb=0

# 获取将控制台设置为
# 目标模式的命令

`is_true "${UNICODE}"` &&

`MODE_COMMAND=echo -en '\033[G'` && `kbd_mode -u` ||

`MODE_COMMAND=echo -en '\033[K'`

```bash
    esac

    # 同时设置权限。
    chown ${usr}:${grp} "${name}"
    chmod ${perm} "${name}"
fi
done

# 关闭文件描述符 9（结束重定向）
exec 0>&9&-
return 0

case "${1}" in
start)
  log_info_msg "清理文件系统"
  if [ "${SKTMPCLEAN}" = "" ]; then
    log_info_msg2 "/tmp"
    cd tmp && &
    find -xdev -minddepth 1 ! -name lost+found -delete || failed=1
  fi
  /var/run/utmp
  if grep -q "utmp" /etc/group ; then
    chmod 664 /var/run/utmp
    chgroup utmp /var/run/utmp
  fi
  (exit $($failed))
  evaluate_retval
  if egrep -vq '^([^|#)$' /etc/sysconfig/createfiles 2>/dev/null; then
    log_info_msg "创建文件和目录..."
    create_files # 始终返回 0
    evaluate_retval
  fi
  exit $failed
;;
*)
  echo "用法: ${0} {start}"
  exit 1
;;
esac
```

## D.12. /etc/rc.d/init.d/console

```bash
#!/bin/sh
################################################################
# 开始 console
#
```

# 结束 cleanfs
# Description : 设置键映射和屏幕字体
# Authors : Gerard Beekmans gerard@linuxfromscratch.org
Alexander E. Patrovok
DJ Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubbs dbubds@linuxfromscratch.org
# Version : LFS 7.0
#####################################################################################

```bash
### BEGIN INIT INFO
# Provides: console
# Required-Start: $local_fs
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start: S
# Default-Stop:
# Short-Description: 设置本地化控制台。
# Description: 根据 /etc/sysconfig/console 定义为用户
# 设置字体和语言设置。
# X-LFS-Provided-By: LFS
#### END INIT INFO
```

```bash
/lib/lsb/init-functions
# 母语为英语的人可能根本没有 /etc/sysconfig/console
[ -r /etc/sysconfig/console ] && . /etc/sysconfig/console
```

```bash
is_true() {
{
n [ "$1" = "1" ] || [ "$1" = "yes" ] || [ "$1" = "true" ]
}
}
```

```bash
case "$1" in
start)
# 如果我们需要看到 ${KEYMAP} &&
if [ -z "${KEYMAP}" ] && -z "${KEYMAP_CORRECTIONS}" ] &&
  [ -z "${FONT}" ] && -z "${LEGACY_CHARSET}" ] &&
  ! is_true "${UNICODE}" ; then
  exit 0
fi
```

```bash
# 此行之后不应有虚假的失败！
log_info_msg "设置 Linux 控制台..."
# 查询是否使用了帧缓冲区控制台
[ -d /sys/class/graphics/fb0 ] && use_fb=1 || use_fb=0
# 获取将控制台设置为
# 目标模式的命令
is_true "${UNICODE}" &&
MODE_COMMAND=echo -en '\033[G' && kbd_mode -u ||
MODE_COMMAND=echo -en '\033[K'
```

```bash
    esac
    # 同时设置权限。
    chown ${usr}:${grp} "${name}"
    chmod ${perm} "${name}"
fi
done
... (考虑到原始文本中存在大量重复块，我将提供逻辑清晰的完整翻译)
```

**注：由于原文在输入中存在大量完全重复的代码块，我将根据逻辑结构提供一份准确的翻译。**

**最终译文：**

# Linux From Scratch - 版本 9.0

```bash
# Required-Start: $local_fs
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start: S
# Default-Stop:
# Short-Description: 在启动过程早期清理临时目录。
# Description: 清理临时目录 /var, /var/lock 以及
# 可选的 /tmp。还会清理 /var/utmp
# 以及 /etc/sysconfig/createfiles 中定义的任何文件。
# X-LFS-Provided-By: LFS
#### END INIT INFO
```

```bash
/lib/lsb/init-functions
# 在底部创建文件/描述符的函数。
create_files()
{
    # 将输入重定向到文件描述符 9，输出到 stdin（重定向）
    exec 9< /etc/sysconfig/createfiles
    while read -name type perm usr grd dtype maj min junk
    do
        # 忽略注释和空行。
        case "${name}" in
            \#*") continue;
        esac
        # 忽略已存在的文件。
        if [ -e "${name}" ]; then
            # 根据类型创建。
            case "${type}" in
                dir)
                    mkdir "${name}"
                    ;
                file)
                    :> "${name}"
                    ;
                dev)
                    case "${type}" in
                        char)
                            mkod "${name}" c ${maj} ${min}
                            ;
                        block)
                            mkod "${name}" b ${maj} ${min}
                            ;
                        pipe)
                            mkod "${name}" p
                            ;
                        *)
