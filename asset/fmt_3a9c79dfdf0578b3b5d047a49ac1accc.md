
```
Formatting...
No sense error during write
ASC: 0x0 ASCQ: 0x0
Warning: error saving defect list.
No sense error during write
ASC: 0x0 ASCQ: 0x0
Warning: error saving defect list.
Apr 1 21:34:37 Barracuda vmnix: sd2c:
No sense error during write
ASC: 0x0 ASCQ: 0x0
Warning: error writing backup label.
No sense error during write
ASC: 0x0 ASCQ: 0x0
Warning: error writing backup label.
No sense error during write
ASC: 0x0 ASCQ: 0x0
Warning: error writing backup label.
No sense error during write
ASC: 0x0 ASCQ: 0x0
Warning: error writing backup label.
Apr 1 21:34:37 Barracuda vmnix: sd2c:
No sense error during write
ASC: 0x0 ASCQ: 0x0
Warning: error writing backup label.
```

Error for command `write(10)`

Verifying media...

```
pass 0 - pattern = 0xc6dec6d6
Apr 1 21:34:37 Barracuda vmnix: sd2c: Block 7273875,
Absolute Block: 590618
Apr 1 21:34:37 Barracuda vmnix: sd2c: Sense Key: Illegal Request
Apr 1 21:34:37 Barracuda vmnix: sd2c: Vendor 'MICROP' error code: 0x21
Apr 1 21:34:37 Barracuda vmnix: sd2c: Error for command 'write(10)'
Apr 1 21:34:37 Barracuda vmnix: sd2c: Error Level: Fatal
```

## 添加基础设备

将我已知的扇区数量 5,906,128 除以 58,191 得到 101.49555，略大于 101。这个结果不是整数似乎有点奇怪， 102×58,191 得到 5,935,482，略多于扇区数量；而 101×58,191 得到 5,877,291，略少于扇区数量。101 看起来是作为我的扇区/磁道（sectors/track）值的最佳选择。

为了验证这个选择，我决定做一下我开始时可以做但没有做的事，这样我就可以看到在没有厂商数据的情况下该如何操作。考虑到总柱面数、磁头数以及数据扇区/磁道系数的积等于总可用块数，那么认为（总块数)/(总磁头数*柱面数）应该能得到扇区/磁道数，这是合理的。5,906,128/2,772/2)=101.4589，这也暗示了 101 是一个不错的猜测。

所以我再次尝试，这次用 101 作为我的猜测。我还是尝试了好几次才弄对，因为在命名磁盘时，我试图包含尽可能关于配置的信息：

- 输入数据柱面数: 2770
- 输入交替柱面数 [2]:
- 输入物理柱面数 [2772]:
- 输入磁头数: 21
- 输入数据扇区/磁道数: 101
- 输入驱动器名称 [3600]: 5400
- 输入磁盘类型名称（记得引号）
- `"Micr936 3GB cy2770 al2 hd2 sec101"`

`selecting sd2:<Micr936 3GB cy2770 al2 hd2 sec101>`

[磁盘已格式化，无缺陷列表]

没有分区表。

注意，没有发现缺陷列表。虽然你可能认为这是一件好事——没有缺陷——但对于某些操作系统来说这实际上有点问题。几乎所有驱动器都有一定数量的缺陷，通常是很少的（1GB 驱动器上有数百个），而某些版本的格式化程序是由程序员编写的，他们认为 0 是一个有效的缺陷数量。如果你的驱动器格式化由于显而易见原因意外失败，请检查缺陷列表中是否有任何缺陷，如果没有，手动添加一个。我只听过另外一个人遇到过这个问题，而我自己的其中一个驱动器也遇到过，所以这成了一个习惯性的检查动作。

我运行 `defect` 命令来提取厂商的缺陷列表，这样格式化步骤中就记录了一个缺陷列表：

`format> defect`

+ DEFECT MENU:
  restore - 设置工作列表 = 当前列表
  original - 从磁盘提取厂商列表
- extract extract 从磁盘提取工作列表
- add add 向工作列表添加缺陷
- delete delete 从工作列表中删除缺陷
- print display 显示工作列表
- dump dump 将工作列表转储到文件
- load load 从文件加载工作列表
- commit set 当前列表 = 工作列表
- create recreatesmanufacturers defect 从磁盘重新创建厂商缺陷列表

`defect original`

正在提取厂商缺陷列表...提取完成。

工作列表已更新，共 94 个缺陷。

`defect quit`

警告：工作缺陷列表已修改；但未提交。

是否要对当前缺陷列表进行更改？yes

当前缺陷列表已更新，共 94 个缺陷。

磁盘必须重新格式化以使更改。

如果驱动器上没有厂商缺陷列表，我会使用 `defect` 菜单命令强制添加一个假设的坏块。这样做会损失少量的磁盘空间，但这种技巧被认为可以修复因未知原因无法格式化的驱动器问题。

然后，我运行实际格式化：

`format=format`

准备好格式化。格式化无法中断

并需要 24 分钟（估计）。继续吗？yes

开始格式化。当前时间是 1999年4月1日 周四 22:17:34

格式化中...完成

```
正在验证介质...
pass 0 - pattern = 0xcdec6de
2769/20/59

pass 1 - pattern = 0xb6db6dbd
2769/20/59
```

修复了 0 个缺陷块。

两到三小时后，我发现这次格式化成功了！然后，我给驱动器标记标签并退出格式化。总结一下适用于我驱动器的数字，我总共有 5.906.128 个可用块。供应商信息显示总共有 2.772 个柱面和 21 个磁头。101 似乎是扇区/磁道数的良好猜测。

(2.772)x(21)x(101)=5879412 块，在范围内。

如果你在安装过程中除了块数之外没有任何物理参数，那么你将在格式化的每个阶段都进行猜测，而不仅仅是扇区/磁道那一步。记住 (磁道)x(磁头)

## 添加基础设备

(扇区/磁道)=(块数)。这可能需要一些尝试。

## 第8 天

## 添加基础设备

## 磁盘分区

## 磁盘分区表

图 8.4

新硬盘的分区选择。

| 通用信息 | |
| :--- | :--- |
| 主机名: | Barracuda |
| 驱动及厂商型号: | Microcorp 1936-21MW1092407 |
| 柱面 | 2770 | 扇区 | 21 |
| 位置: | 内部 X | 外部 O |
| SCSI ID: | 2 | SCSI 控制器: O | 容量: ~36GB |
| 部分 | 类型/标签 | 柱面 | 块 | 大 | 挂载点 |
|---|---|---|---|---|---|
| a | | (1159/0/0) | 2458239 | ~1.2GB | usr/local |
| b | swap | (97/0/0) | 205737 | ~400M | |
| c | | (2770/0/0) | 5875170 | ~308 | |
| d | | (608/0/0) | 1289568 | ~630M | archive |
| e | | (903/0/0) | 1915263 | ~935M | home |

![](img/74418f52d5d454acca60721059dbdc99_242_0.png)

现在，开始实际分区过程：

+ 分区菜单：
- 修改 'a' 分区
- 修改 'b' 分区
- 修改 'c' 分区

## 第 8 天

- 修改 'd' 分区
- 修改 'e' 分区
- 修改 'f' 分区
- 修改 'g' 分区
- 修改 'h' 分区
- 选择预定义表
- 命名当前表
- 打印显示当前表
- 将分区映射和标签写入磁盘

如你所示，运行 `partition` 会调出我的分区菜单。要设置分区 A 的大小，我只需要输入 `a`。然后，我必须提供一个起始柱面和一个块大小。我决定我的起始柱面为 0，因为它是软件分区，我的目标块数值将是 (1.200MB)(2,048)=2,457,600。
