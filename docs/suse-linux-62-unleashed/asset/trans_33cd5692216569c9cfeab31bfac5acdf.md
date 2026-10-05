
## 安装软件包

RPM 的主要用途之一是安装软件包。rpm 安装命令的通用语法如下：

```
rpm -i [options] [packages]
```

其中 `options` 可以是前面的常用选项之一，也可以是下列表涵盖安装选项之一，`packages` 是一个或多个 .rpm 软件包文件的名称。一些安装选项如下：

- -v 输出 rpm 正在执行的操作
- h 或 --hash 在安装包时打印 50 个哈希标记 (#)
- --percent 打印从包中提取的百分比
- --test 运行软件包安装过程，但不安装任何内容；主要用于检测冲突
- --excludedocs 防止安装标记为文档的文件（如 man 页面）
- --includedocs 强制安装标记为文档的文件；这是默认设置
- --nodeps 在安装包之前不进行依赖关系检查
- --replacefiles 允许用正在安装的包中的文件替换已安装的文件
- --replacepkgs 允许用正在安装的包替换已安装的包
- --oldpackage 允许用旧版本替换已安装的较新包
- --force 强制安装软件包

在给 rpm 提供选项时，无论何种模式，所有单字母选项都可以合并成一个块。例如，第一个命令（安装 `lx_suse.rpm` 文件中的 Linux 内核源码）与第二个命令等效：

```
# rpm -i -v -h lx_suse.rpm
```

等效于

```
# rpm -ivh lx_suse.rpm
```

然而，所有以 -- 开头的选项必须单独给出。

现在我们来看安装 RPM 软件包的几个示例。第一个示例是从包安装 teapot（一个电子表格编辑器）：

```
teapot.rpm
```

# SuSE 系统管理
第三部分

但请注意，SuSE Linux 并没有遵循 RPM 软件包的传统命名方式，格式为：

```
name-version-release.arch.rpm
```

其中 `name` 是包名，`version` 是包的版本，`release` 是包的发布级别，`arch` 是其所属的硬件架构，`rpm` 是默认扩展名。这种命名方案非常方便，因为仅通过名称就可以确定特定软件包的关键信息。不过，你可以使用本章稍后（“使用 YaST 命令管理软件”中讨论）的 `yast` 命令通过图形界面获取关键的包信息。

要手动安装 teapot 程序及其文档、man 页面和相关文件，你必须挂载你的 SuSE CD-ROM：

```
# mount /cdrom
```

接下来，输入 `cd` 进入 `/cdrom/SuSE/ap1` 目录。然后，在提示符 (#) 后输入以下命令安装 teapot：

```
# rpm -ivh teapot.rpm
```

当软件包安装时，输出如下：

```
teapot
################
```

安装完成后，会显示 50 个哈希标记。如果你尝试用 root 以外的用户安装此包，将生成类似下面的错误：

```
failed to open /var/lib/rpm/packages.rpm
error: cannot open /var/lib/rpm/packages.rpm
```

这是出于安全考虑。通常，除 root 外的其他用户对系统的 rpm 数据库没有读取或写入权限。如果你尝试安装系统中已经安装的包，你将得到以下（或类似的）错误：

```
package teapot-1.0-52 is already installed
```

要重新安装此包，请使用 `--replacepkgs` 选项：

```
# rpm -ivh --replacepkgs teapot.rpm
```

当你安装的包需要某些其他包才能正常运行时，有时会遇到依赖冲突。虽然忽略依赖问题通常不是一个好主意，但你可以使用 `--nodeps` 选项强制 RPM 忽略这些错误并安装包。

## 升级软件包

RPM 升级模式提供了将现有软件包升级到新版本的简单方法。升级模式与安装模式类似：

```
rpm -U [options] [packages]
```

`options` 可以是任何安装选项或通用选项。

升级软件包的一个示例是：如果系统当前运行 emacs 19.31 版本，需要升级到较新的 emacs 19.34 版本。为了升级，root 将使用以下命令：

```
# rpm -Uvh emacs-19.34-4.1386.rpm
```

升级模式是卸载和安装两个操作的结合。首先，rpm 卸载请求包的所有旧版本，然后安装新版本。如果不存在该包的旧版本，rpm 仅会安装请求的包。

与手动安装和卸载相比，使用升级的额外优势是升级会自动保存配置文件。出于这些原因，有些人倾向于在所有包安装时使用 upgrade 而不是 install。

## 卸载软件包

rpm --uninstall 模式提供了一种清理的方法，从多个位置删除属于软件包的文件。某些软件包的文件散落在文件系统的各个处，例如在 `/etc`、`/usr` 和 `/lib` 中。手动删除包的文件可能会很混乱，但通过 rpm，可以如下方式删除整个包：

```
rpm -e [options] [package]
```

`options` 是本节列出的选项之一，`package` 是要删除的包名。例如，要删除 DOSEMU 包，请使用以下命令：

```
# rpm -e dosemu
```

这里指定的包名只是包的名称，而不是用于安装该包的文件名。如果输入了以下命令：

```
# rpm -e dosemu.rpm
```

将生成以下错误：

```
package dosemu.rpm is not installed
```

尝试卸载包时遇到的另一个常见错误是依赖错误，当正在卸载的包包含另一个包所需的文件。例如，如果你尝试从系统中删除 `klibs` 包，你将得到以下错误：

```
error: removing these packages would break dependencies:
klibs is needed by kbase-1.1.1-20
```

这意味着如果删除了 `klibs` 包，`kbase` 包将无法正常工作。
