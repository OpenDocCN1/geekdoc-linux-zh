
# Linux Shell 命令参考：从 A 到 Z

cat, ln, nam

stat, tee, a

bunzip2, he

iconv, attr

getcap, con

at, batch, z

iotop, addg

usermod, ba

![](img/94f0b4d76a25250c220515a1d5bba83f_0_0.png)

```
user$ rdfind verz1 verz2
Now scanning "verz1", found 211 files.
Now scanning "verz2", found 215 files.
Now have 426 files in total.
Removed 0 files due to non-unique device
Total size is 85754591 bytes or 82 MIB
Removed 103 files due to unique sizes from
Now eliminating candidates based on first
removed 4 files from list, 319 files left.
removed 0 files from list, 319 files left.
Now eliminating candidates based on sha
removed 2 files from list, 317 files left.
It seems like you have 317 files that are n
Totally, 39 MIB can be reduced. Now mak
```

![](img/94f0b4d76a25250c220515a1d5bba83f_0_1.png)

Michael Kofler

![](img/94f0b4d76a25250c220515a1d5bba83f_0_2.png)

Michael Kofler

![](img/94f0b4d76a25250c220515a1d5bba83f_1_0.png)

我们希望你喜欢这本电子书。请向我们提供反馈，并阅读[服务页面]()以了解如何与我们联系。

2025939046

2 Heritage Drive, Suite 305

USA

Rheinkallee 4

Germany

+49 (0) 228 42150-0

# 使用说明

本电子书受版权保护。通过购买本电子书，你同意接受并遵守相关版权规定。你有权出于个人目的使用本电子书。你也可以对其进行打印和复制，但同样仅限个人使用。然而，我们不允许与他人共享电子副本或打印副本，无论是整体还是部分。当然，在互联网或公司网络上提供这些内容也是违法的。

有关详细且具有法律约束力的使用条件，请参考“法律备注”章节。

# 屏幕说明

你正在以文件格式（EPUB 或 Mobi）阅读本电子书，该格式可以适应你的显示需求。这是一好事；但遗憾的是并不是每个设备都能以相同的方式显示内容。如果你想放大图片（特别是在 iPad 上），再次点击即可返回上一个屏幕。你可以在屏幕布局自定义部分找到更多建议。

## 引言

# 命令概述

按主题

### 文件管理

| 命令 | 说明 |
|---|---|
| `cat` | 输出文件 |
| `cd` | 切换目录 |
| `chgrp` | 修改组 |
| `chmod` | 修改权限 |
| `cp` | 复制 |
| `dir` | 显示目录 |
| `erd` | 修改文件 |
| `file` | 识别文件类型 |
| `install` | 安装 |
| `ch` | 修改所有者 |
| `ln` | 创建链接 |
| `ls` | 显示内容 |
| `mkdir` | 创建目录 |
| `mv` | 移动 |
| `rm` | 删除 |
| `rsync` | 同步 |
| `stat` | 提供详细信息 |
| `tee` | 输出到多个文件 |
| `touch` | 创建空文件 |
| `tree` | 显示层次结构 |
| `uermod` | 修改用户 |
| `z` | （待定） |

### 查找文件

| 命令 | 说明 |
|---|---|
| `ack` | 用于文本 |
| `column` | 按列格式化 |
| `csplit` | 按预定义点分割文本 |
| `cut` | 提取列 |
| `delta` | 比较文本并高亮差异 |
| `diff` | 比较两个文本 |
| `expand` | 将制表符替换为空格 |
| `fold` | 将长行折叠 |
| `fzf` | 交互式滚动文件 |
| `grep` | 在文件中搜索 |
| `head` | 输出文件开头 |
| `iconv` | 更改文本字符集 |
| `jq` | 从 JSON 文档提取数据 |
| `less` | 分页查看文本（支持后退） |
| `more` | 分页查看文本 |
| `maxit` | 跟踪多个文件的变化 |
| `paste` | 按行合并文本 |
| `patch` | 根据 diff 文件修改文本 |
| `recode` | 转换不同的字符集 |
| `sed` | 流编辑器（可编程编辑器） |
| `sort` | 排序 |
| `split` | 将文件分割为子文件 |
| `strings` | 从二进制文件中提取字符串 |
| `tac` | 倒序输出文本，即最后一行在前 |
| `tail` | 输出文件末尾 |
| `tr` | 替换定义字符 |
| `unexpand` | 将空格替换为制表符 |
| `uniq` | 消除文本中的重复行 |
| `zcat` | 输出压缩文本文件 |
| `zless` | 分页查看压缩文本（支持后退） |
| `zmore` | 分页查看压缩文本 |

### 压缩与归档

| 命令 | 说明 |
|---|---|
| `bunzip2` | 解压 .bz2 文件 |
| `compress` | 压缩，比 bzip2 强大 |
| `cpio` | 在文件系统中传输存档 |
| `gunzip` | 解压 .gz 文件 |
| `gzip` | 压缩，比 compress 更强大 |
| `lzop` | 压缩文件，比 gzip 更快 |
| `tar` | 创建 .tar 归档 |
| `uncompress` | 使用压缩解压 |
| `unxz` | 解压 .xz 文件 |
| `zip` | 压缩，创建 Windows 兼容归档 |
| `zipinfo` | 显示 ZIP 档 |

### 文本处理

| 命令 | 说明 |
|---|---|
| `awk` | 文本分析编程语言 |
| `bat` | 带语法高亮显示文件 |
| `cat` | 输出文件或合并文本 |
| `column` | 按列格式化信息 |
| `csplit` | 按预定义点分割文本 |
| `cut` | 提取每行的列 |
| `delta` | 比较两个文本并高亮差异 |
| `diff` | 比较两个文本 |
| `expand` | 将制表符替换为空格 |
| `fold` | 将长行折叠为短行 |
| `fzf` | 交互式浏览 JSON 文件 |
| `grep` | 在文件中搜索 |
| `head` | 输出前几行 |
| `iconv` | 更改文件的字符集 |
| `jq` | 从 JSON 文档提取数据 |
| `less` | 分页查看文本（支持后退） |
| `more` | 分页查看文本 |
| `maxit` | 跟踪多个文件的变化 |
| `paste` | 按行合并文本 |
| `patch` | 根据 diff 文件修改文本 |
| `recode` | 转换不同的字符集 |
| `sed` | 流编辑器（可编程编辑器） |
| `sort` | 排序 |
| `split` | 将文件分割为指定大小的子文件 |
| `strings` | 从二进制文件中提取字符串 |
| `tac` | 倒序输出文本，即最后一行在前 |
| `tail` | 输出文件的末尾 |
| `tr` | 将定义的字符替换为其他字符 |
| `unexpand` | 将空格替换为制表符 |
| `uniq` | 消除文本中的重复行 |
| `zcat` | 输出压缩文本文件 |
| `zless` | 分页查看压缩文本（支持后退） |
| `zmore` | 分页查看压缩文本 |
| `getfacl` | 确定文件的 ACL（访问控制列表） |
| `getfattr` | 确定文件的扩展属性 |
| `setcap` | 修改文件的能力（capabilities） |
| `setfacl` | 修改文件的 ACL（访问控制列表） |
| `setfattr` | 修改文件的扩展属性 |

## 转换器 (Converters)

| 命令 | 说明 |
|---|---|
| `convert` | 转换图形文件 |
| `dvips` | 将 DVI 文件转换为 PostScript 格式 |
| `enscript` | 将文本文件转换为 PostScript 格式 |
| `epstopdf` | 将 EPS 文件转换为 PDF 文件 |
| `exiftool` | 读取或修改 JPG 文件中的 Exif 数据 |
| `ffmpeg` | 视频视频 |
| `iconv` | 更改文本文件的字符集 |
