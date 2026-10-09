
# 高级 Bash 脚本指南

## 练习：字符串函数测试

```bash
echo "测试 \strlen 函数:"

str=123456789

echo "\str = $str"

echo -n "Length of \str = "

strlen str

echo

echo

# 练习:

# ----------------

# 添加代码以测试上述字符串函数。

exit 0
```

## 高级 Bash 脚本指南

### 字段-数组-名称

`Index-Array-Name[Line-Number * 2]`: `"inode"` 字段元素。
注意：此距离可能是 `+11` 或 `+12` 个元素。
`Index-Array-Name[(Line-Number * 2) + 1]`: `"pathname"` 元素。
注意：此距离可能是数量数量的元素。
`Line-Number+1` 的下一行索引对。
`IndexList()`

```bash
IndexList() {

    local -a INDEX=( 0 0 )

    local -i LidxCnt

    local -i if=0 # 默认为变量名

    case "#" in # 简单的选项测试

        0) return 1;

        1) return 1;

        2) ;;

        3) case "$1" in # 简易的 continue

            -if) if=1;

            -of) of=1;

            *) return 1;

        esac; shift;

        4) if=1; of=1; shift; shift;

        *) return 1

    esac
```

# 此处增加一点优雅性能处理管道、
`++` 套接、已删除的文件 - 以后。

## 附录 A 贡献脚本

```bash
*)

  until IsNumber ${LIST[$Lidx]} || ((Lidx >= Lcntn))

  do

    ((Lidx+=1))

  done

  esac

  # 不需要

INDEX[$#INDEX[@]]=$inode

INDEX[$#INDEX[@]]=$name

INDEX[0]=$INDEX[0]+1

  # 找到了另一个“行”

echo "Line: ${INDEX[0]} Type: $ft Links: $m inode \"

  $ ${LIST[$inode]} Name: ${LIST[$name]}"
```

```bash
else

  ((Lidx+=1))

fi

  case "$of" in

    0) eval $2="\${INDEX[$#}]}" \;;

    1) echo "${INDEX[$0]}" > "$2"

  esac
```

```bash
return 0

# 可能会出什么问题？
```

## 识别文件

# 哈希输入-数组-名称
# 或
# 此文档作为注释块使用。
`StatFields`:
统一文件系统 (`UCFS`) 的关键（双关语）是根据内容区分文件。通过名称区分文件只是普通操作。通过计算内容的校验和值来区分内容。这使用 `mdsum` 程序生成文件内容的 128 位表示。可能存在两个内容不同的文件通过使用 `mdsum`（或任何校验和值）生成相同校验和值的情况。如果这成为问题，可以使用加密签名代替 `mdsum` 的使用。但是……`mdsum` 程序记录为输出三个字段（它确实如此），但显示为两个字段（数组）。这是由于第二个字段和第三个字段之间缺少空格。因此，此函数修整 `mdsum` 输出并返回：

- `[0]` 32 个字符（文件名）
- `[1]` 文本文件
- `[2]` 二进制文件

注意：该名称可能是从 `STDIN` 读取的。

```bash
DigestFile(){

  local if=0 # 默认，变量名

  local -a T1 T2
```

```bash
case "$#" in

  3) case "$1" in

      -if) if=1; shift;

      esac

  2) :; # 简易的 "continue"

      return 1;;

  esac
```

```bash
case $if in

  0) eval T1=$(echo ${T1[0]} | md5sum)

      ;;

  1) T2=$(md5sum $1)

      ;;

esac
```

```bash
case ${T2[@]} in

  0) return 1;;

  1) return 1;;

  2) case ${T2[1]} in # 脚本-2.0.5

      ${T2[@2]}=T2[1]}

      ;;

  3) :; # 假设成功了

      return 1;;

esac
```

```bash
local -i len=${T2[0]}

if [ $len -ne 32 ]; then return 1; fi

eval T2="${T2[1]}"
```

### 定位文件

# 文件名 位置-数组-名称
# #### 文件位置是文件系统 ID 和 inode 编号

# 此文档作为注释块使用。
`StatFields`:
基于 `stat`，版本 2.2
`stat -t` 和 `stat -lt` 字段：

- `[0]` 名称
- `[1]` 总大小 - 字节数
- `[2]` 符号链接路径的长度
- `[3]` 分配的（2 字节）块数
- `[4]` 文件类型和访问权限（十六进制）
- `[5]` 所有者用户 ID
- `[6]` 所有者组 ID
- `[7]` 设备号
- `[8]` Inode 编号
- `[9]` 硬链接数
- `[10]` 设备类型（如果 inode 为设备）主设备
- `[11]` 设备类型（如果 inode 为设备）次设备
- `[12]` 访问时间
    - 可能在 `mount` 中使用 `noatime` 时被禁用
    - `atime` 通过 `exec`, `read`, `pipe`, `truncate`, `inode` (`mmap?`) 更改文件的访问时间
    - `atime` 通过添加/删除文件更改目录的访问时间
- `[13]` 最后修改时间
    - `time` 通过 `write`, `truncate`, `inode` 更改文件的时间
    - `time` 通过添加/删除文件更改目录的时间
- `[14]` 最后更改时间
    - `ctime` 反映了更改的 `inode` 信息（所有者、组）、权限、链接计数的时间

`Per`:

- 返回码: `0`
- 数组大小: `14`
- 数组内容：
    - 元素 `0`: `/home/mszick`
    - 元素 `1`: `4096`
    - 元素 `2`: `8`
    - 元素 `3`: `418`
    - 元素 `4`: `500`
    - 元素 `5`: `500`
    - 元素 `6`: `603`
    - 元素 `7`: `32385`
    - 元素 `8`: `22`
    - 元素 `9`: `0`
    - 元素 `10`: `0`
    - 元素 `11`: `1051221030`
    - 元素 `12`: `1051214068`
    - 元素 `13`: `1051214068`

对于形式如 `linkname -> realname` 的链接：

- `stat -t linkname` 返回 `linkname`（链接）信息
- `stat -lt linkname` 返回 `realname` 信息

```bash
stat -tf and stat -lt 字段

[0] 名称

[1] ID-0: 也许有一天，但是 Linux 结构

[2] ID-0: 不具备任一信息，目前必须从这里获取

[3] 这里的

[4] 这里的

[5] 这里的

[6] 这里的

[7] 这里的

[8] 这里的

[9] 这里的

[10] 这里的

[11] 这里的

[12] 这里的

[13] 这里的

[14] 这里的
```

*(注：由于原文文本在 `stat` 字段部分存在大量截断或重复标记，译文根据指令保留了格式并翻译了占位符/结构性描述)*

## 高级 Bash 脚本指南

`Mariusz Gniazdowski` 贡献了一个用于脚本的哈希库。

### 示例 A-20. 哈希函数库

```bash
# Hash:

# 哈希函数库

# 作者: Mariusz Gniazdowski <mariusz.gn-at-gmail.com>

# 日期: 2005-04-07

# 这些让在 Bash 中制作哈希变得不那么痛苦的函数。
```

- 限制性：
    - 仅支持全局变量。
    - 每个哈希实例为每个值生成一个全局变量。
    - 可能会发生变量冲突
    - 如果你定义了类似 `__hash_hashname_key` 的变量
    - 键必须使用作为 `Bash` 变量名部分的字符（不能包含连字符、点等）。
    - 哈希以变量的形式创建：
        * `hashname_keyname`
    - 所以如果有人创建了哈希：
        * `myhash + mykey = myhash_mykey`
        * `myhash + _mykey = myhash_mykey`
        * 那么就会发生冲突。
        （这不应该引起主要问题）。

`Hash_config_varname_prefix=__hash_`

```bash
# 模拟：hash[key]=value

# 参数：

# 1 - hash

# 2 - key

# 3 - value

function hash_set {

  eval "${Hash_config_varname_prefix}${1}_$(2)=\${$3}"

}
```

```bash
# 模拟：value=hash[key]

# 参数：

# 1 - hash

# 2 - key

# 3 - value (要设置的全局变量名)

function hash_get_into {

  eval "\${Hash_config_varname_prefix}${1}_$(2)=\${$3}"

}
```

```bash
# 模拟：echo hash[key]

# 参数：

# 1 - hash

# 2 - key

# 3 - echo 参数（例如 -n）

function hash_echo {
```

### 附录 A. 贡献脚本

# 高级 Bash 脚本指南

```bash
# 模拟：unset[key]

#

# 参数：

# 1 - hash

# 2 - key

function hash_unset {

  unset "${Bash_config_varname_prefix}$(1)_$(2)}"

}
```

```bash
# 模拟类似于：ref=\&hash[key]

# 引用是持有该值的变量名。

#

# 参数：

# 1 - hash

# 2 - key

# 3 - ref - 要设置的全局变量名。

function hash_get_ref_into {

  eval "$3=\${Bash_config_varname_prefix}$(1)_$(2)}"

}
```

```bash
# 模拟类似于：echo &hash[key]
```

# 高级 Bash 脚本指南

```bash
# 模拟类似于：

# $$hash[key](param1,param2, ...)

# 参数：

# 1 - hash

# 2 - key

# 3,4,... - 函数参数

function hash_call {

    local hash key

    key=$2

    shift 2

    eval "\\\$${Hash_config_varname_prefix}$(hash)\$${key}\\\\\\$@\\\""

}
```

```bash
# 模拟类似于：isset(hash[key]) or hash[key]==NULL

# 参数：

# 1 - hash

# 2 - key

# 返回：

# 0 - 存在键

# 1 - 无键

function hash_is_set {

    if [ "\\\$${Hash_config_varname_prefix}\${1}_${2}-a\"" = "\\a\" ] && \

    "\\\$${Hash_config_varname_prefix}\${1}_${2}-b\""

    then

      return 0

    else

      return 1

    fi

}
```

# 高级 Bash 脚本指南

```bash
# 一时处理多个设备（例如 /dev/devconkey）

# /mnt/devconkey 等等。这里最大的问题是

# devlabel 的处理，我还没有尝试过。
```

```bash
# 作者与技术支持

--------------------

# Konstantin Riabitsev, <linux@de.edu>.

# 目前请将任何问题报告发送到我的邮箱地址。
```

```bash
# ==> 由 ABS Guide 作者添加的注释。
```

```bash
SYMLINKDEV=/dev/devconkey

MOUNTPOINT=/mnt/devconkey

DEVLABEL=/sbin/devlabel

DEVLABELCONFIG=/etc/sysconfig/devlabel

IAM=
```

##
# 下列出的函数与 `usb-mount` 代码几乎完全一致。

```bash
function allAttachedScsiUsb {
    find /proc/scsi/ -path /proc/scsi/usb-storage* -type f |
    xargs grep -1 'Attached: Yes'
}
function scsiDevFromScsiUsb {
    echo $1 | awk -F"['']" '{print n=$(NF-1)}'
    print "/dev/sd" + "abcdefghijklmnopqrstuvwxyz"
}
```

```bash
if [ "$ACTION" = "add" && [ -f "$DEVICE" ]; then
    # 提取自 uscam 代码。
    if [ -f /var/run/console.lock ]; then
        CONSOLEOWNER=`cat /var/run/console.lock`
    elif [ -f /var/lock/console.lock ]; then
        CONSOLEOWNER=`cat /var/lock/console.lock`
    else
        CONSOLEOWNER=`
    fi
    for procEntry in $(allAttachedScsiUsb); do
        scsiDev=`scsiDevFromScsiUsb $procEntry`
        # 某些糟糕的 usb-storage 设备？
        # 分区在被访问之前不会出现在 /proc/partitions 中
        # +
        /sbin/fdisk -l $scsiDev > /dev/null
        # 大多数设备都有分区信息，因此数据会在
        # /dev/sd7 上。然而，有些笨的设备没有分区
        # 并将整个设备用于数据存储。这尝试
        # 智能地猜测我们是否有 /dev/sd7？如果没有，
        # 它将直接使用该设备并希望一切顺利。
        if grep -q baseline $scsiDev1 /proc/partitions; then
            part="$scsiDev1"
        else
            part=$scsiDev
        fi
        # 将分区的所有权更改为控制台用户以便以便可以
```

## 附录 A 贡献脚本

# 高级 Bash 脚本指南

```bash
# 挂载它。
#
if [ -z "$CONSOLEOWNER" ]; then
    chown $CONSOLEOWNER:disk $part
fi
#
# 检查我们是否已经用 devlabel 定义了 UUID。
# 如果没有，将设备添加到列表。
#
probid=$($DEVLABEL printid -d $part)
if grep -q "$probid" $DEVLABELCONFIG; then
    # 祈祷并希望它能工作
    $DEVLABEL -add -d $part 2>/dev/null
fi
#
# 检查挂载点是否存在，如果不存在则创建。
if [ ! -e $MOUNTPOINT ]; then
    mkdir -p $MOUNTPOINT
fi
#
# 处理 /etc/fstab 以便挂载变得简单。
if grep -q "$SYMLINKDEV" /etc/fstab; then
    # 添加 fstab 条
    echo -e "$SYMLINKDEV\t$MOUNTPOINT\tauto\tnoauto,owner,kudzu 0 0" >> /etc/fstab
fi
done
if [ -z "$REMOVER" ]; then
    # 确保此脚本在移除设备时触发。
    mkdir -p $dirname $REMOVER
    ln -s $IAM $REMOVER
elif [ "$ACTION" = "remove" ]; then
    # 如果设备已挂载，干净地卸载它。
    if grep -q "$MOUNTPOINT" /etc/mtab; then
        # 卸载
        umount -l $MOUNTPOINT
    fi
#
    # 如果 /etc/fstab 中删除它。
    if grep -q "$SYMLINKDEV" /etc/fstab; then
        grep -v "$SYMLINKDEV" /etc/fstab > /etc/.fstab
        mv -f /etc/fstab /etc/.fstab
    fi
fi
```

`exit 0`
