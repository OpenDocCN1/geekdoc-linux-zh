
```bash
#!/bin/sh
###########################################################
# Begin /sbin/ifup
# Description : Interface Up
# Authors : Nathan Colson - nathan@linuxfromscratch.org
# Kevin P. Fleming - kpfleming@linuxfromscratch.org
# Bruce Dubbs - bdubbs@linuxfromscratch.org
# Update : DJ Lucas - dj-lucas@linuxfromscratch.org
# Version : LFS 7.7
# Notes : The IFCONFIG variable is passed to the SERVICE script
# in the /lib/services directory, to indicate what file the
# service should source to get interface specifications.
###########################################################

up() {
  log_info_msg "Bringing up the ${1} interface..."

  if ip link show $1 > /dev/null 2>&1; then
    link_status=$(ip link show $1)

    if [ -n "${link_status}" ]; then
      if ! echo "${link_status}" | grep -q UP; then
        ip link set $1 up
      fi
    else
      log_failure_msg "Interface ${IFACE} doesn't exist."
      exit 1
    fi
  fi
  evaluate_retval
}

RELEASE="7.7"

USAGE="Usage: $0 [-hV] [--help] [--version] interface"
VERSTR="LFS ifup, version ${RELEASE}"

while [ $# -gt 0 ]; do
  case "$1" in
    --help | -h)
      help="y"; break;
    --version | -V)
      echo "${VERSTR}"; exit 0;
    -*)
      echo "ifup: ${1} invalid option" >&2
      echo "${USAGE}" >&2
      exit 2;
    *)
      break;
  esac
done

if [ -n "${help}" ]; then
  echo "${VERSTR}"
  echo "${USAGE}"
  echo
  cat << HERE_EOF
ifup is used to bring up a network interface. The interface
parameter, e.g. eth0 or eth0:2, must match the trailing part of the
interface specifications file, e.g. /etc/sysconfig/ifconfig.eth0:2.
HERE_EOF
  exit 0
fi

file=/etc/sysconfig/ifconfig.${1}

# Skip backup files
if [ "${file}" = "${file}*" ] || exit 0

. /lib/lsb/init-functions

if [ ! -r "${file}" ]; then
  log_failure_msg "Unable to bring up $1 ${file} is missing or cannot be accessed."
  exit 1
fi

$file
if [ "$IFACE" = "$1" ]; then
  log_failure_msg "Unable to bring up $1 ${file} does not define an."
  exit 1
fi
```

# Linux From Scratch - 版本 11.3

```bash
# 跳过备份文件
[ "${file}" = "${file%-*}" ] || exit 0
```

```bash
. /lsb/init-functions
```

```bash
if [ ! -f "${file}" ]; then
  log_warning_msg "${file} 缺失或无法访问。
  exit 1
fi
```

```bash
${file}
if [ "IFACE" = "" ]; then
  log_failure_msg "${file} 未定义接口 [IFACE]"
  exit 1
fi
```

```bash
# 我们只需要第一个服务来关闭接口
S=$(echo "${SERVICE} | cut -f1 -d "")
```

```bash
if ip link show ${IFACE} > /dev/null 2>/dev/null; then
  if [ -n "${SERVICE}" ] && [ -x /lib/services/${SERVICE}" ]; then
    CONFIG=(${file}) /lib/services/${SERVICE} down
  else
    MSG="无法处理 ${file}。可能"
    MSG="${SERVICE} 变量未设置"
    MSG="${MSG} 或指定的服务无法执行。
    log_failure_msg "${MSG}"
    exit 1
  fi
fi
```

```bash
log_warning_msg "接口 $$(1) 不存在。" 
fi
```

```bash
# 如果设备中还有其他接口，则保持接口开启
link_status="$(ip link show ${IFACE} 2>/dev/null)"
```

```bash
if [ -n "${link_status}" ]; then
  if [ "$(echo "${link_status}" | grep inet)" != "" ]; then
    if [ "$(ip addr show ${IFACE} | grep 'inet ')" != "" ]; then
      log_info_msg "正在关闭接口 ${IFACE}..."
      ip link set ${IFACE} down
      evaluate_retval
    fi
  fi
fi
```

```bash
# 结束 /bin/ifdown
```

## D.26. /lib/services/ipv4-static

```bash
#!/bin/sh
######################################################################
# 开始 /lib/services/ipv4-static
# 描述：IPv4 静态启动脚本
# 作者：Nathan Coulson - nathan@linuxfromscratch.org
          # Kevin P. Fleming - kpfleming@linuxfromscratch.org
          # Bruce Dubbs - bdbubbs@linuxfromscratch.org
# 更新： 
# 版本：LFS 7.0
######################################################################
```
