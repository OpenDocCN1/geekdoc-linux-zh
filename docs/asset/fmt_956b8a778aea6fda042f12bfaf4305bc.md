
```bash
# 如果设置了备用方案且仍在运行，则
# 使用备用方案
if [ -n "${fallback}" -a "${piddead}" != "1" ]; then
kill "${fallback}" "${pid}" 2 >/dev/null
sleep 1
fi
```

```bash
# 再次检查，如果仍在运行
kill -0 "${pid}" 2 >/dev/null && return 1
fi
done
```

```bash
# 检查并移除过时的 PID 文件。
if [ -n "${pidlist}" ]; then
# 查找 $program 的基名
prefix=$(echo "${program}" | sed 's|.*/[^/]*//')
progame=$(echo "${program}" | sed "s@${prefix}@@")
```

```bash
if [ -e "/run/${progame}.pid" ]; then
rm -f "/run/${progame}.pid" 2 >/dev/null
else
if [ -e "${pidfile}" ]; then rm -f "${pidfile}" 2 >/dev/null;
fi
```

# 对于不期望程序退出的信号，只需让

# kill 执行工作，并评估 kill 的返回值

```bash
else # check_sig_type - 信号未用于终止程序
for pid in ${pidlist}; do
kill "${signal}" "${pid}"
if [ "$?" -ne "0" ]; then return 1;
done
fi
```

############################################################

# `pidofproc()`

# 用法: `pidofproc [-p pidfile] pathname`

# 目的: 此函数返回特定守护进程的一个或多个 pid

# 输入: `-p pidfile`，使用指定的 pidfile 代替 pidof 查找

#       `pathname`，指定程序的路径

#

# 返回值（由 LSB 状态码定义）：

# 0 - 成功（将 PID 输出到标准输出）

# 1 - 程序已死，pid 文件仍存在（剩余的 PID）

# 3 - 程序未在运行（无输出）

############################################################

```bash
pidofproc()
{
    local pidfile
    local program
    local prefix
    local progname
    local pidlist
    local lpids
    local exitstatus="0"

    # 处理参数
    while true; do
        case "$1" in
            -p)
                pidfile="$2"
                shift 2
                ;;
            program)
                program="$1"
                if [ -n "$2" ]; then
                    # 参数过多
                    # 由于这是状态查询，返回 4
                    return 4
                else
                    break
                fi
                ;;
        esac
    done

    # 如果未指定 PID 文件，则尝试寻找一个。
    if [ -z "$pidfile" ]; then
        # 获取程序的基名
        prefix=$(echo "$program" | sed 's|/[/].*//')
    fi

    if [ -z "$prefix" ]; then
        progname="$program"
    else
        progname=$(echo "$program" | sed "s@${prefix}@@")
    fi

    # 如果存在同名的 PID 文件，假设它就是
    if [ -e "/run/${progname}.pid" ]; then
        pidfile="/run/${progname}.pid"
    fi
fi

# Linux From Scratch - Version 11.3
# 如果设置了 PID 文件且存在，则使用它。
if [ -n "$pidfile" -a -e "$pidfile" ]; then
  # 使用 pid 文件第一行的值
  pidlist=$(head -n1 "$pidfile")
  # 这可以可选地写为 'sed -n1q' 以替换 head -n1
  # LPS 应该将 /bin/head 移动到 /usr/bin/head
else
  # 使用 pidof
  pidlist=$(pidof "$program")
fi

# 确定所有列出的 PID 是否都在运行。
for pid in $pidlist; do
  kill -0 $pid 2>/dev/null
done

if [ "$?" -eq "0" ]; then
  lpids="$lpids$pid"
else
  exitstatus=1
fi

if [ -z "$lpids" -a -f "$pidfile" ]; then
  return 3
else
  echo "$lpids"
  return "$exitstatus"
fi
```

############################################

# `statusproc()`

# 用法: `statusproc [-p pidfile] filename`

# 目的: 此函数打印特定守护进程的状态

# 输入: `-p pidfile`，使用指定的 pidfile 代替 pidof

#       `filename`，指定程序的路径

# 返回值:

#   0 - 已打印状态

#   1 - 错误。未指定守护进程。

############################################

```bash
statusproc()
{
  local pidfile
  local pidlist
  if [ "$1" = "0" ]; then
    echo "Usage: statusproc [-p pidfile] filename"
    exit 1
  fi

  # 处理参数
  while true; do
    case "$1" in
      -p)
        pidfile="$2"
        shift 2
        ;;
      *)
        if [ -n "$2" ]; then
          echo "参数过多"
          return 1
        else
          program="$1"
          break
        fi
        ;;
    esac
  done

  if [ -n "$pidfile" ]; then
    pidlist=$(cat "$pidfile")
  else
    pidlist=$(pidof "$program")
  fi

  # 去除尾部空格
  pidlist=$(echo "$pidlist" | sed 's *$//')
  base=$(echo "$program" | sed 's|.*/[^/]*//')

  if [ -n "$pidlist" ]; then
    for pid in $pidlist; do
      if kill -0 "$pid" 2>/dev/null; then
        echo -e "${INFO}${base} 运行中"
      else
        if [ -e "/run/${base}.pid" ]; then
          echo -e "${WARNING}${base} 未运行但 /run/${base}.pid 存在"
        else
          echo -e "${INFO}${base} 未运行"
        fi
      fi
    done
  fi

  return 0
}
```
