
一旦完成，Kali 可以打开终端并杀死任何可能干扰捕获的进程来检测你的适配器。运行 `airomon-ng check`，并使用 `airomon-ng start` 将适配器进入监听模式。

运行 `airomon-ng interface list` 记录接口名称以寻找你周围的网络，例如地址：

在列表中找到你的目标。记下“SSID”和（通道）。然后运行：`airdump-ng -w <log> -c <channel> --bssid <ssid> -iv <interface>`

例如，这可能是这样的：

![](img/d2d879b5f295fad9b17e4fc9976250c7_114_0.png)
