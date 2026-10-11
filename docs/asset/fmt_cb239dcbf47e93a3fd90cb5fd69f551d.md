
```bash
# 仅返回值
# 记录日志是初始化脚本（或发行版函数）的责任！
case "${retval}" in
  # 程序运行正常
  # 此处什么都不做，让 killproc 继续执行。
  ;;

  # 只有在没有传递信号时，这里才成功。
  if [ -n"${nosig}" ]; then
    return 0
  else
    return 7
  fi

  # 程序未运行且不存在 pidfile
  # 只有在没有传递信号时，这里才成功。
  if [ -n"${nosig}" ]; then
    return 0
  else
    return 7
  fi

  # 其他由状态值返回的内容不应被解释，
  # 并作为未知错误返回。
  return 1
esac

if [ "${retval}" -eq "0" ]; then # 信号用于终止程序
  # 考虑到 pidlist 为空（pid 文件仍存在且未给出信号
  if [ "${pidlist}" != "" ]; then
    # 杀死 PID 列表
    for pid in ${pidlist}; do
      kill -0 "$(pid)" 2> /dev/null
      if [ "$($?)" -ne "0" ]; then
        # 进程已死，继续处理并假设一切正常
        continue
      else
        kill "$(signal)" "$(pid)" 2> /dev/null
        # 等待最多 ${delay}/10 秒让 "$(pid)" 
        # 以 0.1 秒为单位进行终止
        while [ "${delay}" -ne "0" ]; do
          kill -0 "$(pid)" 2> /dev/null || piddead="1"
          if [ "${piddead}" = "1" ]; then break; fi
          sleep 0.1
          delay=$($($(delay) - 1))
        done

        # 如果设置了备用方案且程序仍在运行，
        # 则使用备用方案
        if [ -n "${fallback}" -a "${piddead}" != "1" ]; then
          kill "$(signal)" "$(pid)" 2> /dev/null
          sleep 1
          # 再次检查，如果仍在运行则失败
          kill -0 "$(pid)" 2> /dev/null && return 1
        fi
      fi
    done

    # 检查并移除过期的 PID 文件。
    if [ -z "${pidfile}" ]; then
      # 获取 $program 的基名
      prefix=$(echo "${program}" | sed 's/[^/]*$//')
      programe=$(echo "${program}" | sed "s@${prefix}*@")

      if [ -e "/var/run/${programe}.pid" ]; then
        rm -f "/var/run/${programe}.pid" 2> /dev/null
      fi
    fi
    if [ -f "${pidfile}" ]; then
      rm -f "${pidfile}" 2> /dev/null
    fi
  else
    # 对于不期望程序退出的信号，只需让
    # kill 执行工作，并对 kill 的返回值进行检查
    # check_sig_type - 信号未用于终止程序
    for pid in ${pidlist}; do
      kill "$(signal)" "$(pid)"
      if [ "$($?)" -ne "0" ]; then return 1; fi
    done
  fi
fi
```

################################################################################

# `pidofproc()`

# 用法: `pidofproc [-p pidfile] filename`

#

# 目的: 此函数返回某个特定守护进程的一个或多个 PID

#

# 输入: `-p pidfile`，使用指定的 `pidfile` 代替 `pidof` 路径，指定程序的路径

#

# 返回值（根据 LSB 状态码定义）：

# `0` - 成功（将 PID 输出到 stdout）

# `1` - 程序已死，PID 文件仍存在（输出剩余 PID）

# `3` - 程序未运行（无输出）

################################################################################

```bash
pidofproc()
{
  local pidfile
  local prefix
  local progname
  local pidlist
  local lpid
  local exitstatus="0"

  # 处理参数
  while true; do
    case "${1}" in
      -p)
        pidfile="${2}"
        shift 2
        ;;
      *)
        program="${1}"
        if [ -n "${2}" ]; then
          # 参数过多
          # 因为这是状态查询，返回未知
          return 4
        else
          break
        fi
    esac
  done

  # 如果未指定 PID 文件，尝试查找一个。
  if [ -z "${pidfile}" ]; then
      # 获取程序的基名
      prefix=$(echo "${program}" | sed 's/[^/]*$//')

      if [ -z "${prefix}" ]; then
        progname="${program}"
      else
        progname=$(echo "${program}" | sed "s@${prefix}*@")
      fi

      # 如果存在同名的 PID 文件，则假设它就是。
      if [ -e "/var/run/${progname}.pid" ]; then
        pidfile="/var/run/${progname}.pid"
      fi
  fi

  # 如果设置了 PID 文件且存在，则使用它。
  if [ -n "${pidfile}" -a -e "${pidfile}" ]; then
    # 使用 pidfile 第一行的值
    pidlist=$(head -n 1 "${pidfile}")
    # 这可以可选写为 'sed lq' 来替换 'head -nl'
    # 如果 LFS 将 /bin/head 移动到 /usr/bin/head
  else
    # 使用 pidof
    pidlist=$(pidof "${program}")
  fi

  # 确认所有列出的 PID 都在运行。
  for pid in ${pidlist}; do
    kill -0 "${pid}" 2> /dev/null
    if [ "$$?" -eq 0 ]; then
      lpids="${lpids}"
    else
      exitstatus="1"
    fi
  done

  if [ -z "${lpids}" ]; then
    return 3
  else
    return "${exitstatus}"
  fi
}
```

## 从日志文件中移除非可打印字符

```bash
timespec
logmessage=`echo "$@" | sed 's/\\033[a-zA-Z]*///g'
/bin/echo -e "${STAMP} ${logmessage} FAIL >> ${BOOTLOG}"

return 0
```

```bash
log_failure_msg2()
{
  /bin/echo -n -e "${BMPREFIX}${@"
  /bin/echo -e "${CURS_ZERO}${FAILURE_PREFIX}${SET_COL}${FAILURE_SUFFIX}"

  echo "FAIL" >> ${BOOTLOG}

  return 0
}
```
