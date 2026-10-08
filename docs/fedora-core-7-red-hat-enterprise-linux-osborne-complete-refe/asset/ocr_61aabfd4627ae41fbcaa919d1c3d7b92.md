```
[Dialer Defaults]
Modem = /dev/ttyS0
Baud = 57600
Initl = ATZ
SetVolume = 0
Dial Command = ATDT

[Dialer myisp]
Username = chris
Password = mypassword
Modem = /dev/ttyS0
Phone = 555-5555
Area Code = 555
Baud = 57600
Stupid mode = 0
```

| Variable | Description |
| :--- | :--- |
| **Inherits** | Explicitly inherits from the specified section. By default, sections inherit from the [Dialer Defaults] section. |
| **Modem** | The device wvdial should use as your modem. The default is /dev/modem. |
| **Baud** | The speed at which wvdial communicates with your modem. The default is 57,600 baud. |
| **Init1...Init9** | Specifies the initialization strings to be used by your modem; wvdial can use up to 9. The default is "ATZ" for Initl. |
| **Phone** | The phone number you want wvdial to dial. |
| **Area Code** | Specifies the area code, if any. |
| **Dial Prefix** | Specifies any needed dialing prefix—for example, 70 to disable call waiting or 9 for an outside line. |
| **Dial Command** | Specifies the dial operation. The default is "ATDT." |
| **Login** | Specifies the username you use at your ISP. |
| **Login Prompt** | If your ISP has an unusual login prompt, you can specify it here. |
| **Password** | Specifies the password you use at your ISP. |
| **Password Prompt** | If your ISP has an unusual password prompt, you can specify it here. |
| **Force Address** | Specifies a static IP address to use (for ISPs that provide static IP addresses to users). |
| **Stupid Mode** | In Stupid Mode, wvdial does not attempt to interpret any prompts from the terminal server and starts pppd after the modem connects. |
| **Auto Reconnect** | If enabled, wvdial attempts to reestablish a connection automatically if you are randomly disconnected by the other side. This option is on by default. |

Table 5-2 Variables for wvdial