
# AIX 5L 中的新 ODM 类 (CuOD)

AIX 5L 引入了若干项需要新 ODM 控制的技术，因此 IBM 创建了一个新的 ODM 类 **CuOD**，即定制化按需（On-Demand）对象类。IBM 的新功能之一是动态 CPU 分配。**CuOD** 类允许你订购一台带有额外 CPU 容量的新 pSeries 机器，并且可以即时动态分配这些新 CPU。处理器通过目标系统的特征代码（FC）进行订购。基本上，你只是在订购一台带有额外 CPU 的系统，并具备在稍后日期激活这些额外 CPU 的能力，从而降低了前期成本，并且不会一次性将所有额外算力分配给用户和应用程序。那些按 CPU 时间收费的机构会喜欢这个功能。

同一技术理念的另一部分是动态 CPU 取消分配，它可以将故障 CPU 离线并停止服务，而不会导致系统宕机。内存技术，包括内存芯片保护（Memory ChipKill）、位散射（Bit Scattering）和位引导（Bit Steering），是内存子系统中类似 RAID 5 的技术的一部分。如果内存 DIMM 发生故障，系统将自动禁用对该芯片的访问，系统将继续运行。这是一个硬件特性，不属于 **CuOD** ODM 类。

既然提到了新事物，从 AIX 5L 版本 5.2 开始的逻辑分区（LPAR）允许你在单台机器内创建 1–16 个逻辑系统。这些逻辑系统分区对外部世界而言被视为独立系统，可以作为独立系统进行管理。IBM 允许你通过为逻辑系统指定确切的处理器数量和内存来创建这些 LPAR，并允许不同的操作系统（AIX 和 Linux）版本在同一台机器内运行。这对开发环境来说是一个惊人的突破工具！当他们需要一个沙盒来试验时，只需即时创建一个即可。

ODM 类 CuOD 负责使这些技术中的一部分得以工作的动态机制；当然，还需要 POWER 4 处理器。

> **注意：POWER 4 CPU 芯片实际上是单芯片上的双路 SMP，可以独立控制！**

## ODM 对象类的示例

一个特殊的对象类，预定义连接（**Pd**Cn），定义了设备类和子类的层级结构。设备属性作为独立的属性对象类维护。表 9-3 展示了 AIX 对象类的示例。

你可以使用 **odmshow** 命令显示对象类定义。

```
# odmshow <ObjectClassName>
```

表 9-4 到 9-7 代表了预定义和定制化的设备描述符及属性描述符，让你大致了解设备信息是如何表示和链接的。

### 表 9-3. AIX 对象类的示例

| 类对象 | 对象类内容 |
|---|---|
| PdDy | AIX 支持的预定义设备 |
| PdAt | 预定义设备属性 |
| PdCn | 预定义设备子类连接 |
| CuDy | 连接到系统的定制化设备 |
| CuDvDr | 定制化设备驱动 |
| CuAt | 定制化设备属性 |
| CuDep | 定制设备依赖项 |
| CuVPD | 定制化关键产品数据 |
| Config_Rules | 配置规则集 |

### 表 9-4. PdDv 描述符

| 描述符名称 | 描述符定义 |
|---|---|
| Type | 设备类型 |
| Class | 设备类 |
| Subclass | 设备子类 |
| Prefix | 前缀名称 |
| Devid | 设备 ID |
| Base | 基设备标志 |
| has_vpd | VPD 标志 |
| Detectable | 设备可检测标志 |
| Chgstatus | 变更状态标志 |
| bus_ext | 总线扩展器 |
| Fru | FRU 标志 |
| Led | LED 值 |
| Setno | 集编号 |
| Msgno | 消息编号 |
| Catalog | 目录编号 |
| DvDr | 设备驱动名称 |
| Define | 定义方法 |
| Configure | 配置方法 |
| Change | 变更方法 |
| Unconfigure | 取消配置方法 |
| Undefine | 取消定义方法 |
| Start | 启动方法 |
| Stop | 停止方法 |
| inventory_only | 仅清单标志 |
| Uniquetype | 唯一类型 |

### 表 9-5. PdAt 预定义属性描述符

| 描述符名称 | 描述符定义 |
|---|---|
| Uniquetype | 唯一类型 |
| Attribute | 属性名称 |
| Deftl | 默认值 |
| Values | 属性值 |
| Width | 宽度 |
| Type | 类型标志 |
| Generic | 通用标志 |
| Rep | 代表性标志 |
| nls_index | NLS 索引 |

### 表 9-6. (CuDv) 定制化设备描述符

| 描述符名称 | 描述符定义 |
| :--- | :--- |
| Name | 设备名称 |
| Status | 设备状态标志 |
| Cngstatus | 变更状态标志 |
| Dldins | 设备驱动实例 |
| Location | 位置代码 |
| Parent | 父设备 |
| Connwhere | 连接位置 |

### 表 9-7. (CuAt) 定制化属性描述符

| 描述符名称 | 描述符定义 |
| :--- | :--- |
| Name | 设备名称 |
| Attribute | 属性名称 |
| Value | 属性值 |
| Type | 属性类型 |
| Generic | 通用标志 |
| Rep | 代表性标志 |
| nls_index | NLS 索引 |

## 设备状态

**cfgmgr** 例程负责使用配置规则集更新定制化设备信息。**cfgmgr** 调用每个连接设备指定的方法并更新设备状态。设备方法完成后，设备被设置为三种状态之一：已定义、已停止或可用，如表 9-8 所示。

## 启动设备

代表设备配置信息的小型 ODM 数据库作为 AIX 启动镜像的一部分维护。可以使用 **savebase** 命令从主 ODM 数据库更新此信息。同样，可以通过调用 **restbase** 命令将启动镜像中的 ODM 信息恢复到主 ODM 数据库（参见第 7 章）。

```
# savebase     将主 ODM 定制化设备数据保存到启动镜像
# restbase     将定制化 ODM 数据从启动镜像恢复到主 ODM 数据库
```

[PAGE 170 内容如下]

### 表 9-1. ODM 命令和库子程序

| 库例程 | 命令 | 用途 |
| --- | --- | --- |
| odm.set_path | | 设置 ODM 数据库位置（ODMDIR 代表 shell 环境变量） |
| | RESTBASE | 从启动镜像检索定制对象并存储到 ODM |
| | SAVEBASE | 将 ODM 定制对象存储到启动镜像 |
| odm.rm_class | ODMDROP | 移除一个对象类 |
| | ODMSHOW | 显示对象类定义 |
| odm.create_class | ODMCREATE | 创建空的对象类，并为应用程序关联 C 头文件 |
| odm.add_obj | ODMADD | 向对象类添加一个对象 |
| odm.change_obj | ODMCHANGE | 修改对象属性 |
| odm.rm_obj | ODMDELETE | 从对象类中删除对象 |
| odm.get_obj | ODMGET | 以 odmdat 格式检索对象 |
| odm.get_by_id | | 通过其 ID 检索对象 |
| odm.rm_by_id | | 通过其 ID 移除对象 |
| odm.get_first | | 检索符合标准的第一个对象 |
| odm.get_next | | 检索符合标准的下一个对象 |
| odm.get_list | | 检索符合标准的对象列表 |
| odm.mount_class | | 检索类符号结构 |
| odm.open_class | | 打开一个对象类 |
| odm.free_list | | 释放分配给 odm.get_list 的内存 |
| odm.run_method | | 执行与对象关联的方法 |
| odm.close_class | | 关闭对象类 |
| odm.err_msg | | 检索错误消息字符串 |
| odm.lock | | 锁定对象以进行更新 |
| odm.unlock | | 解除对象锁定 |
| odm.initialize | | 初始化 ODM 会话 |
| odm.terminate | | 终止 ODM 会话 |

### 表 9-2. 最常用的 ODM 命令

| 命令 | 操作 |
| --- | --- |
| # smitty devices | SMIT 快速路径 |
| # mkdev -I tty 0 | 添加 TTY 设备 |
| # lsdv -C -s ascii -H | 列出现有 SCSI 设备 |
| # chdev -l rmt 0 -a block_size = 0 | 更改磁带块大小 |
| # leattr -D -l rmt 0 | 列出磁带属性 |
| # rmdev -I rmt 0 | 关闭磁带设备但保留定义 |
| # rmdev -l rmt 0 -d | 移除磁带设备 |
| # cfcmgr | 更新 ODM 和内核 |

适用于 AIX 支持的所有设备。定制化对象类代表系统中实际存在的设备。

```json
/etc/objrepos/Pdbxx ODM 预定义属性、连接和设备：
```

| PdBt | PDCn | PDCv |
|---|---|---|

| /etc/objrepos/Cuxxx | ODM 定制化属性、依赖项、设备驱动和关键产品数据： | |

| CuAt | CuDP | CuDv | CuDvDr | CuVPD | Config_Rules | CuOD (5L 新增) | |

| /usr/share/lib/objrepos | 软件关键产品数据 (SWVPD) 的组件 | |

| lpp | history | inventory | product | |

设备对象类层次结构链接到子类。例如，7207 和 3590 磁带设备代表 **tape** 对象类下的子类。**tape** 对象类反过来是 **SCSI** 对象类的子类。此层级强制配置关系。

- 必须配置父对象类信息后才能配置子子类。
- 如果存在子子类，则不能修改父对象类信息。
- 如果存在子子类，则不能移除父对象类。


