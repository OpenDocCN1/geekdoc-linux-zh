

在 `/usr/src/linux-2.4` 目录下运行补丁，因此应该使用以下命令：

```
cat patchfile.txt | patch -p3
```

由于 `-p1` 移除了第一个 `/`，因此该补丁将以不带路径名的方式应用。接着，`-p2` 选项移除了 `usr/`，最后，`-p3` 选项移除了 `/linux` 部分。

此外，如果您正在修补内核源代码，并且补丁文件是 gzip 格式的压缩文件（例如 `patch.gz`），您可以在不解压缩的情况下应用该补丁：

```
zcat patch.gz | patch -p0
```

如果您使用 bzip2 格式作为压缩补丁文件（例如 `patch.bz2`），可以以类似的方式使用 `bzcat` 命令：

```
bzcat patch.bz2 | patch -p0
```

## 获取内核源代码

当您决定下载 Linux 内核的源代码时，务必从您的发行版供应商处获取（例如 Red Hat 的源 `.rpm` 文件），或者从 http://www.kernel.org 网站获取。

验证内核源代码的完整性也至关重要，请小心下载该包的 gpg 或 PGP 签名文件，或使用 `md5sum` 实用工具检查 MD5 校验和。

要验证补丁文件的 MD5 校验和，请使用此命令：

```
md5sum patchfile.gz
```

这将返回类似以下的输出：

```
045d532750c91f05261e0012d5491792 patch.gz
```

要验证补丁文件的 gpg 签名，首先下载与补丁代码版本号匹配的 `patch.bz2.sign` 文件。www.kernel.org 网站在补丁下方或旁边列出了相应的签名文件。然后使用此命令验证代码：

```
gpg --verify patch.bz2.sign patch.bz2
```

这将返回类似以下的输出：

```
gpg: Signature made Fri 02 Aug 2002 06:43:54 PM EDT using DSA key ID
2517D0F0E
gpg: Good signature from "Linux Kernel Archives Verification Key <ftpadmin@kernel.org>"
gpg:    aka "Linux Kernel Archives Verification Key
<ftpadmin@kernel.org>"
```

> 如果您看到关于信任路径问题的警告，可以安全地忽略它。这是根据 kernel.org 的说明，可在 http://www.kernel.org/signature.html 找到。

> 您可能会看到关于使用 gpg 签名或 md5 校验和验证内核源代码的问题。下载相关文件并阅读 man 手册页，以确保您理解了我们所涵盖的内容。

## 配置内核

确定即将编译的新内核中哪些内容将被包含或排除，主要有三种方法。以下命令在内核源代码的顶层目录中运行，每个选项都是 `make` 命令的一个参数：

- `make config`——包含大量是/否问题。这是一种基于文本的、非常简单且令人痛苦的内核配置方式，因为错误会导致您重新开始流程。
- `make menuconfig`——包含一个基于文本的选项菜单，导航起来 surprisingly（ surprisingly easy，意即“出奇地容易”）容易。
- `make xconfig`——基于 X 和 GUI，这是适合正在康复中的 MCSE 人群或审美导向人士的选择。

> 我不会详细讨论 `make config` 选项，因为它已过时，其功能完全被更友好的实用程序所涵盖。

### make menuconfig

在配置编译内核中将包含或不包含哪些选项时，了解那些小括号和字符的含义很重要。特别是在 `menuconfig` 命令中，如图 14.2 所示，这一点尤为重要。

## 内核配置与自定义编译

![](img/49f4f38f3aec011238fa50f89e643db3_394_0.png)

**图 14.2 menuconfig 命令。**

图 14.2 显示了图例选项。列表项对这些选项进行了更详细的说明。

- `[]-` 方括号表示开/关切换选项。按空格键会在括号中插入一个星号，标记此选项为开启状态，或将其编译到内核中。
- `[ *] - ` 这是一个已开启的切换选项。
- `< > ` - 大于号/小于号括号表示一个可以开启（`<*>`）或关闭（`< >`）或设置为支持模块（`<M>`）的选项，具有三态切换功能。

尝试这些选项，切换各种选择的开和关；退出而不保存您的配置文件。

> **注意**
>
> 唯一有效的内核参数配置命令是 `make config`、`make menuconfig` 和 `make xconfig`。通常的 `.configure` 以及您在本次会话中未使用的其他任何内容都只是干扰项。

### make xconfig

内核配置命令中最图形化的是 `xconfig` 命令。（实际上，这些并不是真正的实用程序或命令，而是内核 makefile 中的目标——请配合一下。它的界面类似于 `menuconfig` 命令，但视觉上更令人愉悦，如图 14.3 所示。）

![](img/49f4f38f3aec011238fa50f89e643db3_395_0.png)

**图 14.3 `xconfig` 命令。**

如图 14.3 所示，编译项的包含、排除甚至作为模块可用的选项被简化为一组单选按钮并提供给用户。此命令可能是重新配置或设置内核选项的最简单方法。

保存您的内核配置文件很重要。当您完成各种命令后，系统会询问您是否要保存配置文件，如果您准备好编译，当然会保存。

> 内核唯一的配置文件是由 `make config`、`menuconfig` 和 `xconfig` 目标生成的 `.config` 文件。诸如用于配置日志记录的 `kernel.conf` 之类的文件对内核无效。
>
> 在 Red Hat 系统上，完成配置后，`.config` 文件位于 `/usr/src/linux-2.4` 目录中，其他发行版可能有所不同。

## 编译内核的步骤

文档化内核重新编译的过程以便适用于所有机器是非常困难的，比其他任何过程都更甚。步骤集很长，与其试图让它在每台奇怪的机器上都工作，我们更倾向于追求理解以及考试要点。

> 作者在许多不同的机器上成功运行过此过程数百次，因此他非常清楚试图提供一套通用步骤的潜在陷阱。

要开始编译，您必须位于内核源代码的根目录中，通常是 `/usr/src/linux` 或 `/usr/src/linux-2.4`（对于 2.4 内核）。您应该将此复制到一个新的树中，保持原始树不受实验影响：

1. 使用以下命令将 `/usr/src/linux-2.4` 树复制到一个名为 `/usr/src/linux-2.4-lpic` 的新树中：
   ```
   cp -r /usr/src/linux-2.4 /usr/src/linux-2.4-lpic
   ```
2. 进入 `/usr/src/linux-2.4-lpic` 目录。
3. 运行 `make menuconfig` 命令。
4. 导航到 **File Systems**（文件系统）菜单选择并按 Enter 键。

> **注意**
> 您只需要更改几样东西。这些项目本身无关紧要——重点在于执行这些操作并重新编译内核。

5. 将光标移动到 **Minix fs Support**（Minix 文件系统支持）选择上，并按空格键两次以取消选择，或者按任意次直到 `< >` 括号为空。
6. 按 `Esc` 键直到返回主菜单。
7. 导航到 **Amateur Radio Support**（业余无线电支持）选择并按 Enter 键。
8. 通过按空格键直到 `[ ]` 括号为空，取消选择 **Amateur Radio Support**（业余无线电支持）以完全关闭它。
9. 按 `Esc` 键直到返回主菜单。
10. 使用左或右箭头键导航到 `< Exit >`（退出）选择并按 Enter 键。
11. 当询问是否要保存您的新内核配置时，点击 **Yes**（是）并按 Enter 键。
12. 忽略运行 `make dep` 命令的说明。相反，使用以下命令确认当前目录中存在 `.config` 文件：
    ```
    ls -a .config
    ```
    这将返回类似以下的输出：
    ```
    -rw-r--r-- 1 root root 36157 Apr 8 17:56 .config
    ```

