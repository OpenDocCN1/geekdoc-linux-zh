
![](img/739a35b59067f8a55eff80a58765146f_76_0.png)

### 4. 关闭通过交叉编译器提供的默认搜索路径。索引器应该使用内核头文件，而不是工具链 sysroot 中的文件：

![](img/739a35b59067f8a55eff80a58765146f_77_0.png)

### 5. 必须添加内核包含路径。内核不使用任何外部库：

![](img/739a35b59067f8a55eff80a58765146f_77_1.png)

包含文件位于：

- `/my-linux-imx/include`：通用的
- `/my-linux-imx/arch/arm/include`：架构特定的
- `/my-linux-imx/arch/arm/mach-<MACH>/include`：特定于变体，处理底层初始化代码时需要

### 6. 添加 `__KERNEL__` 符号（注意：两个下划线 KERNEL 两个下划线）。它用于许多许多区分包含用户空间 API（未定义）和内核 API（已定义）的文件部分。该符号在编译期间在 Makefile 中设置。

### 7. `arch` 目录包含特定于架构的文件。必须定义过滤器以排除所有包含当前配置中未用架构代码的子目录。选择 `arch/` 下的所有子目录，但排除 `arch/arm`：

![](img/739a35b59067f8a55eff80a58765146f_79_0.png)

同时也过滤掉 `tools` 目录。它包含了冲突的头文件。

## 8. 关闭未包含在构建中的文件索引。这将限制索引的文件数量：

| 资源 | | | |
| :--- | :--- | :--- | :--- |
| Builders | 启用项目特定设置 | 将设置与项目一起存储 | |
| C/C++ Build | Indexer | | |
| C/C++ General | index-opt-ms | 索引未包含在构建中的源文件 |
| Code Analysis | 索引未使用的头文件 | | |
| Documentation | 索引所有头文件变体 | | |
| File Types | 索引特定头文件的所有变体： | | |
| Format | 索引编辑器中打开的源文件和头文件 | | |
| Index | 允许包含的启发式解析 | | |
| Language Mappings | 跳过大于：8 MB 的文件 | | |
| Paths and Symbols | 跳过大于：16 MB 的包含文件 | | |
| Preprocessor Include Path | 跳过所有引用（调用层级和搜索将无法工作） | | |
| Profiling Categories | 跳过类型和宏引用（搜索这些引用将无法工作） | | |
| Link Tool | 索引器的构建配置 | | |
| Project References | 使用活动构建配置 | | |
| Run/Debug Settings | 使用固定的构建配置 | | |

## 9. 设置构建内核所需的参数：

![](img/739a35b59067f8a55eff80a58765146f_81_0.png)

## 10. 使用子页面 `Environment` 设置正确的路径。这样你每次打开 eclipse 就不需要重新加载环境了。点击变量 `PATH`（确保它已高亮）：

![](img/739a35b59067f8a55eff80a58765146f_82_0.png)

### 11. 在设置窗口中点击 OK 保存项目选项并运行索引器。为了确保每个项目都被正确索引，请强制重新构建。这可以通过项目管理器右键菜单完成。

`Project->Properties->Index->Rebuild`

索引将需要几分钟。工作空间目录将创建约 700-800MB 的数据。将解析约 20000 个文件（取决于内核版本）。

如果项目在配置了 Eclipse，它应该展开光标下的符号。这种配置并不理想。某些宏和符号被标记为警告或错误。Eclipse 索引器的行为与 GCC 不相同。我们的目标是让内核源码开发工作变得更容易，而不是消除所有警告。

## 构建系统

### 12. 现在可以使用 Eclipse 来构建内核。注意控制台中打印出的消息：

![](img/739a35b59067f8a55eff80a58765146f_83_0.png)

如果你更改了任何 `CONFIG_*` 设置，为了让 Eclipse 识别这些更改，你可能需要在 Eclipse 内部执行一次“build”。注意，这并不是重新构建索引；而是通过让 Eclipse 调用 `make` 来构建内核（这通常绑定到 Eclipse 中的 Ctrl-B 键）。Eclipse 应该会自动检测到对 `include/generated/autoconf.h` 的更改，重新读取它使用的编译 `#defines` 并重新索引。

## 开发 Linux 驱动程序的 Eclipse 配置

你将在 Eclipse 中创建一个项目，用于编写、构建和部署你的驱动程序。配置看起来与内核源码的情况相同。

### 1. 创建一个新的 Makefile C 项目。指向你存储驱动程序源码的位置。在下一个图中你可以看到路径为 `/home/alberto/Linux_3.14_drivers`。按照下述步骤进行操作：

- `File->New->C Project`。
- 设置项目名称（仅供 Eclipse 使用）。
- 不要使用默认位置（workspace）。指向包含内核模块源码的目录。
- 内核使用 `make` 构建，因此选择 `Makefile`。
- 使用交叉工具链。

## C 项目

指定名称的目录已存在。

![](img/739a35b59067f8a55eff80a58765146f_84_0.png)

创建项目后，修改其设置。进入 `Project->Properties`。

### 2. 需要让索引器了解内核配置。你必须从内核项目中包含 `autoconf.h`。添加工作区路径

## 构建系统

`/my-kernel/include/generated/autoconf.h` 以及 `printk.h`：

![](img/739a35b59067f8a55eff80a58765146f_85_0.png)

### 3. 关闭对工具链内置包含路径的搜索并设置工具链。你必须从内核项目中包含 `autoconf.h`。添加工作区路径

## 构建系统

`/my-kernel/include/generated/autoconf.h` 以及 `printk.h`：

*(注：此处后续文本在原文中重复，已根据要求不进行重复输出，仅保留翻译核心逻辑内容)*

# Linux 设备与驱动模型

- `bus`（总线）：作为其他设备挂载点的设备。

设备模型围绕三个主要数据结构组织：

- 1. `struct bus_type` 结构体，代表一种总线（例如：USB、PCI、I2C）。
- 2. `struct device_driver` 结构体，代表一个能够处理特定总线上的某些设备的驱动程序。
- 3. `struct device` 结构体，代表一个连接到总线上的设备。

Linux 设备和驱动模型代码被分为几个部分：

- 1. 总线驱动程序（核心）。
- 2. 总线控制器驱动程序。
- 3. 设备驱动程序（连接到总线）。

# 总线驱动程序 (Bus Drivers)

对于内核支持的每种总线，都有通用的总线驱动程序。总线是处理器与一个或多个设备之间的通道。对于设备模型而言，所有设备都通过总线连接，即使它是一个内部的、虚拟的、“平台”总线。

设备驱动程序分配一个 `struct bus_type` 结构体并将其注册到内核的总线类型列表中。`struct bus_type` 结构体（Linux/include/linux/device.h）代表一种总线（USB、PCI、I2C 等）。在系统中注册总线是使用 `bus_register()` 完成的。`struct bus_type` 定义如下：
