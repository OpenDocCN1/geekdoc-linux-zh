

# 高级 Bash 脚本指南

字段-数组-名称：
Index-Array-Name[Line-Number * 2] : "inode" 字段元素。
注意：此距离可能是 +11 或 +12 个元素。
Index-Array-Name[(Line-Number * 2) + 1] : "pathname" 元素。
注意：此距离可能是数量数量的元素。
Line-Number+1 的下一行索引对。
IndexList()

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
++ 套接、已删除的文件 - 以后。

# 附录 A 贡献脚本

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

# 识别文件
# 哈希输入-数组-名称
# 或
# 此文档作为注释块使用。
StatFields:
统一文件系统 (UCFS) 的关键（双关语）是根据内容区分文件。通过名称区分文件只是普通操作。通过计算内容的校验和值来区分内容。这使用 mdsum 程序生成文件内容的 128 位表示。可能存在两个内容不同的文件通过使用 mdsum（或任何校验和值）生成相同校验和值的情况。如果这成为问题，可以使用加密签名代替 mdsum 的使用。但是……mdsum 程序记录为输出三个字段（它确实如此），但显示为两个字段（数组）。这是由于第二个字段和第三个字段之间缺少空格。因此，此函数修整 mdsum 输出并返回

[0] 32 个字符（文件名）
[1] 文本文件
[2] 二进制文件
注意：该名称可能是从 STDIN 读取的。

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

# #### 定位文件

# 文件名 位置-数组-名称
# #### 文件位置是文件系统 ID 和 inode 编号

# 此文档作为注释块使用。
StatFields:
基于 stat，版本 2.2
stat -t 和 stat -lt 字段

[0] 名称
[1] 总大小 - 字节数
[2] 符号链接路径的长度
[3] 分配的（2 字节）块数
[4] 文件类型和访问权限（十六进制）
[5] 所有者用户 ID
[6] 所有者组 ID
[7] 设备号
[8] Inode 编号
[9] 硬链接数
[10] 设备类型（如果 inode 为设备）主设备
[11] 设备类型（如果 inode 为设备）次设备
[12] 访问时间
可能在 'mount' 中使用 noatime 时被禁用
atime 通过 exec, read, pipe, truncate, inode (mmap?) 更改文件的访问时间
atime 通过添加/删除文件更改目录的访问时间
[13] 最后修改时间
time 通过 write, truncate, inode 更改文件的时间
time 通过添加/删除文件更改目录的时间
[14] 最后更改时间
ctime 反映了更改的 inode 信息（所有者、组）权限、链接计数的时间

```
Per:
返回码: 0
数组大小: 14
数组内容
元素 0: /home/mszick
元素 1: 4096
元素 2: 8
元素 3: 418
元素 4: 500
元素 5: 500
元素 6: 603
元素 7: 32385
元素 8: 22
元素 9: 0
元素 10: 0
元素 11: 1051221030
元素 12: 1051214068
元素 13: 1051214068
```

```
对于形式如 linkname -> realname 的链接
stat -t linkname 返回 linkname（链接）信息
stat -lt linkname 返回 realname 信息
```

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

