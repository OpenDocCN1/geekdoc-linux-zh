
当 `wine.conf` 设置完成后，你的 PC 就准备好运行 Wine 了。为了测试你的安装，你应该尝试运行一个在 Wine 中运行良好的已知程序，例如随 Windows 捆绑的标准 Microsoft Paint 程序：

When the `wine.conf` settings are complete, your PC is ready to run Wine. To test your installation, you should try to run a program known to work well in Wine, such as the standard Microsoft Paint program bundled with Windows:

1. Open a new command terminal in Linux.

2. 在 Linux 中打开一个新的命令终端。

3. Using the instructions in Chapter 9, use `vmware-mount.pl` to mount your Windows virtual disk on `/mnt/vhd` in your Linux file system.

4. 按照第 9 章中的说明，使用 `vmware-mount.pl` 将你的 Windows 虚拟磁盘挂载到 Linux 文件系统中的 `/mnt/vhd`。

5. Open another command terminal because the first one will be busy running `vmware-mount.pl`.

6. 再打开另一个命令终端，因为第一个终端会忙于运行 `vmware-mount.pl`。

7. If you have a standard Windows installation, Paint is likely located at `/mnt/vhd/Program Files/Accessories/mspaint.exe`, but you might want to browse through the virtual disk to verify the path.

8. 如果你有标准的 Windows 安装，Paint 很可能位于 `/mnt/vhd/Program Files/Accessories/mspaint.exe`，但你可能想浏览虚拟磁盘以验证路径。

9. At the command terminal, type `wine "/mnt/vhd/Program Files/Accessories/mspaint.exe"`. Substitute the correct path if you discover `mspaint.exe` is located elsewhere on your Windows virtual disk.

在命令终端中，输入 `wine "/mnt/vhd/Program Files/Accessories/mspaint.exe"`。如果发现 `mspaint.exe` 位于 Windows 虚拟磁盘上的其他位置，请替换为正确的路径。

> Capitalization and the use of quotation marks are very important. Any time you run a program inside a Windows directory that uses spaces, you need to encompass the entire pathname in quotes.

> 大小写和引号的使用非常重要。只要你在包含空格的 Windows 目录中运行程序，就需要用引号将整个路径名括起来。

10. Don't get discouraged if you see error messages: they're not uncommon, and not all error messages prevent the program from running properly. Because Wine is so developer-focused, it includes a lot of debugging messages.

11. 如果看到错误消息，不要气馁：这种情况并不少见，而且并非所有错误消息都会阻止程序正常运行。由于 Wine 非常注重开发人员，它包含大量调试消息。

12. After a short wait (it can be a minute or more, depending on the speed of your system), you should see the very familiar Microsoft Paint program appear, as it does in Figure 16.7. You can draw, rotate, color, and load and save files.

13. 等待片刻后（可能需要一分钟或更长时间，具体取决于你的系统速度），你应该会看到非常熟悉的 Microsoft Paint 程序出现，如图 16.7 所示。你可以绘制、旋转、上色以及加载和保存文件。

14. When you're finished, simply quit the program. Wine will exit, leaving you free to test another Windows program or move on to another project.

完成后，只需退出程序即可。Wine 将退出，让你自由测试另一个 Windows 程序或进行其他项目。

![](img/b2b6702758c230ce537468351fc8af15_339_0.png)

![](img/b2b6702758c230ce537468351fc8af15_340_0.png)

虽然 Wine 相比加载 VMware 确实能节省一些 RAM，但它仍然需要占用你系统内存中相当可观的一部分。运行 Paint 需要 35MB 内存！（其中大部分是 Wine 仿真层。）随着 Wine 的成熟和调试代码被移除，这种沉重的内存占用可能会略有下降。

Wine 的工作方式确实存在一些怪异之处。正如你已经了解到的那样，它并不是生产质量的软件，错误、调试信息以及通常不可预测的行为在现阶段必须被视为理所当然。

Wine 可以在多种方式下让你的 Windows 程序卡住，而无论发生什么情况，你都需要知道如何重新获得控制权。在最简单的情况中，程序只是没有按你预期的方式运行，但它并没有崩溃。你可以通过尝试以不同方式完成任务来取得成功——使用按钮而不是菜单项，改变步骤的顺序，或尝试更新版本的 Wine。对 Wine 进行调整以使其正确运行复杂程序，有一种特定的黑魔法。

不过，当 Wine 或 Windows 程序崩溃时，事情才真正变得有趣起来。在最简单的情况中，Wine 会将机器状态打印到你的终端中，并让你进入 Wine 调试器，该调试器会作为新的提示符出现在你用于启动 Wine 的终端内。这不是问题——只需输入 `quit` 即可退出。

其他崩溃则更难处理。如果 Windows 程序最大化自身占据整个屏幕然后冻结，你该怎么办？你的窗口管理器

## Chapter 16: Using Wine with VMware

可能无法拯救你，因为 Wine 可以充当自己的窗口管理器。也就是说，关闭、最小化或切换窗口可能无法实现。在这种情况下，返回到控制台（`Ctrl+Alt+F1` 或 `Ctrl+Alt+F2` 应该可以），登录，然后输入 `killall wine`。Wine 应该会退出并带走它那病态的程序，留下你的 X 会话完好无损。在大多数系统上，按 `Alt+F7` 将带你返回 XWindows。

Wine 可追溯至 1993 年，当时 Windows 3.1 是主流。虽然其功能集已扩展到包含 Windows 95/98 的新功能和功能以及其外观和感觉，但 3.1 的一些遗留问题仍然存在。例如，最小化一个 Wine 应用程序会在你的桌面上创建一个小图标，即使你使用的是对最小化程序处理方式不同的窗口管理器（例如屏幕底部 Windows 95 风格的任务栏）。

鉴于我对 Wine 给予了大量健康剂量的警告和不确定性，它可能听起来并不那么诱人。我只是想让你为此做好准备，尽管它提供了很大的希望，但目前它应仅保留用于特殊、非必要的任务。

Wine 的开发前景实际上看起来相当光明。Corel 为移植 WordPerfect Office 而必须做出的许多改进尚未被纳入 Wine 源代码中，但一旦被纳入，它应该为 Wine 开发者和最终用户打开新的可能性。

目前，请将 Wine 视为你的 Windows 兼容性拍苍蝇拍：如果你的问题只是像图 16.8 所示搜索外星生命这样的小麻烦，你可能并不总是需要动用 VMware 这把大锤。

![](img/b2b6702758c230ce537468351fc8af15_341_0.png)

## Chapter 17: Emulating the Macintosh
