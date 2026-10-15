
## 6.4 链接器

第 3 章包含了关于在 Linux 上使用导出映射的更多信息。

### 6.4.2 链接器工具

某些应用程序 Makefile 使用了 HP-UX 中存在的链接器工具。这些工具用于检查对象文件并对其进行操作，以便在 HP-UX 上创建最终的对象文件或可执行文件。表 6-9 比较了其他 HP-UX 链接器工具及其在 Linux 上的等效工具。

表 6-9
HP-UX 与 Linux 链接器工具对比表

| HP-UX 工具 | Linux 等效 | 描述 |
|---|---|---|
| chatr | 无 | 显示或修改对象文件的内部属性。 |
| elfdump | objdump | 显示 ELF 对象文件的内容。 |
| fastbind | 无 | 提高使用共享库程序的启动时间。 |
| ldd | ldd | 列出可执行文件和共享库的动态依赖。 |
| lorder | 无 | 查找对象库的排序关系。 |
| nm | nm | 显示对象文件的符号表。 |
| objdump | objdump | 显示 32 位原生代码对象文件的内容（HP-UX）。 |
| size | size | 打印对象文件元素的大小。 |
| strip | strip | 从对象文件、可执行文件或存档库中剥离符号和调试信息。 |

参见第 2 章获取更多关于 GNU binutils 的信息。

## 6.5 库的版本控制

如果待迁移应用程序的架构需要库的版本控制支持，则需要一些迁移工作将应用程序转换为使用 Linux 的库版本控制实现。

### 6.5.1 HP-UX 上的库版本控制

HP-UX 开发环境通过使用 `+h` 链接器 (`ld`) 选项提供了库的版本控制支持。例如，有一个名为 `libmyown` 的库。要为 `libmyown` 创建版本 0 库，命令行如下所示：

```bash
$ ld -b *.o -o libmyown.0 +h libmyown.0
```

生成的库 `libmyown.0` 通过 `+h` 标志及其参数表示，其内部名称为 `libmyown.0`。在生成共享库 `libmyown.0` 后，它就可以放入其目标目录了——在这种情况下，假设 `/tmp` 是目标目录。要将库安装到 `/tmp`，将 `libmyown.0` 拷贝到 `/tmp`，并使用 `ln` 命令将其链接到文件 `libmyown.sl`：

```bash
$ ln -s libmyown.0 libmyown.sl
```

```bash
$ ls -l libmyown.sl
```

```
$ libmyown.sl -> libmyown.0
```
