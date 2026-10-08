# Bonus track – Understanding the danger of unauthorized IoT devices

Another security risk is related to the use of unauthorized IoT devices connected to your network. In this case, an inadvertent user may mainly connect an IoT device to your network. This may bring a lot of security risks to your network.

Therefore, you must have a system in place to detect those unauthorized devices in your network.

# Detecting unauthorized IoT devices

An easy way to detect unauthorized IoT devices connected to your network is by checking the manufacturers of the devices connected to your network.

You can easily achieve this using a piece of software called Kismet. As you can see in Figure 10.17, with Kismet you can scan the devices on your network and see the manufacturer of the devices, enabling you to detect unauthorized devices such as the Raspberry Pi, Alexa, Google Home, Amazon Echo, and so on:

| MAC | Type | Freq | Pkts | Size | Manuf |
|---|---|---|---|---||}{
| 98:A3:B9:DF:24:C0 | Wireless | 5680 | 5 | 120B | Apple |
| CR:14:BD:33:24:F4 | Wireless | 5680 | 8 | 192B | Google |
| AB:05:B9:DF:24:C5 | Wireless | 5680 | 3 | 72B | Amazon |
| A1:F1:3EE:88:7E:CB | Wireless | 5680 | 7 | 168B | Raspberry |

Figure 10.17 – Checking the name of the manufacturer using Kismet

This tool is already installed on Kali Linux. For more information, visit the following URL: https://tools.kali.org/wireless-attacks/kismet.