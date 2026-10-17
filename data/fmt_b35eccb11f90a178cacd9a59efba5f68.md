
```text
FCX124 Performance Screen Selection (FL530 ) Perf. Monitor
General System Data   I/O Data   History Data (by Time)
1. CPU load and trans.      11. Channel load       31. Graphics selection
2. Storage utilization      12. Control units      32. History data files*
3. Reserved                 13. I/O device load*   33. Benchmark displays*
4. Priv. operations         14. CP owned disks*    34. Correlation coeff.
5. System counters          15. Cache extend. func.* 35. System summary*
6. CPU IUCV services        16. DASD I/O assist    36. Auxiliary storage
7. SPOOL file display*      17. DASD seek distance* 37. CP communications*
8. LPAR data                18. I/O prior. queueing* 38. DASD load
9. Shared segments          19. I/O configuration   39. Minidisk cache*
A. Shared data spaces        1A. I/O config. changes 3A. Storage mgmt. data*
B. Virtt. disks in stor.     3B. Proc. load & config*
C. Transact. statistics      User Data               3C. Logical part. load
D. Monitor data              21. User resource usage* 3D. Response time (all)*
E. Monitor settings          22. User paging load*   3E. RSK data menu*
F. System settings           23. User wait states*    3F. Scheduler queues
G. System configuration       24. User response time*  3G. Scheduler data
H. VM Resource Manager       25. Resources/transact.* 3H. SFS/BFS logs menu*
I. Exceptions                26. User communication*  31. System log
K. User defined data*        27. Multitasking users*  3K. TCP/IP data menu*
                            28. User configuration*   3L. User communication
                            29. Linux systems*        3M. User wait states

标记有星号 (*) 的显示上可以找到指向相关或更详细性能数据的指针。

使用光标选择性能屏幕并按 ENTER
Command ===>
F1=Help F4=Top F5=Bot F7=Bkwd F8=Fwd F12=Return
```

### 图 2-16 IBM z/VM 性能工具包主屏幕

IBM z/VM 性能工具包的用户界面由菜单驱动，但您可以通过输入完整或简化的报告名称来快速路径直达特定的您需要的功能。进入报告后，许多报告都包含子菜单，或者通过将光标移至变量下方并按 Enter 键来实现进一步导航。实际上，许多报告包含多层导航，例如，您可以查看 DASD 卷的顺序列表并查看整体活动，此外还可以查看控制器功能。然后您可以深入查看，更详细地查看特定卷，再进一步深入查看微型磁盘设备活动。这种导航功能极大地促进了问题定位，由于增强了可访问性，使得对系统的整体理解（甚至深入到详细级别）变得更容易。各种数据报告分为通用系统数据、I/O 数据、历史数据和用户数据这几组。

初始菜单上未高亮显示的数字对应的性能屏幕项目无法选择，因为尚未收集这些项目的 CP 监控数据。可能的原因包括：

- 所需的监控记录不可用，因为您的 VM 系统的 CP 级别尚未生成它们。
- 所需的监控域尚未启用。
- 第一个监控采样区间尚未结束，我们仍在等待初始的监控记录集。
- 该显示用于无法在该系统上生成的数据（例如，在未分区系统上的 LPAR 数据）。

#### 2.2.2 选择性能屏幕

屏幕被分组为通用系统数据、I/O 数据、用户数据（显示上一个监控采样区间或整体平均值的数据），以及一系列按时间记录的文件，它们显示每个监控采样区间的单独值集。可以通过执行以下操作之一从初始菜单中选择它们：

- 在命令线输入所选性能数据（显示在命令线上）的编号
- 将光标移动到所选显示项（请注意，如果使用制表键，它只会移动到高亮显示的编号）
- 输入所需屏幕的 `short-path` 命令

然后按 Enter 键。

为了获取用于问题定位的有意义数据，您需要了解在性能工具包中从哪里获取这些数据。

收集系统当前状态信息的一个良好起点是通用系统数据类别中的屏幕。从第一个选项开始，我们开始进行系统性能健康检查。选择 `1` 并按 Enter，或将光标置于屏幕上的适当字段并按 Enter。此选项显示整体处理器利用率、系统争用以及用户群信息。用户数据包括用户总数、活动用户数以及正在等待资源（如存储页或 I/O）的用户数。

显示的屏幕如图 2-17 所示。
