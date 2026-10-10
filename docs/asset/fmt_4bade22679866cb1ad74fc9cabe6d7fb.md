
8. 构建附加软件包`lsbsi-test`、`lsbsi-boot`和`lsbsi-uml`需要额外步骤。此步骤不依赖于 LSB-si（第三阶段）步骤完成，但依赖于中间 LSB-si（第二阶段）步骤完成：

```
# make addons
```

9. 现在你可以构建 UML 可安装软件包（仅限 IA-32 构建主机或目标）。此步骤依赖于所有其他阶段（包括附加组件）完成：

```
# cd rpm
# make
```

> 构建占用大量空间（约 1.4GB），且可能花费大量时间。在快速的 Dual-CPU Pentium 4 上完全构建大约需要 2.5 小时；根据架构、内存和处理速度，可能需要长达 20 小时。

如果构建停止，无论是自愿还是由于某些问题，应该有相当程度的支持重启，但这并不完美。特别是，要小心清理任何构建区域，因为软件包目录可能仍处于绑定挂载状态。团队成员都曾多次意外删除软件包目录，导致在重新获取期间产生巨大延迟（最好在别处制作该目录的副本）。小心！`makefile`有一个`clear_mounts`目标，可能很有用。

### 12.5 测试示例实现

LSB-si（图 12.2）接受与第 6 章描述的相同测试规程：

- `lsb-runtime-test`，目标为零失败
- `lsbiiibchk`，用于检查所有必需库是否存在
- 应用程序 LSTT，运行所有示例应用程序的 FVT

将 LSB 运行时测试安装到 LSB-si 的`chroot`环境（示例 12.17）中。

![](img/d75cffbcb54aabfb0f9854162061d394_199_0.png)

图 12.2：示例实现

## 示例 12.17：运行时测试安装

```
# cp lsb-runtime-test-2.0-1.ia32.rpm  /opt/lsbsi-ia32/tmp
# /sbin/chroot /opt/lsbsi-ia32
# cd /tmp
# rpm -i lsb-runtime-test-2.0-1.ia32.rpm
# password -d vsx0
```

如第 12.2.1 节所示，以用户`vsx0`登录，然后运行 LSB 运行时测试套件（示例 12.18）。

## 示例 12.18：运行运行时测试套件

```
vsx0$ telnet localhost
vsx0$ run_tests
```

### 12.6 打包示例实现

LSB-si 针对以下每种架构以多种配置发布：

1. **基础系统**：一个仅包含 LSB 书面规范所要求内容的压缩包。可以通过`chroot`进入。若要完全符合规范，需要底层 Linux 内核符合 LSB 规范。
2. **可测试系统**：包含基础系统以及启用 LSB-si 作为测试环境所需的其他文件和程序。此捆绑包可以运行 LSB 运行时测试套件和符合 LSB 规范的应用程序。可以通过`chroot`进入。运行后，可以通过`telnet`连接到该环境。若要完全符合规范，底层 Linux 内核必须符合 LSB 规范。
3. **可启动系统**：基础系统的文件加上内核和其他支持，使其能够独立启动。需要一些额外的配置——例如，针对目标硬件的适当启动配置以及必要内核模块的配置。
4. **托管系统**：基础系统的文件加上运行 User-Mode Linux（一种在宿主系统上作为用户级应用程序运行的内核虚拟机）的支持。User-Mode Linux 可能并非在所有 LSB 支持的架构上都可用。托管捆绑包也可用作可安装、即开即用的软件包。

![](img/d75cffbcb54aabfb0f9854162061d394_200_0.png)

> 当软件包扩展超出基础系统时，存在权衡：系统变得更易使用，但包含了各种非 LSB 命令和文件，因此在测试意义上略显不够“纯粹”。

### 12.7 下载示例实现

要下载 LSB 示例实现，请访问 LSB 下载网站。⁶ 表 12.1 展示了可通过万维网访问的信息。

**`lssbi-boot`** LSB 示例实现可启动系统，包含内核及其他支持，使 LSB-si 能够以独立模式启动。需要安装`lssbi-core`并进行安装后的配置。

**`lssbi-core`** LSB 示例实现基础系统，仅包含 LSB 书面规范所要求的内容。可以通过`chroot`进入。

**`lssbi-graphics`** LSB 示例实现图形系统，包含在 LSB-si 内支持图形应用程序所需的文件。需要安装`lssbi-core`。

**表 12.1：示例实现下载页面**

| 规范版本 | 软件包 | 版本 | 架构 |
| :--- | :--- | :--- | :--- |
| 2.0.0 | `lssbi-boot` | 2.0.2 | IA32, IA64, PPC32, PPC64, S390, S390X, x86_64 |
| 2.0.0 | `lssbi-core` | 2.0.2 | IA32, IA64, PPC32, PPC64, S390, S390X, x86_64 |
| 2.0.0 | `lsb-graphics` | 2.0.2 | IA32, IA64, PPC32, PPC64, S390, S390X, x86_64 |
| 2.0.0 | `lsb-test` | 2.0.2 | IA32, IA64, PPC32, PPC64, S390, S390X, x86_64 |
| 2.0.0 | `lsb-uml` | 2.0.2 | IA32, IA64, PPC32, PPC64, S390, S390X, x86_64 |

`lsbsi-test` LSB 示例实现可测试系统，包含将 LSB-si 用作测试环境所需的其他文件和程序。需要安装`lsbsi-core`。

`lsbsi-uml` LSB 示例实现托管系统，包含运行 User-Mode Linux（一种在宿主系统上作为用户级应用程序运行的内核虚拟机）的支持。UML 可能并非在所有 LSB 支持的架构上都可用。需要安装`lsbsi-core`。

`lsb` 此软件包提供基础 LSB 软件包。请注意，此软件包仅应安装在 LSB 示例实现上。在其他任何发行版上安装此软件包可能会损坏系统。

`lsb-uml-si` LSB 示例实现 User-Mode Linux 环境。

# 第十三章

## 使用 LSB 开发环境

LSB 开发环境旨在帮助开发人员构建符合 LSB 书面规范的应用程序。它们主要通过提供以下便捷方式来实现这一目标：

- 针对包含 LSB 书面规范所必需定义的头文件进行编译
- 针对仅包含 LSB 书面规范所必需接口的共享库进行动态链接

### 13.1 理解 LSB 开发环境

LSB 开发环境本身并非集成开发环境（IDE），而是对现有 IDE 的增强，使其能够构建符合 LSB 标准的二进制文件。请注意，虽然 LSB 开发环境有助于程序员构建符合 LSB 标准的应用程序，但它并非唯一的方法。

1. http://www.linuxbase.org/build/
2. http://www.linuxbase.org/download/

该功能允许旧应用程序继续使用旧版本，而新应用程序可以使用新版本。

当创建二进制文件时，它会检查所链接的共享库，并记录其所需的这些接口的版本。在运行时，二进制文件将查找具有记录版本号接口的接口，如果不存在则失败。因此，必须针对包含在符合 LSB 标准的运行时上保证存在的接口版本的共享库进行链接。

对于 LSB 支持的使用符号版本控制的库，规范列出了接口的特定版本。LSB 桩库仅包含 LSB 书面规范允许的接口版本，因此如果使用它们，在构建二进制文件时就不可能使用错误的版本。

共享库中通常包含一些必须符合 LSB 标准的二进制文件不得使用的接口。这些接口通常是私有函数或 LSB 不支持的接口。由于桩库仅包含规范要求的接口，如果应用程序使用了不受支持的接口，将在链接阶段发生错误。

### 13.3.2 LSB 头文件

与库关联的头文件中包含的定义可能会随着该库 ABI 的演变而随时间改变。例如，库的某个版本中的函数可能接受一个参数，而在下一个版本中可能接受两个参数。

LSB 书面规范为每个受支持的库定义了 ABI，用于编译该库的头文件必须完全匹配。为了避免找到包含正确定义的软件准确版本的问题，LSB 开发环境提供了与规范匹配的头文件。

### 13.3.3 使用开发工具

目前有两种开发工具`lsb-build-chroot`和`lsb-build-cc`，它们针对符合标准的头文件和库进行编译和链接。

使用这些工具是构建符合 LSB 标准应用程序的简便方法。这两个工具都使用`lsb-build-base`软件包。该软件包包含 LSB 头文件和桩库。

#### 13.3.3.1 lsb-build-chroot

`lsb-build-chroot`使用`chroot`命令在你的机器上创建一个虚拟 LSB 平台开发环境。默认情况下，它提供一个最小环境，尽可能不包含那些如果对其进行编译会导致生成的二进制文件不符合 LSB 标准的头文件或库。在此环境中，`/usr/include`包含 LSB 头文件，`/usr/lib`包含 LSB 桩库。

为了生成虚拟环境，`lsb-build-chroot`使用绑定挂载而不是复制整个目录结构，因此磁盘空间需求最小。这也意味着在环境中进行更改（如编译二进制文件）会立即反映到环境外部，反之亦然。

你不需要 root 权限就可以使用`lsb-build-chroot`，因为它是在高端口上运行的`ssh`守护进程实现的。`ssh`守护进程将你的主目录绑定挂载到`chroot`环境中，因此你可以登录到受限环境进行编译。你还可以在`chroot`外部运行完整的编辑和调试环境，操作你在受限环境中编译的相同文件。

在应用程序需要针对不符合 LSB 标准的库进行编译或链接的情况下，你可以明确地将这些库和头文件导入`chroot`环境中。根据应用程序构建过程的复杂程度，你可能还需要将其他工具导入环境中，以便它们能够正确运行。

![](img/d75cffbcb54aabfb0f9854162061d394_207_0.png)

如果在`lsb-build-chroot`运行期间更新系统软件包，绑定挂载可能会引起问题。

简单示例。在示例 13.1 中，我们有一个源文件`hello_world.c`。

### 示例 13.1：`hello_world.c` 源文件

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[])
{
    printf("Hello World\n");
    exit(0);
}
```

首先，我们登录到受限环境（示例 13.2）。默认情况下，该环境的`sshd`守护进程监听 5436 端口。

### 示例 13.2：登录受限环境

```bash
$ slogin -p 5436 localhost
lsbdevchroot$ 
```

然后，我们可以像往常一样构建二进制文件（示例 13.3）。

### 示例 13.3：构建和运行二进制文件

```bash
lsbdevchroot$ gcc -Wall -o hello_world hello_world.c
lsbdevchroot$ ./hello_world
Hello World
lsbdevchroot$ 
```

在受限环境之外，如果需要，我们可以附加调试器。

### 13.3.3.2 lsb-build-cc

`lsb-build-cc`是`gcc`的封装程序，用于替代编译器调用。该封装程序会修改传递给实际编译器的参数，以确保您的应用程序使用 LSB 指定的头文件和库版本，而不是系统上安装的版本。但是，原生系统的完整功能可用于构建、开发和调试应用程序。要使用`lsb-build-cc`，可以使用示例 13.4 中显示的任意一个命令。

**示例 13.4：lsb-build-cc**

```bash
# CC=lsbcc ./configure
# CC=lsbccc ./configure (用于 C++)
```

或者

```bash
# CC=lsbcc make
# CC=lsbccc make (用于 C++)
```

有关使用`lsbcc`的更多信息，可以在`lsb-build-cc`软件包中提供的 man 页面中找到。

**简单示例。** 在示例 13.5 中，我们有一个源文件`hello_world.c`。

**示例 13.5：hello_world.c 源文件**

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    printf("Hello World\n");
    exit(0);
}
```

不直接调用`gcc`，而是使用`lsbcc`（示例 13.6）。

**示例 13.6：使用 lsbcc**

```bash
$ lsbcc -Wall -o hello_world hello_world.c
$ ./hello_world
Hello World
$
```

**提示。** 假设`myfunction()`是由`libc`提供的 ABI，并且它有不同的版本。如果`myapplication`使用了`myfunction()` ABI，我们可以比较应用程序和库映像，以查看实际使用的是哪个 ABI，如示例 13.7 所示。

**示例 13.7：测试 myapplication 与 glibc 的兼容性**

```bash
$ /usr/bin/objdump -T myapplication | grep myfunction
08048330 DF *UND* 00000032 GLIBC_2.0 myfunction

$ /usr/bin/objdump -T /lib/i686/libc.so.6 | egrep myfunction
000bb160 g DF .text 00000032 GLIBC_2.0 myfunction
000bb160 w DF .text 00000032 GLIBC_2.1 myfunction
```

`myapplication`使用的`myfunction()`的正确 ABI 应该是`GLIBC_2.0`，这样它将返回 double。库和操作系统允许演进，但 LSB 刷新频率较低，以提供稳定的运行时环境。

### 13.3.3.3 选择

表 13.1 解释何时使用`lsb-build-cc`以及何时使用`lsb-build-chroot`。

**表 13.1：使用 lsb-build-cc 和 lsb-build-chroot**

| 如果使用`lsb-build-cc`，当： | 如果使用`lsb-build-chroot`，当： |
| :--- | :--- |
| - 您的应用程序使用在`lsb-build-chroot`中不可用的工具或共享库。 | - 您的应用程序有硬编码的头文件和共享库路径。 |
| - 您的应用程序有与大多数 Linux 环境不同的测试脚本。 | - 您的应用程序在其`Makefile`中硬编码使用特定编译器。 |
| | - 需要使用 GCC 以外的编译器。 |

### 13.4 共享库

当应用程序使用不属于 LSB 编写规范的库时，可以通过两种方式之一进行构建。要么二进制文件静态链接到该库，或者如果该库符合 LSB 规范，则可以与二进制文件动态链接。如果是动态链接，则共享库必须与应用程序的其余部分一起提供。

要使共享库被视为符合 LSB 规范，其要求基本上与直接可执行程序的要求相同。也就是说，它必须仅使用规范支持的动态接口，或者由另一个随应用程序其余部分一起打包的符合 LSB 规范的共享库提供。

与普通的二进制文件类似，作为符合 LSB 规范的应用程序提供的共享库应该针对 LSB 头文件和桩库进行构建。

不要使用`ld`构建共享库（示例 13.8）。这可能会导致使用不属于 LSB 编写规范的符号版本。

![](img/d75cffbcb54aabfb0f9854162061d394_211_0.png)

如果您使用`lsb-build-cc`技术来构建应用程序，那么共享库也必须使用`lsbcc`进行构建（示例 13.9）。

![](img/d75cffbcb54aabfb0f9854162061d394_211_1.png)

如果您使用`lsb-build-chroot`技术来构建应用程序，则不需要对构建方法进行修改。

在链接应用程序时，如果您使用`lsbcc`，默认情况下只会动态链接 LSB 指定的库，即使搜索路径中同时存在静态库和共享库。可以通过设置环境变量`LSBCC_SHARED_LIBS`来修改此行为。其值是库名称的冒号分隔列表，指定哪些额外的库应该被动态链接。

如果您使用`lsb-build-chroot`，那么编译器将动态链接受限环境中可用的所有共享库，如果库仅存在静态版本，则回退到静态链接。

### 13.5 案例研究：RSYNC

`rsync`应用程序是 LSB 应用程序测试套件中的程序之一。我们将此程序作为开发人员可能遇到的问题类型以及如何尝试构建符合 LSB 规范的二进制文件时绕过这些问题的示例。

我们使用`rsync`版本 2.5.5 的`lsbCC`构建工具。`rsync`的源代码可以从`rsync`网站下载。³

### 13.5.1 使用`lsbCC`构建`rsync`二进制文件

首先，我们解压缩源代码并运行`configure`脚本（示例 13.10）。我们通过设置`CC`环境变量（而不是`cc`，因为`configure`默认可能会使用`cc`）来确保`configure`使用`lsbCC`作为编译器。
