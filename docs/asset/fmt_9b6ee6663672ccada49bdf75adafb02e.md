
`gdb vmlinux /dev/kmsg`

```
```

- **优点**：提供了交互式调试能力，可以设置断点、检查变量和单步执行代码。
- **缺点**：需要特殊的硬件或内核配置。

## 内核跟踪 (Ftrace)

`Ftrace` 是一个用于跟踪内核函数调用的强大工具。

```bash
echo function_graph > /sys/kernel/debug/tracing/events/function_graph/enable
```

- **优点**：提供了有关函数调用、参数和返回值的详细信息。
- **缺点**：会产生大量数据。

## 内存调试

- **`kmemleak`**：检测内核中的内存泄漏。

```bash
kmemleak
```

- **`slabtop`**：监控 `slab` 分配器（`slab allocator`）的使用情况。

```bash
slabtop
```

- **`valgrind`**：（针对用户态组件）检测内存泄漏和无效内存访问等内存错误。

```bash
valgrind --leak-check=full my_user_space_program
```

## 其他工具

- **`perf`**：衡量性能并识别瓶颈。
- **`trace`**：跟踪进程执行的系统调用（针对用户态组件）。
- **`gdb`**：（针对用户态组件）调试用户态应用程序。

# 调试技巧

- **可复现性**：尝试创建可复现的测试用例。
- **隔离**：将问题隔离到特定的代码段。
- **日志**：谨慎地使用 `printk` 记录相关信息。
- **内核配置**：在内核配置中启用调试选项。
- **符号信息**：确保为调试工具提供适当的符号信息。
- **代码审查**：同行评审可以帮助早期识别潜在问题。

示例：调试设备驱动程序崩溃

```cpp
static int my_device_open(struct inode inode, struct file file) // 设备打开逻辑

if (error) {
    printk(KERN_ERR "Error opening device: %d\n", error); return -ENODEV;
}

return 0;
```

如果驱动程序在 `my_device_open` 函数期间崩溃，你可以：

1. **使用 `dmesg` 检查内核日志**查找错误消息。
2. **使用 `printf`** 在崩溃前添加更多的调试信息。
3. **使用 `KGDB` 启用内核调试**以进行交互式调试。
4. **分析内核恐慌**以获取有关崩溃位置的线索。
5. **使用 `kmemleak` 检查内存泄漏**。

调试 Linux 设备驱动程序需要系统的方法和多种工具的结合。通过理解并有效应用这些技术，你可以高效地识别并修复问题，提高驱动程序的可靠性和性能。

# 第13章

## 使用 Printk 进行内核调试

### 理解 Printk

`printk` 是内核开发人员主要的调试工具。它类似于用户态中的 `printf`，但针对内核环境进行了一些关键区别。`printk` 消息通常被定向到内核日志，可以通过 `dmesg` 访问。

```cpp
Basic Printk Usage
#include <linux/kernel.h>

void my_function(int arg) {
    printk(KERN_INFO "My function called with arg: %d\n", arg);
}
```

- `KERN_INFO` 是一个日志级别。还有其他级别，如 `KERN_ERR`（错误）、`KERN_WARNING`（警告）、`KERN_DEBUG`（调试）等。
- 格式字符串和参数的作用与 `printf` 类似。
- `\n` 用于换行。

### 日志级别

`printk` 消息按日志级别分类。内核只会打印高于高于配置日志级别的消息。

```cpp
printk(KERN_EMERG "System unusable!");
printk(KERN_ALERT "Immediate action needed");
printk(KERN_CRIT "Critical conditions");
printk(KERN_ERR "Error conditions");
printk(KERN_WARNING "Warning conditions");
printk(KERN_NOTICE "Normal but significant condition");
printk(KERN_INFO "Informational message");
printk(KERN_DEBUG "Debug-level message");
```

### 条件 Printk

为了避免过度记录日志，你可以根据编译时或运行时的条件使用条件 `printk`。

```cpp
#ifdef DEBUG
printk(KERN_DEBUG "Debug message: %d\n", value);
#endif
```

## Printk 与设备驱动程序

`printk` 在设备驱动程序开发中是无价值的。它可以帮助诊断与设备初始化、数据传输和错误处理相关的问题。

```cpp
static int my_device_open(struct inode *inode, struct file *file) {
	printk(KERN_INFO "my_device_open called\n");
	// 设备打开逻辑
	return 0;
}

static int my_device_read(struct file *file, char *buf, size_t count, loff_t *offset) {
	printk(KERN_INFO "my_device_read called: %zu\n", count);
	// 设备读取逻辑
	return count;
}
```

### 高级 Printk 使用

- **文件和行**：使用 `__FILE__` 和 `__LINE__` 宏来识别日志生成的位置。
- **时间戳**：包含时间戳以跟踪事件的发展。

```cpp
printk(KERN_INFO "%s:%d: message\n", __FILE__, __LINE__);
```

### Printk 的局限性

- **性能开销**：过多的 `printk` 会影响性能。
- **日志缓冲区溢出**：内核日志的大小有限。
- **安全性影响**：在生产环境中不应记录敏感信息。

## 最佳实践

- 使用适当的日志级别以避免日志混乱。
- 消息要简洁。
- 调试后移除必要的 `printk` 语句。

# 不仅仅 Printk

虽然 `printk` 是一个重要的工具，但它通常与其他技术结合使用以采用全面的方法。

- **内核跟踪 (Ftrace)**：提供函数跟踪。
- **内核调试 (KGDB)**：内核的交互式调试。
- **性能分析工具 (perf)**：性能分析。

```cpp
static int my_device_open(struct inode *inode, struct file *file) {
    printk(KERN_INFO, "my_device_open called\n");
    // ... device open logic ...
    return 0;
}
```
