
5. 在 **容器名称** 字段中，输入要在其中创建 iPrint 管理器对象的树中的上下文。

   - 在 **目标服务器** 字段中，输入您的 iPrint 服务器的 IP 地址。

   - 在 **eDir 服务器** 字段中，浏览并选择 eDirectory 树中您的 NNLS 服务器的服务器对象。

   - 在 **驱动程序存储区** 字段中，浏览并选择您之前创建的驱动程序存储区对象。

   - 确保已标记 **创建后启动打印管理器**，然后单击 **确定**。

   - 当提示 iPrint 管理器已创建时，单击 **确定**。

就这样。此时，您的驱动程序存储区和 iPrint 管理器已配置完毕。下一步您需要做的是为网络打印机配置打印机代理。

### 配置打印机代理

请记住，打印机代理代表您网络中的每台物理打印机。打印机代理与打印机之间的关系是一对一的。一个打印机代理只能与一台物理打印机相关联。

![](img/c7771e8540507f2b00c088c7a411b57b_431_0.png)

> 有趣的是，您实际上可以拥有多个代表单个物理打印机的打印机代理。这非常有用，因为您可以通过 eDirectory 权限分配，创建一个具有一套打印机设置（如纸张尺寸、双面打印等）的打印机代理供一类用户使用，然后创建另一个具有不同打印机设置集的打印机代理供另一类用户使用。

此外，单个 iPrint 管理器（每台服务器只能有一个）可以管理多个打印机代理。

与 iPrint 管理器一样，打印机代理使用 iManager 进行配置。您可以使用任何支持的 Web 浏览器来配置打印机代理，并且无需在用于访问 iManager 的工作站上安装 iPrint 客户端。要创建打印机代理，请完成以下步骤：

- 打开 Web 浏览器并导航至 `https://your_server_IP_address/nps/iManager.html`。

- 使用您的 **admin** 用户身份进行身份验证。

- 在 **iPrint** 角色下，选择 **创建打印机** 任务。出现如图 9.19 所示的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_432_0.png)

**图 9.19**

创建打印机代理。

4. 在 **打印机名称** 字段中，输入 eDirectory 树中打印机代理对象的名称。

5. 在 **容器名称** 字段中，输入希望在 eDirectory 树中存放打印机代理对象的上下文。

6. 在 **管理器名称** 字段中，浏览并选择您之前创建的 iPrint 管理器对象。

7. 在 **DNS 名称或 IP 地址** 字段中，输入打印机的 IP 地址或 DNS 名称。

> **提示** Novell 建议您在此字段中使用 DNS 名称。这样，如果您移动了打印机并且它最终获得了不同的 IP 地址，您就不必编辑打印机代理对象了。

8. 在 **位置** 字段中，输入打印机物理位置的描述。

9. 在 **描述** 字段中，输入物理打印机的描述。

10. 单击 **下一步**。出现如图 9.20 所示的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_432_1.png)

**图 9.20**

为打印机代理配置打印机驱动程序。

11. 在 Windows 每个版本的下拉列表中，从驱动程序存储区对象中选择适当的打印机驱动程序。

12. 单击“下一步”。

13. 当提示已创建打印机代理时，单击“确定”。

这就是在树中创建打印机代理的全部步骤。在继续之前，您需要了解有关 iPrint 客户端、iPrint 管理器和打印机代理之间 TCP/IP 通信的几个问题。

首先，iPrint 客户端和 iPrint 管理器之间发送的数据可以使用 IP 端口 443 进行加密。您也可以使用 IP 端口 631 在这两个组件之间未加密地发送数据。除非有充分的理由不这样做，否则您始终应使用加密通信。

其次，从打印机代理和物理打印机传输的数据是使用 LPR 协议发送的。LPR 不支持加密；因此，在服务器上的打印机代理和物理打印机硬件之间发送的数据以明文传递。考虑到这一点，您应确保这两个组件之间的通信不跨越公共网络（如 Internet）。防止这种情况的最佳方法是将这两个组件放在同一个防火墙后面。

话虽如此，仍有一项打印机代理配置任务需要完成。这与打印机如何被添加到 Windows NT、2000 和 XP 工作站有关。请记住，这些操作系统是多用户系统。系统中的每个本地用户都有自己的配置文件、桌面和“我的文档”目录（以及其他内容）。

> **警告** 在此上下文中，术语 *本地用户* 指的是 Windows 用户帐户，而不是 eDirectory 用户帐户。提到的 *管理员* 和 *高级用户* 组指的是本地工作站上的 Windows 组，而不是 eDirectory 组。

另一方面，Windows 95、98 和 Me 不是多用户系统。

> **提示** 可以将 Windows Me 配置为准多用户系统，但其默认配置是单用户系统。

在 Windows 9x 和 Me 系统中，使用系统的每个用户都会看到相同的桌面和相同的“我的文档”文件夹，并且可以访问相同的已安装打印机。如果在其中一个操作系统上下载并安装了 iPrint 打印机，则该打印机可供系统中的所有本地用户使用。

在 Windows NT、2000 和 XP 中，可以安装打印机使其对系统上的所有本地用户可用，很像 Windows 9x 或 Me 系统。只有 Administrators 或 Power Users 组的成员才能创建此类型的打印机。

然而，在这些系统上，也可以配置打印机使其仅对安装它的本地用户可用。任何本地用户都可以创建此类型的打印机。

可以配置 iPrint 以支持任一种类型的打印机。这是通过编辑 NNLS 服务器上的 `/var/opt/novell/httpd/htdocs/ippdocs/iprint.ini` 文件来实现的，图 9.21 显示了该文件的一部分。

```
;DEFAULT = The installed name on client will
; Follow the full UNC/URL format:
; \\\\ipprint\\domain.com\\pa_name
;YOURNAME = This is any name you want to show
; for the installed printer’s UNC server name.
; Use only lower ASCII characters;
; DO NOT USE slash, quote, space, or comma.
; The new installed printer name format is:
; \\\\YOURNAME\\pa_name
AllowUserPrinters = 0
;Printer Installation Profile
;
;Terminal/Citrix Server clients
; These settings will be ignored!
; Instead, you must configure this on the
; Terminal/Citrix server (must have rights
; to see the tab and administer it).
; Start->Programs->Novell iPrint->Print Client
;
Settings:
;
;Windows clients
```

![](img/c7771e8540507f2b00c088c7a411b57b_434_0.png)

在图 9.21 中，请注意 `AllowUserPrinters` 参数。该参数用于定义 iPrint 在 Windows 系统中安装的打印机是如何实现的。如果该参数设置为 0（这是默认值），则只有属于 Administrators 或 Power Users 组的本地用户才能安装 iPrint 打印机。在这种情况下，安装的 iPrint 打印机可供系统中所有本地用户访问。

如果该参数设置为 1，则属于 Administrators 或 Power Users 组的本地用户可以像在设置为 0 时那样为系统中所有用户安装 iPrint 打印机。但是，如果本地用户不属于这两个组中的任何一个，他或她只能为他或她自己的用户账户安装 iPrint 打印机。在这种情况下，打印机仅对该用户可用，其他本地用户将看不到该打印机。

如果该参数设置为 2，则所有用户只能为他们自己的本地用户账户安装 iPrint 打印机。即使是 Administrators 或 Power Users 组中的用户也只能为他们自己安装 iPrint 打印机。

如前所述，这些参数对 Windows 95、98 和 Me 工作站没有影响。

配置此文件的最佳方式取决于您的组织标准。有些组织会指示只为单个 Windows 用户创建 iPrint 打印机。其他组织可能不会那么严格。当完成此文件的配置后，您就准备好完成最后一项 iPrint 配置任务：创建打印机位置地图。
