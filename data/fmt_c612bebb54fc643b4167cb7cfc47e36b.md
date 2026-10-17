
图 15-1 显示了 SunSolve 的主界面，其中列出了 Solaris 9 的所有可用大型补丁（jumbo patches）和推荐集群。

## 第 15 章：基础命令语法

### 图 15-1

从 SunSolve 获取补丁。

![](img/0ce985fd07a5af27ed793d64cf4b977d_338_0.png)

#### 补丁示例

要检查系统上安装了哪些补丁，您需要使用如下 `showcmd` 命令：

```
# showcmd -p
Patch: 107430-01 Obsolete: Requires: Incompatibles: Packages: SUNWsar
Patch: 108029-01 Obsolete: Requires: Incompatibles: Packages: SUNWsar
Patch: 107697-03 Obsolete: Requires: Incompatibles: Packages: SUNWtiub
Patch: 107316-01 Obsolete: Requires: Incompatibles: Packages: SUNWvloc
Patch: 107453-01 Obsolete: Requires: Incompatibles: Packages: SUNWkvm, SunWC
```

`Patch: 106451-06 Obsolete: 106976-01, 107029-01, 107030-01, 107334-01 Requires: Incompatibles: Packages: SUNWsar, SunWcu, SunWcr, SunWcscl, SUNWesar, SUNWfar, SUNWatfs, SUNWcp, SUNWdwpl, SUNWdp1, SUNWipmc, SUNWpcmp, SUNWpcmc, SUNWntfc, WNVolr`

`Patch: 106451-10 Obsolete: 106832-03, 106976-01, 107029-01, 107334-01 1, 107031-01, 107117-05, 107899-01 Requires: 107544-02 Incompatibles: Packages: SUNWkvm, SunWcsu, SunWcsr, SunWcscl, SUNWicar, SUNWarc, SUNWatfs, SUNWsar cpu, SUNWcpr, SUNWdwpl, SUNWdp1, SUNWipmc, SUNWpcmp, SUNWpcmc, SUNWntfc, WNVolr`

`Patch: 106451-15 Obsolete: 106832-03, 106976-01, 107029-01, 107334-01 1, 107031-01, 107117-05, 107899-01, 107548-01, 109104-04 Requires: 10 7544-02 Incompatibles: SUNWkvm, SunWcsu, SunWcsr, SunWcscl, SUNWicar, 0, SUNWesar, SUNWarc, SUNWatfs, SUNWcpr, SUNWdwpl, SUNWdp1, SUNWipmc, 0, SUNWesar, SUNWpcmc, SUNWpcmc, SUNWntfc, Volr`

从此示例中我们可以看到 `showcmd` 报告了每个已安装补丁的不同属性：

- 补丁编号。
- 补丁是否替换了先前发布的补丁（或多个补丁）以及版本号是多少。
- 当前补丁是否依赖于任何先决补丁（以及它们的版本号）。
- 补丁是否与其他补丁不兼容。
- 安装该补丁影响了哪些标准 Solaris 软件包。

从这些示例之一（`106451-15`）中，我们可以看到：

11. 测试 `"-d file"` 的逻辑结果是什么？

- A. 且仅当 `file` 是特殊块设备文件时，为真。
- B. 且仅当 `file` 是特殊字符设备文件时，为真。
- C. 且仅当 `file` 是一个目录时，为真。
- D. 且仅当 `file` 是一个普通文件时，为真。

12. 测试 `"-f file"` 的逻辑结果是什么？

- A. 且仅当 `file` 是特殊块设备文件时，为真。
- B. 且仅当 `file` 是特殊字符设备文件时，为真。
- C. 且仅当 `file` 是一个目录时，为真。
- D. 且仅当 `file` 是一个普通文件时，为真。

13. 测试 `"-p file"` 的逻辑结果是什么？

- A. 且仅当 `file` 是命名管道时，为真。
- B. 且仅当 `file` 大不为零时，为真。
- C. 且仅当当前用户对 `file` 有可写权限时，为真。
- D. 且仅当当前用户对 `file` 有执行权限时，为真。

14. 测试 `"-s file"` 的逻辑结果是什么？

- A. 且仅当 `file` 是命名管道时，为真。
- B. 且仅当 `file` 大不为零时，为真。
- C. 且仅当当前用户对 `file` 有可写权限时，为真。
- D. 且仅当当前用户对 `file` 有执行权限时，为真。

15. 测试 `"-w file"` 的逻辑结果是什么？

- A. 且仅当 `file` 是命名管道时，为真。
- B. 且仅当 `file` 大不为零时，为真。
- C. 且仅当当前用户对 `file` 有可写权限时，为真。
- D. 且仅当当前用户对 `file` 有执行权限时，为真。

## 答案

- 1. D. 测试 `"-n str"` 的逻辑结果且仅当字符串 `str` 的长度不为零时为真。
- 2. C. 测试 `"str"` 的逻辑结果且仅当字符串 `str` 不空时为真。
- 3. B. 测试 `"str1 != str2"` 的逻辑结果且仅当组成字符串 `str1` 的字符与组成字符串 `str2` 的字符不相同且顺序不同时为真。
- 4. A. 测试 `"-z str"` 的逻辑结果且仅当字符串长度为零时为真。
- 5. D. 测试 `"-eq b"` 的逻辑结果且仅当 `a` 等于 `b` 时为真。
- 6. C. 测试 `"-ge b"` 的逻辑结果且仅当 `a` 大于或等于 `b` 时为真。
- 7. B. 测试 `"-gt b"` 的逻辑结果且仅当 `a` 大于 `b` 时为真。
- 8. A. 测试 `"-le b"` 的逻辑结果且仅当 `a` 小于或等于 `b` 时为真。
- 9. A. 测试 `"-b file"` 的逻辑结果且仅当 `file` 是特殊块设备文件时为真。
- 10. B. 测试 `"-c file"` 的逻辑结果且仅当 `file` 是特殊字符设备文件时为真。
- 11. C. 测试 `"-d file"` 的逻辑结果且仅当 `file` 是一个目录时为真。
- 12. D. 测试 `"-f file"` 的逻辑结果且仅当 `file` 是一个普通文件时为真。
- 13. A. 测试 `"-p file"` 的逻辑结果且仅当 `file` 是命名管道时为真。
- 14. B. 测试 `"-s file"` 的逻辑结果且仅当 `file` 大不为零时为真。
- 15. C. 测试 `"-w file"` 的逻辑结果且仅当当前用户对 `file` 有可写权限时为真。

# Sun 认证 Solaris 9.0 系统和网络管理员合一考试指南

# 编辑器

在本章中，你将：

- 学习如何使用 `vi` 编辑器
- 创建新的文本文件
- 编辑现有的文本文件

编辑器主要用于创建新的文本文件或编辑现有的文本文件。在学习使用 Solaris shell 时，很少有 UNIX 用户能避免学习视觉编辑器（`"vi"`）。在本章中，目标是回顾一些较深奥的用法，以及常用的命令模式和 ex 模式命令。

# 视觉编辑器 (vi)

`vi` 是一个在 Solaris 和其他 UNIX 系统上执行以下任务的文本处理工具：

- 创建新的文本文件
- 修改现有文件
- 在文件中搜索文本字符串
- 在文件中将一个字符串替换为另一个
- 在文件内移动或复制字符串
- 从文件中删除字符串

要从命令行运行 `vi` 并创建一个新文件，可以使用以下命令：

```
$ vi
```

要从命令行运行 `vi` 并编辑现有文件，可以使用以下命令：

```
$ vi file.txt
```

其中 `file.txt` 是要编辑的文件名。编辑文件（如 `/etc/passwd.txt`）的结果如如图 16-1 所示。

# 图 16-1

编辑 `/etc/passwd` 文件

```
root:x:0:0:Super-User::/bin/sh
demon:x:1:1:::
bin:x:2:2::/usr/bin
sys:x:3:3::
adm:x:4::/var/adm
lp:x:5::/usr/spool/lp
uucp:x:6::/usr/lib/uucp
listen:x:7::/var/net
nobody:x:8::
natasha:x:9::/export/home/natasha/bin
pwatters:x:10::/export/home/pwatters/bin
```
