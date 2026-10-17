
## 表 4-2: `notdir`, `basename`, 和 `suffix` 的结果

| 函数 | 结果 |
|---|---|
| `dir` | `/foo/bar/` |
| `notdir` | `source.c` |
| `basename` | `source` |
| `suffix` | `.c` |

你可以看到，目录、非目录部分、后缀（或扩展名）以及不带后缀的非目录部分都被提取出来了。这四个函数使得文件名操作变得简单。如果没有指定目录，GNU make 将使用当前目录（`./`）。例如，假设 `FILE` 仅仅是 `source.c`。表 4-3 显示了每个函数的结果。

## 表 4-3: 未指定目录时 `notdir`, `basename`, 和 `suffix` 的结果

| 函数 | 结果 |
|---|---|
| `dir` | `./` |
| `notdir` | `source.c` |
| `basename` | `source` |
| `suffix` | `.c` |

这些函数通常与 GNU 自动变量（如 `$$`）结合使用，GNU make 提供了一种修符语法。在任何自动变量后附加 `D` 或 `F` 等同于对它调用 `$$(notdir)`。例如，`$(@D)` 等同于 `$(@D)`，而 `$(@F)` 等同于 `$$(notdir $$)`。

### 3.81 中的实用函数：`abspath` 和 `realpath`

`realpath` 是 GNU make 对 C 库 `realpath` 函数的封装，它会移除 `../`、移除重复的 `/` 并跟踪符号链接。`realpath` 的参数必须在文件系统中存在。`realpath` 返回的路径是绝对路径。如果路径不存在，该函数返回空字符串。

例如，你可以这样找到当前目录的全路径：`current := $(realpath)`。

`abspath` 与其类似，但它不会跟踪符号链接，且其参数不需要指向存在的文件或目录。

## 奥斯曼定律 (Usman's Law)

`make clean` 并不真的让一切干净。这就是奥斯曼定律（以我的一位聪明的同事命名，他曾花了几个月处理真实的 makefiles）。`make clean` 的目的是返回到一个所有内容都将从头开始的状态。但通常并非如此。继续读下去了解原因：

### 人为因素

OpenSSL `Makefile` 中的 `clean` 规则看起来如下：

```
clean:
→ rm -f *.o *.obj lib tags core .pure .nfs* *.old *.bak fluff $(EXE)
```

注意，这是一系列由人工维护的目录、模式和文件名的列表，为了回到干净状态需要删除这些内容。人工维护意味着人为错误。有人添加了一条规则，创建一个固定名称的临时文件。这个临时文件应该被添加到 `clean` 规则中，但很可能不会被添加。
奥斯曼定律发生了。

### 糟糕的命名

以下是在许多自动生成的 makefiles 中发现的片段：

```
mostlyclean:
→ rm -f *.o

clean::mostlyclean
→ $(LIBTOOL) --mode=clean -f $(program) $(programs)
→ rm -f $(library).a squeeze *.bad *.dvi *.lj

extraclean:
→ rm -f *.aux *.bak *.bbl *.blg *.vi *.log *.pl *.tm *.vf *.vpl
→ rm -f *.pk *.gf *.mpx *.i *.s *.orig *.rej *.ij#
→ rm -f CONTENTS.tex.a core mputf. texput *.mpout.
```

在这个示例中，三种类型的 clean 似乎具有不同程度的干净：`mostlyclean`、`clean` 和 `extraclean`。`mostlyclean` 只是删除从源码编译的对象文件。`clean` 则确实如此。你可能认为 `extraclean` 比其他两个删除得更多，但它实际上删除的是一组不同的文件。我甚至见过带有 `reallyclean`、`veryclean`、`deepclean` 甚至 `partiallyclean` 规则的 makefile！

当你无法从命名中判断每个规则的作用时，这很容易导致后续出现潜在问题。
奥斯曼定律再次发生。

### 静默失败

这是另一个有时可以运行的 Makefile 片段：

```
clean:
-> @-rm * & /dev/null
```

`@` 表示该命令不会回显。`-` 意味着任何返回的错误都会被忽略，并且所有输出通过 `&` 重定向到 `/dev/null`，使其变得不可见。由于 `rm` 命令上没有 `-f`，任何失败（例如权限问题）将完全不会被察觉。
奥斯曼定律再次发生。

### 递归清理

许多 makefiles 是递归的，`make clean` 也必须是是递归的，因此我们看到了如下模式：

```
SUBDIRS = library executable

.PHONY: clean

clean:
-> for dir in $(SUBDIRS); do
-> $(MAKE) -C $$dir clean;
-> done
```

此问题在于，这意味着 `make clean` 必须在每个 `SUBDIRS` 目录中都能正常工作，导致了更多出错的机会。
奥斯曼定律再次发生。

## GNU make 并行的陷阱与收益

许多过程需要运行数小时，因此构建管理器通常遇到问题后就下班回家。GNU make 对此问题的解决方案是并行执行：这是一个简单的命令行选项，可以导致 GNU make 使用 Makefile 中的依赖信息并行运行作业，并按照正确的顺序执行。

然而在实践中，由于所有 Makefile 在编写时都基于规则串行运行的假设，GNU make 的并行执行受到了严重限制。Makefile 作者在编写时很少考虑并行。这导致了隐藏的陷阱，要么导致构建因致命错误失败，要么更糟糕——构建成功，但产生了错误的二进制文件。

列表 4-9 并行运行的输出可能是：

```
$ make --jobs=16
touch t4
touch t5
touch t3
cp t3 t2
touch t1
Making all
```

甚至：

```
$ make --jobs=16
touch t3
cp t3 t2
touch t4
touch t1
touch t5
Making all
```

这使得任何检查日志文件以检测构建问题（如对比日志文件）的过程都变得困难。遗憾的是，在没有 `--output-sync` 选项的情况下，GNU make 没有简单的解决方法，除非你升级到 GNU make 4.0，否则你必须忍受。

### 使用 `-j` (or `jobs`)

要以并行模式启动 GNU make，你可以在命令行上指定 `-j` 或 `--jobs`。例如，输入 `make -j4` 允许 GNU make 运行最多四个进程。然而，实际的加速效果受限于阿姆达尔以及以及过程是串行的事实。

### 缺失的依赖项

列表 4-9 中的示例还有一个额外的问题。作者在编写 Makefile 时掉进了经典的“从左到右”陷阱，因此当它并行运行时，可能会出现以下情况：

```
$ make --jobs=16
touch t5
touch t4
cp t3 t2
c: cannot stat `t2`: No file or directory
make: *** [t2] Error 1
```

原因是当并行运行时，构建 `t2` 的规则可能发生在构建 `t3` 的规则之前，而 `t2` 需要 `t3` 已经构建完成。在串行情况下这种情况没有发生，是因为从左到右的假设：构建 `t1` 的规则是 `t1: t3 t2`，这意味着 `t3` 会在 `t2` 之前构建。

但 Makefile 中并没有实际存在 `t3` 必须在 `t2` 之前构建的依赖。修复方法很简单：只需在 Makefile 中添加 `t2: t3` 即可。

这是一个缺失或隐式（从左到右）依赖的真实问题示例，这种问题在 Makefile 并行运行时非常棘手。如果一个 Makefile 在并行运行时崩溃，值得立即寻找缺失的依赖，因为它们非常常见。

### 隐藏的临时文件问题

GNU make 在并行运行时可能导致崩溃的另一种方式是多个规则使用了同一个临时文件。考虑列表 4-10 中的示例 Makefile：

```
TMP_FILE := /tmp/scratch_file

.PHONY: all

all: t

t: t1 t2
-> cat t1 t2 > $@

t1:
-> echo Output from $@ > $(TMP_FILE)
-> cat $(TMP_FILE) > $@

t2:
-> echo Output from $@ > $(TMP_FILE)
-> cat $(TMP_FILE) > $@
```

列表 4-10：一个破坏并行构建的隐藏临时文件

在不带并行选项的情况下运行，GNU make产生以下输出：

```
$ make
```
