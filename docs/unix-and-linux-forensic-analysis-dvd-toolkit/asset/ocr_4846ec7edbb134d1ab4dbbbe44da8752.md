# Figure 5.13 Memory Usage

![](bbox=[0.118, 0.085, 0.881, 0.193])

| | | | | | | | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||
| 5346 | | 15 | 3172 | 3028 | 5 | 6 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 5190 | | 15 | 3172 | 3028 | 5 | 6 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 17168 | | 15 | 7184 | 1170 | 8 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 2620 | | 15 | 7184 | 1170 | 8 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 3 | | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 3 root | | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 5 root | | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 5 root | | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 26 root | | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 28 root | | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 92 root | | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 106 root | | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 116 root | | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 117 root | | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

Module: exploit/windows/msclient/messenger_trojan
This module exploits a stack overflow in Symantec Client 3.0.0. This module has not been tested against Symantec Client 3.0.2 build 10.2.2005. This exploit was written by MC Lyd@000-shell.net

> References:
http://www.exploit-db.com/exploits/21107/
http://www.exploit-db.com/exploits/21108/
http://www.exploit-db.com/exploits/21109/
http://cheeseah.se/home/index.php?ac20006812.html

Why would intruder, presumably have to be ready to have through the additional trouble to install MSF in the first place, go configuring the GUI to reach his remote host? The answer is... he wouldn't. So, again, knowing the GUIs exists and runs on Ruby is good knowledge, but I would better deal to doughnuts that you would never see this in any other environment.

What you would likely see in a larger corporate environment would either be attacks coming from the traditional command line or the Web GUI. So what you say?! So an attack would most likely come from one of these sources? What would that look like? Well, I'm glad you asked!

In my example, I launched an attack against a local Windows 2000 SP 4 install using both the command line and GUI interfaces. The attack I chose is the Windows/smb/ms06-004_netapi buffer overflow exploit.¹³ Using the command-line interface, I targeted 192.168.10.125, my Windows 2000 server, using local port 34333, and payload windows/vinject/bind_tcp. (See Figure 5.14).

¹³ www.securityfocus.com/bid/19409/info