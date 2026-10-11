
**安装依赖于：** `Bash`, `Binutils`, `Coreutils`, `GCC`, `Glibc`, `Make`, 和 `Sed`

**测试套件依赖于：** 无

**必须安装之前：** `File`, `Kmod`, `Perl`, 和 `Util-linux`

**可选依赖于：** 无

## 附录 D. Boot 和 sysconfig 脚本

version-20190524

### D.1. `/etc/rc.d/init.d/rc`

`rc` 脚本是 `init` 用的第一个脚本，并初始化启动过程。

```bash
#!/bin/bash
################################################################
# 开始 rc
# ：主运行级别控制脚本
# 作者
  : Gerard Beekemans - gerard@linuxfromscratch.org
  : DJ Lucas - djluc@linuxfromscratch.org
# 更新
  : Bruce Dubbs - bdubbs@linuxfromscratch.org
# 版本
  : LFS 7.0
################################################################

/lib/lsb/init-functions

print_error_msg() {
  log_failure_msg
  # $i 在调用时设置
  MSG="$FAILURE\/nYou不应该读取此错误消息。\n\n"
  MSG="$MSG)$i 意味着发生了发生了意料之外的错误\n"
  MSG="$MSG)${i},\n"
  MSG="$MSG)$其退出时的返回值为 $(error_value)。\n"

  MSG="$MSG)如果你能将此错误追踪到 ${DISTRO_MINI} 书中提供的"
  MSG="$MSG)文件中的某一行，\n"
  MSG="$MSG)请务必向 ${DISTRO_CONTACT} 通知我们。\n"
  log_failure_msg "$MSG"
}

log_info_msg "按回车键继续..."
  wait_for_user
}

check_script_status() {
  # $i 在调用时设置
  if [ ! -f ${i} ]; then
    log_warning_msg "${i} 不是一个有效的符号链接。"
    SCRIPT_STAT="1"
  fi
}

if [ ! -x ${i} ]; then
  log_warning_msg "${i} 不可执行，跳过。"
  SCRIPT_STAT="1"
fi

run()
{
    if [ -z $interactive ]; then
        ${1} $($2)
        return $?
    fi

    while true; do
        read -p "运行 $($1) $($2) (是/否/继续)? " -n 1 run
        echo
        case $($1) in
            c | C)
                interactive=""
                $($1) $($2)
                ret=$?
                break;
                ;;
            n | N)
                return 0
                ;;
            y | Y)
                $($1) $($2)
                ret=$?
                break;
                ;;
        esac
    done
    return $$
}

# 读取任何本地设置/覆盖
[ -r /etc/sysconfig/rc.site ] && source /etc/sysconfig/rc.site
DISTRO=$DISTRO-"Linux from Scratch"
DISTRO_CONTACT=$DISTRO_CONTACT-"lfs-dev@linuxfromscratch.org (需要注册)"
DISTRO_MINI=$DISTRO_MINI-"LFS"
IPROMPT=$IPROMPT-"no"

# 这 3 个信号不会导致我们的脚本退出
trap "" INT QSTOP
```

```bash
[ "${1}" != "" ] && runlevel=$($1)
```

```bash
if [ "${runlevel}" == "" ]; then
    echo "用法: $0 <runlevel>" >&2
    exit 1
fi
```

```bash
previous=$(PRELEVEL)
[ "$(previous)" = "" ] && previous=N
```

```bash
if [ ! -d /etc/rc.d/$(runlevel).d ]; then
  log_info_msg "/etc/rc.d/$(runlevel).d 不存在。"
fi
```

```bash
if [ "$runlevel" = "6" -o "$runlevel" = "0" ]; then iPROMPT="no"; fi
```

```bash
if [ "$iPROMPT" = "yes" -a "$runlevel" = "S" ]; then
# 发行版消息的总长度
len=$(echo "Welcome to ${DISTRO}" | wc -c)
welcome_message="Welcome to ${DISTRO}"
# 交互式字符串的总长度
ilen=$(echo "Press to enter startup" | wc -c)
image_message="Press ${FAILURE} to enter startup"
# dcol 和 icol 是在屏幕上居中消息前的空格
# 以及用户按键的时间
wcol=$(( COLUMNS) - $len ) / 2
icol=$(( COLUMNS) - $ilen ) / 2
time=$(( -t ))
echo -e "\n"
echo -e "\033[${wcol}${welcome_message}"
echo -e "\033[${icol}${image_message}"
echo -e ""
read -t ${time} -n 1 interactive 2>/dev/null
# 转小写
[ "$interactive" = "I" ] && interactive="i"
[ "$interactive" != "i" ] && interactive="i"
# 如果存在则读取文件
[ -r /var/interactive ] && source /var/interactive
# 停止上一个运行级别启动的所有
# 在此运行级别被杀死
if [ "${previous}" != "N" ]; then
  for i in $(ls -v /etc/rc.d/$(runlevel).d/K* 2>/dev/null);
  do
    check_script_status
    if [ "$SCRIPT_STAT" = "1" ]; then
      SCRIPT_STAT="0"
      continue
    fi
    suffix=${i#/etc/rc.d/$(runlevel).d/K[0-9][0-9]}
    prev_start=/etc/rc.d/$(previous).S[0-9][0-9]
    sysinit_start=/etc/rc.d/$(runlevel).d/S[0-9][0-9]
    if [ "$runlevel" != "0" -a "$runlevel" != "6" ]; then
      if [ ! -f "${prev_start}" ] -a ! -f "${sysinit_start}" ]; then
        MSG="$(MSG)警告：n$(i) 无法执行因为它没有在上一个运行级别 (${previous})中启动"
        log_warning_msg "$MSG"
        continue
      fi
    run${i} stop
    error_value=${?}
    if [ "${error_value}" != "0" ]; then print_error_msg;fi
    if [ "${previous}" != "N" ]; then export IN_BOOT=1; fi
    if [ "$runlevel}" != "6" -a n "${FASTBOOT}" ]; then
