
## umask() 的主要用途

umask() 的主要用途是创建临时文件或永久文件，以防止这些文件被意外读取或写入。

```c
    if ( S_ISDIR(statbuf.st_mode) )
    {
        // Ignore . and ..
        if ( strcmp(".", entry->d_name) == 0 || strcmp("..", entry->d_name) == 0) 
            continue;
        // Print the current directory
        printf("%s/\n", entry->d_name);
        /* Recurse at a new indent level */
        printDir(entry->d_name);
    }
    else if ( S_ISLNK(statbuf.st_mode) )
        totalSymlinkLinks++;
    else
        continue;
    }
    chdir("..");
    closedir(dp);
}
```

```c
int main(int argc, char** argv)
{
    char *rootDir = "";
    if ( argc != 2 )
    {
        printf("Please provide exactly 1 command line argument.\n");
        return -1;
    }
    rootDir = argv[1];

    printf("Scanning %s for symbolic links!\n", rootDir);
    printDir(rootDir);
    printf("Found %d Symlink Links!\n", totalSymlinkLinks);
    return 0;
}
```

## 文件的各类时间

每个文件都有三个时间字段：修改时间 (st_mtime)、状态变更时间 (st_ctime) 和最后访问时间 (st_atime)。修改时间和状态变更时间之间存在细微差别。修改时间表示文件数据发生了更改，而状态变更时间表示文件的元数据发生了修改，这会导致文件的 inode 发生变化。

## 使用 Haskell 进行系统编程

Haskell 是一种函数式编译编程语言，可用于系统编程。Haskell 是执行文件名匹配操作的最佳选择。Haskell 方式唯一的缺点是，不同的操作系统使用不同的专用模块。

`System.Directory` 模块包含许多函数，可用于从文件系统获取信息，包括获取目录中的文件列表、重命名或删除文件、复制文件、更改当前工作目录 (`setCurrentDirectory`) 以及创建新目录。好消息是，`System.Directory` 是可移植的，并且可以在 GHC（格拉斯哥 Haskell 编译器）本身支持的任何平台上运行。

以下输出展示了使用 Haskell 的优势：

```
ghci> :module System.Directory
ghci> getDirectoryContents "/tmp"
["update-cache-2all3caac","upload_progress",
 cache":"update-extraction-2all3caac", "xdrch-env-x", "font=unix-x", "haccesse", "ghe414750_@", "XH=
 unix*x","hspersidata_root*", "IEC=unix*x","XL1=unix*",
 "test=unix*" ]

ghci> getDirectoryContents "/tmp" >>= return . filter
 (notElem [".", ".."])
["update-cache-2all3caac","upload_progress",
 cache","update-extraction-2all3caac", "xdrch-env-x", "font=unix-x", "haccesse", "ghe414750_@", "XH=
 unix*x","hspersidata_root*", "IEC=unix*x","XL1=unix*"]
```

第一个 `getDirectoryContents` 命令返回 `/tmp` 目录的所有内容。第二个命令执行相同的操作，但有一个小差别：它使用模式匹配排除了特殊值 `"."` 和 `".."`。

根据用于访问文件的函数，部分或所有时间字段可能会改变。此外，修改、删除或添加目录项肯定会改变父目录的部分或所有时间。

现在让我们看看 `filetimes.c`。您需要将获取到的时间值转换为用户更容易理解的格式——这是使用 `ctime` 函数完成的。像往常一样，首先应该调用 `stat( )` 或 `fstat( )` 来获取必要的数据。获取数据后，应提取并在屏幕上打印，这是一个直接且无痛的过程。正如您已经了解到的，然后使用 `chmod( )` 函数更改文本文件的权限。最后，向文件末尾追加一些文本。编译并执行程序，查看文件的各类时间如何变化。

## 处理目录

在底层，UNIX 机器将目录实现并视为普通文件；它们之间只有两个区别。第一个是内核不允许在目录上写入，第二个是它们的 inode 中设置了一个特殊位。

虽然知道如何处理单个文件是很好的，但大多数时候您将处理整个目录或目录树。操作目录的两个最有用系统调用是 `opendir( )` 和 `readdir( )`。

通过查看 `find.c` 中展示的 C 代码，您可以看到 `opendir( )` 和 `readdir( )` 的实际操作。请注意，`S_ISDIR(statbuf.st_mode)` 有助于确保您处理的是实际目录，而不是普通文件或网卡！

### 遍历目录结构

展示的程序 `find.c` 的目的是遍历目录结构以查找具有特定文件名的文件——就像 find 实用程序的一个简化版本。如果所需的文件名是“任意”，则 `find.c` 会打印它找到的每个文件和目录。为程序添加一些额外功能总是好的——这在第 34 行实现。

下载并检查 `find.c` 文件。`find.pl` 中展示的 Perl 版本更为先进，因为它使用正则表达式而不是精确匹配；然而，`find.c` 和 `find.pl` 之间的相似之处比差异更多。如您所料，C 版本比 Perl 版本更大。

请注意，在 C 中比较字符串是否相等可以通过逐个字符比较或使用 `strcmp(3)` 函数来完成，后者是更好的解决方案。拥有一个单独的函数来打印目录内容（名为 `printd()`）的主要原因是程序是递归操作的；由于 `main()` 不能调用自身，我们需要一个单独的函数！

该程序使用 `chdir(2)` 函数将当前工作目录更改为提供的根目录（第 19 行）。这不是强制性的，但它使程序员的工作更简单。每次 `printd()` 找到一个目录项时，它会访问该目录。当它完成检查一个目录后，它会返回到父目录（第 39 行）。

请注意，`find.c` 使用 `lstat(1)` 而不是 `stat(1)` 以便能够跳过符号链接——这不是强制性的，但请记住符号链接并不安全，因为它们甚至可能使您的程序跳转到不同的文件系统。此外，多个符号链接可以创建一个循环，这将使您的程序永远运行！在程序上修复符号链接循环并不是一项容易的任务；因此，使用 `lstat()` 代替 `stat(1)` 并执行必要的检查是一个安全且安全的选择。

### 计算符号链接

`countSymlinks.c` 实现了另一个命令行实用程序，它搜索目录树中的符号链接并对其进行计数。您应该已经知道如何从 `find.c` 中的代码遍历目录结构，这将是 `countSymlinks.c` 的基础。`countSymlinks.c` 中应该有两点变化。第一点是它应该使用全局变量来保持迄今为止找到的符号链接数量。第二点是它必须使用 `S_ISLNK(1)` 代替 `S_ISDIR(1)`，以确保检查的项确实是符号链接（第 34 行）。请查看 `countSymlinks.c` 以获取完整的 C 代码。

上一页的图像显示了比较 `countSymlinks.c` 和 `find.c` 的 `diff` 命令的输出。由于大多数所需功能已经存在，您只需要查看修改部分。虽然 `find.c` 中 `lstat(1)` 的使用是可选的，但这并不适用于 `countSymlinks.c`：`countSymlinks.c` 中必须使用 `lstat(1)` 系统调用，因为如您所知，`stat(1)` 会跟随符号链接！

### 搜索 PATH

`path.c` 显示了 `path.c` 文件的完整 C 代码，该文件在 PATH 环境变量中搜索可执行文件，类似于 `which` 实用程序。您应该熟悉大部分展示的代码，但最好快速回顾一下。

首先，程序读取 PATH 变量并存储其内容。然后，它将 PATH 变量的各个部分——即目录——分离出来，以便独立使用每个部分。最后，它检查所需的可执行文件是否位于 PATH 环境变量的目录之一中。程序列出找到的可执行文件的所有实例，而不仅仅是第一个。

PATH 变量棘手的地方在于它可能包含当前工作目录，该目录用点表示：“.”。`realpath(3)` 函数解析给定路径的规范绝对路径名。因此，`opendir(1)` 系统调用打开在 PATH 环境变量中找到的每个目录的规范绝对路径名。小细节会产生巨大差异，所以总是要注意它们！

请注意，如果您要搜索的程序在当前的 PATH 中但它不是一个可执行文件，`path.c` 会显示它。这种检查通过第 38 行的 `access(1)` 函数进行。`access(2)` 函数检查调用进程是否可以访问指定的文件（即其第一个参数）；其第二个参数指定将要执行的可访问性测试。`R_OK` 常量检查读权限。

![](img/0fc17bd4c29dc437e3ac28a53f7559db_31_0.png)

## 从 Haskell 调用 C 代码

如果说 Haskell 本身还不够好，我们也可以调用 C 代码！请注意，这里 Haskell 仅作为示例，因为许多其他语言也可以调用 C 代码。

以下程序 (`git`) 针对使用 Haskell 代码包装的 C 代码的过程。

```haskell
(* -- LANGUAGE ForeignFunctionInterface -- *)
module Main where
import System.Posix.Types

foreign import ccall unsafe "getpid" c_getpid :: IO PID
main = do
    print = c_getpid
```

虽然您可能不熟悉 Haskell 代码，但您应该理解刚才发生的事情多么非凡：您使用了一种完全不同的编程语言中的 C 系统调用来获取您想要的核心信息。简而言之，c_getpid Haskell 函数使用 get{1}(2) 来获取进程 ID。采用稍微不同的方法，您可以从 Haskell 代码中调用自己的 C 函数。

> “PATH 变量棘手的地方在于它可能包含当前工作目录，该目录用点表示：”。

