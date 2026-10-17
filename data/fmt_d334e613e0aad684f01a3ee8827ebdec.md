
## D.21. `/etc/sysconfig/modules`

```
####################################################################
# Begin /etc/sysconfig/modules
# Description : 模块自动加载配置
# Authors :
# Version : 00.00
# Notes : 此文件的语法如下：
# <module> [<arg1> <arg2> ...]

# 每个模块应该独占一行，任何想要传递给模块的选项
# 都应该紧随其后。行分隔符可以是空格或制表符。
####################################################
# End /etc/sysconfig/modules
```

## D.22. `/etc/sysconfig/createfiles`

```
####################################################

# Begin /etc/sysconfig/createfiles

# Description : Createfiles 配置

# Authors :

# Version : 00.00

# Notes : 此文件的语法如下：

# 如果 type 等于 "file" 或 "dir"

# <filename> <type> <permissions> <user> <group>

# 如果 type 等于 "dev"

# <filename> <permissions> <user> <devtype> <major> <minor>

# <filename> 是创建的文件名

# <type> 为 file, dir 或 dev 之一

# file 创建新文件

# dir 创建一个目录

# dev 创建一个设备

# block 创建一个块设备

# char 创建一个字符设备

# pipe 创建一个管道，这将忽略 <major> 和 <minor> 字段

# <major> 和 <minor> 不用于设备。
```

## D.23. `/etc/sysconfig/udev`

```
####################################################

# Begin /etc/sysconfig/udev

# Description : udev 脚本配置

# Authors :

# Version : 00.00

# Notes : 挂载后可能需要触发的每个子系统

# 都应该列在此文件中。可能的子系统列在此处，

# 是于 /var/lib/hwclock/adjtime 和 sound（由于两者 /var/lib/alsa/asound.state）

# 条目之间用空格分隔。

####################################

# End /etc/sysconfig/udev
```

## D.24. `/sbin/ifup`

```bash
#!/bin/sh

################################################################

# (此处文本不完整，未翻译后续内容)

# Linux From Scratch - Version 11.0
```
```bash
if [ $ -gt 0 ]; do
  case "$1" in
    --help | -h)
      help="y"; break ;;

    --version | -V)
      echo "${VERSTR}"; exit 0 ;;

    -*)
      echo "${1}: invalid option" >&2
      echo "${USAGE}" >&2
      exit 2 ;;

    break ;;
  esac
fi

if [ -n "$help" ]; then
echo "${VERSTR}"
echo "${USAGE}"
echo

cat << HERE_EOF
down 命令用于关闭网络接口。接口参数（例如 eth0 或 eth0:2）必须匹配接口规范文件的末尾部分，例如 /etc/sysconfig/ifconfig.eth0:2。

HERE_EOF
exit 0

file=/etc/sysconfig/ifconfig.$1

```
```bash
# 跳过备份文件
[ "$file" = "${file%~}" ] || exit 0
/lib/lsb/init-functions
```
```bash
if [ -r "$file" ]; then
log_warning_msg "$file" 缺失或无法访问。
exit 1
fi

$file
```
```bash
if [ "$INTERFACE" = "" ]; then
log_failure_msg "$file" 未定义接口 [IFACE]。
exit 1
fi

# 我们只需要第一个服务来关闭接口
S=$(echo "${SERVICE}" | cut -f1 -d " ")
```
```bash
exit 1

fi

else

  log_warning_msg "接口 ${1} 不存在。"

fi

```
```bash
# 如果设备中还有其他额外的接口，则保留该接口

link_status=$(ip link show ${IFACE} 2>/dev/null)

if [ -n "${link_status}" ]; then

  if [ "$(echo "${link_status}" | grep UP)" != "" ]; then

    if [ "$(ip addr show ${IFACE}" | grep 'inet ') ="" ]; then

      log_info_msg "正在关闭 ${IFACE} 接口..."

      ip link set ${IFACE} down

    fi

  fi

fi

evaluate_retval

fi

```
```bash
# 结束 /sbin/ifdown
```

## D.26. `/lib/services/ipv4-static`

```bash
#!/bin/sh

################################################################################

# 开始 /lib/services/ipv4-static

################################################################################

# ：IPv4 静态启动脚本

#

# 作者：Nathan Colson - nathan@linuxfromscratch.org

           Kevin P. Fleming - kpfleming@linuxfromscratch.org

           Bruce Dubbs - bdubbs@linuxfromscratch.org
# 更新： 
# 版本  : LFS 7.0
################################################################################
```
```bash
/lib/sb/init-functions

. ${IFCONFIG}

if [ -z "${IFACE}" ]; then

  log_failure_msg "\n${IFCONFIG} 中缺少 IP 变量，无法继续。"

  exit 1

fi
```
```bash
if [ -z "${PREFIX}" -a -z "${PEER}" ]; then

  log_warning_msg "\n${IFCONFIG} 中缺少 PREFIX 变量，假设为 24。"

  PREFIX=24

  args="${args} ${IP}/${PREFIX}"
```
```bash
elif [ -n "${PREFIX}" -a -n "${PEER}" ]; then

  log_failure_msg "\n${IFCONFIG} 中同时指定了 PREFIX 和 PEER，无法继续。"

  exit 1
```
```bash
elif [ -n "${PREFIX}" ]; then

  args="${args} ${IP}/${PREFIX}"
```
```bash
elif [ -n "${PEER}" ]; then

args="${args} peer ${PEER}"
fi

if [ -n "${LABEL}" ]; then

args="${args} label ${LABEL}"
fi

if [ -n "${BROCAST}" ]; then

args="${args} broadcast ${BROCAST}"
fi

case "${2}" in

up)

  if [ $(ip addr show ${1} 2>/dev/null | grep ${$IP}/) = "" ]; then

    log_info_msg "正在向 ${1} 接口添加 IPv4 地址 ${$IP}..."

    ip addr add ${$IP} dev ${1}

    evaluate_retval

  else

    log_warning "无法向 ${1} 添加 IPv4 地址 ${$IP}。已存在。"

  fi

down)

  if [ $(ip addr show ${1} 2>/dev/null | grep ${$IP}/) != "" ]; then

    log_info_msg "正在从 ${1} 接口移除 IPv4 地址..."

    ip addr del ${$IP} dev ${1}

    evaluate_retval

  fi

  if [ -n "${GATEWAY}" ]; then

    # 只有在没有剩余 ipv4 地址时才移除网关

    if [ $(ip addr show ${1} 2>/dev/null | grep 'inet') != "" ]; then

      log_info_msg "正在移除默认网关..."

      ip route del default

      evaluate_retval

    fi

  fi

*)

  echo "用法: ${0} [interface] (up|down)"

  exit 1

esac
```

## D.27. `/lib/services/ipv4-static-route`

```bash
#!/bin/sh

################################################################################

# 开始 /lib/services/ipv4-static-route

################################################################################

# ：IPv4 静态路由脚本
# 描述：IPv4 静态路由脚本
# 作者：Kevin P. Fleming - kpfleming@linuxfromscratch.org
# DJ Lucas - dj@linuxfromscratch.org
# 更新：Bruce Dubbs - bdubbs@linuxfromscratch.org
# 版本：LFS 7.0
################################################################################
```
```bash
/lib/lsb/init-functions

. ${IFCONFIG}

case "${TYPE}" in

  ("network")

    need_ip=1

    need_gateway=1

  ;;

  ("default")

    need_gateway=1

    args="${args} default"

    desc="default"

  ;;

  ("host")

    need_ip=1

  ;;

  ("unreachable")

    need_ip=1

    args="${args} unreachable"

    desc="unreachable"

  ;;

  (*)

    log_failure_msg "${IFCONFIG} 中未知路由类型 ${TYPE}无法继续。"

    exit 1

esac

if [ -n "${GATEWAY}" ]; then

  MSG="静态路由无法在 ${IFCONFIG} 中设置 GATEWAY 变量。"

  log_failure_msg "${MSG} 使用 STATIC_GATEWAY，无法继续"

  exit 1

fi

if [ -n "${need_ip}" ]; then

  if [ -z "${IP}" ]; then

    log_failure_msg "${IFCONFIG} 中缺少 IP 变量，无法继续。"

    exit 1

  fi

fi

if [ -z "${PREFIX}" ]; then

  log_failure_msg "${IFCONFIG} 中缺少 PREFIX 变量，无法继续。"

  exit 1

fi

args="${args}(${PREFIX}"

desc="${desc}/${PREFIX}"

if [ -n "${need_gateway}" ]; then

  if [ -z "${STATIC_GATEWAY}" ]; then

    log_failure_msg "${IFCONFIG} 中缺少 STATIC_GATEWAY 变量，无法继续。"

    exit 1

  fi

  args="${args} via ${STATIC_GATEWAY}"

fi

if [ -n "${SOURCE}" ]; then

  args="${args} src ${SOURCE}"

fi

case "$2" in

  up)

    log_info_msg "正在向 ${1} 接口添加 '${desc}' 路由..."

    ip route add ${args} dev ${1}

    evaluate_retval

  ;;

  down)

    log_info_msg "正在从 ${1} 接口移除 '${desc}' 路由..."

    ip route del ${args} dev ${1}

    evaluate_retval

  ;;

  *)

    echo "用法: ${0} [interface] {up|down}"

    exit 1

esac

# 结束 /lib/services/ipv4-static-route
```

## 附录 E. Udev 配置规则

附录中的规则是为了方便列出。安装通常通过第 8.6 节完成。

## E.1. 55-lfs.rules

```bash
# /etc/udev/rules.d/55-lfs.rules: LFS 规则定义

# 内核设备

# 这使得 /dev/rtc 可用时立即设置系统时钟
SUBSYSTEM="rtc", ACTION="add", MODE="0644", RUN+="/etc/rc.d/init.d/setclock"
KERNEL="rtc", ACTION="add", MODE="0644", RUN+="/etc/rc.d/init.d/setclock"

# 通信设备

KERNEL="ippp[0-9]*", GROUP="dialout"
KERNEL="isdn[0-9]*", GROUP="dialout"
KERNEL="isdnctrl[0-9]*", GROUP="dialout"
KERNEL="dcbri[0-9]*", GROUP="dialout"
```

## 附录 F. LFS 许可证

本书根据知识共享 署名-非商业-相同性 2.0 许可证许可。

计算机指令可以根据 MIT 许可证从书中提取。

## F.1. 知识共享法律代码

知识共享 署名-非商业-相同性 2.0

> **重要信息**
> 知识共享公司不是律师事务所，不提供法律服务。本许可证的分发不构成律师与客户关系。知识共享按“原样”提供此类信息。知识共享对所提供的信息不作任何保证，并对其在使用可能造成的损害不承担责任。

许可证

本作品（下所示）根据知识共享通用许可证（“CCPL”或“许可证”）的条款提供。

作品受版权和/其他适用法律保护。除本许可证或版权法允许外，对作品的任何使用都是禁止的。

通过行使此处提供的作品的任何权利，您即接受并同意受本许可证条款的约束。许可方考虑到您接受此类条款和条件，特授予您此处包含的权利。

+ 1. 定义

a. “集体作品”是指一种作品，例如期刊杂志、选集或百科全书，其中作品的完整且未经修改的形式，连同若干其他本身构成独立作品的贡献，被汇成一个整体。构成集体作品的作品在在本许可证的目的下不被视为衍生作品（见下文定义）。

b. “衍生作品”是指基于作品或作品与其他现有作品而创作的作品，例如翻译、音乐改编、戏剧化、虚构化、电影版本、声音录制品，作为复制、节选、浓缩或作品可能重构、转换或改编的任何其他形式，构成集体作品的作品在本许可证的目的下不被视为衍生作品。为避免疑问，当作品为音乐作品或声音录制品时，作品与移动图像的时间关系同步（“同步”）在本许可证的目的下被视为衍生作品。

c. “许可方”是指根据本许可证条款提供作品的个人或实体。

d. “原作者”是指创作作品的个人或实体。
