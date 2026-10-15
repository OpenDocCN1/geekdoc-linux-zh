
# 第 13 章 • 静态库与共享库 251

## 列表 13.3 import.cc—保护成员 `Passwd::_import()` 和 `Passwd::_dispose()` 方法的实现

```cpp
// import.cc

#include "passwd.h"
#include <string.h>

extern "C" char *strdup(const char *str);
// 处理对象的内容（如果有）
// 1. 检查状态（如果已定义）
// 2. 删除所有分配的字符串
// 3. 将状态设为“未定义”

void
Passwd::_dispose() {
  if (state == defined) {
    delete pw_name; pw_name = 0;
    delete pw_passwd; pw_passwd = 0;
    delete pw_gecos; pw_gecos = 0;
    delete pw_dir; pw_dir = 0;
    delete pw_shell; pw_shell = 0;
  }
  state = undefined;
}
// 将一个结构体导入此对象
// 1. 处理当前内容
// 2. 复制并 strdup(3) 成员组件
// 3. 将状态设为“已定义”

void
Passwd::_import(passwd *pw) {

  if (state == defined) {
    _dispose(); // 处理现有内容

    pw_name = strdup(pw->pw_name);
    pw_passwd = strdup(pw->pw_passwd);
    pw_uid = pw->pw_uid;
    pw_gid = pw->pw_gid;
    pw_gecos = strdup(pw->pw_gecos);
    pw_dir = strdup(pw->pw_dir);
    pw_shell = strdup(pw->pw_shell);

    state = defined; // 设置为已定义状态
  }

// import.cc 结束
```

为了测试列表 13.1 到 13.3 中实现的 `Passwd` 类，列表 13.4 提供了一个 `main()` 程序。

## 列表 13.4 main.cc—用于 Passwd 类的 main() 测试程序

```cpp
// main.cc

#include <iostream.h>
#include <string.h>
#include <passwd.h>

int
  main(int argc, char **argv) {
  unsigned ux;
  Passwd pw;
  const char *accts[] = { "uucp", "xyzy", "games" };

  (void) argc;
  (void) argv;

  // report root 的主目录：

  try {
    pw.getuid(0);      // 查找 root
    cout << "Root's home dir is " << pw.pw_dir << "\n";
  } catch (int e) {
    cerr << strerror(e) << ": looking up uid(ux)" << "\n";
  }


  // 尝试几个账户

  for (int ux=0; ux<sizeof accts/sizeof accts[0]; ++ux) {
    pw.getnam(accts[ux]); // 查找账户
    cout << "Account " << accts[ux] << " uses the shell " << pw.pw_shell << "\n";
  }
  } catch (int e) {
    cerr << strerror(e) << ": looking up account "
    << accts[ux] << "\n";
  }

  return 0;
}
```

`main()` 程序在列表 13.4 的第 10 行初始化 `Passwd` 类。第一个测试（18–23）简单地查找 root 的主目录并报告（第 20 行）。

第二组测试在第 27–31 行的 `for` 循环中执行。该循环查找 `uucp`、`xyzy` 和 `games` 账户名。如果账户存在，则列出每个程序。预计大多数系统上不存在 `xyzy` 账户，它是作为对象 `pw` 抛出错误异常的测试。

# 第 13 章 • 静态库与共享库 253

`getuid` 的结果以及运行此测试的结果应该类似于：

```bash
$ make
cc -c -D_POSIX_SOURCE=19939 -D_POSIX_SOURCE -Wall -handle-exceptions import.cc
cc -c -D_POSIX_SOURCE=19939 -D_POSIX_SOURCE -Wall -handle-exceptions getuid.cc
ar -r passwd.a getuid.o
cc -c -D_POSIX_SOURCE=19939 -D_POSIX_SOURCE -Wall -handle-exceptions main.cc
cc -o getuid main.o
$ ./getuid
Root's home is /root.
Account uucp the shell /usr/bin/.
No such file or directory: looking up account xyzy.
Account uses the shell /sbin/nologin.
```

为了帮助你进行后续测试，请删除我们生成的存档文件：
```bash
$ rm passwd.a
```

项目编译后由以下对象文件组成，它们构成了链接器的输入：

| 主程序 | `main.o` |
| :--- | :--- |
| 某些方法 | `import.o` |
| 方法 `getuid` 和 `getnam` | `getuid.o` |

链接过程所使用的步骤可以总结如下：

- 1. 链接过程从加载 `main.o` 模块开始（在本例中）。
- 2. 然后，链接器注意到 `main()` 函数引用了符号 `Passwd::getuid()` 和 `Passwd::getnam()` 的未定义引用。
- 3. 由于已经提供了一个库（`libpasswd.a`），链接器会在该归档中搜索定义符号 `Passwd::getuid` 的对象模块。链接器在包含于归档文件对象 `getuid.o` 中找到了名为 `Passwd::getnam()` 的符号。链接器从归档中提取出模块 `getuid.o` 并加载它。在此过程中，符号 `Passwd::getnam()` 得到了解析，它也包含在同一个对象模块中。
- 4. 链接器检查其未解析符号列表。符号 `Passwd::__import()` 现在被解析了。这个新引用来自链接器刚刚加载的对象模块 `getuid.o`。
- 5. 从列表顶部开始，链接器再次搜索归档 `libpasswd.a`，并确定必须提取并加载模块 `import.o`。这满足了符号 `Passwd::__import()`。

这是对链接过程的简化，因为对 C 库函数的引用是免费的（相当于 C++ 关键字 `delete`）。然而，这阐明了当静态库参与链接过程时会发生什么。

从这个过程中可以证明，对象模块仅在需要时才由链接器引入。这对于那些希望在大型函数集中使用少数函数的人来说，这种方式非常好。毕竟，如果你只需要库的一小部分，你不想与每一个对象模块进行链接。

### 共享库

在本节中，你将学习如何创建和使用共享库。你已经在图 13.1 中看到了关于库的提示。

## 静态库的局限性

图 13.2 显示了链接器如何自动从归档中提取对象模块并按需加载它们。虽然只链接你需要的部分可以为你的程序提供某种经济性，但从系统范围来看，仍然存在重复。想象有一个巨大的假设静态库，它包含了 Netscape Web 浏览器使用的 90% 的函数。Netscape 与此库链接，产生一个可能 5MB 的可执行文件。该可执行文件中大约 90% 的内容将静态库中内容的副本。

假设你想构建一个支持 Web 的程序，从你的应用程序创建一个 Netscape X 窗口。你的 200KB 对象模块与这个 Netscape 静态库链接，生成的程序写入大小为 4.5MB。现在你拥有一个 5MB 的 Netscape 可执行文件，且两个程序中有 90% 的代码是相同的。

考虑一下，五个运行 Netscape 的用户和三个运行你的自定义应用程序的用户在系统内消耗了大量内存。增加用户后，UNIX 内核将开始进行严重的交换（swapping）。

共享库提供了一种机制，允许系统中的多个程序实例共享同一份代码。

## 创建共享库

在过去，库的创建和维护需要 UNIX 系统管理员进行一些真正的“手部操作”。在 FreeBSD 或 Linux 下为自己使用创建一个共享库，你可以简单地使用 `gcc(1)` 命令的 `-shared` 选项。使用之前的示例，类 `Passwd` 的共享库创建方式如下：

使用 `-shared` 选项执行 `gcc(1)` 命令，导致输出文件为共享库而非可执行文件。在该文件中创建了库 `libshared.so`。后缀 `.so` 用于在 FreeBSD 和 Linux 下表示共享库文件。

## 与共享库链接

使用共享库非常简单，但可能会有一些复杂之处。首先，检查链接步骤是如何执行的：

```
$ gcc main.o -o getuid -L -lshared -stdc++
```

注意使用 `-L` 和 `-l` 选项。`-L` 选项指定了用于搜索共享库的额外目录。`-l` 选项告诉要搜索的库名（共享库会添加前缀 `lib` 和后缀 `.so`，导致搜索 `libshared.so`）。因为链接器知道方法 `Passwd::getuid()` 和 `Passwd::getnam()` 在共享库中，所以链接器仅在写入的最终可执行文件中对此“做了一个标记”。这些标记允许共享库在程序执行时被加载。

## 选择静态库或动态库

当静态库和共享库都可用用时，`gcc(1)` 通常会选择共享库。然而，如果你在 `gcc(1)` 命令上指定了 `-static` 选项，链接阶段将使用静态库而非可能的选项。

## 列出共享库引用

在 FreeBSD 和 Linux 中，你可以检查新的可执行文件 `getuid`，查看它是否引用了之前创建的新共享库：

```
$ ld .//getuid
  libshared.so => not found (0x0)
  libc++.so.2 => /usr/lib/libstdc++.so.2 (0x28063000)
  libc.so.3 => /usr/lib/libc.so.3 (0x2809a000)
  libm.so.2 => /usr/lib/libm.so.2 (0x2811b000)
```

从输出可以看出，`./getuid` 确实引用了名为 `libshared.so` 的共享库。`not found` 信息表示 `ld` 无法定位库。在这些条件下运行程序：

```
$ ./getuid
libshared.so: shared object "libshared.so" not found
```

为什么动态加载器没有找到共享库？

### 动态加载器

共享库比静态库需要更多关注。因为共享库必须按需查找。

## 搜索共享库

FreeBSD 和 Linux 都共享一个指示库位置的缓存。以下列出了这些文件的位置：

| FreeBSD cache | `/var/run/ld.so` |
| FreeBSD ELF | `/var/run/ld.so` |
| Linux cache | `/etc/ld.so` |

这些缓存文件由 `ldconfig(8)` 命令更新。其他 UNIX 平台使用环境变量来选择库目录。在不同的 UNIX 平台中有三个路径变量。

| 环境变量 | UNIX 平台 |
| :--- | :--- |
| `LD_LIBRARY_PATH` | Solaris, UnixWare, IRIX, Alpha OS, FreeBSD 和 Linux |
| `LIBPATH` | AIX |
| `SHLIB_PATH` | HPUX |

## 使用 LD_LIBRARY_PATH

由于 FreeBSD 使用此变量，给出的示例将使用它。回想之前的示例：

```
$ ld ~getuid
libshared.so => not found (0x0)
libstdc++.so.2 => /usr/lib/libstdc++.so.2 (0x28063000)
libc.so.3 => /usr/lib/libc.so.3 (0x2809a000)
libm.so.2 => /usr/lib/libm.so.2 (0x2811b000)
```

为了解决新创建的共享库的困难，修改 `LD_LIBRARY_PATH` 变量以包含当前目录（使用 变量 `$PWD`）：

```
$ LD_LIBRARY_PATH=$PWD
$ export LD_LIBRARY_PATH
$ ld ~getuid
libshared.so => /home/me/myproject/libshared.so (0x28063000)
libstdc++.so.2 => /usr/lib/libstdc++.so.2 (0x28065000)
libc.so.3 => /usr/lib/libc.so.3 (0x2809c000)
libm.so.2 => /usr/lib/libm.so.2 (0x28111d00)
```

注意，`LD_LIBRARY_PATH` 修改为包含当前目录后，动态加载器能够定位你的共享库文件 `libshared.so`。如果你在当前的 `LD_LIBRARY_PATH` 变量中已经包含了其他目录，这种方法更好：

```
$ LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$PWD
```

这仅仅将你的当前目录追加到已生效的值之后。

## 测试 LD_LIBRARY_PATH 变量

在正确设置了 `LD_LIBRARY_PATH` 变量后，你现在可以按照如下方式运行测试程序：

```
$ getuid
Root's home dir is /root.
```
