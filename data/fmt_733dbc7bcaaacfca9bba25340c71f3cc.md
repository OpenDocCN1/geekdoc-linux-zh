
- b. 创建一个包含整个系统的 tar 文件，名为 `fullbackup.tar.Z`，然后进行压缩。使用 `tar czf fullbackup.tar.gz` 将获得更大的压缩率。

- c. 创建一个包含整个系统的 tar 文件，名为 `fullbackup.tar.Z`，然后进行压缩。更好的命令将是 `tar cf fullbackup.tar.gz | gzip`。

- d. 创建一个包含整个系统的 tar 文件，名为 `fullbackup.tar.Z`，然后保存 `compress` 目录。

答案 a 不正确；`compress` 工具是一个较旧的压缩工具，没有最优质的压缩算法。答案 b 正确；此命令将使用 `gzip` 而不是 `compress` 来执行压缩，从而生成较小的文件。答案 c 不正确；虽然此命令行也能达到与 b 相同的结果，但效率较低。答案 d 不正确；该命令将 `tar` 文件通过管道传递给 `compress` 工具；它并未将其保存到 `compress` 目录。

10. 你使用命令 `gzip memo.bill` 压缩了文件 `memo.bill`。现在你想查看包含在此文件中的某些数字。你该怎么做？

- a. `zcat memo.bill.gz`

- b. `gunzip memo.bill.gz; less memo.bill`

- c. `cat memo.bill.gz`

- d. `less memo.bill.gz`

答案 a 正确；`zcat` 工具允许你查看压缩文件的内容而无需解压它。答案 b 不正确；这将解压文件，然后使用 `less` 命令显示它，但你之后必须重新压缩它。答案 c 不正确；`cat` 命令无法显示压缩文件。答案 d 不正确；`less` 命令无法显示压缩文件。

# 附录 A

## 词汇表

`access`（访问） 连接并利用设备；存储和检索存储在硬磁盘等外围设备上的信息。

`account`（账户） 用户与操作系统之间的关系；由用户名、密码和权限组成。

`address`（地址） 内存中的一个位置；分配给声卡等设备标识符；管理。

`administer`（管理） 控制计算机或其他设备的运行和使用；系统管理员的任务。

`algorithm`（算法） 用于解决问题的逻辑步骤；将生成满足特定要求的输出结果。

`alias`（别名） 用于识别程序的替代名称。

`Alt` 键盘上的替代键。

`analog`（模拟） 原始信号的表示，如电话将振动转换为电信号。

`ANSI` 美国国家标准学会，负责制定许多协议的标准，如电信协议。

`API` 应用程序编程接口，用于应用程序与操作系统或另一个应用程序通信。

`application`（应用程序） 计算机或程序在操作系统之上的特定用途。

`archive`（归档） 将数据复制到另一个设备以供保留；包含一个或多个文件的文件。

`argument`（参数） 传递给命令、函数或程序的值。

`ASCII` 美国标准信息交换码；用于文本的二进制代码。

`background`（后台） 运行非交互进程的方法。

`backup`（备份） 为保险目的保存的数据副本；制作数据的副本。

`binary`（二进制） 由 1 和 0 组成的数字；在计算机中用作开/关开关；包含编译代码的文件。

`BIOS` 基本输入/输出系统，在操作系统和硬件之间提供接口。

`bit`（比特） 二进制位；计算机存储的最小度量单位；单个二进制数字（0 或 1）。

`block device`（块设备） 一次移动一组字节的外围设备。

`boot`（启动） 计算机开始执行指令的动作。

`boot loader`（引导加载程序） 用于启动操作系统的应用程序。

`buffer`（缓冲区） 临时保存待处理数据的内存。

`build`（构建） 程序的版本；编译程序。

`bus`（总线） 多个设备之间的路径。

`byte`（字节） 二进制表。由 8 位组成的存储度量单位；单个字符。

`cache`（缓存） 用于提高速度的临时数据存储。

`card`（卡片） 可以插入计算机扩展槽的任何印刷电路板。

`CD-ROM` 光盘只读存储器。一种可移除介质，用于存储数据，如文本、二进制文件、声音和视频；访问此数据的设备。

`character`（字符） 等同于字节的字母、数字或符号；命令驱动接口。

`character device`（字符设备） 一次移动一个字符或字节的设备。

`child process`（子进程） 由另一个进程调用的进程。

`client`（客户端） 连接到另一台计算机并接收信息的计算机。

`command-line interface`（命令行界面） 用于输入命令的基于文本的界面。

`compression`（压缩） 去除冗余信息以减少文件大小过程。

`computer`（计算机） 处理数据及其附加设备的机器。

`console`（控制台） 用于控制和监视计算机的显示终端；计算机的用户界面。

`core dump`（核心转储） 当程序崩溃时，内存内容写入文件，通常称为 `core`。

`corrupted`（损坏的） 损坏的文件或数据。

`CPU` 中央处理单元。计算机的处理器或计算组件。

`crack`（破解） 未经授权的访问计算机系统，通常出于破坏性原因。

`cracker`（破解者） 破解计算机系统的人；用于破解计算机系统的程序。

`crash` 程序或计算机系统的意外停止；由于某种故障或错误导致的软件或硬件终止。

`Ctrl` 键盘上的 Control 键。

`current working directory` 文件系统层次结构中的当前位置。

`cwd` 参见 `current working directory`（当前工作目录）。

`cylinder` 位于每个磁盘表面相同位置的所有磁道。

`daemon` 在后台运行并在需要时执行操作的程序。

`data` 可被处理以提供信息的事实和数字。

`database` 以逻辑且可访问的方式存储的数据集合；用于访问此数据的程序。

`default` 如果未明确指定值，参数的假定值。

`Del` 键盘上的 Delete 键。

`delete` 移除或擦除数据。

`device` 可连接到计算机的硬件部件。

`die` 停止执行。

`Direct Memory Access` 将数据从一个内存块移动到另一个内存块，绕过 `CPU` 的电路。

`directory` 磁盘上的一种文件类型，用于组织其他文件。

`disk` 直接访问存储设备。

`display` 用于显示计算机信息的屏幕或监视器。

`distribution` 运行计算机所需的软件集合，包括 `Linux` 内核以及各种实用程序和应用。

`DMA` 参见 `Direct Memory Access`（直接内存访问）。

`documentation` 描述系统或应用程序的书面文档。

`drive` 提供存储和检索数据功能的设备。

`driver` 提供对外围设备访问权限的软件。

`dynamic` 在处理过程中而非之前做出的决策或执行的操作。

`editor` 用于创建和编辑文本文件的软件。

`emulator` 模拟另一种类型硬件或软件的软件。

`environment` 进程所使用的硬件或软件变量的配置。

`environment variables` 用于定义硬件或软件配置的参数。

`Esc` 键盘上的 Escape 键。

`Ethernet` 一种共享介质的局域网类型，其中所有节点共享可用带宽。

`event` 发生的事件或活动。

`executable` 可运行的二进制文件或脚本。

`execute` 启动程序。

`execute permission` 设置在文件上，允许运行该文件的权限。

`export` 使某个值对另一个进程可用。

`FAT` 参见 `File Allocation Table`（文件分配表）。

`FHS` 参见 `Filesystem Hierarchy Standard`（文件系统层次结构标准）。

`file` 作为带有名称的单一条目存储的字节集合。

`File Allocation Table` 一种简单的文件系统，用于跟踪数据存储的位置。

`filesystem` 用于控制数据存储和检索的结构。

`Filesystem Hierarchy Standard` `UNIX` 系统上文件位置的拟定标准。

`Filesystem standard` 一个关于 `Linux` 文件系统结构的旧标准，已被 `FHS` 取代。

`filter` 更改文件或显示数据内容的过程。

`floppy disk` 可移除、可重用的磁存储介质。

`floppy drive` 用于读写软盘的驱动器。
