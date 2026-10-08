

# 第 2 部分 | 分层安全与 Linux

## 配置 TrustedGRUB

如果你想配置一个利用本地系统 TPM 芯片的启动加载程序，可以考虑 TrustedGRUB。配置完成后，它可以成为所谓的“信任链”的一部分，用于验证启动过程中的重要部分。TrustedGRUB 并没有作为 Red Hat Enterprise Linux 5 或 Ubuntu Server Edition 的普通软件包提供。

然而，截至 2010 年初，已经可以直接从其开发者在 sourceforge.net/projects/trustedgrub/ 处获取 TrustedGRUB。IBM 的文档（http://publish.ibm.com/infocenter/linuxinfo/v3r0mol/index.jsp）中包含了一个使用该软件的安装过程。在进行任何更改之前，请务必按照之前的建议备份启动加载程序。

以下步骤实现在运行 Red Enterprise Linux 5 的服务器系统上部署 TrustedGRUB。编译编译此包时涉及的某些相关软件包稍后会被删除，以防止黑客利用它们。图中显示的一些脚本和编译命令可能需要几分钟（或更长时间）。类似的方法在其他 Linux 发行版上同样适用：

- 1. 从上述 http://sourceforge.net 网站的 SourceForge 项目区域下载最新版本的 TrustedGRUB。此处假设该包为 tar .gz 压缩格式。此类包俗称为 tarballs（tar 包）。

- 2. 解压并解压缩指定的软件包。例如，在此情况下，`tar xzf TrustedGRUB-1.1.4.tar.gz` 命令将解压并解压缩指定的归文件。文件将被加载到同名的目录中。

- 3. 在解压后的子目录下运行 `build_grub.sh` 脚本。如果你看到与 automake 和 autoconf 相关的错误信息，请安装 `automake`、`autoconf` 和 `gcc` 包及其依赖项。（如果你在基准主机上安装这些包，稍后可能需要删除它们，因为它们可能会帮助黑客创建更危险的恶意软件）。

- 4. 进入二级 TrustedGRUB 子目录。如果你在 root 用户的目录下下载了该 tar 包，路径将是 `/root/TrustedGRUB-1.1.4/TrustedGRUB-1.1.4/directory`。查看该目录下的 `INSTALL` 文本文件。你看到的任何指令都优于后续的任何说明。

- 5. 运行 `./configure` 命令设置已解压的代码。运行 `make` 和 `install` 命令来编译并安装代码。

- 6. 现在你可以准备好替换旧 GRUB 启动加载程序中的关键文件了。假设你的备份已就，这不应该让你感到害怕。在 `/boot/grub/` 目录下，删除该目录下的 `stage1`、`stage2` 和 `*.5` 文件。

- 7. 进入二级 TrustedGRUB 子目录。使用以下命令替换已删除的启动加载程序文件：

```
# cp stage1/stage1 /boot/grub/
# cp stage2/stage2 /boot/grub/
```

# 第 3 章 | 安全：通过启动过程实现

8. 要实施这些更改，需要在 GRUB 命令提示符处运行命令。以下命令假设 /boot 目录挂载在第一个硬盘的分区上：

```
# grub
grub> root (hd0,0)
grub> setup (hd0)
grub> quit
```

你应该能看到与 stage I 和 stage 2 启动加载程序相关的消息。不要担心与 stage 1.5 启动加载程序相关的消息。此外，如果 /boot 目录挂载在第二个硬盘的第三个分区上，则 grub> 提示符 处的命令将是 `(hd1,2)` 和 `setup (hd1)`。

9. 系统现在应该准备好重启了。确保备份已就绪，并在出现问题时准备好救援/恢复磁盘或 Live CD。

在未来的某个时刻，让 TrustedGRUB 成为由系统主板 TPM 芯片验证的信任链的一部分将变得更容易。到那时，这些软件包将出现在开源仓库中，可以在像 Red Hat 和 Ubuntu 发行的企业级发行版上进行标准安装。

菜单看起来与普通的传统的 GRUB 菜单没有太大区别。它也保留了传统 GRUB 配置文件 `/boot/grub/grub.conf` 中的选项。但通过 TrustedGRUB 和 TPM，你将对已启动的操作系统的完整性多进行一次检查。

## 标准内核的挑战

如果你在桌面电脑上运行 Linux，标准内核可能包含许多你不需要且永远不会使用的服务器相关功能。同样，如果你在服务器上运行 Linux，标准内核可能包含许多你不需要且永远不会使用的桌面相关功能。出于这些原因，Red Hat、Ubuntu 以及许多其他 Linux 发行版包含了一些经过定制的内核。

本节中关于标准内核的问题是多方面的：

- 你的系统可以安装哪些内核？
- 什么内核最适合你的需求？
- 什么时候该使用标准内核？

