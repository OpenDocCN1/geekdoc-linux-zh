
虽然这些步骤是针对 XMS 的，但大多数其他软件包也遵循这些步骤——`configure`、`make` 和 `install`。`configure` shell 脚本会猜测系统相关的变量，并创建一个 `Makefile`，其中包含构建和安装软件所需的命令。

通常，除了输入构建软件的命令外，你不需要做任何其他事情，但你必须安装系统上的软件开发工具。在安装 Fedora Core 时，你必须安装软件开发软件包。为了构建和运行 XMS，你还必须安装 X 软件开发软件包，因为它是一个 X 应用程序。

要开始构建 XMS，请键入以下命令以运行 `configure` 脚本（键入此命令时，你必须位于 `xms-1.2.10` 目录中）：

```
./configure
```

`configure` 脚本开始运行，并在检查系统的各种功能时打印大量消息——从 C 编译器的存在到构建 XMS 所需的各种库。最后，`configure` 脚本创建一个 `Makefile`，你可以使用它来构建软件。

如果 `configure` 脚本显示错误消息并失败，请查看 `INSTALL` 和 `README` 文件以寻找解决问题的线索。你也许可以通过通过命令行参数向 `configure` 脚本提供某些信息来绕过它。

`configure` 脚本完成后，键入 `make` 来构建软件。此命令运行 GNU `make` 实用程序，该实用程序读取 `Makefile` 并根据 `Makefile` 中指定的信息开始编译源文件。`make` 命令遍历所有源目录，编译源文件，并创建运行 XMS 所需的可执行文件和库。随着每个文件被编译，你会看到大量消息滚动经过。这些消息显示了用于编译和链接文件的命令。

`make` 命令可能需要 10 到 15 分钟才能完成。`make` 完成后，你可以使用以下命令安装 XMS 软件：

```
make install
```

此命令也运行 GNU `make`，但 `install` 参数指示 GNU `make` 执行 `Makefile` 中的一组特定命令。这些指令基本上遍历所有子目录，并将各种文件复制到其最终位置。例如，二进制可执行文件 `xms`、`gnomexms`、`wmxms` 和 `xms-config` 复制到 `/usr/bin` 目录。

既然你已安装了 XMMS，请尝试通过键入 `xmms` 或在终端窗口中选择主菜单 > 声音与视频 > 音频播放器，从 GNOME 或 KDE 桌面运行它。XMMS 已随 Fedora Core 提供，但现在你获得了 XMMS 的新版本（区别在于新构建的版本可以在没有任何附加组件的情况下播放 MP3 文件）。从 XMMS 窗口，按 L 键打开加载文件对话框，并选择一个 MP3 文件进行播放。你的 PC 必须有一个声卡，并且声卡必须正确配置，XMMS 才能工作。图 4-1 显示了 XMMS 播放 MP3 音乐片段的典型视图。

![](img/9f89727199836b0f871f1745838aa8b2_499_0.png)

以下是下载、解包、构建和安装典型软件包步骤的概述：

- 1. 使用 Web 浏览器从匿名 FTP 站点或 Web 站点下载源代码，通常以 .tar.gz 文件的形式。
- 2. 使用 `tar zxvf filename` 命令解包文件。
- 3. 使用诸如 `cd software_dir` 之类的命令更改目录到软件解包后的新子目录。
- 4. 阅读任何 README 或 INSTALL 文件，以了解构建和安装软件时必须遵循的任何特定说明。
- 5. 构建软件的细节可能因软件包而异，但通常你键入以下命令来构建和安装软件：
  - `./configure`
  - `make`
  - `make install`
- 6. 阅读随软件提供的任何其他文档，以了解如何使用该软件以及在使用前是否必须进一步配置该软件。

## 安装 SRPMS

如果你有 Fedora Core 的源光盘（你可以从 *fedora.redhat.com/download/mirrors.html* 列出的站点之一下载源 CD 镜像），你可以直接从源文件安装源文件并构建各种应用程序。Red Hat 提供源代码文件为 RPM 包，就像可执行二进制文件一样，这些源 RPM 文件通常被称为 SRPMS（*即源 RPM*）。

要安装特定的源 RPM 并构建应用程序，请遵循这些步骤：

- 1. **通过键入 `mount /mnt/cdrom` 或等待 GNOME 桌面自动挂载 DVD 来挂载 DVD-ROM。**
- 2. **通常源 RPM 位于 SRPMS 目录中。通过键入以下命令更改到该目录：**
  - `cd /mnt/cdrom/SRPMS`
- 3. **使用 `rpm -i` 命令安装源 RPM 文件。例如，要安装 Web 服务器（`httpd`）的源，请键入：**
  - `rpm -ivh httpd*.src.rpm`
  - 文件安装在 `/usr/src/redhat/SOURCES` 目录中。带有 `.spec` 扩展名的 spec 文件被放置在 `/usr/src/redhat/SPECS` 目录中。*spec 文件*描述了软件，并包含用于*构建*和安装软件的信息。
- 4. **使用 spec 文件和 `rpmbuild` 命令来构建软件。** 通过为 `rpmbuild` 命令使用不同的选项，你可以执行从解包源文件到构建和安装二进制文件的各项不同任务。例如，要处理*整个* spec 文件，请键入：
  - `rpmbuild -ba packagename.spec`
  - 这里 *packagename* 是 SRPM 的名称。此命令通常构建软件并安装二进制文件。

## 使用 Up2date 更新 Fedora Core 应用程序

Fedora Core 附带 Up2date——一个图形化更新代理，它可以下载你的系统所需的任何新 RPM 文件并为你安装这些文件。我简要概述了如何使用 Up2date 更新系统。Up2date 也被称为 Red Hat 更新代理，因为 Red Hat 为其 Red Hat Network（Red Hat 通过该网络向其商业客户提供服务）开发了该代理。

要使用 Up2date 更新软件包，请遵循这些步骤：

- 1. **以 *root* 身份登录，并选择 *主菜单：* **系统工具：** *Red Hat Network*。你也可以在终端窗口中键入 *up2date*。

Red Hat 更新代理启动，如果你首次使用 Up2date，对话框会提示你在你的 GPG 密钥环中安装公钥。(*GPG* 指 GNU Privacy Guard 或 GnuPG，一个使用 OpenPGP Internet 标准加密、解密和签名电子邮件及其他数据的程序。)该公钥 GPG 密钥验证包开发者是否已安全地签署了 Up2date 下载的软件包。如果提示这样做，点击 **Yes**（是）安装公钥。

- 2. Up2date 显示一个带有欢迎信息的窗口。点击 **Forward**（下一步）按钮继续。

- 3. Up2date 显示一个它称之为通道（channels）的列表——代理从中下载软件包头信息的仓库。点击 **Forward**（下一步）继续。

默认情况下，更新代理使用与 *Yum* 一起工作的通道——我将在下一节描述的命令行软件包更新/安装工具。通道在文本配置文件 */etc/sysconfig/rhn/sources* 中识别。除了 *Yum*，Up2date 还可以访问专为 Apt（另一个软件包更新器）准备的仓库。

点击 **Forward**（下一步）后，Up2date 确定需要更新的内容，并检索指定通道的全部头信息列表。

- 4. Up2date 下载头信息后，它显示软件包列表。然后你可以滚动列表并选择你想更新的软件包；点击软件包名称左侧的复选框以选择它。点击 **Forward**（下一步）继续。

然后 Up2date 检查任何软件包依赖关系并开始下载软件包。进度条显示下载状态。

- 5. 下载完成后，点击 **Forward**（下一步）按钮继续安装。

- 6. Up2date 安装每个软件包更新时显示进度条。安装完成后，点击 **Forward**（下一步）按钮。

Up2date 显示一条消息，关于它成功安装的软件包。

- 7. 点击 **Finish**（完成）按钮退出 Up2date。

### 使用 Yellow dog Updater, Modified (Yum)

Yellow dog Updater, Modified (Yum) 是一个用于更新以及安装和移除 RPM 软件包的命令行实用程序。Yum 从指定的 Web 站点下载 RPM 软件包头，然后使用 `rpm` 实用程序来确定
