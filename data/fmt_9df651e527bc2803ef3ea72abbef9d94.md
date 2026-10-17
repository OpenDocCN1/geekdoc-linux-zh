
我们可以使用`chmod`命令为文件分配执行权限。`chmod`命令将在本节稍后部分描述。当我们创建一个文件时，默认不会分配执行权限。

## 更改权限：符号模式

- 符号模式下`chmod`命令的语法为：

`chmod symbolic_mode filename`

- `symbolic_mode`选项由三部分组成：

  - 受影响的用户类别（所有者、组或其他）
  - 执行的操作
  - 受影响的权限

- 例如，如果选项是`g+x`，则为组添加执行权限。

```
student@krosum~$ ls -l pl.txt
-rw-r--r. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~$ chmod u+x pl.txt # 为用户添加执行权限
student@krosum~
student@krosum~$ ls -l pl.txt
-rwx-r--. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~
student@krosum~$ chmod o-r pl.txt # 删除其他用户的读权限
student@krosum~
student@krosum~$ ls -l pl.txt
-rw-r--. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~~
```

- 下面示例说明了如何使用符号模式修改文件和目录的权限。

```
$ chmod symbolic_mode filename
```

```
who op permissions
```

| | u 所有者 (用户) 权限 |
|---|---|

| g | 组权限 |
| o | 其他权限 |
| a | 所有权限 (所有者、组、其他) |

- `+` 添加权限
- `-` 删除权限
- `=` 绝对分配权限
- `r` 读
- `w` 写
- `x` 执行

### 符号模式语法说明

- 上图显示了符号模式命令语法的组成部分。
- 前三个字母代表“谁”`who`，由以下代码组成：

`u` : 所有者（用户）权限

`g` : 组权限

`o` : 其他权限

`a` : 所有权限（所有者、组、其他）

- 下一部分是“操作”`op`部分，包含以下：

`+` : 添加权限

`-` : 删除权限

`=` : 分配权限

- 最后一部分是“权限”`permissions`部分，包含以下：

`r` : 读

`w` : 写

`x` : 执行

## 更改权限：八进制模式

- 八进制模式下的`chmod`命令语法为：

`chmod octal_mode filename`

- `octal_mode`选项由三个八进制数字 4、2 和 1 组成，代表文件/目录从 0–7 的权限组合。

| 八进制值 | 权限 |
|---|---|
| 4 | 读 |
| 2 | 写 |
| 1 | 执行 |

- 上图显示了与权限对应的八进制数字。
- 对于每个权限集，这些数字组合成一个单一数字。

| 八进制值 | 权限 | 二进制 |
|---|---|---|
| 7 | rwx | 111(4+2+1) |
| 6 | rw- | 110(4+2+0) |
| 5 | r-x | 101(4+0+1) |
| 4 | r-- | 100(4+0+0) |
| 3 | -wx | 011(0+2+1) |
| 2 | -w- | 010(0+2+0) |
| 1 | --x | 001(0+0+1) |
| 0 | --- | 000(0+0+0) |

### 八进制模式示例

- 表格显示了代表组合权限的八进制数字。
- 我们通过组合八进制数字来修改每个类别的权限。
- 第一组八进制数字定义所有者权限，第二组定义组权限，第三组定义其他权限。

| 八进制模式 | 权限 |
|---|---|
| 644 | rw-r-- |
| 751 | rwxr-x-- |
| 775 | rwxrx-x |
| 777 | rwxrwxrwx |

```
student@krosum~$ ls -l pl.txt
-rw-r--. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~$ chmod 755 pl.txt
student@krosum~
student@krosum~$ ls -l pl.txt
-rwxr-xr-x 1 student 47 Mar 20 20:59 pl.txt
```

| 八进制模式 | 权限 |
|---|---|
| 644 | rw-r-- |
| 751 | rwxr-x-- |
| 775 | rwxrx-x |
| 777 | rwxrwxrwx |

- 第一组八进制数字定义所有者权限，第二组定义组权限，第三组定义其他权限。
- 第一个字符代表所有者的 UID。
- 第五个字符代表组的 GID。
- 第六组代表大小。
- 第七组字符代表文件或目录最后修改的时间日期。
- 最后一组字符代表文件或目录名称。

## 第12章 - UMASK 命令

- 当创建文件和目录时，会自动分配权限。
- 文件的初始权限是 666 `rw-rw-`，目录是 777 `rwxrwx`。
- 码影响文件和目录的默认权限。
- 我们可以通过`umask`在用户文件中设置掩码。
- 查看`umask`值，运行`umask`命令。

```
student@krosum~$ umask
root@krosum]# umask
002 22
```

**注意：**

- 非 root 用户默认`umask`值为 002。
- root 用户默认`umask`值为 022。
- `umask`工具影响文件和目录的初始权限。
- `umask`工具是一个三位八进制值，与读、写、执行权限相关。
- 第一个数字决定所有者的默认权限，第二个数字决定组的默认权限，第三个数字决定其他用户的权限。
- 例如，要将用户文件的默认权限设置为`rw-rw-rw-`，运行以下命令：

```
umask000
```

### 确定 umask 值

| umask 八进制值 | 文件权限 | 目录权限 |
|---|---|---|
| 0 | rw- | rwx |
| 1 | rw- | rw- |
| 2 | r-- | r-- |
| 3 | r-- | r-- |
| 4 | -w- | -wx |
| 5 | -w- | -w- |
| 6 | --- | - |

- 表格显示了每个`umask`八进制值对应的文件和目录权限。
- 该表格也可以帮助我们确定要在文件和目录上设置的`umask`值。
- 要确定文件的`umask`值，从 666 或目录的 777 中减去我们想要的权限值。
- 假设我们想将文件的`umask`值改为 644 `rw-r--`，666 减去 644 得到 022，这就是你作为`umask`命令参数使用的值。

| 777 |
| 00 2(-) |
| 775 |
| 默认目录权限（非 root 用户） |
| rwxwxr-x |

```
[student@ksum ~]$ umask
0002
[student@ksum ~]$ vi t1.txt # creating new file
[student@ksum ~]$ ls -l t1.txt
-rw-rw-r--. 1 student student 3 Jun 14 13:20 t1.txt
[student@ksum ~]$$
[student@ksum ~]$ mkdir Demo # creating new directory
[student@ksum ~]$$
[student@ksum ~]$ ls -ld Demo
drwxrxr-x. 2 student student 4096 Jun 14 13:21 Demo
[student@ksum ~]$ $
```

```

| 777 |
| 02 2(-) |
| 755 |
| 默认目录权限（root 用户） |
| rwxrxr-x |

| 666 |
| 02 2(-) |

### 6 4 4

默认文件权限
（root 用户）

```

rw-r--r--

```

```

[root@krosum T]# umask

0022

[root@krosum T]# vi t1.txt # creating new file

[root@krosum T]# ls -l t1.txt

-rw-r--r--. 1 root root 4 Jun 14 13:25 t1.txt

[root@krosum T]##

[root@krosum T]# mkdir Demo # creating new directory

[root@krosum T]#

[root@krosum T]# ls -ld Demo

drwxr-xr-x. 2 root root 4096 Jun 14 13:25 Demo

[root@krosum T]# 

```
