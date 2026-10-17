
## Configuring Replaced or Unsupported Ethernet Cards

If you change your Ethernet card or if your card is not supported and you need to manually load a driver for it, you will have to manually configure the card. For supported cards, `Kudzu` will automatically detect the card when your system starts up and prompt you to configure it. For dynamic connections, simply select `DHCP` to automatically determine your network configuration. For static connections, enter the required network information, such as your IP address and DNS servers.

If the device is not supported or if you elected not to configure it with `Kudzu`, you can use `redhat-network-config` to manually create a new device for the card. For unsupported devices, make sure you have first obtained the required Linux kernel module for it and have installed that module using `modprobe` as described in the preceding chapter. Then, start up `redhat-network-config` and click the `New` button in the Device panel. Select `Ethernet` as the type of device and then select the Ethernet card from the list provided. On the Configure Network Setting panel, click `Automatically Obtain IP Address`, and select the method from the drop-down menu, usually `DHCP`. Also click `Automatically Obtain DNS Information`. For static connections, enter the required information, such as your IP and DNS server addresses. Your new device will now appear in the Devices panel. To activate it, select it and then click `Activate`.

## Network Device Control

With the Network Device Control tool, you can activate or deactivate configured network connections. A pop-up menu will let you select available profiles, automatically activating network connections associated with each profile, and deactivating those that are not. The Network Device Control tool is accessible in the `System Tools` menu. Selecting a device and clicking the `Configure` button will open the `redhat-config-network` tool. You can then select and configure any network device, as well as add new ones.

## The Internet Configuration Wizard

To configure a new network connection, you use the Internet Connection Wizard, accessible from the `System Tools` menu. If you already have `redhat-config-network` open and want to add a new network connection, clicking `New` will also start the Internet Connection Wizard. The wizard initially displays a list of all possible network connections (see Figure 5-4). When you select an entry, panels will prompt you to enter basic information about a connection; this will include phone number, username, and password for modem, DSL, and ISDN connections, whereas Ethernet connections will prompt only for IP addresses. The types of connections and devices currently supported are `Ethernet` (`eth`), `ISDN` (`isdn`), `Modem` (`ppp`), `xDSL` (`ppp`), `Token Ring` (`tr`), `Crypto IP Encapsulation for Virtual Private Networks` (`cipcb`), and wireless connections (`eth`). After completing your entries, the wizard will configure your connection setting and the new connection will be ready for use.

## Modem Configuration

You can also use a modem with telephone lines to connect to a network. For a modem connection, the Internet Configuration Wizard will probe and detect your modem. A window will then display entries for the serial device, baud rate, hardware control, and modem volume, which you can modify. You are then prompted to enter the phone number, provider, username, and password for your ISP account. The `redhat-config-network` tool is then started up, listing your modem device as a `ppp` connection (`ppp` stands for the

![](img/6c226e8ba1efd427dec3bf582418d33f_106_0.png)

*点对点协议 [PPP] 协议，可通过电话线传输 IP 通信)。然后你可以编辑 `ppp` 设备以修改你的设置并输入其他任何设置；例如，你可以输入静态连接的 IP 地址，指定压缩方法，或列出你的 DNS 服务器。*

## DSL 和 ISDN 配置

要配置 DSL，你需要提供 DSL（数字用户线路）和 ISDN 的登录名和密码信息。在其他方面，DSL 和 ISDN 连接的操作方式与局域网（LAN）非常相似，将主机视为网络的集成部分。在 Red Hat 上，你可以使用 Internet 配置向导设置 DSL 或 ISDN 连接。对于 DSL，Internet 配置向导将显示一个对话框，其中包含用于输入你的登录名、你的密码以及 DSL 调制解调器所连接的以太网接口的条目。你还需要输入 ISP 提供的 DNS 服务器的 IP 地址。你可以选择在系统启动时自动建立连接（取决于你选择的网络配置文件）。
