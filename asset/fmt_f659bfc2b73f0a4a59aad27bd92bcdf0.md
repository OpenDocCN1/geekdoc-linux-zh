
## `cp -f IBMconfig /usr/bin/`

如果你正在运行 IBM 带驱动程序 V1.4.1 或更高版本，`IBMTaped` 进程将自动为你在 `/dev` 目录下创建特殊文件。在我们的案例中，`IBMTaped` 自动启动了。否则，你需要运行 `IBMtapeconfig` 来管理已连接设备的特殊文件的创建。

示例 4-33 所示的两个命令允许你查看由 `IBMTape` 设备驱动程序创建的设备（带驱动器和更改）：

```bash
cat /proc/scsi/IBMTape
cat /proc/scsi/IBMTunchanger
```

### 示例 4-33 通过 IBMTapeconfig 创建的设备

```bash
## cat /proc/scsi/IBMTunchanger
IBMTape version: 2.0.6
IBMTape major number: 253
Attached Tape Devices:
Number Model SN HBA FO Path
0 ULTRIM-TD3 1200001355 qla2xxx NA
1 ULTRIM-TD3 1200001377 qla2xxx NA
2 ULTRIM-TD3 1200001376 qla2xxx NA
## cat /proc/scsi/IBMTunchanger
IBMTape version: 2.0.6
IBMTape major number: 253
Attached Tape Devices:
Number Model SN HBA FO Path
0 0358L32 0000013100080744 qla2xxx NA
```

要验证安装是否成功，请使用命令 `rpm -qs IBMTape`，如第 205 页示例 4-34 所示。如果安装成功，状态应显示为 normal（正常）。

### 示例 4-34 检查 IBM Ultrium 驱动程序的状态

```bash
## rpm -qs IBMTape
normal /etc/IBMTape.conf
normal /lib/modules/2.6.5-7.151-bigmp/kernel/drivers/scsi/IBMTape.ko
normal /lib/modules/2.6.5-7.151-default/kernel/scsi/IBMTape.ko
normal /lib/modules/2.6.5-7.151-smmp/kernel/drivers/scsi/IBMTape.ko
normal /usr/bin/IBMTape
normal /usr/bin/startIBMTape
normal /usr/include/sys/IBMTape.h
normal /usr/share/doc/packages/IBMTape
normal /usr/share/doc/packages/IBMTape/IBMTape_359X.ReadMe
normal /usr/share/doc/packages/IBMTape/IBMTape_Ultrium.ReadMe
normal /usr/share/doc/packages/IBMTape/IBMTaped.ReadMe
```

现在我们准备好使用 IBM 驱动程序使用 Ultrium 磁和库设备了。即使你计划使用原生 Linux 驱动程序使用带和库设备，我们也建议安装 IBM 驱动程序，以便对 Ultrium 带和库设备进行微代码更新。如果你使用的是 IBM 驱动程序不支持的 Linux 内核，我们建议安装受支持的内核作为此目的备用启动内核。

示例 4-35 显示了 `IBMtapeutil` 的初始调用界面。

### 示例 4-35 IBMtapeutil 启动界面

```
IBMTapeutil for Linux, Version 1.3.1, Sept. 14, 2004
===============================================================================
1. Tape
2. Changer
3. Quit
================================================================================
```

输入你的选择：

示例 4-36 显示了通过 `IBMtapeutil` 可用的通用 SCSI 命令以及磁带特定命令。

### 示例 4-36 Linux 下 IBMtapeutil 磁带命令选择界面

| 通用命令: | |
| :--- | :--- |
| 1. 打开设备 | 9. 模式感知页 |
| 2. 关闭设备 | 10. 切换磁带/变化器设备 |
| 3. 查询 | 11. 创建特殊文件 |
| 4. 测试单元就绪 | 12. 查询驱动程序版本 |
| 5. 保留 | 13. 查询设备路径 |
| 6. 释放设备 | 14. 显示所有路径 |
| 7. 请求感知 | 15. 启用 A 路 |
| 8. 日志感知页 | 16. 禁用 A 路 |
| | Quit IBMtapeutil |
| 磁带命令: | |
| :--- | :--- |
| 20. 回卷 | 33. 设置块大小 |
| 21. 前向空标记 | 34. 留存带 |
| 22. 反向空标记 | 35. 查询/设置磁带位置 |
| 23. 前向空记录 | 36. 查询磁带状态 |
| 24. 反向空记录 | 37. 加载磁带 |
| 25. FSM | 38. 卸载磁带 |
| 26. BFM | 39. 锁定带门 |
| 27. 到末尾 | 40. 解锁带门 |
| 28. 读取和写入 | 41. 取出磁带 |
| 29. 写入空标记 | 42. 启用/禁用压缩 |
| 30. 读取或写入 | 43. 刷新缓冲区 |
| 31. 擦除 | 44. 自检 |
| 32. 重置驱动器 | 45. 显示消息 |
| IBM 命令: | |
| :--- | :--- |
| 46. 查询感知 | 52. 定位磁带 |
| 47. 查询 | 53. 读取磁带位置 |
| 48. 查询/设置磁带参数 | 54. 查询设备号 |
| 49. 查询/设置磁带位置 | 55. 同步缓冲区 |
| 50. 查询/设置 MT/ST 模式 | 56. 列出带空标记 |
| 51. 报告密度 | |
| 服务辅助命令: | |
| :--- | :--- |
| 70. 转储设备 | 74. 读取留存键 |
| 71. 强制转储 | 75. 读取留存 |
| 72. 加载 Ucode | 76. 注册留存键 |
| 73. 重置驱动器 | 77. 删除留存 |
| 78. 清除所有注册 | |
| 99. 返回主菜单 | |

输入选择：

示例 4-37 显示了如何使用 `IBMtapeutil` 将 SCSI 命令发送到磁带设备。

### 示例 4-37 使用 IBMtapeutil 向 LTO 磁带驱动器发送 SCSI 命令

输入选择: 1
输入 `/dev/IBMTape0` 设备名称: `/dev/IBMTape1`
选择模式 (1=读取/写入, 2=只读, 3=只写, 4=追加): 1
正在打开设备...
按 `<enter>` 继续...
为 `/dev/IBMTape1` 选择 3 进行标准查询:
正在执行查询...

```
查询数据:
外围限定符: 000
外围设备类型: 001
移除介质: 1
设备修饰: 00
ISO 版本: 00
ECMA 版本: 00
ANSI 版本: 03
异步事件通知位: 0
终止 I/O 进程消息位: 0
响应数据格式: 002
附加长度: 035
介质变化器模式: 000
相对寻址: 0
32 位宽数据: 0
16 位宽数据: 0
链接命令位: 0
命令队列位: 01
软重置位: 0
厂商 ID: IBM
产品 ID: ULTUM-TD3
产品版本: 54KC
```

vendor1, 长度 20
```
0 1 2 3 4 5 6 7 8 9 A B C D E F 0123456789ABCDEF
0000 0000 0000 0000 0000 0000 0000 2030 [......0]
0010 0000 0000 0000 0000 0000 [...... ]
```

vendor2, 长度 31
```
0 1 2 3 4 5 6 7 8 9 A B C D E F 0123456789ABCDEF
0000 0000 0000 0000 0000 0000 [................]
0010 0000 0000 0000 0000 0000 00 [................].
```
