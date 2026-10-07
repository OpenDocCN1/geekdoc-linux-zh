
```bash
if [ ! -x ${i} ]; then
  log_warning_msg "${i} is not executable, skipping."
  continue
fi
```

```bash
run() {
  if [ -z ${interactive} ]; then
    ${1} ${2}
    return $?
  fi
```

```bash
while true; do
  read -p "Run ${1} ${2} (Yes/no/continue)?" -n 1 runit
  echo
  case ${1} in
    c | C)
      interactive=""
      ${2}
      ret=$?
      break;
      ;;
    n | N)
      return 0
      ;;
    y | Y)
      ${2}
      ret=$?
      break
      ;;
  esac
done
return $ret
```

# 读取所有本地设置/覆盖
[ - /etc/sysconfig/rc.site ] && source /etc/sysconfig/rc.site

`DISTRO=${DISTRO:-Linux From Scratch}`
`DISTRO_CONTACT=${DISTRO_CONTACT:-lfs-dev@linuxfromscratch.org (Registration required)}`
`DISTRO_MINI=${DISTRO_MINI:---LFS}`
`IPPROMPT=${IPPROMPT:-no}`

# 这 3 个信号不会导致我们的脚本退出
`trap "" INT QUIT TSTP`

```bash
[ "${1}" != "" ] && runlevel=${1}
if [ "${runlevel}" == "" ]; then
  echo "Usage: ${0} <runlevel>" >&2
fi
```

# Linux Scratch - 版本 7.1

`previous=${PRELEVEL}`
`[ ${previous} == "" ] && previous=N`

246

```bash
MSG="WARNING:\n\n${i} can't be "
MSG="${MSG}executed because it was not "
MSG="${MSG}not started in the previous "
MSG="${MSG}runlevel (${previous})."
log_warning_msg "${MSG}"
continue
```

fi

`run ${i} stop`
`error_value=$?`
`if [ "${error_value}" = "0" ]; then print_error_msg; fi`
done

`if [ "${previous}" == "N" ]; then export IN_BOOT=1; fi`
`if [ "${runlevel}" == "6" -a n "${FASTBOOT}" ]; then`
  touch /fastboot
fi

do

# 在此运行级别下启动所有函数
for i in $(ls -v /etc/rc.dc/rc${runlevel}/d/S* 2>/dev/null)
do

if [ "${previous}" == "*" ]; then
  suffix=/etc/rc.dc/rc${runlevel}.d/S[0-9]-[0-9]
  stop=/etc/rc.dc/rc${runlevel}.d/K[0-9]$suffix
  prev_start=/etc/rc.dc/rc${previous}.d/S[0-9]-[0-9]$suffix
```

```bash
[ -f "${prev_start}" -a ! -f "${stop}" && continue
```
fi

check_script_status

case ${runlevel} in

0|6)
```bash
run ${i} stop
;;
*
run ${i} start
;;
```
esac

error_value=$?
if [ "${error_value}" != "0" ]; then print_error_msg; fi
done

# 在切换运行级别 S 时存储交互变量，如果不存在则删除

if [ "${runlevel}" == "S" -a "${interactive}" == "i" ]; then
  echo "interactive=$i" > /var/run/interactive
else
```bash
rm /var/run/interactive 2>/dev/null
```
fi

```bash
# 仅在初始启动时拷贝启动日志
if [ "${previous}" != "${runlevel}" ] && [ "${runlevel}" != "S" ]; then
  cat /var/run/bootlog >> /var/log/boot.log
  # 标记启动结束
  echo "----------------" >> /var/log/boot.log
  # 删除临时文件
  rm -f /run/var/bootlog 2>/dev/null
fi
# 结束 rc
```

## D.2. /lib/lsb/init-functions

```bash
#!/bin/sh
###################################################################################
# /lib/lsb/init-functions
#
# 开始：运行级别控制函数
# 作者      : Gerard Beekmans - gerard@linuxfromscratch.org
#              : DJ Lucas - djlucas@linuxfrom.org
# 更新      : Bruce Dubbs - dbubds@linuxfromscratch.org
# 版本      : LFS 7.0
# 注意        ：代码基于 Matthias Benmann 的 simpleinit-msb
#               http://winterdrache.de/linux/newboot/index.html
#
#               该文件应位于 /lib/ls
###################################################################################
```

## 环境变量设置
# 为环境设置默认值
`umask 022`
`export PATH="/bin:/usr/bin:/usr/sbin"`

## 屏幕尺寸
# Find当前屏幕尺寸
if [ -z "${COLUMNS}" ]; then
  `COLUMNS=$(stty size)`
  `COLUMNS=${COLUMNS%%,*}`
fi

## 当使用远程连接（如串口）时，stty size 返回 0
if [ "${COLUMNS}" = "0" ]; then
  `COLUMNS=80`
fi

## 定位测量值
`COL=$((COLUMNS - 8))`
`WCOL=$((COLUMNS - 2))`
# Linux From Scratch - 版本 7.1

```bash
## 设置光标位置，通过 echo 使用
SET_COL="\033[${COL}G"          # 在 COL 字符处
SET_WCOL="\033[${WCOL}G"        # 在 WCOL 字符处
CURS_UP="\033[1A"               # 向上一行，在 0 字符处
CURS_ZERO="\033[0G"
```

## 设置颜色，通过 echo 使用

# 请查看图形渲染下的代码

# 注意：从 8bit 切换到 9bit 字体时，控制台将重新解释 glyphs (1;2)。这不影响 framebuffer。

```bash
NORMAL="\033[0m"               # 标准控制台灰色
SUCCESS="\033[2m"             # 成功为绿色
WARNING="\033[3m"             # 警告为黄色
FAILURE="\033[1m"             # 失败为红色
INFO="\033[6m"                # 信息青色
BRACKET="\033[4m"             # 括号为蓝色
```

## 使用彩色前缀

`SUCCESS_PREFIX="${SUCCESS}*${NORMAL}"`
`FAILURE_PREFIX="${FAILURE}*****${NORMAL}"`
`WARNING_PREFIX="${WARNING}***${NORMAL}"`
`SUCCESS_SUFFIX="${BRACKET}${SUCCESS} OK${BRACKET}"`
`FAILURE_SUFFIX="${BRACKET}${FAILURE} FAIL${BRACKET}"`
`WARNING_SUFFIX="${BRACKET}${WARNING}WARN${BRACKET}"`

`BOOTLOG=/run/var/bootlog`
`IDELAY=3`

# 设置任何环境变量

[ - /etc/sysconfig/rc.site

################################

# 启动守护进程

# 用法：start daemon [-f] [-n nicelevel] [-p pidfile] pathname [args...]

# 目的：作为守护进程运行程序

# 输入：-f 强制运行程序

#   -n nicelevel：指定 nice 级别。参见 man(1)。

#   -p pidfile：使用指定的文件确定 PIDs。

#   pathname：指定程序的路径

#   args：传递给程序的额外参数

# 返回值（由 LSB 退出码定义）：

#   0 - 程序正在运行或服务正常

#   1 - 通用或参数过多

#   2 - 无效或参数过多

#   5 - 程序未安装

################################################

start_daemon() {
local force=""
local nice="0"
local pidfile=""
local pidlist=""
local retrieval=""

# 处理参数
while true
do
  case "${1}" in
    -f)
      force="1"
      shift 1
      ;;
    -n)
      nice="${2}"
      shift 2
      ;;
    -p)
      pidfile="${2}"
      shift 2
      ;;
    -*)
      return 2
      ;;
    *)
      program="${1}"
      break
      ;;
  esac
done

# 检查有效程序
if [ ! -e "${program}" ]; then return 5; fi

# 执行
if [ -z "${force}" ]; then
  if [ -z "${pidfile}" ]; then
    # 通过发现确定 pid
    pidlist="pidof "${program}"
    retrieval="${?}"
  else
    # PID 文件包含所需的 PIDs
    # 注意，根据 LSB 要求，路径必须传递给 pidof
    # 但当前实现或标准未使用它。
    pidlist="pidof -p "${pidfile}" "${program}"
    retrieval="${?}"
  fi
fi

# 仅返回值
# 记录消息是 init 脚本（或发行版函数）的责任
case "${retrieval}" in
  0)
    # 程序已正确运行，这是成功的启动。
    return 0
    ;;
  1)
    # 程序未运行，存在无效的 pid 文件
    # 删除 pid 文件并继续
    rm -f "${pidfile}"
    ;;
  3)
    # 程序未运行且不存在 pidfile
    # 此处什么都不做，让 start daemon 继续。
    ;;
  *)
    # 状态值返回的其他值将不被解释
    # 并作为未知错误返回。
    return 1
    ;;
esac

# 执行启动！
nice -n "${nice}" "${program}"
#####################################

# killproc() {
# killproc [-p pidfile] pathname [signal]
# 用法：向正在运行的进程发送控制信号
# 目的：向正在运行的进程发送控制信号
# 输入：-p pidfile，使用指定的 pidfile
#   pathname，指定程序的路径
#   signal，向 pathname 发送此信号
# 返回值（由 LSB 退出码定义）：已停止或：
#   0 - 正在运行的程序 (pathname) 已发送指定信号并成功停止
#   1 - 通用或未指定的错误
#   2 - 无效或参数过多
#   5 - 程序未安装
#   7 - 程序未运行且提供了信号
#####################################################

killproc()
{
  local pidfile
  local program
  local prefix
  local progname
```

```bash
local signal="-TERM"
local fallback="-KILL"
local nosig
local pidlist
local retval
local pid
local delay="30"
local piddead
local Springtime
```

```bash
# 处理参数
while true; do
  case "${1}" in
    p)
      pidfile="${2}"
      shift 2
      ;
    *)
      program="${1}"
      if [ -n "${2}" ]; then
        signal="${2}"
        fallback=""
      else
        nosig=1
        # 有额外参数时报错
        if [ -n "${3}" ]; then
          return 2
        else
          break
        fi
  esac
done
```

```bash
# 检查有效程序
if [ ! -e "${program}" ]; then return 5; fi
```

```bash
# 检查有效信号
check_signal "${signal}"
if [ "${?}" -ne 0 ]; then return 2; fi
```

```bash
else
  # PID 包含了需要的 PID
  # 注意 LSB 限制，路径必须传递给 pidofproc，
  # 但当前的实现或标准并未使用它
  pidlist="pidofproc -p "${pidfile}" "${1}""
  retval="${?}"
fi
```

```bash
# 仅返回值
# 记录日志是初始化脚本（或发行版函数）的责任！
case ${retval} in
```

```bash
0)
    # 程序正常运行
    # 在此处什么都不做，让 killproc 继续
    ;;
1)
    # 程序未运行，但存在无效的 pid 文件
    # 删除 pid 文件
rm -f "${pidfile}"
    # 只有在没有传递信号时才视为成功
    if [ -n "${nosig}" ]; then
        return 0
    else
        return 7
    fi
    ;
3)
    # 程序未运行且不存在 pidfile
    # 只有在没有传递信号时视为成功
    if [ -n "${nosig}" ]; then
        return 0
    else
        return 7
    fi
    ;
*)
    # 状态值返回的其他内容不应被解释，
    # 并作为未指定的错误返回
    return 1
    ;
esac
```

```bash
# 为退出信号和控制信号执行不同的操作
check_sig_type "${signal}"
if [ "$?" -eq "0" ]; then # 信号用于终止程序
```

```bash
# 考虑到空 pidlist [pid 文件存在且
# 未给出信号]
if [ "${pidlist}" != "" ]; then
    # 杀死 pid 列表
    for pid in ${pidlist}; do
        kill -0 "${pid}" 2 > /dev/null
```
