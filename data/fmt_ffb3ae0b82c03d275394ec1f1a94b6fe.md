
获取实际、有效和保存设置用户 ID。成功时返回 0，错误时返回 -1，`errno` 指出问题。

`getresgid(gid_t *rgid, gid_t *egid, gid_t *sgid)`

获取实际、有效和保存设置组 ID。成功时返回 0，错误时返回 -1，`errno` 指出问题。

`setresuid(uid_t ruid, uid_t euid, uid_t suid)`

分别设置实际、有效和保存设置用户 ID。当参数值为 -1 时，相应的 UID 不变。（然而，对 `ruid` 使用非值会导致永久丢失 root 权限）。否则，参数必须是当前的实际、有效或设置用户 ID 值。

`setresgid(gid_t rgid, gid_t egid, gid_t sgid)`

分别设置实际、有效和保存设置组 ID。当参数值为 -1 时，相应的 GID 不变。否则，参数必须是当前的实际、有效或设置组 ID 值。

这些函数特别有价值，因为它们的语义是明确定义的。

## 11.8 跨越安全雷区：Setuid

真正的雷区很难但并非无法跨越。然而，这不是一个在没有训练或经验的情况下轻率尝试的事情。

同样，编写以 `root` 运行的程序也是一项艰巨的任务。有许多需要注意的问题，几乎任何操作都可能产生意外的安全后果。这种尝试应该谨慎进行。

## 11.9 建议阅读

特别是，阅读关于 `Linux/Unix` 安全的问题并花时间学习如何编写 `setuid` 程序是非常值得的。如果你在读完这本书且没有阅读其他任何内容的情况下直接尝试这种挑战，请放心，你的系统将轻易且立即被攻破。你或你的客户可能都不会感到高兴。

以下是一些指导原则：

- 尽可能少使用 `root` 权限。谨慎使用你的“超能力”，只在绝对需要时才使用。

- 妥善设计你的程序。对程序进行模块化，使得所有的 `root` 操作都可以提前完成，程序的其余部分作为普通用户运行。

- 在更改或丢弃权限时，如果可以使用 `setresuid()`，请使用它。否则使用 `setuid()`，因为这两个的语义最清晰。只有当你想要让更改永久生效时才使用 `setuid()`。

- 按正确的顺序从 `root` 切换到普通用户：先设置组和 `GID` 值，然后设置 `UID` 值。

- 小心 `fork()` 和 `exec()`；除非你显式更改它们，否则真实的 `UID` 和有效 `UID` 不会在这些调用中发生改变。

- 考虑为你的应用程序使用 `setgid` 权限和特殊组。如果这行得通，它将为你节省很多麻烦。

- 考虑丢弃继承的环境变量。如果你必须保留某些环境变量，请尽可能少保留。确保为 `PATH` 和 `IFS` 环境变量提供合理的值。

- 避免使用 `execcl()` 和 `execve()`，它们取决于 `PATH` 环境变量的值（尽管如果你自己重置了 `PATH`，这个问题就没那么严重）。

这些只是在穿越一个充满陷阱、机关和地雷的区域时的众多策略中的几个。请下一节以获取其他信息来源的提示。

`Unix`（以及 `GNU/Linux`）安全是一个需要知识和经验才能正确处理的话题。在互联网时代，它变得越来越难，而不是变得更简单。

## 424 第11章 权限与用户和组 ID 数字

1. `Practical UNIX & Internet Security`, 第3版，Simson Garfinkel, Gene Spafford 和 Alan Schwartz 著，O'Reilly & Associates, Sebastopol, CA, USA, 2003. ISBN: 0-596-00323-4。

   这是关于 `Unix` 安全的标准书籍。

2. `Building Secure Software: How to Avoid Security Problems the Right Way`, John Viega 和 Gary McGraw 著。Addison-Wesley, Reading, Massachusetts, USA, 2001. ISBN: 0-201-72152-X。

   这是一本关于编写安全软件的好书，它包含了如何处理 `setuid` 问题。它假设你已经熟悉基本的 `Linux/Unix API`；当你读完我们的书时，应该准备好阅读它了。

3. “Setuid Demystified,” Hao Chen, David Wagner 和 Drew Dean 著。`Proceedings of the 11th USENIX Symposium`, 2002年8月5–9日。`http://www.cs.berkeley.edu/~daw/papers/setuid-unixid02.pdf`。

   Garfinkel, Spafford 和 Schwartz 建议在甚至考虑编写尝试保存和恢复权限的代码之前阅读这篇论文。我们非常同意他们的观点。

## 11.10 总结

- 使用用户和组 ID 值（`UID` 和 `GID`）来识别文件和进程，这使得 `Linux` 和 `Unix` 变成了多用户系统。进程同时带有真实和有效的 `UID` 以及 `GID` 值，以及一个补充组集。通常是有效 `UID` 决定一个进程如何影响另一个进程，并且在检查文件权限时检查的是有效 `UID`、`GID` 和组集。有效 `UID` 为零的（称为 `root` 或超级用户）被允许随心所欲操作；系统不会对他们进行权限检查。

- 保存的组用户 ID（saved set-user ID）和保存的组 ID（saved set-group ID）源自 `System V`，并已被 `POSIX` 采纳并在 `GNU/Linux` 中得到完全支持。拥有这些独立的 `UID` 值使得能够根据需要轻松且正确地交换真实和有效 `UID`（以及 `GID`）。

- `Setuid` 和 `setgid` 程序创建的有效 ID 和真实 ID 不同的进程。这些程序通过文件权限中的额外位标记为此类。必须在创建文件后向文件添加 `setuid` 和 `setgid` 位。

- `getuid()` 和 `getegid()` 分别获取真实和有效的 `UID` 值，`getgid()` 和 `getegid()` 分别获取真实和有效的 `GID` 值。`groups()` 在 `POSIX` 环境中获取组集，可以查询系统该组集包含多少成员。

- `access()` 函数以真实用户的身份进行文件权限检查，使得 `setuid` 程序能够检查用户的权限。注意，由于文件可能存在于非一致性或网络文件系统中，通常检查 `stat()` 获取的信息可能无法提供全貌。

- `GLIBC` 的 `euidaccess()` 函数与 `access()` 类似，但它是基于有效 `UID` 和 `GID` 值进行检查的。

- `setgid` 位和粘滞位（sticky bits）应用于目录时，会引入额外的语义。当目录设置了 `setgid` 位时，该目录中的新文件将继承目录的组。新目录也是如此，并且会自动继承 `setgid` 位的设置。如果没有 `setgid` 位，[它们将继承创建进程的组]。

- 组集通过 `setgroups()` 更改。虽然不是 `POSIX` 标准，但在所有现代系统中都存在。

- 当可用时应使用 `setresuid()` 和 `setresgid()` 函数，因为它们提供了最清晰、最可靠的行为。

- 编写 `setuid-root` 应用不是初者的工作。如果你需要这样做，请先阅读相关安全的内容。

## 练习题

1. 编写一个 `id` 命令的简单版本。它的功能是向标准输出打印带有组名的用户 ID 和组 ID。当有效 ID 和真实 ID 不同时，打印两者。例如：

```
$ id
uid=2076(arnold) gid=42(devel) groups=19(floppy),42(devel),2076(arnold)
```

带有用户参数时显示该用户的信息；否则，`id` 显示调用者的信息。用法如下：

```
id [ user ]
id -G [ -nr ] { user }
id -g [ -nr ] { user }
id -u [ -nr ] { user }
```

选项如下：

- 以数值格式打印所有组值。

- 仅打印名称，不带数值。适用于用户和组值。

- 仅打印有效 `GID`。

- 仅打印有效 `UID`。

2. 编写一个名为 `sum` 的 `setuid` 程序。它应该提示密码（参见 `getpass(3)`），对于本次练习，密码可以硬编码在程序源码中。如果运行程序的人正确输入密码，`sum` 应该执行 `shell`。找另一个用户帮助你测试。

3. 对于将 `sum` 提供给你的朋友？提供给你的同学或同事？提供给系统上的每个用户？你感觉如何？

第 6 章“通用库接口——部分 1”第 165 页介绍了第一组通用库 API。从某种意义上说，这些 API 支持对 `Linux` 和 `Unix` 系统管理的基础对象进行操作：日期时间、文件的用户和用户组，以及排序和搜索。

这一章的内容更加杂杂；这里涵盖的 API 之间并没有特别的联系。然而，它们对于日常的 `Linux/Unix` 编程来说都是非常有用的。你的介绍将从简单、更通用的 API 转向更复杂、更专门的 API。

## 12.1 断言语句：`assert()`
