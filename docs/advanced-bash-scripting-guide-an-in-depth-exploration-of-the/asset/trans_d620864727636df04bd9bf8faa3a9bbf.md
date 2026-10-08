

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
# 下列出的函数与 usb-mount 代码几乎完全一致。
```

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

附录 A 贡献脚本

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

exit 0
将文件转换为 HTML 格式。

# 示例 . A. 贡献脚本

```bash
#!/bin/bash
# tohtml.sh [v.0.2, 有点 Bug

# 将文本文件转换为 HTML 格式。
# 作者: Mendel Cooper
# 许可证: GPL
# 用法: sh tohtml.sh <textfile> 脚本可以轻松修改以接受文件名。

# 假设
# 1) 目标文件的段落由空行分隔。
# 2) 图片 (.jpg) 位于 "images"。
# 在目标文件中，图像名称包含在方括号中，
# 例如，[image01.jpg]。
# 3) *斜体* 短语以空格或下划线开始，
# 并以空格或下划线结束。

# 设置
# FNTSIZE=3           # 中等字体大小
# IMGDIR="images"    # 图片目录
# 表头
# HDR01="<!DOCTYPE HTML PUBLIC "-//W3//DTD HTML 4.0 Transitional//EN">
# HDR02="<!-- Converted to HTML by tohtml.sh -->"
# HDR03="<!-- author: Leo Cooper <leo@gmail.com> -->"
# HDR11="<head>"
# HDR1a="</head>"
# HDR12="<title>"
# HDR20="</title>"
# HDR21="<meta NAME="GENERATOR" CONTENT="tohtml.sh">
# HDR13="<body bgcolor="#ddd"> # 修改背景颜色。
# HDR14a="<font size="
# HDR14b="</font>"
# 页脚
# FTR10="</body>"
# FTR11="</html>"

# 标签
# BOLD="<b>"
# CENTER="<center>"
# END_CENTER="</center>"
# LF="br>"

write_headers ()
{
echo "$HDR01"
echo "$HDR02"
echo "$HDR03"
echo
echo "$HDR10"
echo "$HDR11"
echo "$HDR21"
echo "$HDR1a"
echo "$HDR13"
echo -n "$HDR14a"
echo -n "$FNTSIZE"
echo "$HDR14b"
```

# 附录 A. 贡献脚本

# 高级 Bash 脚本指南

```bash
echo
echo "$BOLD" # 全部加粗（更具可读性）
}
```

```bash
process_text () {
    while read line; # 一行读取
    do
        if [ -z "$line" ]; # 空行？
            echo                    #后续是段落。
            echo "$SLF" # 插入 <br> 标签。
            echo "$SLF"
            continue                # 跳过下划线测试。
        else                        # 否则。
        fi
        if [ "$line" = "*.jpg" ]; # 是图片吗？
        then                        # 去掉括号。
            temp=$(echo "$line" | sed 's/\[//g' -e 's\]//g')
            line="<CENTER><img src="$temp">$END_CENTER>" # 添加图像标签。
        else                        # 并且居中。
        fi
    done
```

```bash
echo "$line" | grep -q
if [ "$?" -eq 0 ]; # 如果行包含下划线
then
    #
    temp=$(echo "$line" | sed 's/_/ /' -e 's/_/<i>' | sed 's/_<i>' -e 's/_></i>')
    # 只处理空格前缀的、位于行开头或结尾的下划线。
    # 不要转换单词内部的下划线！
    line="$temp"
    # 降低脚本执行。可以优化吗？
fi
```

```bash
echo
echo "$line"
echo
# 不要在生成的文本中产生额外的空行！
) # 结束 while
done
) # 结束 process_text ()
```

```bash
write_footers () { # 结束标签。
    echo "$FTR10"
    echo "$FTR11"
}
```

附录 A. 贡献脚本

```bash
# main () {
# ==========
write_headers
process_text
write_footers
# ==========
}

exit $?
```

+ # 练习：
# --------------------------------
# 1) 修复：检查逗号或句号之前的结束下划线。
# 2) 添加一个针对待斜体化短语中是否存在结束下划线的测试。

