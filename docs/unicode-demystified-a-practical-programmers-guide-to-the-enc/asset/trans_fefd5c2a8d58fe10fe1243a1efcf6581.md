

# 练习

- 1. 每一个 C 程序都具有什么函数？为什么你应该将大型程序拆分成几个函数？

- 2. 你可以使用什么命令将 `prog.c` 和 `func.c` 编译成可执行文件 `cprog`？

- 3. 展示两种指示 C 预处理器在你的 C 程序中包含头文件 `/usr/include/math.h` 的方法。假设 `declare.h` 头文件位于你家目录下名为 `headers` 的子目录中，请描述两种指示 C 预处理器在你的 C 程序中包含该头文件的方法。

- 4. `getchar` 和 `putchar` 两个都出现在标准 C 库 `libc.so` 中。证明 `getchar` 和 `putchar` 在你的系统上也是宏。你能想到比一种更多的方法来证明这一点吗？

- 5. `gcc` 命令行是如何缩写系统库名称的？`gcc` 在哪里搜索此类命名的库？描述如何在 `gcc` 命令行中指定你自己的库。

- 6. 你可以使用什么命令为名为 `answers` 的文件创建一个 RCS 文件？可以使用什么命令检索 `answers` 的可编辑版本？

- 7. 编写一个 Makefile，反映以下关系：

  a. C 源文件 `transactions.c` 和 `reports.c` 编译生成可执行文件 `accts`。

  b. `transactions.c` 和 `reports.c` 都包含头文件 `accts.h`。

  c. 头文件 `accts.h` 由另外两个头文件组成：`trans.h` 和 `reps.h`。

- 8. 你如何检索 RCS 工作文件 `answers` 以：

  a. 只有 Barbara 和 hls 可以进行更改？
  b. 除了所有者和超级用户（Superuser），没有人可以修改 Release 2？

- 9. 如果你检索 `answers` 文件的第 4.1 版本进行编辑，然后尝试再次检索同一个版本，RCS 会做什么？为什么 RCS 要这样设置？

- 10. 为 CVS 回答练习 9 中的问题。

# 高级练习

- 11. 哪些 RCS 命令可以修改访问列表？解释如何确保只有文件所有者或超级用户才能检出（check out）一个锁定的 RCS 文件修订版本。

- 12. 修改 `tabs.c` 程序使其干净地退出（带有特定的返回值）。编译该程序，并使用 `dbx` 或另一个调试器运行它。当程序执行完毕时，调试器报告了哪些值？

- 13. 对于以下 makefile，识别出：

  a. 目标（Targets）
  b. 构建命令（Construction commands）
  c. 依赖项（Prerequisites）

```
$ cat Makefile
leads: menu.o users.o resellers.o prospects.o
	gcc -o leads menu.o users.o resellers.o prospects.o

menu.o: menu.h dialog.h inquiry.h

users.o: menu.h dialog.h

spects.o: dialog.h
```

- 14. 参考练习 13 中的 Makefile 回答以下问题：

  a. 如果目标 `leads` 是最新的，而你随后更改了 `users.c`，再次运行 `make` 时会发生什么？请具体说明。

  b. 重写 Makefile 以包含以下宏：

```
OBJECTS = menu.o users.o resellers.o prospects.o
HFILES = menu.h dialog.h
```

- 15. 阅读第三部分第 1247 页关于 make 的内容以及 man 手页，回答以下问题：

  a. `-t` 选项的作用是什么？

  b. 如果你在工作目录中有名为 `make` 和 `Makefile` 的文件，你如何指示 `make` 使用 `Makefile`？

  c. 给出两种定义变量的方法，以便在 makefile 中使用它。

- 16. 假设名为 `synchr.c` 的文件有四个从 1.1 到 1.4 的修订版本。展示如何：

  a. 检出最新的修订版本进行编辑。
  b. 仅检出最新的修订版本进行编译。
  c. 提交（check in）最新的修订版本。
  d. 检出版本 1.2。
  e. 删除修订版本。

- 17. 阅读关于 RCS 的内容并回答以下问题：

  a. 如何为修订版本分配符号名称？
  b. 如何创建一个分支（branch）？
  c. 当你尝试提交一个更新的修订版本时会发生什么？
  d. 如何让系统保持更新？

- 18. 参考第 853 页关于 makefile 的讨论，当工作目录中有名为 `make` 和 `Makefile` 的文件时，RCS 会：

```
make.h
```

  a. 这种方法可以备份数据。
  b. 这种方法可以删除修订版本。

# 本章内容

- 系统管理员 896
- 安装 Red Hat Linux 896
- 安装和删除软件 926
- 保持系统更新 933
- 系统操作 942
- GUI 系统管理 985
- 配置用户和组 992
- 备份数据 997
- 配置网络服务 1005
- 重建 Linux 内核 1031
- PAM 1043
- 管理工具 1045
- 管理任务 1055
- 获取帮助 1075

# Red Hat 系统管理

系统管理员的工作是让系统变得有用且方便。一个维护良好的系统：

- 运行足够快，使用户不需要等待。
- 有足够的存储空间来适应用户的需求。
- 提供适合用户的环境。
- 免受恶意或意外行为对性能或数据的影响。
- 定期进行备份。
- 拥有用户所需的最新软件。
- 比维护糟糕的系统更容易管理。

此外，系统管理员应该帮助用户解决各种类型的问题：从登录、获取和安装软件，到排查模糊的网络问题。

本章让你熟悉理解所需的概念以及维护系统所需的工具。在无法深入探讨某些主题时，本章提供了其他来源。

GNU/Linux 系统越来越容易设置和维护。如果你没有运行安装好的 Red Hat Linux 并需要安装，过程比以前简单得多。Red Hat 做了很多工作来简化安装。Red Hat 开发的一个工具是 `rpm`（Red Hat 软件包管理器），它使得安装/升级系统和应用程序变得容易得多。由于遵循 GNU GPL（第 7 页），rpm 被 Red Hat 之外的工程师进行了改进，并出现在其他 GNU/Linux 发行中。一个较新的开发是 RHN（Red Hat Network），它允许在极少或无交互的情况下保持系统更新¹通过 Kickstart 配置器，你可以设计一个简单的脚本，以便在多台机器上安装相同的 Red Hat Linux 配置。最后，所有这些工具以及其他管理工具都有 GUI 版本，使得每个工具都更易设置和使用。

¹ 此服务可能产生费用。

