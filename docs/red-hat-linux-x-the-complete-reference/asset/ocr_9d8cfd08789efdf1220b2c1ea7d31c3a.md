# Command Line PPP Access: wvdial

If, for some reason, you have been unable to set up a modem connection on your X Window System, you may have to set it up from the command line interface instead of a desktop. For a dial-up PPP connection, you can use the wvdial dialer. wvdial is an intelligent dialer, which not only dials up an ISP service but also performs login operations, supplying your username and password. wvdial first loads its configuration from the /etc/wvdial.conf file. In here, you can place modem and account information, including modem speed and serial device, as well as ISP phone number, username, and password. The wvdial.conf file is organized into sections, beginning with a section label enclosed in brackets. A section holds variables for different parameters that are assigned values, such as username = chris. The default section holds default values inherited by other sections, so you needn't repeat them. Table 5-2 lists the wvdial variables.

Table 5-2: Variables for wvdial

| Variable | Description |
|---|---|
| Inherits | Explicitly inherits from the specified section. By default, sections inherit from the [Dialer Defaults] section. |
| Modem | The device wvdial should use as your modem. The default is /dev/modem. |
| Baud | The speed at which wvdial communicates with your modem. The default is 57,600 baud. |
| Init1 ... Init9 | Specifies the initialization strings to be used by your modem. wvdial can use up to 9. The default is "ATZ" for Init1. |
| Phone | The phone number you want wvdial to dial. |
| Area Code | Specifies the area code, if any. |
| Dial Prefix | Specifies any needed dialing prefix-for example, 70 to disable call waiting or 9 for an outside line. |
| Dial Command | Specifies the dial operation. The default is "ATDT". |
| Login | Specifies the username you use at your ISP. |
| Login Prompt | If your ISP has an unusual login prompt, you can specify it here. |
| Password | Specifies the password you use at your ISP. |
| Password Prompt | If your ISP has an unusual password prompt, you can specify it here. |
| Force Address | Specifies a static IP address to use (for ISPs that provide static IP addresses to users). |
| Remote Name | For PAP or CHAP authentication, you may have to change this to your ISP's authentication name. The default value is *. |
| Carrier Check | Setting this option to No disables the carrier check by your modem. Used for a modem that reports its carrier line is always down. |
| Stupid Mode | In Stupid Mode, wvdial does not attempt to interpret any prompts from the terminal server and starts pppd after the modem connects. |
| Auto Reconnect | If enabled, wvdial attempts to reestablish a connection automatically if you are randomly disconnected by the other side. This option is on by default. |

You can use the wvdialconf utility to create a default wvdial.conf file for you automatically. wvdialconf will