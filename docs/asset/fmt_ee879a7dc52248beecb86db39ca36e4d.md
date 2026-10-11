
输出如下：

注释：此脚本是 `./untar_1.ksh`。

目的：展示如何只解压 1 个文件。

输出：`untar_1.file.`

脚本执行方式：`./untar_1.ksh`

```
# $STARFILE = tar 包的文件名为 $STARFILE

# 你想要放置解压数据的目录：
# /tmp
```

```
print "现在我们正在从 tar 包中提取 (-x) 一个文件
print "并将其放入当前目录 (/tmp)："
tar -xf $STARFILE home/larry/ROSSETTA/INPUT_FILES/CENT_SALES_DATA_Apr
# -x = 提取；v = 详细；-f $STARFILE = tar 包文件名
```

```
print "这里是我们从 tar 包获取的文件：/home/larry/ROSSETTA/INPUT_FILES/CENT_SALES_DATA_Apr
```

第 544 页

### 注意：
### 本脚本末尾提供了两个详尽的解释：
### 1. “echo/egrep 命令中元字符的解释。”
### 2. “关于 s/'（替换）命令工作原理的说明。”

```bash
### END_NOTES.

### 另请：read_input_from_keyboard.ksh

### 另请：split_into_pieces_using_a_pattern.ksh

### 另请：validate_user_input.ksh

### 另请：validate_phone_numbers.ksh
```
