

## 7.3 z/VM的性能与监控工具

使用各种工具来监控和提升性能是非常普遍的做法。性能监控工具可提供更多有关z/VM系统状态的功能和报告。

在本节中，我们将介绍几种性能监控工具。更详细的信息，请参阅IBM红皮书《Linux on IBM System z: Performance Measurement and Tuning》，编号SG24-6926。

### 7.3.1 用于VM的IBM Performance Toolkit

IBM Performance Toolkit for VM是一款增强的实时性能监控器和全屏操作器，允许系统程序员监控系统性能并分析瓶颈。该工具包可帮助系统程序员更高效地利用系统资源、提高系统生产率并提升用户满意度。除了分析z/VM性能数据外，Performance Toolkit for VM还能处理从IBM资源测量设施（RMF）和Linux性能收集器rmfpm获取的Linux性能数据。Performance Toolkit for z/VM还提供其他几项功能，包括：

- 以全屏模式操作系统操作员控制台
- 管理多个z/VM系统（本地或远程）
- 对MONWRITE实用程序捕获的Performance Toolkit for VM监控数据进行后处理
- 通过Web浏览器或基于PC的3270仿真器图形查看性能监控数据
- TCP/IP性能报告

第339页上的图7-2展示了一个典型的Performance Toolkit窗口。

> 注意：有关Performance Toolkit的更多信息，请参阅《Linux on IBM eServer zSeries and S/390: Performance Toolkit for VM》，SG24-6059。

*图7-2 Performance Toolkit*

### 7.3.2 用于z/VM和Linux的Tivoli OMEGAMON

OMEGAMON®是一款用于VM（虚拟机）操作系统的实时软件性能监控器。它在会话监控系统（CMS）操作系统下运行。OMEGAMON会自动向您发出异常情况警告，并实时显示VM内部操作和资源的状态。

所有OMEGAMON特性和功能都围绕逻辑调优方法的概念而设计，以改善系统性能。逻辑调优方法包括以下步骤：

1. 在您的安装环境中定义VM性能的标准。

### 7.3.3 用于z/OS的IBM Tivoli Performance Modeler

现有的信息已不足以进行容量规划。可以使用IBM Tivoli Performance Modeler for z/OS V2.3对更改以下项目的影响进行建模：

- CPU的数量和速度
- 磁盘I/O响应时间
- 分页速率（辅助存储器和扩充存储器分页）
- 逻辑分区（LPAR）定义和参数变更

Tivoli Performance Modeler从z/OS映像获取输入，包括系统和应用程序性能数据，作为建模程序的基础。然后，用户可以更改处理器类型并调整工作负载配置，以创建新模型。然后，该建模器会生成一系列图形来描述所建模的工作负载。

### 7.3.4 用于IBM System z处理器上Linux客户机的IBM z/VM Planner

面向IBM System z处理器上的Linux客户机的z/VM Planner（简称z/VM Planner）是一款基于PC的生产力工具，在Microsoft Windows下运行。（IBM员工和经授权的IBM业务合作伙伴可以与其客户一起使用该工具。）它旨在为在VM下作为客户机运行各种Linux工作负载环境的IBM大型机处理器提供容量规划洞察。输入主要包括z/VM客户机定义以及每个预期Linux客户机的容量需求。总客户机容量需求基于客户机定义进行计算；同时，由于所有客户机可能不会同时达到峰值利用率，因此使用用户指定的互补峰值百分比来计算所评估的z/VM客户机的真实综合容量需求。该工具还模拟将新客户机合并到现有VM映像时的z/VM处理器需求。由此得出的客户机容量需求与VM的容量需求相结合，以支持全部客户机集合。

z/VM Planner会生成若干图形来描述所建模的系统。这些图形说明了支持所建模工作负载所需的处理器规模、工作负载中每个应用程序使用的处理器百分比，以及工作负载所需的最小和最大处理能力估算值。第342页上的图7-4表示一个所建模工作负载的最小和最大容量需求，该工作负载包含五个运行混合Web应用程序、数据库和文件服务器的Linux客户机。

