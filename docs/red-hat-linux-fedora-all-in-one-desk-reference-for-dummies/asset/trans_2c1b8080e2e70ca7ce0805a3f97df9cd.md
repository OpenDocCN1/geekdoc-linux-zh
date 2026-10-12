
如果你看到如下信息，则 Linux 已在你的 PC 中检测到串行端口：

```
ttyS0 at 0x03f8 (irq = 4) is a 16550A
```

在这种情况下，该消息表示 Linux 内核已检测到第一个串行端口（COM1）。它显示了 I/O 地址（十六进制），0x3f8，以及 IRQ 4。消息的最后一部分 — 16550A — 指的是通用异步收发器/发送器（UART）芯片的识别编号，该芯片是所有串行通信硬件的核心（UART 将每个字节转换为 1 和 0 的流，并在接收此类流时反向转换）。

你也可以使用 setserial 命令检查串行端口。输入以下命令以查看有关串行端口的详细信息：

```
setserial -g /dev/ttyS?
```

任何在此命令输出中列出且 UART 未知的设备，要么未安装，要么未被 Linux 内核检测到。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_329_0.png)

## 测试调制解调器

完成调制解调器的物理安装并验证 Linux 内核检测到串行端口后，你可以尝试通过调制解调器拨号。最佳方法是使用随 Red Hat Linux 提供的 Minicom 串行通信程序。

Minicom 类似于你在 MS-DOS 或 Windows 下可能使用过的其他通信软件，例如 Procomm 或 Crosstalk。

要运行 Minicom，请以 root 身份登录，并在终端窗口（或虚拟控制台）中的 shell 提示符下输入 minicom。Minicom 运行并重置调制解调器。图 1-8 显示了在终端窗口中运行 Minicom 的结果。

如果看不到 OK，这可能意味着此特定串行设备名称未设置正确。要设置串行设备，请按照以下步骤操作：

- 1. 按 Ctrl+A 然后按 Z。
- Minicom 显示其帮助屏幕。
- 2. 按 O。
- Minicom 显示其配置菜单。
- 3. 使用方向键选择 Serial port setup 并按 Enter。
- Minicom 显示串行端口设置。
- 4. 按 A。

Minicom 将光标放在显示串行设备名称的行中。编辑设备名称以匹配调制解调器的连接位置。例如，如果调制解调器位于第一个串行端口，请确保设备名称为 /dev/ttyS0。

- 5. 按两次 Enter。
- Minicom 返回到配置菜单。
- 6. 选择 Save setup as dfl 并按 Enter。
- Minicom 保存设置。
- 7. 选择 Exit 并按 Enter。
- Minicom 返回在线模式。
- 8. 按 Ctrl+A 和 X。
- Minicom 提示你是否真的要退出。
- 9. 按 Enter 退出。
- 设置调制解调器所连接串行端口的正确设备名称后，请确保调制解调器已通电并连接到电话线。
- 10. 再次启动 Minicom（在终端窗口中输入 minicom）。
- 11. 按 Ctrl+A 以获取 Minicom 程序的注意。
- 按下 Ctrl+A 后，如果按下 Z，则会以文本窗口的形式显示帮助屏幕。在帮助屏幕中，你可以获取有关其他 Minicom 命令的信息。

图 1-8：你可以使用 Minicom 手动测试调制解调器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_330_0.png)

12. 从帮助屏幕按 Enter 返回在线模式。

在线模式下，你可以使用调制解调器的 AT 命令拨号。特别是，你可以使用 ATDT 命令拨打另一台调制解调器的电话号码（例如，拨打你的 ISP 号码）。当你收到登录提示时，就知道调制解调器正在工作。图 1-9 显示了使用 Minicom 进行典型拨号的结果：使用 56 Kbps 调制解调器仅为 38.4 Kbps。（难怪我需要 DSL 或有线调制解调器！）

![](img/a7eec43a54473e95dc5ea333fecf1bd7_331_0.png)

图 1-9：
使用 ATDT 命令通过 Minicom 手动拨号。

13. 要退出 Minicom，请按 Ctrl+A 然后输入 X。

14. 再次按 Enter 关闭 Minicom。

## 设置和激活 PPP 连接

大多数 ISP 通过 ISP 维护的一个或多个系统提供对 Internet 的 PPP 拨号访问。如果你注册此类服务，ISP 应该为你提供建立与 ISP 系统的 PPP 连接所需的信息。通常，此信息包括以下内容：

- 拨号以连接到远程系统的电话号码
- 你必须用于登录远程系统的用户名和密码
- ISP 的邮件和新闻服务器的名称
- 你的 PPP 连接的 IP 地址。ISP 不提供此地址如果 IP 地址动态分配（这意味着每次系统建立连接时 IP 地址可能会更改）。
- ISP 的域名服务器（DNS）的 IP 地址。ISP 不提供这些地址如果它动态分配 IP 地址。

这些信息中，前两项是设置 PPP 连接所需的内容。

按照以下步骤使用 Red Hat 的 Internet 配置向导设置 PPP 连接：

- 1. **以 root 身份登录并从 GNOME 桌面选择 主菜单→系统工具→Internet 配置向导。**

如果你未以 root 身份登录，在提示时输入 `root` 密码。

选择设备类型对话框出现（如图 1-10 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_332_0.png)

图 1-10：
从此对话框配置调制解调器连接。

- 2. **从设备类型列表中选择 Modem connection，然后单击 Forward。**

选择调制解调器对话框显示有关你的调制解调器的信息。

- 3. **单击 Forward 继续。**

选择提供商对话框出现。

- 4. **在文本框中填写连接信息 — ISP 的电话号码、你的登录名和密码（见图 1-11）；单击 Forward 继续。**

图 1-11：
在此对话框中填写连接信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_333_0.png)

5. 输入 IP 设置 — 是否想要自动获取 IP 地址或提供静态 IP 地址 — 然后单击 Forward 继续。

通常，你会选择从 ISP 自动获取 IP 地址和名称服务器设置的选项。

6. 单击 Apply 保存拨号配置信息，然后关闭 Internet 配置向导。

网络配置对话框出现，其中列出了新拨号连接的名称（图 1-12）。

图 1-12：
在网络配置对话框中单击 Activate 以建立 PPP 连接。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_333_1.png)

7. 选择连接名称，然后单击 Activate。
8. 完成后，单击 Deactivate 关闭 PPP 连接。

## 配置 CHAP 和 PAP 认证

系统上的 PPP 服务器必须在 PPP 连接完全建立之前向 ISP 的 PPP 服务器进行身份验证。身份验证需要证明你拥有 ISP 的有效账户；本质上这涉及提供用户名和密钥（即密码）。PPP 规定了在连接两端之间交换身份验证信息的两种方式：

- **Challenge Handshake Authentication Protocol (CHAP)** 要求远程端发送随机生成的挑战字符串以及远程服务器的名称。本地系统使用服务器名称查找密钥；然后它发送回一个响应，其中包含其名称和一个结合了密钥和挑战的值，使用单向哈希函数。远程系统然后将该值与自己计算的预期哈希值进行比较。如果值匹配，则身份验证成功；否则，远程系统终止连接。在这种情况下，名称和密钥存储在 `/etc/ppp/chap-secrets` 文件中。请注意，远程系统可以在 PPP 链路处于活动状态时随时重复 CHAP 身份验证。
- **Password Authentication Protocol (PAP)** 与正常登录过程类似。使用 PAP 时，本地系统会重复发送用户名（名称）和密码（密钥），直到远程系统确认身份验证或结束连接。名称和密钥存储在 `/etc/ppp/pap-secrets` 文件中。请注意，用户名和密码以明文形式发送（即未加密）。

Linux PPP 服务器支持这两种类型的身份验证。对于 PAP 和 CHAP，PPP 服务器所需的信息是名称和密钥 — 一个用户名-密码对。此身份验证信息存储在以下配置文件中：

- `/etc/ppp/chap-secrets` 存储 CHAP 的信息。典型的 chap-secrets 文件如下所示：

```
# Secrets for authentication using CHAP
# client    server    secret    IP addresses
"naba"      *        "mypassword"
```

- `/etc/ppp/pap-secrets` 存储 PAP 的信息。典型的 pap-secrets 文件如下所示：

```
# Secrets for authentication using PAP
# client    server    secret    IP addresses
"naba"      *        "mypassword"
```
