
```bash
time=":3"

echo -e "\n"

echo -e "\033${wcol}G${welcome_message}"

echo -e "\033${col}G${i_message}"

echo ""

read -t "$time" -n 1 interactive 2>&1 < /dev/null

fi
```

# 转换为小写

```bash
[ "${interactive}" == "I" ] && interactive="i"

[ "${interactive}" != "i" ] && interactive=""
```

# 如果存在，读取运行级别的状态文件

```bash
[ -r /run/interactive ] && source /run/interactive
```

# 尝试停止上一个运行级别启动的所有，在此运行级别被杀死

```bash
if [ "${previous}" != "!" ]; then

  for i in $(ls -v /etc/rc.d/${runlevel}.d* 2>/dev/null)
  do

    check_status_script

    if [ "${SCRIPT_STAT}" == "1" ]; then

      SCRIPT_STAT="0"

      continue

    fi

    suffix=${i#*/}/etc/rc.d/rc${runlevel}.D[0-9][0-9]
    prev_start=/etc/rc.d/${runlevel}.d/S[0-9][0-9]$suffix
    sys_istint_start=/etc/rc.d/${runlevel}.d/S[0-9][0-9]$suffix

    if [ "${runlevel}" != "6" ]; then
      if [ ! -f ($prev_start) -a ! -f ($sys_istint_start) ]; then
        MSG="警告：\nS${i}无法"
        MSG="${MSG}执行，因为它没有在"
        MSG="${MSG}上一个"
        MSG="${MSG}运行级别 (${previous})."
        continue
      fi
    fi

    run ${i} stop
    error_value=$?

    if [ "${error_value}" != "0" ]; then print_error_msg; fi
  done
fi
```

```bash
if [ "${previous}" != "N" ]; then export IN_BOOT=1; fi
if [ "${runlevel}" = "G" -a n "${FASTBOOT}" ]; then
  touch /fastboot
fi
```

# 启动此运行级别的所有函数

```bash
for i in $(ls -v /etc/rc.d/rc${runlevel}.d/S* 2>/dev/null)
do
# ... (注：此处由于原文重复且不完整，已根据逻辑停止翻译重复部分)
```

```bash
if [ "${error_value}" != "0" ]; then print_error_msg; fi

done
```

```bash
# 在切换到运行级别 S 时存储交互式变量，如果不存在则删除

if [ "${runlevel}" == "S" -a "${interactive}" == "i" ]; then

  echo interactive="i" > /run/interactive

else

  rm -f /run/interactive 2>/dev/null

fi
```

```bash
# 仅在初始启动时拷贝启动日志

if [ "${previous}" == "N" -a "${runlevel}" != "S" ]; then

  cat BOOTLOG >>var/log/boot.log

fi
```

```bash
# 标记启动结束

echo "----------" >> /var/log/boot.log
```

```bash
# 删除临时文件

rm -f BOOTLOG 2>/dev/null

# 结束 rc
```

## D.2. `/lib/lsb/init-functions`

```sh
#!/bin/sh

################################################################################

# 开始 /lib/lsb/init-functions

# ：运行级别控制函数

# 作者 :: Gerard Beekemans - gerard@linuxfromscratch.org

          : D Lucas - dj@linuxfromscratch.org

# 更新 :: Bruce Dubbs - bdububs@linuxfromscratch.org

# 版本 :: LFS 7.0

# 注意：代码基于 Matthias Benkens 的 simpleinit-msb

          http://winterdreche.de/linux/newboot/index.html

################################################################################
```

```bash
# 该文件应位于 /lib/lsb 目录下

################################################################################

## 环境设置

# 为环境设置默认值

umask 022

export PATH=/bin:/usr/bin:/usr/sbin

# 设置颜色命令，通过 echo 使用

# 请参阅 console_codes 获取更多信息

# 位于“ECMA-48 Set Graphics Rendition”章节

# 警告：当从 8 位字体切换到 9 位字体时，

# linux 控制台将重新解释加粗 (1)；

# 使用 9 位字体的前 256 个字符形。这不会影响帧缓冲控制台 (framebuffer consoles)

NORMAL="\033[39m"      # 标准控制台灰色

SUCCESS="\033[32m"      # 成功绿色

WARNING="\033[33m"     # 警告黄色

FAILURE="\033[31m"     # 失败红色

INFO="\033[36m"        # 信息浅青

BRACKET="\033[34m"     # 括号蓝色

# 使用带颜色的前缀

BMPREFIX=""

SUCCESS_PREFIX=$(SUCCESS) * $(NORMAL) ""

FAILURE_PREFIX=$(FAILURE) $(NORMAL) ""

WARNING_PREFIX=$(WARNING) *** $(NORMAL) ""

SKIP_PREFIX=$(INFO) S $(NORMAL) ""

SUCCESS_SUFFIX=$(SUCCESS) OK $[BRACKET]$(NORMAL)

FAILURE_SUFFIX=$(FAILURE) $[BRACKET] FAIL $[BRACKET]$(NORMAL)

WARNING_SUFFIX=$(WARNING) $[WARN]N $[BRACKET]$(NORMAL)

SKIP_SUFFIX=$(BRACKET) $[INFO] SKIP $[BRACKET]$(NORMAL)

BOOTLOG=/run/bootlog

KILLDELAY=0

SCRIPT_STAT="0"

# 设置任何用户定义的环境变量。无界面

[ -r /etc/config/rc.site ] && . /etc/config/rc.site

# 屏幕尺寸

# 查找当前屏幕大小

if [ -z "$(COLUMNS)" ]; then

  COLUMNS=$(stty)

  COLUMNS=${COLUMNS##*}

fi

# 当使用远程连接（如串口）时，tty尺寸返回

if [ "$COLUMNS" = "0" ]; then

  COLUMNS=80

fi

# 用于定位结果消息的测量

COL=$($($(COLUMNS) - 8))

WCOL=$($($(WCOL) - 2))

# 设置光标位置命令，通过 echo 使用

SET_COL="\033[$$(COL)H"      # 在 $COL 处

SET_WCOL="\033[$$(WCOL)G"     # 在 $WCOL 处

CUR_UP="\033[1A\033[0G"     # 向上移动，位于第0个字符

CURS_ZERO="\033[0G"
```

```bash
# start_daemon()

# 用法: start_daemon [-f] [-n nicelevel] [-p pidfile] filename [args...]

# 目的：将指定的程序作为守护进程运行

# 输入: -f (强制) 即使程序已运行也运行程序。

# -n nicelevel: 指定 nice 级别。参见 'man nice(1)'。

# -p pidfile: 使用指定的文件确定 PID。

# pathname: 指定程序的完整路径

# args: 传递给程序 (pathname) 的额外参数

# 返回值（由 LSB 退出状态码定义）：

#   - 0 - 程序正在运行或服务正常

#   - 1 - 通用或未指定的错误

#   - 2 - 无效或过多的参数

#   - 5 - 程序未安装

################################################################################

start_daemon()
{

  local force=""

  local nice=""

  local pidfile=""

  local retval=""

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

  # 检查程序是否存在
  if [ ! -f "$program" ]; then return 5; fi
  if [ -n "$pidfile" ]; then
    # 检查 PID 是否运行
    if kill -0 `cat "$pidfile"` 2>/dev/null; then
      return 0 # 程序正在运行
    fi
  fi

  # 执行程序
  if [ -n "$nice" ]; then
    nice -n "$nice" "$program" "$@" &
  else
    "$program" "$@" &
  fi

  local pid=$!

  if [ -n "$pidfile" ]; then
    echo $pid > "$pidfile"
  fi

  return 0
}
```

```bash
# killproc()

# 用法: killproc [-p pidfile] [signal]

# 目的：向程序发送信号

# 输入：-p pidfile 指定包含 PID 文件

# signal：要发送的信号（默认 TERM）

# pathname：要停止的程序

# 返回值（由 LSB 退出状态定义）：

#   - 0 - 程序已停止

#   - 1 - 通用或未指定的错误

#   - 2 - 无效或过多的参数

#   - 5 - 程序未找到

killproc()
{

  local pidfile=""

  local signal="${TERM}"

  local pathname

  # 处理参数
  while true
  do
    case "${1}" in
      -p)
        pidfile="${2}"
        shift 2
        ;;
      -*)
        signal="${1# -}"
        shift
        ;;
      *)
        pathname="${1}"
        break
        ;;
    esac
  done

  # 检查 PID
  if [ -n "$pidfile" ]; then
    local pid=$(cat "$pidfile" 2>/dev/null)
    if [ -z "$pid" ]; then
      return 0 # PID 文件不存在，视为停止
    fi

    # 发送信号
    kill -"$signal" "$pid" 2>/dev/null
    if [ $? -eq 0 ]; then
      # 等待进程退出
      local timeout=0
      while kill -0 "$pid" 2>/dev/null; do
        sleep 1
        timeout=$((timeout + 1))
        if [ $timeout -ge 10 ]; then
          kill -9 "$pid" 2>/dev/null
          return 1 # 超时错误
        fi
      done

      rm -f "$pidfile"
      return 0
    else
      return 1 # 发送信号失败
    fi
  else
    # 如果没有 PID 文件，使用 pkill
    if pkill -f "$pathname" 2>/dev/null; then
      return 0
    else
      return 1
    fi
  fi
}
```
