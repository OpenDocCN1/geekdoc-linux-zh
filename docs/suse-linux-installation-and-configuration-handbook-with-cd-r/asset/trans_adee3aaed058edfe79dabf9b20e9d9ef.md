

## FIGURE 8.8

内核的基于菜单的配置实用程序组织得非常好。

![](img/659f91d9da7b29976c0625e2e9628511_196_0.png)

这个程序非常容易使用。你使用方向键在菜单中导航，按 Enter 键进入子菜单，并使用高亮的字母作为导航快捷方式。例如，你可以通过按 L 键然后按 Enter 来进入可加载模块支持页面。要退出菜单并返回上一级，按两次 Esc 键。

在选择组件时，按 Y 包含该组件，N 排除它，M 将其作为模块包含。你也可以使用空格键在这些选项之间循环，而不是使用相应的字母。带有 <> 的组件可以制作为模块。[*] 或 <*> 表示该组件将内置于内核中，<M> 表示该组件将作为模块构建，而 [ ] 表示该组件将不被构建。

当你通过此程序完成内核配置后，从主菜单中选择 Exit。程序会询问“Do you wish to save your new kernel configuration?”；选择 Yes。现在你就可以编译内核了。为此，你需要在正确的顺序中执行几个命令。你可以一个一个输入，也可以将它们全部放在一行中用分号 (;) 分隔，然后等待完成。正确的顺序命令如下：

- **make dep**—此命令检查你是否拥有编译内核所需的所有文件。
- **make clean**—此命令删除之前编译的所有痕迹。它会减慢编译过程，但能确保基于 solely 你的配置的干净内核。
- **make bzImage**—此命令编译实际的内核。
- **make bzlilo**—此命令将内核安装为默认内核。请谨慎使用！如果你不确定是否要安装此内核，不要运行它。继续阅读以了解如何为测试目的安装新内核。
- **make modules**—如果你有一些组件是模块，则需要运行此命令来编译它们。
- **make modules_install**—如果你有模块，运行此命令来安装它们。

或者作为一行命令，输入以下内容：

```
root@linux:/usr/src/linux > make dep; make clean; make bzImage; make bzlilo;
make modules; make modules_install
```

现在可能是你去倒杯咖啡的好时机，因为这是一个漫长的过程。根据你的硬件配置，可能需要七分钟到一个多小时。当它完成时，如果你已执行 make bzImage 命令，则需要重新启动才能加载新内核。否则，继续阅读以了解如何在将其作为默认安装之前测试新内核。

## Running the Text-Based Kernel Configuration Utility

最后但并非最不重要的一点是，你学习如何使用古老的内核配置方法，即基于文本的实用程序。按照以下步骤操作：

- 1. 你需要做的第一件事是确保你以 root 身份运行。你可以通过以 root 身份登录，或者如果你已作为普通用户登录，则通过运行命令 su 并输入 root 密码来切换到 root，如以下示例所示：
```
crash@linux:~ > su
```
- 2. 在以下提示符下输入你的密码：
```
root@linux:/home/crash >
```
- 3. 现在你已是 root，有权限运行配置实用程序。为此，使用以下命令将当前路径更改为内核目录：
```
root@linux:/home/crash > cd /usr/src/linux
root@linux:/usr/src/linux >
```
- 4. 输入运行该实用程序的命令：
```
root@linux:/usr/src/linux > make config
```
- 5. 此过程耗时较长。你会被以问答形式呈现内核的每个选项，可用选项在括号中。例如：
```
* Code maturity level options
  * Prompt for development and/or incomplete code/drivers (CONFIG_EXPERIMENTAL)
[Y/n/?]
```
在此示例中，询问你是否希望被提示开发和/或不完整的代码/驱动程序。你有以下选项：Y 表示是，现在的默认值；n 表示否；? 表示该选项的帮助。
- 6. 通过回答问题继续配置内核。

完成后，通过按正确顺序执行几个命令继续编译内核。你可以一个一个输入，也可以将它们全部放在一行中用分号 (;) 分隔，然后等待完成。正确的顺序命令如下：

- **make dep**—此命令检查你是否拥有编译内核所需的所有文件。
- **make clean**—此命令删除之前编译的所有痕迹，这会减慢编译过程，但能确保基于 solely 你的配置的干净内核。
- **make bzImage**—此命令编译实际的内核。
- **make bzlilo**—此命令将内核安装为默认内核。请谨慎使用！如果你不确定是否要安装此内核，不要运行它。继续阅读以了解如何为测试目的安装新内核。
- **make modules**—如果你有一些组件是模块，则需要运行此命令来编译它们。
- **make modules_install**—如果你有模块，运行此命令来安装它们。

或者作为一行命令，输入以下命令：

```
root@linux:/usr/src/linux > make dep; make clean; make bzImage; make bzlilo;
make modules; make modules_install
```

现在可能是你去倒杯咖啡的好时机，因为这是一个漫长的过程。根据你的硬件配置，可能需要七分钟到一个多小时。当它完成时，如果你已执行 make bzlilo 命令，则需要重新启动才能加载新内核。否则，继续阅读以了解如何在将其作为默认安装之前测试新内核。

## Testing a Kernel Before Installing It

这是一个重要问题，因为如果你不确定新内核是否能正确启动，就没有必要在未先测试的情况下将其安装为默认内核！这实际上是一个简单的过程。不要执行 make bzlilo 步骤，而是将其替换为 make bzdisk 并确保你的 A: 驱动器中有软盘。

这将把内核安装到磁盘上以便你可以测试它。重新启动计算机，它将从该磁盘启动。如果一切顺利且内核运行正常，你可以通过运行 make bzlilo 来安装它。如果出现问题，取出磁盘并重新启动计算机以启动旧内核。

但如果没有磁盘驱动器怎么办？没问题——你可以配置 LILO 以启动多个内核。跳过 make bzlilo 步骤并使用 YaST 设置 LILO 以具有加载测试内核的选项。以 root 身份运行 YaST：

```
root@linux:/ > yast
```

接下来，从菜单中选择 System Administration, Kernel and Boot Configuration, LILO Configuration。或者，要直接进入 LILO 配置，可以这样运行 YaST：

```
root@linux:~> yast --mask lilo
```

现在你准备好配置 LILO 了（见 Figure 8.9）。按照以下步骤操作：

FIGURE 8.9
使用 YaST 配置 LILO 非常容易。

![](img/659f91d9da7b29976c0625e2e9628511_199_0.png)

- 1. 你需要做的第一件事是为测试内核创建新的配置。按 F4。
- 2. 对于配置名称，输入 test 并按 Tab 移动到下一个字段。
- 3. 选择 Boot Linux 作为 Which Operating System 选项。YaST 然后应自动在 (Root) Partition to Boot 选项中填入正确的分区；只需检查以确保。
- 4. 对于 Kernel to be Booted by LILO Option，按 F3 以获取文件选择框。
- 5. 浏览到 /usr/src/linux/arch/i386/boot/ 并选择 bzImage（见 Figure 8.10）。

FIGURE 8.10
选择要启动的内核。

![](img/659f91d9da7b29976c0625e2e9628511_199_1.png)

- 6. 保存并退出。
- 7. 你现在应该有一个名为 test 的新条目。按 Enter 保存 LILO 配置并退出。

