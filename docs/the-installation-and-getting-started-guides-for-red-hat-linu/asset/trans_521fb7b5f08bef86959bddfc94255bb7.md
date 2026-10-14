

你需要的信息不止于此。Red Hat 已使用智能默认值和 Linuxconf 等工具简化了所需信息，以简化此过程。除非他们有专门针对 Red Hat Linux 的文档，否则只需请求以下信息即可开始。具体来说，你需要：

- 一个域名服务器（DNS）的 IP 地址；
- 需要拨号的电话号码；
- 你的登录名和密码；
- 如果你要连接的网络不会为你提供动态地址，则需要你的机器的 IP 地址；
- 你的 ISP 是否使用 PAP、CHAP 或 MS-CHAP 等身份验证方法。如果是，则你需要一个“密钥”来启用身份验证。密钥将是一个单词或字符序列。CHAP 和 MS-CHAP 目前不使用 Linuxconf 支持，并且很少使用。

可能有帮助但不是必需的额外信息包括辅助域名服务器地址和搜索域。一旦你拥有所有这些信息，你就可以准备连接了。

- 在 shell 提示符下输入 linuxconf 启动 Linuxconf。
- 打开 [Config] -> [Networking] -> [PPP/SLIP/PLIP]。
- 选择 Add。

## Figure 8-15: PPP/SLIP/PLIP Configurations Screen

最初不会指定任何配置。选择 Add 后，你将可以选择 PPP、SLIP 和 PLIP。

![](img/46f4935125ba89e12897afbe9d77a097_208_0.png)

## Figure 8-16: Type of Interface Screen

PPP 是最常用的接口，也是默认接口。要设置 PPP 连接，请选择 PPP 并点击 Accept。

![](img/46f4935125ba89e12897afbe9d77a097_209_0.png)

## Figure 8-17: PPP Interface Screen

你会看到以下字段：

- Phone number - 用于访问远程系统的号码；
- Modem port - 指示你的调制解调器所在位置。应已设置好。
- Use PAP authentication (check box) - 如果你知道你要拨入的系统需要此项，请勾选；
- Login name - 你的 PPP 账户的登录名；
- Password - 你的 PPP 账户的密码。

请注意，标题栏为 PPP interface ppp0。ppp0 是第一个 PPP 接口，ppp1 将是第二个，以此类推。如果你有多个接口，跟踪你正在使用的接口非常重要。SLIP 连接使用 sl 而不是 ppp 作为其接口前缀。除了 PAP 身份验证选项外，添加 PPP 或 SLIP 账户的输入屏幕是相同的。

## Figure 8-18: SLIP Interface Screen

输入远程机器的完整电话号码，并确保包含访问外线所需的任何号码。例如，如果你需要先拨“9”然后再拨号码，而你要连接的计算机的电话号码为“555-0111”，那么你应输入“95550111”。接下来它会要求你输入调制解调器端口。这是一个可用端口的下拉框。如果你使用的是双启动 Linux/Windows 系统并且知道调制解调器所在的 COM 端口，以下映射可能有用：映射到 Windows COM 端口如下：

- cua0 — COM1: under MS-DOS;
- cua1 — COM2: under MS-DOS;
- cua2 — COM3: under MS-DOS;
- cua3 — COM4: under MS-DOS.

登录名是 PPP 账户的登录名。你输入的密码将以明文显示，因此在输入时请注意周围的人！如果你将使用 PAP 身份验证，请勾选该框；在输入其他所需信息后，选择屏幕底部的 Customize 按钮。所有其他信息都提供在各个标签页中，可以在 Customize 屏幕中设置，但将所有信息集中在主屏幕上更容易查找。

![](img/46f4935125ba89e12897afbe9d77a097_211_0.png)

## Figure 8-19: PPP Interface Customization Screen

选择 PAP 标签并输入你的用户名，然后在 Secret 字段中输入 ISP 为你提供的密钥。其他默认值应足够，但如果需要，你可以使用 Customize 选项编辑初始设置。

