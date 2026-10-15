

DR DOS 7 或许比 MS-DOS 更好：它的内存需求更轻，支持多任务，并且有一个不错的配置程序。如果你认真使用 DOS，我建议你去研究一下。

> 一些 VMware 用户报告称使用 IBM 的 PC DOS 2000 成功了，可直接从 http://www.ibm.com 在线购买。

## 安装 DOS 核心

如果你有一套原版（非“升级版”）MS-DOS 磁盘，开始操作就和插入磁盘 1 然后开始安装一样简单。升级版要求在磁盘上先安装操作系统才能工作；你需要在开始升级前找到某种方法（可能使用 Windows 虚拟机并将虚拟磁盘挂载为次要驱动器）先在虚拟磁盘上安装一个初步版本。

一些较旧的 DOS CD-ROM 发行版（例如随零售 PC 提供的）可能无法从 CD-ROM 启动以开始安装过程。你可能需要使用提供 CD-ROM 支持的启动盘，例如随 Windows 95 和 98 提供的启动盘。

由于 DOS 版本差异很大，没有单一的“权威”安装方法。由于 MS-DOS 通常很熟悉且易于理解，我将逐步介绍并演示从 CD-ROM 安装 DR DOS 7。你可能必须根据最终使用的 DOS 版本和发行版自行寻找方法：

- 1. 在插入 DR DOS 7 CD-ROM 的情况下启动虚拟机。
- 2. 在到达 DOS 提示符之前你应该会看到错误消息，因为目前还没有可用的硬盘。你需要对虚拟磁盘进行分区和格式化。运行 fdisk。
- 3. 你应该会看到提示初始化磁盘。回答 Yes。
- 4. 在图 14.3 所示的屏幕中选择选项 4，Select alternate fixed disk。
- 5. 选择选项 1，Create Partition。创建 DOS 主分区，并让 fdisk 使用所有可用空间。

> DR DOS 的 fdisk 坚持验证所有磁盘块，这很耗时。它会在过程中自动格式化磁盘，这很方便。

![](img/b2b6702758c230ce537468351fc8af15_294_0.png)

图 14.3 DR DOS 使用了不寻常版本的 fdisk。

- 6. 完成后退出 fdisk 并重置虚拟机。保持 CD-ROM 在驱动器中。
- 7. 安装过程开始，如图 14.4 所示。
- 8. 选择 Continue with installation。
- 9. 阅读然后接受 DR DOS 许可协议。
- 10. 输入你的姓名、组织和序列号（如适用）。
- 11. DR DOS 7 的某些版本附带 Novell NetWare 就绪的网络系统。它占用空间很小。你应该接受图 14.5 所示屏幕上的默认值并继续。

![](img/b2b6702758c230ce537468351fc8af15_294_1.png)

图 14.4 DR DOS 使用伪图形安装界面。

![](img/b2b6702758c230ce537468351fc8af15_295_0.png)

图 14.5 DOS 可以小到令人惊讶。

- 12. 在下一个屏幕（见图 14.6）中，选择 DOS System & Memory Management，Memory Manager。关闭 i386/486/586 Memory Manager 并打开 80286 Memory Manager。

![](img/b2b6702758c230ce537468351fc8af15_295_1.png)

> 在任何情况下都不要让 DOS 内存管理器配置 EMS 内存。在 MS-DOS 中，性能不可预测，而 DR DOS 在 VMware 中运行 EMM386 时可能会直接崩溃。

![](img/b2b6702758c230ce537468351fc8af15_295_2.png)

图 14.6 只有 80286 内存管理器与 VMware 兼容。

- 13. 从 DOS System & Memory Management 菜单中，选择 Optional DOS Drivers and Utilities（见图 14.7），并打开 ANSI.SYS。

![](img/b2b6702758c230ce537468351fc8af15_296_0.png)

图 14.7 启用 ANSI.SYS 以获得 DOS 中的颜色支持。

- 14. 从图 14.8 所示的主配置菜单中，选择 Disk Performance，并关闭 NWCACHE Disk Cache。由于 Linux 已经进行磁盘缓存，安装此项只会浪费内存。

![](img/b2b6702758c230ce537468351fc8af15_296_1.png)

图 14.8

