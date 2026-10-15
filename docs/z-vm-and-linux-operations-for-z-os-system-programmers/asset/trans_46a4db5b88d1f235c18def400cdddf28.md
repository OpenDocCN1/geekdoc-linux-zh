

![](img/b0a4b9056f819dccd4781a5105c92d45_357_0.png)

图 7-4 面向 Linux 客户机的 IBM z/VM Planner

## 7.3.5 Tivoli Workload Scheduling Suite

Tivoli Workload Scheduling Suite 是一套最先进的生产工作负载管理器，旨在帮助您应对当前和未来的数据处理挑战。它的范围涵盖您的整个企业信息系统，包括异构环境。

Tivoli Workload Scheduling Suite 通过集成系统管理功能，简化了异构环境中的系统管理。该套件的三个主要组件是：

- Tivoli Workload Scheduler for z/OS：z/OS 环境中的调度程序
- Tivoli Workload Scheduler：分布式环境中的调度程序
- Tivoli Job Scheduling Console：面向 Tivoli Workload Scheduler for z/OS 和 Tivoli Workload Scheduler 的通用用户界面

> 注：有关 Tivoli Workload Scheduling Suite 的更多信息，请参阅：
> http://publib.boulder.ibm.com/infocenter/tivihelp/v3r1/index.jsp?toc=/com.ibm.tivoli.itws.doc/toc.xml

### Linux 客户机的容量规划注意事项

Linux 内存模型对运行在 z/VM 下的 Linux 客户机有着深远的影响：

- z/VM 内存是一种共享资源。尽管激进缓存会降低磁盘 I/O 的可能性并有利于内存访问，但必须考虑缓存成本。Linux 客户机中的缓存页面会减少可供其他 z/VM 客户机使用的 z/VM 页面数。
- 更大的虚拟内存地址空间需要更多 Linux 内核内存来进行 Linux 内存管理。在为 Linux 客户机确定内存需求时，请选择对该客户机性能影响最小的最小内存占用。为了减少较小虚拟机中可能发生的偶发交换带来的性能损失，请使用快速交换设备。

尽管 512 MB 服务器并不需要那么多内存，但最终它看起来会将其全部用完。其内存成本是 128 MB 服务器的四倍。

> 注：更多信息可在 z/VM 网站上的 Performance Report 中找到：
> http://www.ibm.com/servers/eserver/zseries/zvm/perf/docs/
>
> 其他 z/VM 性能技巧可在 z/VM 网站上获取：
> http://www.ibm.com/servers/eserver/zseries/zvm/perf/tips/

## 7.3.6 为 z/VM Linux 客户机调优内存

存储调优在虚拟化环境中非常有用，尤其是在虚拟机监控程序能够超量分配资源的情况下。z/VM 是现存功能最强大的软件虚拟机监控程序操作系统。为了获得最佳的整体系统性能，建议在所有关键资源领域（如内存）进行微调。

为了最大程度地减少系统开销并降低其占用空间，缩小实际运行的机器规模通常很有帮助。可以通过多种方式减少服务器的内存占用。一种常见且直观的方法是终止不必要的进程。您还可以通过将虚拟机大小缩减到尽可能小的尺寸来调优 z/VM 内存使用量。最佳的最小尺寸可能需要多次尝试和实验。

> 注：有关 Linux 虚拟内存容量规划的更多信息，请参阅 Linux on IBM System z: Performance Measurement and Tuning, SG24-6926。

将较大的服务器划分为多个更小、更专用的服务器，可以证明是有效的。较小的服务器可以针对特定操作进行定制。但这是有代价的，因为每台服务器都需要一定内存来运行自己的操作系统。

使用带 DIAGNOSE 访问方法的 VDISK 作为交换设备，可以减少交换带来的性能损失。此建议仅适用于您在 System z 上有大量真实内存可用的情况。使用虚拟磁盘进行交换可以减少真实设备上由交换产生的 I/O，但同时会增加使用的存储总量。当 Linux 和 z/VM 产生高换页率时，这一技巧很有用。在这种情况下，可能会遇到双分页（z/VM 将已被 Linux 换出的客户机存储再次换出）的影响，而使用 VDISK 作为交换设备有助于减少这种影响。

使用 DIAGNOSE 驱动程序进行 DASD 和 MDC 记录缓存，以降低基础设施存储成本。使用记录级小型磁盘（minidisk）缓存可减少 MDC 所需的存储量。这需要 DIAGNOSE 驱动程序。

> 注：更多信息请参阅 IBM Linux on System z: Device Drivers, Features, and Commands, SC33-8289。

如果您在 z/VM 下运行 Linux，可以利用协作内存管理 1（CMM1）功能，在客户机之间实现更好的存储分配。

另一种减少内存使用的方法是使用共享内核或就地执行（execute-in-place）技术。这些新技术可用于减少管理 Linux 实例所需的总存储量。

## 7.3.7 就地执行技术

您可以使用不连续保存段（DCSS）来最小化虚拟 Linux 的内存需求并提高其性能。在虚拟化环境中，多个 Linux 映像可能在同一时刻需要相同的数据。这意味着相同的数据可能会多次加载到内存中。其中的很大一部分

