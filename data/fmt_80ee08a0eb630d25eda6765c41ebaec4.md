
```
lrwxrwxrwx  1 root  sys  22 Nov 23 18:09 /var/local/foo
file://D/Coo/Stuff/old/unix-hints-and-hacks.ta/unix-hints-and-hacks/unix-hints-and-hacks/19270092.html (vol 1 [12.05.2000 15:13:18])
```

## 文件管理：6.8 移动和重命名文件组

- `/usr/local/foo`
- `/usr/local/foo.OLD`

当文件或目录跨文件系统移动时，它必须将文件复制到新位置。完成后，`mv` 命令会删除原始文件或目录。如果文件或目录不是跨文件系统移动（本地或远程系统），则只需更改原始名称，inode指向新名称。

### 示例二：使用 mv 重命名文件

变体：AT&T, BSD
Shell：`sh`

- `/usr/local/foo`
- 

当文件或目录跨文件系统移动时，它必须将文件复制到新位置。完成后，`mv` 命令会删除原始文件或目录。如果文件或目录不是跨文件系统移动（本地或远程系统），则只需更改原始名称，inode指向新名称。

### 示例三：将文件名重命名为小写

变体：AT&T, BSD
Shell：`sh`

- `/usr/local/foo`
- 

当文件或目录跨文件系统移动时，它必须将文件复制到新位置。完成后，`mv` 命令会删除原始文件或目录。如果文件或目录不是跨文件系统移动（本地或远程系统），则只需更改原始名称，inode指向新名称。

```
PASSWD -> password

RC.LOCAL -> rc-local

SendMail.CF -> sendmail.cf

rocket 59% ls -1

alias

password

rc.local

sendmail.cf
```

## 理由

文件可能是下载而来的，或者处于在个人环境中运行不良好的状态。重命名或移动文件是让各种文件进入对我们最有用状态的最佳方法之一。

## 真实世界经验

随着网络中出现越来越多的 DOS 和 NT 机器，传输文件可能会导致文件名大小写错误，或者限制组成文件名的字符数。我们需要将这些文件移动或重命名为 UNIX 管理员可以处理的命名规范。

## 其他资源

帮助页 (Man pages)：

`mv`, `tr`

## UNIX 技巧与窍门
目录 | 索引

第 6 章：文件管理
上一章 | 下一章

本章章节：
6.1 带有权限和时间戳复制文件 | 6.5 使用 grep 查找文件 | 6.8 移动和重命名文件组 | 6.11 分割文件
6.2 远程复制文件 | 6.6 多重 grep | 6.9 去除帮助页 | 6.12 限制核心文件大小
6.3 哪个 tmp 是好的临时目录？ | 6.7 使用 find 递归执行命令 | 6.10 清理 DOS 文件 | 6.13 uencode 和 uidecode
6.4 处理符号链接

上一节 | 下一节

© Macmillan USA. 版权所有。

## UNIX 技巧与窍门
去除帮助页

第 6 章：文件管理

本章章节：
- 6.1 带有权限和时间戳复制文件
- 6.2 远程复制文件
- 6.3 哪个 Temp 是好的临时目录？
- 6.4 处理符号链接
- 6.5 使用 grep 查找文件
- 6.6 多重 grep
- 6.7 使用 find 递归执行命令
- 6.8 移动和重命名文件
- 6.9 清理 DOS 文件
- 6.11 分割文件
- 6.12 限制核心文件大小
- 6.13 unicode 和 decode

上一章 | 下一章
上一节 | 下一节

## 6.9 去除帮助页

### 6.9.1

有一种方法可以去除所有非必要的转义字符，使帮助页更具可读性。

版本：AT&T, BSD

语法：
`man - [manpage] | col -b > [file]`

帮助页对于学习命令和函数非常有用。它们可以根据传递给它们的参数进行处理。如果帮助页中嵌入的所有转义序列对终端难以解析，有一种方法可以将帮助页转换为纯文本。要在 `vi` 编辑器中查看帮助页，你通常需要执行以下步骤：

```
rocket 60% man tar > /usr/tmp/tar.man
```

将帮助页的输出重定向到文件，以便你对该文件运行编辑器。

```
rocket 61 vi /usr/tmp/tar.man
```

当用 `vi` 编辑文件时，由于传递了所有的转义序列，文件会变得非常晦涩。

```
tar(1)
```

## 用户命令

```
tar(1)
```

## 名称
`tar` - 创建磁带存档，并添加或提取文件

### 概要
```
/usr/sbin/tar c [ bBefFilhlwX [ 0 -7 ] ] [ _Hd_He_^He_He_Hv_Hi_^Hc_He ] [ _Hb_HL_Ho_Hc_Hk ] [ _He_Hx_Hc_Hl_Hu_Hd_He- _Hf_Hi_^Hi_He_En_Na_Hm_He ... ] [ -I_Hf_Hi_He_Hl_Hu_Hd_He- _Hf_Hi_^Hi_He_En_Na_Hm_He ... ] [ -C _Hd_Hi_^Hi_Hr_He_Hc_Ht_O_Hr_Hy_Hf_Hi_^Hi_Hu_He_En_Na_Hm_He ... ] /usr/sbin/tar r [ bBefFilhlwX [ 0 -7 ] [ _Hd_He_^Hv_Hi_^Hc_He ] [ _Hb_HL_Ho_Hc_Hk ] [ -I_Hf_Hi_He_Hl_Hu_Hd_He- _Hf_Hi_^Hi_He_En_Na_Hm_He ... ] - _Hf_Hi_He_Hi_Na_Hm_He ...
```

## 第 6 章：文件管理：9 去除帮助页

为了清理所有转义序列，请通过 `col` 命令运行它们。通过添加 `-b` 选项。当帮助页通过 `col` 命令管道时，转义序列会被 `-b` 选项去除。现在帮助页被重定向到文件并带入编辑器，你就可以看到纯文本。

```
rocket 62 man - tar | col -b > /usr/tmp/tar.man

rocket 63 vi | /usr/tmp/tar.man
```

## 用户命令

## tar(1)

## 名称
`tar` - 创建磁带存档，并添加或提取文件

### 概要
```
/usr/bin/tar c [ bBefFilhwx [ 0-7 ] [ device ] [ block ]
```
