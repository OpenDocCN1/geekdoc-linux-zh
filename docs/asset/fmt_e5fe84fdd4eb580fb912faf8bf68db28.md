
现在，让我们继续创建我们的虚拟分区。

## 创建虚拟分区的步骤

在本节中，我们将介绍创建虚拟分区的步骤。这些是第 1 步，是在处理 vPars 的某些非常早期的安装期间执行的。此列表应作为处理 vPars 的框架。您可能选择不执行某些步骤并添加其他步骤。这只是一个使 vPars 在您的系统上运行的框架。

在我们将要创建虚拟分区的示例中，我们将执行图 2-3 中所示的步骤。

1. 将 HP-UX 11i 加载到您希望运行虚拟分区的磁盘上*（介质或 Ignite/UX 服务器。）
2. 将虚拟分区软件加载到您希望运行虚拟分区的磁盘上。
3. 使用 `ioscan`、`dmesg` 和其他命令收集系统组件和硬件路径的信息。
4. 列出组成虚拟分区的组件。
5. 在所有将运行虚拟分区的卷上使用 `mk_kernel` 和 `knupdate` 构建新的 HP-UX 11i 内核*（自动完成，用于所有将运行 vPars 的 11i 实例。）
6. 使用 `vparcreate` 创建第一个虚拟分区。
7. 在 `MON>` 提示符下使用 `vparload` 启动第一个虚拟分区。使用 `vparstatus -v` 查看正在运行的 vPar，使用 `vparstatus -A` 查看可用组件。
8. 使用 `vparcreate` 创建第二个虚拟分区（也可以在启动任何 vPar 之前完成）。
9. 从第一个 vPar 使用 `vparboot` 启动第二个虚拟分区，并使用 `vparstatus` 监视其启动过程。启动后，使用 `vparstatus -A` 查看剩余的可用组件。
10. 根据需要，使用 `vparmodify` 修改虚拟分区，并使用 `vparstatus -v` 和 `vparstatus -A` 查看修改内容。修改可以是任何类型，例如添加 CPU、更改属性等。

### 其他任务和备注

- 可以执行许多其他任务。上述步骤中未使用命令 `vparremove` 和 `vparreset`。
- 典型的 vPar 组件列表如下所示：

```text
name          cabled
processors    min of 1 (bound) max of 3 (1 bound 2 unbound) with num equal to 1
memory        1024 MB
LAN           0/0/0/0 (not specified explicitly)
boot disk     0/0/1/1.2.0
kernel        /stand/vmunix
autoboot      off (manual)
console       0/0/4/0 (not specified explicitly)
```

* 必须在创建虚拟分区之前或之后将 HP-UX 11i 加载到卷上。如果在创建 vPar 之后加载 HP-UX 11i，则使用 `vparboot -p vp_name -i ignite_kernel` 来加载 11i。

![](img/eff8b9287a5f38c5adf538f24aacf29e_109_0.png)

### 1) 加载 HP-UX 11i

必须将 HP-UX 11i 加载到将用于托管所有 vPar&s 的卷上。您用于安装 11i 的方法，无论是介质、Ignite-UX 还是其他技术，只要 HP-UX 11i 存在于所有磁盘上都是可接受的。在您开始创建 vPar 之前，第一个磁盘上必须存在 HP-UX 11i。您可以在其他磁盘上创建 vPar&s，而在 HP-UX 11i 加载到它们之前，然后使用 `vparboot -p vp_name -i ignite.kernel` 在其他磁盘上启动并加载 HP-UX 11i。在本章中，我在创建 vPar&s 之前首先在 11i 上加载了 HP-UX 11i。第 1 章介绍了加载 HP-UX 11i 和 vPar&s 软件。在我们的即将推出的示例中，第一个虚拟分区将在 L-Class 系统的内部磁盘上创建。第二个虚拟分区将在外部磁盘上创建。在其中一个根卷上加载 HP-UX 11i 后，我发出了 `uname`，结果输出如下：

```bash
# uname -a
HP-UX cvhdccon3 B.11.11 U 9000/800 136414696 unlimited-user license
#
```

显示了主机名 *cvhdccon3* 和 HP-UX 修订版 *11.11*，这是撰写本文时可用的最新 HP-UX 11i。

处理 vPar&s 的一个有趣细节是主机和 vPar&s 的命名。第 1 章中有一个主机名部分，您可能需要重新阅读。简而言之，您在安装 11i 时提供主机名，在创建 vPar&s 时提供虚拟分区名称。如果 HP-UX 11i 实例的主机名和 vPar 名称相同，可以减少混淆。然而，在某些情况下，组织要求主机名符合导致名称难以记忆的约定。在这种情况下，一些系统管理员会选择一个容易记住的 vPar 名称。在即将到来的示例中，我们为 vPar&s 和主机名使用了不同的名称。

我们即将展示的示例的主机名为 *cvhdccon3* 和 *cvhdccon4*。使用的相应 vPar 名称为 *cable1* 和 *cable2*。

### 2) 加载虚拟分区应用软件

还必须将虚拟分区软件加载到将用于托管所有 vPars 的卷上。在撰写本文时，软件有 *base* 和 *full* 版本。*base* 软件的限制是最大两个 vPars，其中一个 vPar 中最大一个 CPU。在一个根卷上加载 vPars 软件后，我运行了 `swlist`，结果输出如下：

```bash
# swlist
# Initializing ...
# Contacting target "cvh3dcn3" ...
#
# Target:   cvh3dcn3 /
#
# Bundle(el):
#
BUNDLE11
usrv 2001 B.11.11.0202.2  Required  Exxct Bundle for HP-UX 11i. rev
C06-English B.11.11 English TCS Enforcement
FC01-00 B.11.11.01  PCI FDDISuppdrd Hw:A558A559A560A566
AA
FibrChannel-00 B.11.11.36  PCI/HSC FibreChannel/Suppdrd Hw:A56842,A56
85A.AD158A
GLGELther-00 B.11.11.14  PCI/HSC GigELther/Suppdrd Hw:A4926A/A4928A/
A4924A/A4925A/SW=31642A
HECX11-08-MC B.11.11.3136  HP-UX Mission Critical Operating Envirem
ent Component
HEXBase64 B.11.11  HP-UX 64-bit Base OS
HPUXBaseAux B.11.11.1500 HP-UX Base OS Auxiliary
HWEnableB11i B.11.11.324  Hardware Enablement Patches for HP-UX 11i
June 2001 B.11.11.05308 HPDX 11.11 Support Tools Bundle, Jun 2001
OnLineDiag
RAID-00 B.11.11.01  PCI RAID: Suppdrd Hw:A5856A
VPARSBASE A.03.05.01  HP-UX Virtual Partitions
```

*HP-UX Virtual Partitions* 软件是此列表中显示的最后一项。

## 使用 vPars 进行操作

在使用 vPars 时，您将深入了解您的硬件。您不仅需要知道系统由哪些组件构成，还需要知道许多硬件的路径。某些系统组件，如 `System Bus Adapters`（系统总线适配器）和 `memory controller`（内存控制器），在 vPars 之间是共享的，因此您不需要将这些组件作为各个虚拟分区的一部分进行指定。系统中的大多数其他组件，如处理器、I/O 卡、磁盘等，则固定分配到特定的 vPar 中。

为了查看示例系统由哪些组件组成，我们将在下面的列表中运行 `ioscan -f` 和 `dmesg`：

### ioscan -f 输出
