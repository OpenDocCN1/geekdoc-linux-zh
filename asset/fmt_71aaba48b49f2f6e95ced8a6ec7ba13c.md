
原始的 Environment Modules 项目（也称为 Tcl modules 或 Tcl/C modules）在 2012 年发布 3.2.10 版本时开发了一段时间。该版本遇到的主要缺点是：如果已经加载了另一个版本，则加载该包很困难，以及难以跟踪不同模块之间的依赖关系（例如使用不同编译器构建的 MPI 实现）。

为了解决这些及其他问题，创建了替代方案 Lua Modules (`LMOD`)。正如名称所示，该项目设计用于 Lua 语言编写模块文件。同时，它可以使用由 Tcl 编写的原始模块文件。`LMOD` 解决了上述两个问题。当加载另一个已加载版本的模块时，之前加载的模块会自动卸载（打印更改）。这避免了同时存在两个版本编译器的情况。

> ⁵https://www.tacc.utex.edu/research-development/tacc-projects/lmod

此外，`LMOD` 支持动态更改模块文件的路径列表（`MODULEPATH` 变量）。这允许你动态生成可用模块列表。例如，当加载编译器模块时，模块目录的路径会被添加到软件包 `MODULEPATH` 变量中。当 `MODULEPATH` 变化时，不仅有新模块可用，某些模块也会变得不可。这些模块被标记为非激活，即环境变量的修改类似于卸载模块时，但模块本身仍保留在加载列表中（带有相应的标记）。

如果以后由于 `MODULEPATH` 变量的变化，同名的模块变得可用，它将自动加载。通过这种方式，实现了对该模块所依赖的其他模块版本的替换。

`LMOD` 提供了 `module spider` 命令，可以提供关于所有可用模块、选定模块或单个模块版本的详细信息。以下是所有模块信息的示例：

```bash
$ module spider
```

以下是当前可用模块的列表：

```
gcc: gcc/4.8.1, gcc/10.4.0, gcc/15.1.0
The GNU Compiler Collection
lmod: lmod/8.7.60
Lmod: An Environment Module System
openmpi: openmpi/4.1.8, openmpi/5.0.7
Openmpi Version of the Message Passing Interface Library
```

# 第 21 章 针对并行技术的编译器与环境

使用 `module spider MODULENAME` 命令可以获取某个模块的所有版本信息，这与上述内容非常相似。关于特定模块版本的详细信息更有趣：

```
$ module spider openmpi/5.0.7
```

```
openmpi: openmpi/5.0.7
```

描述：

消息传递接口库（Message Passing Interface Library）的 Openmpi 版本

在 "openmpi/5.0.7" 模块可用加载之前，你需要在下面的行中加载任意一个模块。

- gcc/10.4.0

- gcc/15.1.0

你可以仅指定模块名称来加载模块，也可以指定版本（如 gcc/15.1.0）；在第一种情况下，将使用默认版本。在 `LMOD` 和最新的 modules 软件包中，你可以显式指定；否则，将选择最高版本。在 `LMOD` 中，版本按数字排序；在 modules 中则按字符串排序（mk1/4.0 高于 mkl1/11.0）。

`LMOD` 的其他优秀功能：保存/恢复一组模块、隐藏模块（例如用于测试）以及灵活的依赖系统。

我不会描述 Lua 中模块的语法。大多数命令（如 `prepend-path`）都继承自原始项目，但使用时应考虑到 Lua 语法。其他命令可以在 `LMOD` 文档中找到。

2017 年底，原始 Modules 项目开始再次非常活跃。到目前为止，它的开发趋向于其他功能，这些功能如何应用到使用 `LMOD` 解决的问题尚不清楚，此外还有许多纯技术性的更改。但这个项目值得关注；也许，它会有自己一些有用功能。

## 构建系统

许多 HPC 软件包依赖于大量的其他包和库。如果你需要构建一个全新的包，这可能会是一件头疼的事。为了帮助管理员构建和管理 HPC 软件，至少有两个流行的软件包——EasyBuild 和 SPACK。让我们来看看如何使用它们。

EasyBuild¹ 是一个开源的 Python 软件包，你可以使用 `pip` 安装它。请使用 python 3.6 或更高版本，我建议使用 `venv` 将其安装到独立的命名空间中：

```
python3 -m venv easybuild
source easybuild/bin/activate
pip install easybuild
```

如果你使用 Lmod 或 EnvironmentModules（你确实在使用，对吧？），你可以在完成上述安装后，将 easybuild 安装为一个模块：

```
eb --install-latest-eb-release --prefix /opt/easybuild
module use /opt/easybuild/modules/all
# 如何加载模块：
module load EasyBuild
```

加载模块后，你就可以使用 `eb` 命令了。简单示例——构建一个新包：

```
eb HPL-2.3-foss-2024a.eb
== 崩溃时的临时日志文件 /tmp/eb-rpngdte7/\asybuild-3/6is4k7.log
== 为 /home/foo/eb/easybuild/easyconfigs 找到了有效索引，正在使用它...
== 正在处理 EasyBuild easyconfig /home/foo/eb/easybuild/easyconfigs/h/
HPL-2.3-foss-2024a.eb
== 正在构建并安装 HPL/2.3-foss-2024a...
>> 安装前缀: /home/foo/.local/easybuild/software/HPL/2.3-
foss-2024a
== 正在获取文件并验证校验和...
...
```

> ¹https://docs.easybuild.io/

我们在用户的 foo 家目录中使用了 EasyBuild 安装，并使用 GCC 工具链构建了 HPL-2.3 包。带有配置文件、构建描述和默认安装路径的目录列表可以通过运行 `eb-showconfig` 命令找到。构建完成后，spack 模块及其依赖项将可以通过模块可用。EasyBuild 拥有良好的文档，如果你想使用它，请查看详细信息、使用优化、特定库（如 CUDA）等。

另一个流行的构建工具是 Spack.^7。安装非常简单：

```
git clone -c feature.manyFiles=true --depth=2 \
https://github.com/spack/spack.git
source pack/share/spack/setup-env.sh
```

如果你想在每个会话中激活 Spack，应将最后一行添加到你的 shell 配置文件中。安装完成后，你可以立即运行它，例如尝试安装 HPL 包：

```
spack install hpl
== 正在获取 https://ghcr.io/... (省略)
== 正在获取文件并验证校验和...
== 正在构建 HPL/2.3...
== 正在构建构建并安装 HPL/2.3-foss-2024a...
== 安装前缀: /home/foo/.local/easybuild/software/HPL/2.3-
foss-2024a
```

## 简要

并行编程并不容易，目前流行的是 MPI、OpenMP、CUDA、OpenCL、OpenACC 和 SHMEM。

MPI 和 SHMEM 是库，但需要在多个节点上特殊方式工作。这就是为什么管理员负责安装和配置它们。
