
其中`hd1`指的是第一个磁盘上的分区（出于某些原因，GRUB从零开始计数并相应分区）。请根据你的系统进行调整。

## 高级救援 github

重新安装，在其他地方有单独的按钮，但你也可以在这里更改引导程序的位置。你多久搜索一次为`Grub`添加选项的解决方案？你可以去编辑配置文件，但引导程序修复（`Boot Repair`）现在有一个标签，你可以在其中不编辑系统关键文件的情况下添加选项，这比让情况变糟风险小。

当前版本的`Rescatuer`是测试版，包含一些`bug`。如果其中一两个工具无法正常工作，尽管我们没有发现任何异常情况，但如果你需要

![img/09c2db624d208d272aaec8e2a116126d_111_0.png](img/09c2db624d208d272aaec8e2a116126d_111_0.png)

![img/09c2db624d208d272aaec8e2a116126d_112_0.png](img/09c2db624d208d272aaec8e2a116126d_112_0.png)

![img/09c2db624d208d272aaec8e2a116126d_112_1.png](img/09c2db624d208d272aaec8e2a116126d_112_1.png)

![img/09c2db624d208d272aaec8e2a116126d_112_2.png](img/09c2db624d208d272aaec8e2a116126d_112_2.png)

![img/09c2db624d208d272aaec8e2a116126d_112_3.png](img/09c2db624d208d272aaec8e2a116126d_112_3.png)

![img/09c2db624d208d272aaec8e2a116126d_112_4.png](img/09c2db624d208d272aaec8e2a116126d_112_4.png)

# 启动过程

当你按下电源键时，控制权最初会被交给电脑的`EFI`或`BIOS`，它会启动相关组件、执行基础诊断并找到启动设备（通常是你的硬盘）。一旦`EFI`或`BIOS`在启动初期加载了引导程序（loader），该程序就会加载下一阶段（例如`eifs_stage_1`），随后再次加载引导程序。

引导程序的出现出现意味着你需要救援支持来完成诊断，无论是在`UEFI`还是`BIOS`环境下。一旦启动成功，它会加载一个文件菜单，其中包含你在启动菜单看到的选项列表。每个条目标识了包含`Linux`内核、内核使用的`RAM`磁盘的驱动器、分区和文件，可能包含内核的额外参数。

控制权传递给内核，内核会尝试挂载根文件系统。这是一个关键时刻，如果失败，可能会导致内核崩溃（kernel panic）或硬盘无法挂载。如果成功，它会创建一个作为`/init`运行的进程。如果出现问题，你会遇到内核崩溃或被掉入`root shell`。随后`init`进程会启动其他服务，并最终带你进入登录界面。

![](img/09c2db624d208d272aaec8e2a116126d_114_0.png)

```
GRUB version 2.02-ubuntu

GRUB menu for Ubuntu

Ubuntu

Advanced options for Ubuntu

Advanced options for Ubuntu 20.04.6 LTS (recovery mode)

Advanced options for Ubuntu 20.04.6 LTS (old kernel versions)
```
