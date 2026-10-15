
## 安装 PuTTY

- 4. 在下载页面向下滚动直到找到 `Windows (仅限 x86)`。
- 5. 将 `putty-setup.exe` 保存到磁盘。
- 6. 启动安装。
- 7. 出现安装向导。点击 `Next`（下一步）。
- 8. 出现选择安装文件夹。点击 `Next`（下一步）。
- 9. 出现选择快捷方式文件夹。点击 `Next`（下一步）。
- 10. 如果需要，勾选“Create a desktop shortcut”（创建桌面快捷方式）。点击 `Next`（下一步）。
- 11. 出现开始菜单文件夹。点击 `Next`（下一步）。
- 12. 出现准备安装界面。点击 `Next`（下一步）。
- 13. 出现完成设置界面。点击 `Next`（下一步）。
- 14. 出现完成界面。点击 `Finish`（完成）。

现在有了 PuTTY，你可以随时启动安全外壳连接，为 VNC 流量创建隧道。首先，我们需要调整 `linserv1.corp.com` 上的防火墙，以确保允许 `ssh` 流量。VNC 通常通过端口 `5900` 进入系统，但通过隧道时，它到达 `ssh` 端口，即端口 `22`。如果无法在端口 `22` 上建立 `ssh` 连接，就无法建立隧道。

按照以下步骤在 `linserv1.corp.com` 的 Fedora 防火墙上允许 `ssh` 流量：

- 1. 选择 `Applications`（应用程序）> `System Settings`（系统设置）> `Security Level`（安全级别）。
- 2. 勾选 `Trusted Services`（信任服务）下的“`ssh`”框框。
- 3. 点击 `OK` 完成调整。当提示确认时，点击 `Yes`（是）。

一旦配置了 PuTTY，你可以随时启动安全外壳连接，为 VNC 流量创建隧道。要打开安全的 VNC 连接，请在 `xpprol1.ad.corp.com` 上执行以下步骤：

- 1. 打开 PuTTY。
- 2. 在左侧树控件中选择 `Connection`（连接）。
- 3. 选择 `Connection` 下的 `Tunnels`（隧道）。
- 4. `Source Port`（源端口）输入 `5950`。
- 5. `Destination`（目的）输入 `linserv1.corp.com:5900`。
- 6. 选择顶部的 `Session`（会话）。
- 7. 在 `Saved Sessions`（保存会话）文本框中输入 `linserv1.corp.com (VNC)`。
- 8. 点击 `Save`（保存）以保留这些设置。
- 9. 点击 `Open`（打开）开始连接。

当 SSH 提示出现时，输入你的用户名和密码。然后 TightVNC 客户端程序中会出现 Fedora 登录提示。再次输入凭据。你现在拥有加密的 VNC 会话！

- 3. 选择“PuTTY”应用程序。
- 4. 在“Saved Sessions”（保存会话）下方的列表框中双击“`inserv1.corp.com (VNC)`”。
- 5. PuTTY 终端窗口出现，显示登录提示。使用用户 `user1` 和密码 `password` 登录。
- 6. 出现 Linux shell 提示符。你现在可以最小化（而非关闭）PuTTY 终端窗口。
- 7. 选择 `Start All Programs`（启动所有程序）。
- 8. 选择“`TightVNC Viewer (Fast Compression)`”。
- 9. 选择“`TightVNC Viewer (Fast Compression)`”。如果通过慢速连接，你可能更喜欢选择“Best Compression”（最佳压缩）。
- 10. 将出现“Connection details”（连接详情）提示框。在“VNC Server”字段中输入 `localhost::5950`。注意 `localhost` 和端口号之间是两个冒号。
- 11. 点击“OK”。片刻后，Linux 桌面将出现在 Windows 桌面面的一个窗口中，显示 Fedora 登录提示，与之前图 8.20 所示完全一致。当然，你的 Fedora 登录将通过所有的 VNC 活动被安全加密。

## 通过 LTSP 进行 Linux 主机的终端计算

你是否想允许坐在 Windows 工作站前的一整间用户登录并访问 Linux 终端服务器上的远程桌面？我们已经实现了！我们之前为 Linux 主机 `inserv1.corp.com` 设置远程计算所遵循的步骤是经过仔细选择的，以适应多个用户。在 Linux 下，没有需要担心的每个用户许可问题。只需从多个工作站启动 VNC 连接即可。同时运行桌面的能力仅限于服务器的可用内存。

尽管如此，还有其他方法可以进一步减少客户端所需的功率。如果客户端硬件成本对你来说是一个至关重要的问题，那么这些方法是值得的。其中之一就是 Linux 终端服务器项目 `LTSP`，我们将简要介绍它，因为这是一个 Windows-Linux 互操作性问题。

`LTSP` 的核心是让更少的机器（即没有硬盘、通过网络启动）与 Linux 主机进行通信。这其中没有太多的 Windows 操作。我们也不会花大量时间讨论来客人与 Linux 主机的通信。然而，我们会提供一些提示，以使 `LTSP` 与 Windows 主机协同工作。

`LTSP` 尽管名为如此，但并不是 Windows Terminal Services 的 Linux 对应物。我们已经在“Linux 主机的远程计算”部分设置了它，完全仅使用 Fedora Linux 自带的软件。`LTSP` 也提供了远程登录功能，但 `LTSP` 真正的名声在于可以通过网络启动无盘、低功耗机器，即时加载最小的 Linux 内核和系统，并在服务器上完成所有计算。

## Linux 主机的远程、终端和辅助计算

当然，在正常情况下，`LTSP` 在客户端端和主机端都是 Linux 特有的产物。也就是说，服务器运行 Linux `LTSP`。客户端在启动时，使用以网卡上“引导 ROM”芯片中的一个简单程序下载 Linux 内核。

`LTSP` 客户端也可能使用 `rdesktop` 访问 Windows 终端服务器。这并不是一个标准且完全支持的配置，但在理论上，从 Windows 服务器启动 `LTSP` 客户端工作站是可行的。

为什么有人想这么做呢？嗯，`LTSP` 对客户端的内存要求很低，磁盘空间需求显然为零。

从负面来看，配置 Windows 主机以远程启动 `LTSP` 客户端虽然可行，但并不简单。此外，`rdesktop` 不是 `LTSP` 软件包的标准部分，必须使用第三方单独添加，而这些第三方在本文写作时的版本与 `LTSP` 版本不同步。此外，网络启动过程信任下载到客户端的 Linux 内核是合法的，因此本地网络必须是可靠的。在本书中，我们强调了加密以获得更好的安全性和身份验证这至少是可能的解决方案。这就是为什么例如，在第 2 章中，我们提倡使用 SSL 加密的 LDAP 而不是熟悉的 NIS。

最后，归功于“低要求”是一个非常现实的词汇！你的雇主正在使用的那些五年前的 Pentium 系统完全有能力作为基于 Fedora Linux 的客户端，我们将在名为“Fedora 作为瘦客户端”的注释中准确地告诉你如何在不使用 `LTSP` 的情况下实现，该内容将在 `www.WinLinAnswers.com` 提供。因此，除非你急于运行某些 486 时代的硬件，否则 `LTSP` 的优势是值得商疑的。有关 `LTSP` 的更多信息，请参考以下资源：

- `LTSP` 主页，它将帮助你最初在 Linux 环境中运行 `LTSP`，并提供 `LTSP` 的 Linux 到 Windows 提示：`www.ltsp.org/`
- “Configuring Windows 2000/2003 For Etherboot”页面，讨论了如何说服你的 `LTSP` 客户端从 Windows 服务器而非 Linux 服务器通过网络启动的细微之处：`http://diet-pc.sourceforge.net/windows/etherboot-w2k.html`
- 支持 Windows 的 `LTSP` 补丁：`www.wilisystem.com/`

## 将 Windows 工作站变为 Linux 主机的瘦客户端

我们提到过，在 `WinLinAnswers.com` 上，我们将提供如何设置一个简单的 Fedora Linux 客户端作为 Windows 终端计算主机的瘦客户端的说明。我们还写了另一份文档解释了如何相反操作：将一个简单的 Windows 客户端设置为 Linux 终端主机的瘦客户端。

这是通过配置 VNC 客户端实现的，使其在 Windows 完成启动后立即启动。你可以在 `www.WinLinAnswers.com` 找到它。

## Linux 主机的辅助计算

你已经看到了如何通过 VNC 登录到 Linux 主机。我们也看到了客人登录桌面的远程计算。但我们如何在 Linux 主机上设置辅助计算，以便一个用户可以帮助另一个用户呢？幸运的是，Fedora 包含一个类似于 Windows 远程协助的功能。该功能被称为远程桌面，Windows 客户端可以轻松连接到它。之前，我们看到 `salesperson1`（Linux 工作站）协助 `salesperson2`（Windows 工作站）。现在轮到 `salesperson2`（Windows）通过协助 `salesperson1` 的 Linux 工作站来报答。
