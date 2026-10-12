
# 附录 B：安装 Fedora

## 创建用户账户

这可能是您在安装过程中完成的最任务之一。在登录 Fedora 时，创建并使用普通用户账户极其重要。否则您将被迫使用 root 账户，该账户仅用于系统管理。

您看到如图 B-28 所示的屏幕时，填写用户名。最好使用简单的名称，例如您的名字，或者名字的首字母加上姓氏（中间不要留空格）。在本文示例中，我们选择了 `carlotta` 这个名字。

然后输入您的全名，在我们的示例中为 `Carlotta Tendant`。输入两次密码。关于选择良好密码的提示，请参阅本章节前面的“设置 root 密码”部分。

此用户账户是您每次登录 Fedora 时应该使用的账户。

点击“下一步”按钮继续。

![](img/67d9607982940021da1fe4247b9b224c_232_0.png)

**图 B-28：**用户账户

## 检查您的声卡

此时，Fedora 应该已经检测到系统中可能存在的任何声卡。示例见图 B-29。如果 Fedora 检测到声卡，它将向您显示一个“播放测试音”的按钮。点击此按钮听测试音（取决于您声学系统的设置，您可能需要调整任何外部音量控制）。

### 声卡

您的计算机上检测到一张声卡。

点击“播放声音”按钮听示例声音。您应该听到一系列三个声音。第一个声音在右声道；第二个声音在左声道，第三个声音在中心。

- 厂商：VIA Technologies
- 模型：VT82C66B AC97 Audio Controller
- 模块：`vt82c66_audio`

![](img/67d9607982940021da1fe4247b9b224c_233_0.png)

图 B-29：声卡

声音播放，Fedora 将询问您是否听到了测试音（见图 B-30）。如果听到了请点击“是”，如果没有则点击“否”。如果没有听到声音，请参阅附录 C 获取有关如何重新配置声学设置的提示。

![](img/67d9607982940021da1fe4247b9b224c_233_1.png)

图 B-30：听到声音了吗？

点击“下一步”继续。

## 加额外的 CD

Fedora 将询问您是否有任何额外的 CD 需要安装（见图 B-31）。您不太可能。但如果有，请现在插入它们并点击“安装”按钮，然后按照该特定 CD 的说明操作。完成后点击“下一步”。

### 额外的 CD

如果您有列出的任何 CD，可以通过安装 CD 并点击相应的按钮来安装软件包。

![](img/67d9607982940021da1fe4247b9b224c_234_0.png)

图 B-31：额外的 CD

## 完成安装

就是。您应该看到“完成安装”屏幕。点击“下一步”按钮，Fedora 将启动并向您显示一个新的登录界面，您可以使用章节前面“创建用户账户”步骤中创建的用户登录。

## Fedora 安装故障

本附录讨论了一些常见的安装问题及其解决方案。

### 无法启动 Fedora

如果您无法启动 Fedora，后续章节将帮助您解决问题。

### 无法从 CD-ROM 启动？

如果您无法从 Fedora CD-ROM 启动，您有两个选择：

- 修改您的 BIOS 顺序，使从 CD-ROM 启动被识别为第一启动顺序
- 使用您创建的启动盘

在某些情况下，系统 BIOS 不允许 Fedora CD-ROM 启动，因为 CD-ROM 上的启动镜像的大小。在这种情况下，应该制作启动盘来启动。

## 进入图形化安装

某些显卡无法与安装程序正常工作。最终结果是进入图形化安装的问题。如果安装程序无法使用默认设置运行，它将尝试以较低分辨率模式运行。

如果您无法以 800 x 600 运行显卡，请在 `boot:` 提示符处输入 `lowres` 以 640 x 480 运行安装程序。

# 附录 C：Fedora 安装故障排除

如果网卡在启动过程中没有初始化，安装程序将无法让您在安装期间或之后配置网络。

检查 `http://hardware.redhat.com/hcl/` 上的硬件兼容列表，查看您的网卡是否兼容并受支持。如果您的卡未列在其中，它可能与 Fedora 不兼容。

## 其他分区问题？

如果你正在使用 Disk Druid 创建分区，但无法进入下一个屏幕，可能由于你没有创建满足 Disk Druid 依赖项所需的所有分区。

你至少必须拥有以下分区：

- 类型为 Linux native 的 `/boot` 分区
- 类型为 Linux native 的 `/` (root) 分区
- 类型为 Linux swap 的 swap 分区

在定义分区类型为 Linux swap 时，你不需要分配挂载点，因为交换分区是不挂载的。

### 你是否看到了 Python 错误？

在 Fedora 的某些升级或安装过程中，安装程序（也称为 Anaconda）可能会因 Python 或回溯（traceback）错误而失败。该错误可能在选择软件包之后或尝试在 `/tmp` 中保存升级日志时发生。错误可能类似于所示：

```
Traceback (innermost last):
  File "/var/tmp/anaconda-7.1//usr/lib/anaconda/iw/progress_gui.py"
    line 20, in run
    rc = self.todo.doInstall ()
  File "/var/tmp/anaconda-7.1//usr/lib/anaconda/todo.py"
    line 1468, in install
    self.fstab.savePartitions (
  File "fstab.py", line 221, in savePartitions
    sys.exit(0)
SystemExit: 0
```

```
Local variables in innermost frame:
  self: <fstab.Guistab instance at 8446fe0>
  sys: module 'sys' (built-in)>
  Todo object:
    (Itodo)
    Todo
    p1
    (dp2)
    Smethod'
    p3
    (image)
    CdrominstallMethod
    p4
    (dp5)
    SprogressWindow'
    p6
```

<failed>

## 附录 C：Fedora 21 安装故障排除

此错误发生在某些系统中，其中指向 `/tmp` 的链接指向其他位置或自创建以来已被更改。这些符号链接或更改后的链接在安装过程中是无效的，因此安装程序无法写入信息并失败。

如果你遇到此错误，首先尝试下载 Anaconda 的任何错误更正（errata）。你可以在 Fedora 项目网站找到错误更正：`http://fedora.redhat.com/`。你也可以搜索该问题的 bug 报告。要搜索 Red Hat 的 bug 跟踪系统，请访问 `http://bugzilla.redhat.com/bugzilla`。

## 安装后的问题

如果你在安装 Fedora 后遇到问题，以下章节将帮助你排排除故障。

## 图形 GRUB 屏幕问题
